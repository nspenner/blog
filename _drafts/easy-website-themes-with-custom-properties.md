---
title: Easy Website Themes with CSS Custom Properties
author: Nathan Minchow
layout: post
date: 2020-02-23 06:00:00 +0000

---
With the [advent of dark mode](https://mashable.com/article/dark-mode-apps-instagram-google-chrome-apple-ios13/), website theme customization is becoming an expectation instead of a feature.

Plenty of websites go a step further and allow their users to select from multiple themes (like [dev.to](https://dev.to)):

![](/assets/dev.to_theme_picker.png)

Full website theme customization may be overkill for some sites, but it's still something we ought to keep in mind when designing and developing for the web. Thankfully, modern CSS includes features that make implementing website customization easy. Most of it boils down to CSS Custom Properties.

# CSS Properties: A Quick Overview

[CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*) allow us to define reusable variables in CSS without a preprocessor. They aren't exactly _new_; [most modern browsers have supported them since 2016](https://caniuse.com/#feat=css-variables). And since they are variables, we can update them dynamically.

To see this in action, I've defined three different colors in the example below. When the checkbox is toggled, the CSS properties update and colors change wherever they are referenced:

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="result" data-user="nathanspenner" data-slug-hash="LYVxpjP" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Custom Property Update No JS">
<span>See the Pen <a href="https://codepen.io/nathanspenner/pen/LYVxpjP">
Custom Property Update No JS</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Custom Properties can do a lot of useful things. While this article is focused on theme customization, I'd recommend reading [this excellent article](https://www.smashingmagazine.com/2018/05/css-custom-properties-strategy-guide/) by Michael Riethmuller for a more in-depth look at CSS Custom Properties, how to use them, and how they differ from preprocessor variables.

# Using Custom Properties on a Page

# Customization Use Cases

## Implementing Dark Mode

The most straightforward way to add a dark mode to your site is via the [`prefers-color-scheme`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) media query. This media query typically corresponds to the theme of the user's operating system.

So, if we have some scoped properties defined like so:

```css
    main {
      --primary-color: cyan;
      --secondary-color: orange;
      --tertiary-color: yellow;
    }
```

We can simply update their values in the media query:

```css
    @media (prefers-color-scheme: dark) {
      main {
        --primary-color: gray;
        --secondary-color: darkgray;
        --tertiary-color: lightgray;
      }
    }
```

And any elements using those properties will update dynamically when the user's theme changes. Here's how that might look in practice:

![](/assets/prefers_color_scheme.gif)

## Custom Theme Selection

While `prefers-color-scheme` is a great starting point, sometimes we want to give the user the ability to select a theme at will.

If you've designed your site to take advantage of Custom Properties, we can accomplish this fairly easily. All we need to do is modify them, which we can do via CSS or Javascript.

### Modify Custom Properties with CSS

Custom Properties, like any other CSS, can be updated as long as we have the proper selector.

If you examine the CSS from my earlier example, you'll notice that I've scoped my Custom Properties to the `main` element. When the checkbox is toggled, a selector updates the scoped properties inside it. This causes all elements within the `main` element to update with the new values:

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="nathanspenner" data-slug-hash="LYVxpjP" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Custom Property Update No JS">
<span>See the Pen <a href="https://codepen.io/nathanspenner/pen/LYVxpjP">
Custom Property Update No JS</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

While this method is pretty quick to implement, CSS selectors can be somewhat fickle (and dependent on our HTML). Furthermore, in most cases we'd want to save a user's theme choice. Javascript gives us more flexibility.

### Modify Custom Properties with Javascript

We can use the [`setProperty()` method](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration/setProperty) to update our Custom Properties from Javascript.

If we have some Custom Properties scoped to a `main` element, we can query for it in our Javascript and call `setProperty()` to update its properties to new values:

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="js,result" data-user="nathanspenner" data-slug-hash="zYGEVGx" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Javascript Style Updates">
<span>See the Pen <a href="https://codepen.io/nathanspenner/pen/zYGEVGx">
Javascript Style Updates</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

It's common to see Custom Properties defined in the `:root` pseudo-class. In that case, the Custom Properties can be updated by calling `setProperty` on the root element:

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="js,result" data-user="nathanspenner" data-slug-hash="QWbqXKY" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Javascript Style Updates Root">
<span>See the Pen <a href="https://codepen.io/nathanspenner/pen/QWbqXKY">
Javascript Style Updates Root</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

While those examples only altered a few `div` elements, the same technique can be used to alter the theme for an entire site. To demonstrate this, I modified [a template from HTML5UP](https://html5up.net/read-only) to use Custom Properties for most backgrounds, text colors, and accents. Then, I added a toggle button that updates those properties with dark values instead:

![](/assets/theme_demo.gif)

## Custom Color Selection