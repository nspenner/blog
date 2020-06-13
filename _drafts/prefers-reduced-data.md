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

`min-width` and `max-width` are common media queries to pair with the `<picture>` element because they allow us to load different images based on the form factor of the user's device. In the pen below, the image swaps to a different one once the width of the window shrinks below 400px.

<p class="codepen" data-height="456" data-theme-id="dark" data-default-tab="html,result" data-user="nathanspenner" data-slug-hash="zYrBNYM" style="height: 456px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Picture element example">
  <span>See the Pen <a href="https://codepen.io/nathanspenner/pen/zYrBNYM">
  Picture element example</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

If we wanted to use `prefers-reduced-data` to minimize our data load, we could use [this technique from a blog post by Mike Masey](https://medium.com/@mike_masey/how-to-use-the-picture-element-to-prevent-images-loading-on-mobile-devices-1376e33b190e) to load a tiny, 1x1 transparent gif instead of a full image:

```html
    <picture>
        <source srcset="https://upload.wikimedia.org/wikipedia/commons/c/ce/Transparent.gif" media="(prefers-reduced-data: reduce)">
        <img src="https://unsplash.com/photos/7hQ4Y_-bSb4/download?force=true&w=640" />
    </picture>
```
The best part about using the `<picture>` element like this is that no request is made to the full image at all, which could quite a bit of data for the user.

We could do something similar to prevent the loading and use of web fonts (this example comes from MDN):

```html
<head>
  <link rel="preload" href="fonts/montserrat-regular.woff2" as="font" media="(prefers-reduced-data: no-preference)" crossorigin>
  <link rel="stylesheet" href="style.css">
</head>
```
```css
@media (prefers-reduced-data: no-preference) {
    @font-face {
        font-family: Montserrat;
        font-style: normal;
        font-weight: 400;
        font-display: swap;
        /* latin */
        src: local('Montserrat Regular'), local('Montserrat-Regular'), url('fonts/montserrat-regular.woff2') format('woff2');
        unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
    }
}

body {
  font-family: Montserrat, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, "Microsoft YaHei", sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}
```