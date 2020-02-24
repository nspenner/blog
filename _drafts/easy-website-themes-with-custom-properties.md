---
title: Easy Website Themes with CSS Custom Properties
author: Nathan Minchow
layout: post
date: 2020-02-23 06:00:00 +0000

---
With the [advent of dark mode](https://mashable.com/article/dark-mode-apps-instagram-google-chrome-apple-ios13/), website theme customization is becoming an expectation instead of a feature. We even have a [CSS media feature](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme), `prefers-color-scheme`, to tell us if a user wants a light or dark theme.

Plenty of website go a step further and allow their users to select from multiple themes instead (like [dev.to](https://dev.to)):

![](/assets/dev.to_theme_picker.png)

Thankfully, modern CSS has some features that make implementing website customization easy. Most of it boils down to CSS Properties.

# CSS Properties: A Quick Overview

Not long ago, if we wanted to use variables in CSS, we were limited to preprocessors like [Sass](https://sass-lang.com). Preprocessors, while useful for many things, still output standard CSS at the end of the day. This meant that all references to our variables vanished once our CSS was served to the user.

It would be great if we could keep references to our CSS variables with our final output. Thankfully, we can.

[CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*) allow us to define variables in CSS, no preprocessor required. They aren't exactly _new_; [most modern browsers have supported them since 2016](https://caniuse.com/#feat=css-variables).

## How they are different from preprocessor variables

# Overview of Technique