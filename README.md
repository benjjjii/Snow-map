# Europe Snow Map

A zoomable map of current snow depth across Europe, built as a single static page (`index.html`).

- **Data:** [Open-Meteo DWD ICON API](https://open-meteo.com/en/docs/dwd-api) (`current=snow_depth,temperature_2m`). Over Europe this is ICON-EU at about 7 km resolution. No API key needed.
- **Map:** [Leaflet](https://leafletjs.com/) with CARTO light basemap tiles. Place labels are drawn on top of the snow layer.

## How it works

- The page samples a grid of points across the current view and fetches them in batches of 100 locations per request.
- The grid gets finer as you zoom in: about 2.5° for all of Europe, down to 0.0625° (roughly the ICON-EU grid) when zoomed in close.
- Values are bilinearly interpolated into a Web-Mercator image overlay. The colour bands run from 1 cm to more than 2 m.
- Click anywhere on the map for that exact point's snow depth, temperature and model elevation.
- Readings are cached in `localStorage` for the current hour, so panning back or reloading doesn't refetch data.

## Free API limits

Open-Meteo's free tier allows about 600 locations per minute and 10,000 per day. To stay within that, each view is capped at 500 points. If you pan and zoom a lot, you may briefly see a rate-limit message. Wait a minute and it will resume.

## Run

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
```

You can also host it on GitHub Pages.
