---
title: Easy Website Themes with CSS Custom Properties
author: Nathan Minchow
layout: post
date: 2020-03-07 06:00:00 +0000

---
With the [advent of dark mode](https://mashable.com/article/dark-mode-apps-instagram-google-chrome-apple-ios13/), website theme customization is becoming an expectation instead of a feature.

Plenty of websites go a step further and allow their users to select from multiple themes (like [dev.to](https://dev.to)):

![](/assets/dev.to_theme_picker.png)

Full website theme customization may be overkill for some sites, but it's still something we ought to keep in mind when designing and developing for the web. Thankfully, modern CSS includes features that make implementing website customization easy. Most of it boils down to CSS Custom Properties.

# CSS Properties: A Quick Overview

[CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*) allow us to define reusable variables in CSS without a preprocessor. They aren't exactly _new_; [most modern browsers have supported them since 2016](https://caniuse.com/#feat=css-variables). And since they are variables, we can update them dynamically.

Custom Properties can be defined on any element by prefixing the property name with `--`. If we wanted to create reusable properties on the `root` element, we could define them like so (these examples are taken from [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/--*)):

```css
:root {
  --first-color: #488cff;
  --second-color: #ffff8c;
}
```

We can access these properties in child elements via the `var()` keyword:

```css
#firstParagraph {
  background-color: var(--first-color);
  color: var(--second-color);
}

#secondParagraph {
  background-color: var(--second-color);
  color: var(--first-color);
}

#container {
  --first-color: #48ff32;
}
```

To see this in action, I've defined three different colors in the example below. When the checkbox is toggled, the CSS properties update and colors change wherever they are referenced:

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="result" data-user="nathanspenner" data-slug-hash="LYVxpjP" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Custom Property Update No JS">
<span>See the Pen <a href="https://codepen.io/nathanspenner/pen/LYVxpjP">
Custom Property Update No JS</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Custom Properties can do a lot of useful things. I recommend reading [this excellent article](https://www.smashingmagazine.com/2018/05/css-custom-properties-strategy-guide/) by Michael Riethmuller for a more in-depth look at CSS Custom Properties, how to use them, and how they differ from preprocessor variables.

# Theme Customization Use Cases

Since Custom Properties can be reused and updated dynamically, they are a good fit for theme customization. Let's look at how we can use Custom Properties to customize a site.

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

The code for the theme switch is very similar to the CodePens above. I define a couple "Theme" objects in my Javascript:

```js
const darkTheme = {
  "--accent-color": "#4acaa8",
  "--background-color": "#343737",
  "--active-scroll-background": "#343737",
  "--color-text": "white",
  "--sidebar-color": "#444c48"
};
    
const lightTheme = {
  "--accent-color": "#4bcdab",
  "--background-color": "#f0ffff",
  "--active-scroll-background": "#f0ffff",
  "--color-text": "#777",
  "--sidebar-color": "#4bcdab"
};
```

Then, when the toggle button is pressed, I update the Custom Properties I've defined on the root element with properties from a given "Theme":

```js
function applyTheme(theme) {
  let root = document.documentElement;
  root.style.setProperty("--accent-color", theme["--accent-color"]);
  root.style.setProperty("--background-color", theme["--background-color"]);
  root.style.setProperty(
    "--active-scroll-background",
    theme["--active-scroll-background"]
  );
  root.style.setProperty("--color-text", theme["--color-text"]);
  root.style.setProperty("--sidebar-color", theme["--sidebar-color"]);
}
```

Feel free to take a look at the preview [here](https://nspenner.github.io/theme-lab/), with the source code available [here](https://github.com/nspenner/theme-lab).

By implementing theme customization like this, adding a new theme to the site is as simple as creating a new theme object. We could save a user's preference via [local storage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) or a database depending on what tools we have available.

## Custom Color Selection

Some websites and apps allow users to create and modify themes directly. Once again, we can use `setProperty()` to update a Custom Property with any value, including ones exposed for input.

In the Codepen below, the colors of the first square and the borders of all squares are exposed as input elements. When the form is submitted, these values are updated and are reflected in the result:

<p class="codepen" data-height="357" data-theme-id="dark" data-default-tab="result" data-user="nathanspenner" data-slug-hash="yLNPExq" style="height: 357px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Javascript Style Updates Custom Selection">
<span>See the Pen <a href="https://codepen.io/nathanspenner/pen/yLNPExq">
Javascript Style Updates Custom Selection</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Naturally, we could extend this to expose the various properties used on an entire website or application. Those preferences could then be exported or saved to remember a user's choice (or to allow users to share themes). 

# Conclusion

Custom Properties allow us to make sweeping changes to our website without much work. This makes them a great tool for implementing theme customization, whether for automatically detecting a user's theme preference with `prefers-color-scheme` or allowing them to pick (and potentially modify) their own themes.