---
title: Let's Look at prefers-reduced-data
author: Nathan Minchow
layout: ''
date: 2020-06-13 16:00:00 +0000

---
I like web fonts. They are an easy way to enable consistent typography and design for a website.

Still, sometimes I wonder if I ought to force my users to download a font (even if it _might_ be cached already) just to view my site. I've encountered plenty of websites that are filled with custom fonts and images that can take quite a while to load. This is especially frustrating when I just want to _read the content_. And while I do my best to minimize the data load on my sites, I still want things to look nice by default.

It would be great if users could indicate that they'd prefer to minimize their data load as they browse the web, potentially at the cost of high-res images or detailed typography. That's where `prefers-reduced-data` comes into play.

`prefers-reduced-data` is a user preference media feature, like `prefers-color-scheme` and `prefers-reduced-motion`. Unlike those, `prefers-reduced-data` is not supported in any browsers yet, and it's functionality could change bit before we see it implemented anywhere.

Curiously, `prefers-reduced-motion`, `prefers-color-scheme`, and `prefers-reduced-data` (among others) were all introduced in the [Media Queries 5 ](https://drafts.csswg.org/mediaqueries-5/) spec from the W3C, but `prefers-reduced-data` has not seen the progress of the other two. There are some [open questions](https://github.com/w3c/csswg-drafts/issues?q=is%3Aissue+is%3Aopen+label%3Amediaqueries-5+prefers-reduced-data) related to the feature which could be slowing it down.

I'm hopeful that we'll see this feature implemented sooner rather than later. The `<picture>` and `<link>` elements both support media queries already, which means we could already account for images, fonts, and libraries without much work. Let's look at a potential method to prevent an image from loading if a user indicated they preferred reduced data.

`min-width` and `max-width` are common media queries to pair with the `<picture>` element because they allow us to load different images based on the form factor of the user's device. So we could a smaller image for mobile users and a larger image for desktop users.

<p class="codepen" data-height="456" data-theme-id="dark" data-default-tab="html,result" data-user="nathanspenner" data-slug-hash="zYrBNYM" style="height: 456px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;.cp_embed_wrapper {
  /* required for resize to work */
  overflow: hidden;

  /* make resizeble! */
  resize: both;

  /* required to see the handle */
  background: white;
  padding-bottom: 10px;

  /* default height */
  height: 400px;
}
.cp_embed_wrapper iframe {
  height: 100% !important;
}" data-pen-title="Picture element example">
  <span>See the Pen <a href="https://codepen.io/nathanspenner/pen/zYrBNYM">
  Picture element example</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>