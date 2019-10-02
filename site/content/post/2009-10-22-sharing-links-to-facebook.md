---
author: pavsaund
categories:
- DevDiary
date: "2009-10-22T22:41:06Z"
guid: http://pavsaund.wordpress.com/?p=71
id: 71
tags:
- facebook
- how to
- social media
title: Sharing links to Facebook
url: /2009/10/22/sharing-links-to-facebook/
---

<img class="size-full wp-image-72 alignright" title="sharetofacebook" src="/wp-content/uploads/2009/10/untitled.png" alt="sharetofacebook" width="186" height="57" />

Need to spread the word on your latest blog-post or article? Look no further than the Facebook sharer! Facebook has over 300 million users world-wide, and the chances are good that you can recruit readers. Adding a "share to facebook" icon easily allows your readers to spread YOUR word. This can be accomplished by using plugins for your blog-service, or "share-all" widgets like <a href="http://www.addthis.com/" target="_blank">AddThis</a> or <a href="http://sharethis.com/" target="_blank">ShareThis</a>. The problem with these services, are that they over-complicate the simple share functionality that's often wanted. That's where implementing specefic Facebook-share functionality comes in very handy.
<h3>The Facebook sharer</h3>
Facebook has a large <a href="http://wiki.developers.facebook.com/index.php/Main_Page" target="_blank">development community</a> that uses its extensive API to publish applications, and advanced Facebook features on their sites. The simplest way to spread the word is the basic <a href="http://www.facebook.com/share_partners.php" target="_self">facebook sharer-url.</a>
<blockquote>http://www.facebook.com/sharer.php?</blockquote>
By visiting the <a href="http://www.facebook.com/share_partners.php" target="_self">facebook-sharer</a> page, you can get code to copy/paste into your site to enable sharing fast and simple. All you need to do is choose the desired look of your link, and copy the accompanying code-snippet.

Facebook provides  4 options here:
<ul>
<li><a href="/wp-content/uploads/2009/10/fbshare_icon.png"><img class="alignnone size-full wp-image-77" title="fbshare_icon" src="/wp-content/uploads/2009/10/fbshare_icon.png" alt="fbshare_icon" width="14" height="14" /></a></li>
<li><a href="/wp-content/uploads/2009/10/fbshare_text.png"><img class="alignnone size-full wp-image-80" title="fbshare_text" src="/wp-content/uploads/2009/10/fbshare_text.png" alt="fbshare_text" width="94" height="14" /></a></li>
<li><a href="/wp-content/uploads/2009/10/fbshare_icontext.png"><img class="alignnone size-full wp-image-78" title="fbshare_icontext" src="/wp-content/uploads/2009/10/fbshare_icontext.png" alt="fbshare_icontext" width="111" height="14" /></a></li>
<li><a href="/wp-content/uploads/2009/10/fbshare_javascript.png"><img class="alignnone size-full wp-image-79" title="fbshare_javascript" src="/wp-content/uploads/2009/10/fbshare_javascript.png" alt="fbshare_javascript" width="55" height="18" /></a></li>
</ul>
<h3></h3>
<h3>Linking to the sharer</h3>
The sharer accepts 2 parameters when passing in the URL to share. Remember that each variable has to be <a href="http://en.wikipedia.org/wiki/Url_encoding" target="_blank">encoded</a>. Refer to the script provided by Facebook for the exact code for this.
<ul>
<li>u=</li>
<li>t=</li>
</ul>
This would give the following url
<blockquote><a href="http://www.facebook.com/sharer.php?u=http%3A%2F%2Fpavsaund.wordpress.com%2F2009%2F10%2F22%2Fsharing-links-to-facebook%2F&amp;t=Sharing%20links%20to%20Facebook" target="_blank">http://www.facebook.com/sharer.php?<strong>u=</strong>http://pavsaund.wordpress.com/2<span id="sample-permalink">009/</span><span id="sample-permalink">10</span>/<span id="sample-permalink">22/</span><span id="sample-permalink"><span id="editable-post-name" title="Click to edit this part of the permalink">sharing-links-to-facebook/</span></span><strong>&amp;t=</strong>Sharing links to Facebook</a></blockquote>
<h3></h3>
<h3>Help the sharer with !</h3>
The sharer-bot does a crawl of the url sent in, and extracts the <strong>title</strong>, <strong>page content</strong> and <strong>relevant images</strong>. The bot does this based on it's own algorithm, and usually this works just fine. The problem occurs when you share a page filled with content and images that may confuse the bot. In these cases, the bot may share the wrong picture or unrelated content.

If you want to control exactly what's shared then you need to include the following meta tags in your page's head.
<blockquote>



</blockquote>
This way, you control exactly what the reader shares from your page. Consider also adding your blog-info in the content, as this rarely gets picked up by the bot (since this is reserved for the end of an article or a separate page)

<strong>A few things to keep in mind</strong>

The meta names <strong>title </strong>and <strong>description </strong>have to be lowercased for the bot to pick them up. Other wise it seemingly ignores them.

The facebook sharer states that when using meta tags, the minimum tags to include are title and description, otherwise metatags are ignored.

Beware when sharing sites with dynamic content linked to a static url. Facebook caches all pages it crawls and may store this cache for several weeks. This may also cause problems for sites with dynamic url, as it seems Facebook my have old DNS lookups cached.
<h3>Rounding up..</h3>
I hope this post is of some value to you. Feedback is always welcome!