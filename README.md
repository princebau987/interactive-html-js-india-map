# Bharat Atlas — Interactive Map of India for websites and web applications

Bharat Atlas is a responsive interactive map of India with clickable states
and union territories, city markers, search, region filters, zoom and pan,
state details, city details, and reusable website embedding.

View demo video: https://github.com/user-attachments/assets/ac5b872b-4d56-4bc7-b0aa-cdf23462fe6f

# Download
https://prince987.gumroad.com/l/fzzpk

<img width="953" height="452" alt="2_map" src="https://github.com/user-attachments/assets/549756e5-a219-49b1-ad29-56d1d7a106c4" />

## Files

```text
index.html          Full dashboard with hero, map, details, legend, and footer
embed.html          Map-and-details view used for website embeds
css/style.css       Theme and responsive layout styles
js/map-data.js      State/UT boundaries and state information
js/cities-data.js   City information and geographic coordinates
js/app.js           Map rendering and interaction logic
js/bharat-atlas.js  <bharat-atlas> web component wrapper
README.md           This documentation
```

There is no build process. Open `index.html` or `embed.html` directly, or
upload the complete folder to a web host.

## Embed in another website
**Route 1:**
Use `embed.html`

```html
<iframe
  src="https://your-site.example/bharat-atlas/embed.html"
  style="width:100%; height:700px; border:0;"
  title="Interactive India map">
</iframe>
```

**Route 2:**
Add the component script and custom element to any HTML page:

```html
<script
  src="https://your-site.example/bharat-atlas/js/bharat-atlas.js"
  defer>
</script>

<bharat-atlas height="700px" title="Explore India"></bharat-atlas>
```

The component loads `embed.html` in an isolated iframe. This prevents Bharat
Atlas styles, IDs, and event handlers from conflicting with the host website.
It fills the width of its parent, supports multiple instances on one page,
and limits the default height to the available viewport.

### Component attributes

```html
<bharat-atlas
  src="https://your-site.example/maps/custom-india.html"
  height="720px"
  title="Interactive India map">
</bharat-atlas>
```

- `src` — optional URL for a custom hosted map page. By default, the
  component loads `embed.html` next to `bharat-atlas.js`.
- `height` — optional iframe height such as `600px`, `70vh`, or
  `min(900px, 100vh)`.
- `title` — optional accessible title for the embedded map.

Because the component uses an iframe, host-page CSS cannot directly style
elements inside the map. Customize `css/style.css` in the Bharat Atlas copy
or provide your own `src` page.

## Included functionality

- Clickable SVG regions for all 28 states and 8 union territories
- State detail panel with capital, region, overview, known-for tags, and
  featured cities
- Search across states and cities
- Region filters for North, South, East, West, Central, Northeast, and Islands
- Drag-to-pan and scroll-to-zoom
- Zoom in, zoom out, and reset controls
- Toggleable city labels
- Toggleable state labels generated from each SVG region
- City markers with capital/city distinction
- Selected-city highlighting in both the map and featured-city list
- Responsive desktop, tablet, and mobile layouts
- No JavaScript framework or build tool required
- Add new cities to the Map
- Edit existing states/city details

<img width="944" height="419" alt="6_map" src="https://github.com/user-attachments/assets/2df2461e-a1c4-464f-a11b-dedfeb3f7f8a" />

## Customizing state content

Edit `js/map-data.js`. Each state or union territory contains fields such as:

```js
{
  "id": "mh",
  "name": "Maharashtra",
  "capital": "Mumbai",
  "region": "west",
  "famous": ["Gateway of India", "Ajanta & Ellora Caves", "Bollywood"],
  "desc": "Replace this sample description with your own content.",
  "d": "SVG path data — do not edit"
}
```

Edit `capital`, `region`, `famous`, and `desc`. Keep `id`, `name`, and `d`
unchanged unless you are intentionally changing the map data.

## Customizing city data

City markers are listed in `js/cities-data.js`. Geographic coordinates are
stored in the `CITY_LATLON` table using decimal degrees:

```js
"Mumbai": [19.0760, 72.8777]
```

Latitude is north-positive and longitude is east-positive. Add a new city to
the `CITIES` array, then add its coordinates to `CITY_LATLON`:

```js
{
  "name": "Mumbai",
  "state": "Maharashtra",
  "capital": false,
  "tier": 1,
  "blurb": "Replace this sample city description."
}
```

Legacy `x` and `y` values are still supported as a fallback for custom city
entries without latitude/longitude coordinates. New entries should use
`CITY_LATLON`. The map uses a simple India-focused geographic projection to
convert latitude/longitude into the SVG viewBox.

## Editing text in the full dashboard

The full `index.html` dashboard includes an Edit Text control. Enable edit
mode, select editable text, and click away to save. Edited text is stored in
the visitor's browser using `localStorage` under the `bharat-atlas:` prefix.

The map-only `embed.html` view intentionally omits the dashboard edit control.
For permanent changes, edit the data files or customize the HTML directly.

## Theming

The main colors, fonts, radii, shadows, and region colors are CSS variables at
the top of `css/style.css`. Common variables include:

```css
:root {
  --ink-900: #0b0f1e;
  --gold: #c9a24b;
  --marigold: #e3960a;
  --r-north: #c9a24b;
  --r-south: #3f8f7a;
}
```

The stylesheet imports Fraunces, Work Sans, and JetBrains Mono from Google
Fonts. Replace that import with self-hosted fonts if external requests are
not desired.

## Attribution

State and union-territory boundary geometry is adapted from the open-source
[`@svg-maps/india`](https://www.npmjs.com/package/@svg-maps/india) package,
licensed under Creative Commons Attribution 4.0 (CC BY 4.0). Keep the
attribution link in the footer, or include an equivalent credit in any
published or embedded version.

All other HTML, CSS, and JavaScript in this project is available for your own
customization and reuse according to your project license.

## Browser support

Modern Chrome, Edge, Firefox, and Safari are supported. The app uses standard
SVG, CSS custom properties, Web Components, Pointer Events, and localStorage.
No polyfills are included.
