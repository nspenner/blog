---
title: "Gradient Element Backgrounds with Psuedo-Elements"
author: "Nathan Minchow"
layout: "post"
---

Recently, I was playing around with some web site mockups and came up with the following idea for a simple todo list app:

![Todo App Mockup](/assets/my-do-mockup.png "Todo App Mockup with Gradient Background Behind Todo Items")

I really liked the idea of using a consistent gradient that persisted across the todo list.

In order to accomplish the effect, I took use of [CSS Pseudo-Elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements). Behind the todo list is a simple gradient:

<p class="codepen" data-height="351" data-theme-id="0" data-default-tab="css,result" data-user="nathanspenner" data-slug-hash="bGGrLay" style="height: 351px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Gradient Todo Background Only">
  <span>See the Pen <a href="https://codepen.io/nathanspenner/pen/bGGrLay">
  Gradient Todo Background Only</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Each todo item is given a transparent background, and a pseudo-element spanning the width of the element with a white background is placed after each item:

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="css,result" data-user="nathanspenner" data-slug-hash="ZEEKMYN" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Gradient Todo">
  <span>See the Pen <a href="https://codepen.io/nathanspenner/pen/ZEEKMYN">
  Gradient Todo</a> by Nathan Minchow (<a href="https://codepen.io/nathanspenner">@nathanspenner</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

This helps with the illusion that there's a natural transparent gap between the items. If you were using this in an actual app, you'd probably want to use a custom property to keep the color of the pseudo-elements and the background in sync.

But that's about it! Nothing too special -- just a neat use case where pseudo-elements made a somewhat tricky sounding task fairly easy.