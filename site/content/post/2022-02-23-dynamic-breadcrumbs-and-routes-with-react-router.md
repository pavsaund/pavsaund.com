---
layout: blog
draft: false
title: Build dynamic breadcrumb routes and child routes with mathPath in React Router v6
date: 2022-02-23T21:56:56.732Z
coverSize: partial
thumbnailImagePosition: ""
tags:
  - frontend
  - react
  - react-router
  - routing
categories:
  - DevDiary
---

When faced with a challenge of implementing breadcrumbs for a business critical application recently I went down a rabbit hole of trying to understand the semantics of react-router and finding a good way of building a dynamic breadcrumb component that didn't break every time a route was added or changed. Let alone need to implement a custom route for every new page. In this post I go into what I ended up with as a routing model that supports dynamic breadcrumbs

## The requirements
- Maintain a single routing model (or composition of models) as the source of truth for the app
- Not have to manually maintain breadcrumbs for different pages
- Support child routes
- Use the same model to generate bread crumbs for the currently active page.
- Be able to show dynamic breadcrumb title based on parameters.
- Bonus: Support generating Navlinks

## TLDR;
You can check out this github repository to see my trail and error: https://github.com/pavsaund/react-routing-model/

You can view the code in action on stackblitz: https://stackblitz.com/github/pavsaund/react-routing-model/

## Digging into details

It took me a while to really grok the routing model with nested routs in React Router v6. I put this down to coming from very basic use of v5 and mostly using other frameworks. I found this article on nested routes most useful https://ui.dev/react-router-nested-routes. Based on this I realized I wanted to define my routes as a single model, where possible and to use the `<Outlet />` component to render the routes for a given path. [More info on the usage of `<Outlet />`](https://reactrouter.com/docs/en/v6/getting-started/concepts#outlets).

Let's start with how the routes look like from a React Router perspective, and what you'll likely see in your regular react app.

```ts
  <Routes>
    <Route path="/" element={<Page title="home" />} />
    <Route path="/away" element={<Page title="away" />} />
    <Route path="/sub" element={<Page title="sub" withOutlet />}>
      <Route path="zero" element={<Page title="sub-zero" />} />
    </Route>
  </Routes>

```
I started with the model I wanted, which was built separate from React Router's. The idea being that a simple model that can easily be parsed and mapped into something React Router could understand. I didn't want to implement ALL the features of React Router, but just enough for my use case. This worked fine for the initial proof of concept. Then after experimenting a bit and also understanding more of the route model that React Router expected I actually ended up augmenting the `RouteObject` model with custom properties. This is the end result.

```ts
  export interface RoutePathDefinition extends RouteObject {
    title: string;
    nav?: boolean;
    children?: RoutePathDefinition[];
    path: string;
  };

  const routes: RoutePathDefinition[] = [
    {
      title: "Home", path: "/", element: <Page title="home" />,
    },
    {
      title: "Away", path: "/away", element: <Page title="away" />,
    },
    {
      title: "Sub",
      path: "/sub",
      element: <Page title="sub" withOutlet />,
      children: [
        {
          title: "Sub-Zero", path: "zero", element: <Page title="sub-zero" />,
        },
      ],
    }
  ];
```

