# killua15.github.io

Personal portfolio site for David Lopez — Senior Mobile Engineer.
Live at **https://killua15.github.io**

Plain static HTML: no framework, no build step, no dependencies. Push to `main` and GitHub Pages publishes it within a couple of minutes.

## Layout

```
index.html      the whole page — styles and scripts inline, icons as an inline SVG sprite
assets/         app icons and store screenshots (JPEG)
cv.pdf          CV linked from the header button
robots.txt      indexing allowed: recruiters should be able to find this by name
.nojekyll       skip Jekyll processing — the HTML is already final
```

## Editing

Open `index.html` and edit it directly. The page is organised as seven numbered sections — Profile, Capabilities, Technology, Experience, Projects, Education & Languages, Contact — and the CSS at the top is grouped with the same headings.

Colours, spacing and fonts come from custom properties on `:root`, with the dark palette redefined in two places: a `prefers-color-scheme` block for viewers on system default, and a `[data-theme="dark"]` block so the header toggle wins. Change a colour in all three or it will only apply to one theme.

## Assets

App icons and screenshots were downloaded from the official store listings (Apple's iTunes Lookup API and Google Play), resized to 256px for icons and 800px wide for screenshots. They are the real current listings, not mockups.

To refresh a screenshot after an app updates:

```bash
curl -s "https://itunes.apple.com/lookup?id=<APP_ID>&country=<CC>" | python3 -m json.tool
# take a screenshotUrls entry, swap the trailing /392x696bb.png for /800x0w.png
sips -s format jpeg -s formatOptions 70 shot.png --out assets/<name>.jpg
```

## Adding the portrait

The Profile section currently shows a "DL" monogram. To use a photo, drop it at `assets/portrait.jpg` and replace the monogram element in `index.html`:

```html
<!-- from -->
<span class="monogram">DL</span>
<!-- to -->
<img src="assets/portrait.jpg" alt="David Lopez">
```

The frame crops to a 4:5 portrait with `object-fit: cover`, so any reasonably centred photo works.

## Custom domain

Add a `CNAME` file containing the bare domain, then point the DNS at GitHub:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

GitHub keeps `killua15.github.io` redirecting to the new domain, so existing links stay valid.
