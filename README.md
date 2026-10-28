<div align="center">

# 🌊 ocean · world map

**A hand-drawn, anime-flavoured world map where little waves roll in, ships drift by, and a friend waves hello from Bangladesh.**

<br>

![HTML](https://img.shields.io/badge/HTML-single_file-3ec8cf?style=for-the-badge&labelColor=0b3a57)
![D3](https://img.shields.io/badge/d3-v7-93c66b?style=for-the-badge&labelColor=0b3a57)
![No build](https://img.shields.io/badge/build_step-none-f6e7b4?style=for-the-badge&labelColor=0b3a57)
![Data](https://img.shields.io/badge/Natural_Earth-1:50m-ffffff?style=for-the-badge&labelColor=0b3a57)

<br>

<img src="map.png" alt="ocean world map preview" width="860">

</div>

---

## ✨ What is this?

An interactive world map drawn entirely with SVG, a pinch of CSS and zero image files. The coastline is pixel-exact (Natural Earth 1:50m), but it's rendered with a soft, hand-drawn wobble and a palette of sea-glass teal, foam white and warm sand.

It's one HTML file. Open it and the ocean comes alive.

## 🏖️ Features

| | |
|---|---|
| 🗺️ **Exact coastlines** | Every country is drawn from real Natural Earth 1:50m data using the Natural Earth projection. |
| 🌊 **Cartoon surf waves** | Every so often a wave rises out of the open sea, rolls toward the shore and breaks into foam. Then the sea goes calm, and the next wave appears somewhere else along the coast. |
| 🚢 **Sailing ships** | Eight little cargo ships and sailboats cruise slow routes across the oceans. They bob on the water, leave white wakes and fade in and out at the ends of their routes. |
| 🧑 **Ahanaf, based in Bangladesh** | A pure-CSS avatar floats in the Indian Ocean with an animated arrow pointing at Bangladesh. He blinks, and if you hover or press his nose or face, he reacts. |
| 🏝️ **Layered shoreline** | Shallows, foam, sand and dune rings are grown outward from the coast and gently breathe like surf. |
| 🖱️ **Hover any country** | Countries light up with a soft white glow and a name tooltip follows your cursor. |
| 🌿 **Tinted land** | Each country gets its own subtle shade of green, picked deterministically from its name. |
| 📱 **Responsive** | The map, ships and avatar all scale with the container. |
| ♿ **Motion-friendly** | If `prefers-reduced-motion` is on, the animations freeze into a calm still frame. |

## 🚀 Quick start

No install, no bundler, no `npm`.

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

Then either **double-click `world-map-precise.html`**, or serve it locally:

```bash
python3 -m http.server 8000
# open http://localhost:8000/world-map-precise.html
```

> **Heads up:** the map loads `d3`, `topojson-client` and the country data from the jsDelivr CDN, so you need an internet connection the first time it loads.

## 🎛️ Make it yours

Everything lives in `world-map-precise.html`.

**🎨 Colors**: change the CSS variables on `.ocean-backdrop`:

```css
--ocean-deep: #0b3a57;
--shallow:    #3ec8cfb1;
--foam:       #ffffffa3;
--sand:       #f6e7b4;
--land:       #93c66b;
```

**🌊 Waves**: in `buildWaves()`:

| Setting | What it does |
|---|---|
| `waves = [{ dur: 14 }, { dur: 19 }]` | How many waves run, and how long each cycle lasts. A longer `dur` gives longer calm gaps. |
| `OUT` / `IN` | How far out a wave starts and how thick its foam crest is. |
| `r: 230` (the spotlight circle) | How wide a stretch of coast one wave covers. |
| `layers` | Colors and dashes of the wave body, outline and foam. |

**🚢 Ships**: add or edit routes in `buildShips()` using plain `[longitude, latitude]` pairs:

```js
{ a: [-56, 36], b: [-14, 41], hull: "#d9534f", type: "cargo", dur: 70, begin: -10 }
```

`type` is `"cargo"` or `"sail"`. `dur` is the seconds one crossing takes.

**🧑 The avatar**: in `buildAvatar()`:

```js
var S  = 0.27;           // size relative to a 1600px-wide map
var bd = projection([90.3, 23.8]);   // where the arrow points (Bangladesh)
var an = projection([86, -9]);       // where the avatar floats
```

To change the label, edit the `.tag` markup inside `<template id="avatarTpl">`.

## 🧩 How it works

```
countries-50m.json ──► topojson ──► d3.geoNaturalEarth1 ──► one merged land path
                                                             │
        ┌────────────────────────────────────────────────────┤
        ▼                                                    ▼
 shore rings (shallow → foam → sand → dune)           land fill + clip
   widened strokes on the exact coastline            dark core, light edge
        │
        ▼
 surf waves = masks whose stroke-widths animate
   (a thin ridge far out ➜ thickens ➜ hits the coast ➜ splash ➜ fades)
        │
        ▼
 ships (animateMotion) · avatar (HTML/CSS overlay) · country hover layer
```

The trick behind the waves: a stroke centred on the coastline has a width of `2 × distance from shore`. Animating that width from large to small makes a band glide toward the beach, with no extra geometry needed. An SVG displacement filter adds the hand-drawn wobble.

## 🗂️ Project structure

```
.
├── world-map-precise.html   # the whole app: markup, styles, scripts
├── map.png                  # preview image used in this README
└── README.md
```

## 🙏 Credits

- **[Natural Earth](https://www.naturalearthdata.com/)**: public-domain map data
- **[world-atlas](https://github.com/topojson/world-atlas)**: Natural Earth data packaged as TopoJSON
- **[D3](https://d3js.org/)** and **[topojson-client](https://github.com/topojson/topojson-client)**: projection and geometry

## 📜 License

Released under the [MIT License](LICENSE). Feel free to fork it, remix it and sail your own ships across it. (Add a `LICENSE` file, or swap this line for the license you prefer.)

<div align="center">

<br>

made with 🌊 salt, foam and a little bit of CSS

**Ahanaf** · based in Bangladesh 🇧🇩

</div>