The `<Page />` component is a simple helper component to render a page with a title, and the `withOutlet` prop is an indication to rener an `<Outlet />`for the sub routes to render. [Implementation here.](https://github.com/pavsaund/react-routing-model/blob/7bad0d2a1ebbb2e1bb6ca047746414efab73c2b4/src/Layout/Page.tsx)

## Building the breadcrumbs

Now, for the fun part - actually understanding how to get the active path from React Router. This is where grokking how React Router builds its path's was important. I realised after hitting my head on the wall that there is no central place where all the routes are stored that is exposed through public api. ([There is an exposed `UNSAFE_RouteContext` if you want to live on the edge](https://github.com/remix-run/react-router/blob/8601f27e74021c3d0da13cfa036f38c0cd7af9b3/packages/react-router-dom/index.tsx#L119)). My current understanding is that React Router and nested routes seem to work by each level of the router owning it's own routes and the next level to take over. Meaning that a parent route doesn't actually know anything about it's children, and a child only knows its own path pattern based on the resolved parent's route. Now to build the breadcrumb.

### Matching the top level crumb with `matchPath`

Using the [`matchPath` utility](https://reactrouter.com/docs/en/v6/api#matchpath) the React Router will match the given location against the path provided. It also returns the resolved pathname, and any params it resolves. By specifying `end = false;` on the `PathPattern` option will allow a partial match on the supplied location. This allows us to know if a given pattern is part of the current location, and should be included in the breadcrumb or not.

So, let's resolve the top level paths aginst to our second route `/sub/zero`

```ts
const location = useLocation(); //for '/sub/zero'
matchPath({path: '/', end: false, },location.pathname); // returns match
matchPath({path: '/away', end: false, },location.pathname); // returns null
matchPath({path: '/sub', end: false, },location.pathname); // returns match
```

Great, so this means that both the `Home` and `Sub` paths match, and can be added to our breadcrumb. Like so:

```ts
function matchRouteDefinitions(
  definitions: RoutePathDefinition[],
  locationPathname: string
): PathMatch[] {
  const crumbs: PathMatch[] = [];

  definitions.forEach((definition, index) => {
    const match = matchPath(
      { path: definition.path, end: false },
      location.pathname
    );
    if (match) {
      crumbs.push(match);
    }
  });

  return crumbs;
}

const matches = matchRouteDefinitions(routes, '/sub/zero');
/** simplified matches
 * [
 *  {pattern: '/'},
 *  {pattern: '/sub'}
 * ]
 * /

```

### Matching children

So, now how can we match the `zero` child route? Let's manually match again

```ts
const location = useLocation(); //for '/sub/zero'
matchPath({path: 'zero', end: false, },location.pathname); // returns null
matchPath({path: '/sub/zero', end: false, },location.pathname); // returns match
```
OK! Now we're getting somewhere. It's not enough to match against the path pattern itself, you also need to match with the parent pathname. So let's add the parent path into the mix.

```ts

function joinPaths(paths: string[]): string {
  return paths.join("/").replace(/\/\/+/g, "/");
}

function matchRouteDefinitions(
  definitions: RoutePathDefinition[],
  locationPathname: string,
  parentPath: string = ''
): PathMatch[] {
  const crumbs: PathMatch[] = [];
  const pathPatternWithParent = joinPaths([parentPath, definition.path]);

  definitions.forEach((definition, index) => {
    const match = matchPath(
      { path: pathPatternWithParent, end: false },
      location.pathname
    );
    if (match) {
      crumbs.push(match);

      if (definition.children) {
        const nestedMatches = matchRouteDefinitions(
          definition.children,
          locationPathname,
          pathPatternWithParent
        );

        crumbs.push(...nestedMatches);
      }
    }
  });

  return crumbs;
}

const matches = matchRouteDefinitions(routes, '/sub/zero');
/** simplified matches
 * [
 *  {pattern: '/'},
 *  {pattern: '/sub'}
 *  {pattern: '/sub/zero'}
 * ]
 * /

```

There's a bit more going on here so let's break down what's happening.
`parentPath` has been added as a parameter with a default value of `''`. Then using the `joinPaths` function the parent and definition path are joined, and any redundant `//` are replaced with a single slash.

Next, if there are children on the matched route, then recursively call the `matchRouteDefinitions` with the child routes. This time we pass in the `pathPatternWithParent` as a the parentPath parameter, which then allows the child router paths to match.

Now this is the happy path (pun intended 😏) implementation. There are some edge cases you may or may not want to support.

### Edge case 1: Don't match breadcrumb for `/` - Home route
For my use case I didn't want `Home` to show up, so I added another path check before deciding to add the path match

```ts

 //...
   definitions.forEach((definition, index) => {
    //...
    if (match && definition.path != '/') {
      crumbs.push(match);
    }
    //...
  });

  const matches = matchRouteDefinitions(routes, '/sub/zero');
  /** simplified matches
   * [
   *  {pattern: '/sub'}
   *  {pattern: '/sub/zero'}
   * ]
   * /

```

### Edge case 2: Don't match a no-match/catch-all route
It's common to add a NoMatch route to serve a user with a 404 page of some kind. The problem is that this route will match anything - which is kind of the point.

```ts
  routes.push({
    title: "404", path: "*", element: <Page title="404 Not Found" />,
  });
  const matches = matchRouteDefinitions(routes, '/sub/zero');
  /** simplified matches
   * [
   *  {pattern: '/'},
   *  {pattern: '/sub'},
   *  {pattern: '/sub/zero'},
   *  {pattern: '*'},
   * ]
   * /

```
So, we can add the `*` pattern to the ignore list as well.

```ts
  const skipPaths = ['/', '*'];
 //...
   definitions.forEach((definition, index) => {
    //...
    if (match && !ignoredPaths.includes(definition.path) {
      crumbs.push(match);
    }
    //...
  });

  const matches = matchRouteDefinitions(routes, '/sub/zero');
  /** simplified matches
   * [
   *  {pattern: '/sub'}
   *  {pattern: '/sub/zero'}
   * ]
   * /
```

### Edge case 3 - Child route with ''-path with redirect matches parent route
For a use case where a child route has an empty path then the resolved from `matchPath` ends up being the same. This may actually be what React Router refers to as an [`Index` path](https://reactrouter.com/docs/en/v6/getting-started/concepts#index-route) - but I haven't explored that aspect enough yet.

```ts
 routes.push({
    title: "Another",
    path: "/another",
    element: <Page title="Another" />,
    children: [
      { title: "Another-index", path: "", element: <Page title='Empty' />}
      { title: "Another-other", path: "other", element: <Page title='Other' />}
    ]
  });

  const matches = matchRouteDefinitions(routes, '/another/');
  /** simplified matches
   * [
   *  {pattern: '/'},
   *  {pattern: '/another'},
   *  {pattern: '/another'},
   * ]
   * /

```

This means you need a guard or check in in place before adding the match.

```ts
function getPreviousMatch(previousMatches: PathMatch[]): PathMatch | undefined {
  return previousMatches[previousMatches.length - 1];
}

function isNotSameAsPreviousMatch(previousMatches: PathMatch[], match: PathMatch): boolean {
  const previousMatchedPathname = getPreviousMatch(previousMatches)?.pattern ?? "";
  return previousMatchedPathname !== match.pattern;
}

function isMoreSpecificThanPreviousMatch(previousMatches: PathMatch[], toPathname: string): boolean {
  const previousMatchedPathname = getPreviousMatch(previousMatches)?.pathname ?? "";
  return toPathname.length > previousMatchedPathname.length;
}

function canBeAddedToMatch(matches: PathMatch[], match: PathMatch) {
  return (
    isNotSameAsPreviousMatch(matches, match) &&
    isMoreSpecificThanPreviousMatch(matches, match.pathname)
  );
}

 //...
   definitions.forEach((definition) => {
    //...
    if (
      match &&
      !ignoredPaths.includes(definition.path &&
      canBeAddedToMatch(matches, match)
    ) {
      crumbs.push(match);
      if (definition.children) {
        //...
        nestedMatches.forEach((nestedMatch) => {
          if(canBeAddedToMatch(matches, nestedMatch)) {
            crumbs.push(nestedMatch);
          }
        });
      }
    }
    //...
  });

  const matches = matchRouteDefinitions(routes, '/another/');
  /** simplified matches
   * [
   *  {pattern: '/'},
   *  {pattern: '/another'},
   * ]
   * /
```

## Rendering routes
So, now that we have all our route defined in a nice object, wouldn't it be good to render them using that same object? As i mentioned in the introduction, this caused me some pain until I realised I could extend the `RouteObject` that React Router already exposes. Then it's possible to use the `useRoutes` hook to do the rendering for you.

```ts
import { routes } from './routes';

export default function App(){
  const routesToRender = useRoutes(routes);
  return (
    <div>
      <h1>My App</h1>
      {routesToRender}
    </div>
    )
}
```

Then in the page that has child routes, include the `<Outlet />` component. Remember to do this for each component that has child routes. React Router will then figure out which child routes to render there.

```ts
import { Outlet } from "react-router-dom";

export default function Sub() {
  const routesToRender = useRoutes(routes);
  return (
    <div>
      <h1>Sub</h1>
      <Outlet />
    </div>
    )
}
```

## Rendering the breadcrumbs
Now that we have all the moving parts in place, we can put it all together in the `Breadcrumbs` component. In the below exampled the `matchRouteDefinitions` function now returns an `ActiveRoutePath` which is a structure that includes both the `match` and the `RoutePathDefinition` for convenience.

```ts
export type ActiveRoutePath = {
  title: string;
  match: PathMatch<string>
  definition: RoutePathDefinition;
};

function useActiveRoutePaths(routes: RoutePathDefinition[]): ActiveRoutePath[] {
  const location = useLocation();
  const activeRoutePaths: ActiveRoutePath[] = matchRouteDefinitions(routes, location.pathname);
  return activeRoutePaths;
}

export function Breadcrumbs({ routes }: BreadcrumbsProps) {
  const activeRoutePaths: ActiveRoutePath[] = useActiveRoutePaths(routes);
  return (
    <>
      {activeRoutePaths.map((active, index, { length }) => (
        <span key={index}>
          {index === 0 ? "" : " > "}
          {index !== length - 1 ? (
            <Link to={active.match.pathname}>{active.title}</Link>
          ) : (
            <>{active.title}</>
          )}
        </span>
      ))}
    </>
  );
```

Now, in our `App.tsx` we can include th breadcrums path and it will render breadcrumbs automatically based on the page you are visiting.

```ts
export default function App(){
  const routesToRender = useRoutes(routes);
  return (
    <div>
      <div><Breadcrumbs routes={routes} /></div>
      <h1>My App</h1>
      {routesToRender}
    </div>
    )
}
```

## Conclusion
In conclusion, `matchPath` can be used to manually match a path pattern against the current url to build breadcrumbs for the rotues along the path. As a bonus, by extending the `RouteObject` type exposed from React Router 6, you can add capabilities specifc to your applications needs.

There are two requirements I haven't dug into yet in this post. Stay tuned for the follow up posts that will cover these cases:
- Be able to show dynamic breadcrumb title based on parameters.
- Bonus: Support generating Navlinks

I hope you enjoyed this post. Let me know if it's been useful to you, or if you have feedback.