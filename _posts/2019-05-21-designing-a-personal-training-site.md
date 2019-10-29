---
title: "Custom Shadows with Clip-Path"
author: "Nathan Minchow"
layout: "post"
---

I recently designed a static website for a personal trainer, and (with his permission) I thought it would be fun to write a post about a particular challenge I encountered while developing it.

I wanted to place a few images with slanted borders throughout the site. Additionally, I wanted a shadow effect on the slanted border to give them depth.

This idea posed some difficulties. First I needed to actually create the slant; this turned out to be pretty easy by using the `clip-path` property to clip the images into polygons (I'd recommend Firefox's clip-path editor to help draw these out). 

Now I needed to make sure that the image actually fit inside its unusual shape. `object-fit` helped make sure the images looked nice inside of their respective polygons. Adding a shadow to the slant was more difficult. 

`box-shadow`, as the name would imply, typically only applies shadows to box-shaped elements. I found a couple blog posts that mentioned the technique of using `clip-path`, `filter`, and `drop-shadow` together to give a custom shape its own box shadow. The trick was to apply a filtered drop shadow on the parent of the clipped element, like so:

```css
#parent {
  filter: drop-shadow(3px 0px 6px rgba(0, 0, 0, 0.3));
}

#child {
  clip-path: polygon(100% 0%, 60% 100%, 0% 100%, 0% 0%);
}
```

I tried to incorporate this technique into my own design, with the following disastrous result:

![Incorrect Drop Shadow](/assets/2019-05-21-designing-a-personal-training-site/bad-drop-shadow.png "Drop Shadow Applied to Entire Child Element")

It turned out that applying a `background-color` to the parent element caused the drop-shadow to extend to the edges of the element. Removing the `background-color` property from the parent element resolved the issue (I simply added another element above the parent with the `background-color` instead):

![Correct Drop Shadow](/assets/2019-05-21-designing-a-personal-training-site/good-drop-shadow.png "Drop Shadow Applied to Clipped Child Element")

In the end, the CSS for most of the slanted images looked something like this:

```css
#superparent {
  background-color: var(--primary);
}

#parent {
  width: 100%;
  height: 100%;
  filter: drop-shadow(3px 0px 6px rgba(0, 0, 0, 0.3));
}

#child-image {
  object-fit: cover;
  width: inherit;
  height: inherit;
  clip-path: polygon(100% 0%, 60% 100%, 0% 100%, 0% 0%);
}
```

And with that, it worked beautifully! I used this same technique to create a few other slanted image effects: 

![Other Shadows](/assets/2019-05-21-designing-a-personal-training-site/other-shadows.png "Other Shadows")

I use shadows frequently to add depth to a design and to make elements pop. Using `clip-path` and `filter` to extend shadows to custom shapes seems like a particularly powerful tool, and I'm eager to use it elsewhere (just note that browser support is still a _little_ iffy!).

For further reading:

- https://css-tricks.com/using-box-shadows-and-clip-path-together/
- https://developer.mozilla.org/en-US/docs/Web/CSS/clip-path
- https://developer.mozilla.org/en-US/docs/Web/CSS/filter