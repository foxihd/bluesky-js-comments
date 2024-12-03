# bluesky-js-comments
Plain JavaScript implementation of Bluesky webpage comments


[https://nicholas.sideras.net/blog/2024/11/26/bluesky-comments-for-hugo-in-plain-javascript](https://nicholas.sideras.net/blog/2024/11/26/bluesky-website-comments-using-just-javascript-for-hugo-blogs-or-anywhere-else/)

This is a quick no-dependancy plain JavaScript version of the Bluesky comments idea popularized this week by [Emily Liu](https://emilyliu.me/blog/comments). My version probably breaks in all sorts of situations.


To use this script, add a `div` tag to your page with an `id` of "comments" and a `data-uri` attribute pointing to the bsky.app post URL. After this div, or at the end of the page `body`, add a `script` tag referencing `bsky-comments.js`.

For example:

```HTML
<div id="comments" data-uri="https://bsky.app/profile/did:plc:tmrrt2lsbtbippdbqky7umi6/post/3lbkaag45us2o" style="width: 600px;"></div>
<script src="bsky-comments.js"></script>
```


In Hugo specifically, I have a `bsky_thread` parameter in the markdown frontmatter params:

```markdown
---
date: '2024-11-26T08:06:35-06:00'
title: 'Bluesky Website Comments Using Just JavaScript (for Hugo Blogs or Anywhere Else)'
author: Nicholas Sideras
bsky_thread: https://bsky.app/profile/nicholas.sideras.net/post/3lbudoukz7c2y
categories:
 - technology
---
```

Then in my template, I check for that value and render the markup:
```HTML
      {{- if .Params.bsky_thread }}
      <h5 style="margin: 2em 0em 1em 0em;">Reply to <a style="text-decoration: underline;" href="{{.Params.bsky_thread}}">this post on Bluesky</a> to leave a comment</h5>
      <div id="comments" data-uri="{{.Params.bsky_thread}}" style="width: 600px; margin-bottom: 2em;"></div>
      <script src="/bsky-comments.js"></script>
      {{ end }}
```
