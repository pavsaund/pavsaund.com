---
layout: blog
draft: false
title: Tagged template literals - How the gql`query` syntax works
date: 2020-10-26T21:58:26.789Z
coverSize: partial
thumbnailImagePosition: ""
tags:
  - javascript
  - graphql
  - typescript
  - ""
categories:
  - DevDiary
---
When exploring some graphql I stumbled over it's quite special syntax for defining a query ``gql`query` `` . Now this seemed like a nice shorthand way of expressing an inline query, but I just couldn't understand which construct made this possible. Typescript? Ecmascript 2016? Or maybe some other feature?

Here's an example of a graphql query:

```typescript
import gql from 'graphql-tag';

const query = gql`
  query {
    products {
      id,
      productNumber,
      facilityName,
      description
    }
  }
`;
```

As you see we're importing the default `gql` export from graphql-tag and using it directly when definfing a query.

Then we're appending a [template literals/strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals "https\://developer.mozilla.org/en-us/docs/web/javascript/reference/template_literals") to the import and defining a query to be executed. I've omitted the code to actually execute the query, but that isn't important for this example.

The typescript syntax declaration looks like this:


```typescript
declare module "graphql-tag" {
  function gql(
    literals: ReadonlyArray<string> | Readonly<string>,
    ...placeholders: any[]
  ): import("graphql").DocumentNode;

```


Which means that `gql` is a function with two parameters.

1. A readonly array of strings or a readonly string
2. Any number of placeholders (deconstructed array)

But why aren't we calling `gql` in our example above like a function, like this?

```typescript
import gql from 'graphql-tag';
const query = gql(`
  query {
    products {
      id,
      productNumber,
      facilityName,
      description
    }
  }
`);

```


That's because of a neat feature in Javascript template literals called [Tagged template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_templates "https\://developer.mozilla.org/en-us/docs/web/javascript/reference/template_literals#tagged_templates"). What this means is that a function with the first parameter as a string, and subsequent parameters as arguments, can parse a string literal with template arguments. It can then do logic on the args as it sees fit.

Here's the [example from MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_templates):

```typescript
let person = 'Mike';
let age = 28;
function myTag(strings, personExp, ageExp) {
 /*Omitted - full example on MDN*/
}

let output = myTag`That ${ person } is a ${ age }`;
```


So, without digging too much further into details and caveats, this is how graphql can be written as ``gql`query with ${parameters}` ``.