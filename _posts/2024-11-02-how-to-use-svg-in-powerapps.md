---
layout: post
title:  "How to use SVG in Power Apps"
date:   2024-11-02 20:30:00 -0500
categories: ["Power Apps"]
---
Short post on how to use SVG images in Power Apps, with links to sites that has lots of icons to download/copy.

## Step 1- The Image Control
Add an image control to your Power Apps with this code in the `Image` property

```html
Concatenate("data:image/svg+xml;utf8, ", EncodeUrl("
  <!-- Your SVG Tag here -->
"))
```

## Step 2 - The SVG tag
Copy the SVG tag and replace any double quotes with single quotes, then paste the result in the place mentioned above.
It should look like this:

```html
Concatenate("data:image/svg+xml;utf8, ", EncodeUrl("
  <svg xmlns='http://www.w3.org/2000/svg' width='1em' height='1em' viewBox='0 0 24 24'><rect width='6' height='14' x='1' y='4' fill='#ac23be'><animate id='svgSpinnersBarsScaleFade0' fill='freeze' attributeName='y' begin='0;svgSpinnersBarsScaleFade1.end-0.25s' dur='0.75s' values='1;5'/><animate fill='freeze' attributeName='height' begin='0;svgSpinnersBarsScaleFade1.end-0.25s' dur='0.75s' values='22;14'/><animate fill='freeze' attributeName='opacity' begin='0;svgSpinnersBarsScaleFade1.end-0.25s' dur='0.75s' values='1;0.2'/></rect><rect width='6' height='14' x='9' y='4' fill='#ac23be' opacity='0.4'><animate fill='freeze' attributeName='y' begin='svgSpinnersBarsScaleFade0.begin+0.15s' dur='0.75s' values='1;5'/><animate fill='freeze' attributeName='height' begin='svgSpinnersBarsScaleFade0.begin+0.15s' dur='0.75s' values='22;14'/><animate fill='freeze' attributeName='opacity' begin='svgSpinnersBarsScaleFade0.begin+0.15s' dur='0.75s' values='1;0.2'/></rect><rect width='6' height='14' x='17' y='4' fill='#ac23be' opacity='0.3'><animate id='svgSpinnersBarsScaleFade1' fill='freeze' attributeName='y' begin='svgSpinnersBarsScaleFade0.begin+0.3s' dur='0.75s' values='1;5'/><animate fill='freeze' attributeName='height' begin='svgSpinnersBarsScaleFade0.begin+0.3s' dur='0.75s' values='22;14'/><animate fill='freeze' attributeName='opacity' begin='svgSpinnersBarsScaleFade0.begin+0.3s' dur='0.75s' values='1;0.2'/></rect></svg>
"))
```

## The result
This is how the above svg will look like in Power Apps:
<svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24"><rect width="6" height="14" x="1" y="4" fill="#ac23be"><animate id="svgSpinnersBarsScaleFade0" fill="freeze" attributeName="y" begin="0;svgSpinnersBarsScaleFade1.end-0.25s" dur="0.75s" values="1;5"/><animate fill="freeze" attributeName="height" begin="0;svgSpinnersBarsScaleFade1.end-0.25s" dur="0.75s" values="22;14"/><animate fill="freeze" attributeName="opacity" begin="0;svgSpinnersBarsScaleFade1.end-0.25s" dur="0.75s" values="1;0.2"/></rect><rect width="6" height="14" x="9" y="4" fill="#ac23be" opacity="0.4"><animate fill="freeze" attributeName="y" begin="svgSpinnersBarsScaleFade0.begin+0.15s" dur="0.75s" values="1;5"/><animate fill="freeze" attributeName="height" begin="svgSpinnersBarsScaleFade0.begin+0.15s" dur="0.75s" values="22;14"/><animate fill="freeze" attributeName="opacity" begin="svgSpinnersBarsScaleFade0.begin+0.15s" dur="0.75s" values="1;0.2"/></rect><rect width="6" height="14" x="17" y="4" fill="#ac23be" opacity="0.3"><animate id="svgSpinnersBarsScaleFade1" fill="freeze" attributeName="y" begin="svgSpinnersBarsScaleFade0.begin+0.3s" dur="0.75s" values="1;5"/><animate fill="freeze" attributeName="height" begin="svgSpinnersBarsScaleFade0.begin+0.3s" dur="0.75s" values="22;14"/><animate fill="freeze" attributeName="opacity" begin="svgSpinnersBarsScaleFade0.begin+0.3s" dur="0.75s" values="1;0.2"/></rect></svg>


## Other Links
- [iconify.design - Over 200k icons](https://icon-sets.iconify.design/)
- [iconify.design - Spinners](https://icon-sets.iconify.design/svg-spinners/)
- [Flicon - Fluent UI icons](https://www.flicon.io/)
