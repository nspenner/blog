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

For example, I've defined three different colors below. When the checkbox is toggled, the CSS properties update and colors change wherever they are referenced:

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="nathanspenner" data-slug-hash="LYVxpjP" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Custom Property Update No JS">
<span>See the Pen <a href="https://codepen.io/nathanspenner/pen/LYVxpjP">
Custom Property Update No JS</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Custom Properties can do a lot of useful things. While this article is focused on theme customization, I'd recommend reading [this excellent article](https://www.smashingmagazine.com/2018/05/css-custom-properties-strategy-guide/) by Michael Riethmuller for a more in-depth look at CSS Custom Properties, how to use them, and how they differ from preprocessor variables.

# Using Custom Properties on a Page

# Customization Use Cases

## Implementing Dark Mode

The most straightforward way to add dark mode to your site is via the [`prefers-color-scheme`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) media query. This media query typically corresponds to the theme of the user's operating system.

So, if we have some properties defined like so:
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
And any elements using those properties will update dynamically. Here's how that might look in practice:

![](/assets/prefers_color_scheme.gif)

## Custom Theme Selection

## Custom Color Selection