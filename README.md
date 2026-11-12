# Image Isometric

An infinite, scroll-driven photo gallery rendered with WebGL. Cards ride a horizontal track that skews, bends and ripples with scroll speed, and the whole gallery can morph into an isometric staircase. Hover a card to lift it; click it to make it jump and flip.

## Features

- **Infinite horizontal scroll** — mouse wheel / trackpad or the arrow keys, smoothed with GSAP.
- **Velocity effects** — shear, drag bend, ripple, RGB split and vignette, all driven by scroll speed in custom shaders.
- **Flat ↔ isometric view** — the button at the bottom tweens every card from a flat row into a slanted staircase.
- **Hover lift** — the card under the cursor rises with an ease-out.
- **Click to jump & flip** — the hovered card jumps up and spins around its vertical axis, then lands back at its hover position. In isometric view it swings round through the mirrored slant like a real 3D turn.
- **Live tuning panel** — every parameter is exposed in a [DialKit](https://www.npmjs.com/package/dialkit) panel (top right). Values persist in `localStorage`; use the panel's copy button to export them.

## Run it

It's a single static page, so any static file server works:

```bash
npx http-server . -p 5173 -c-1
```

Then open http://localhost:5173.

Opening `index.html` directly from disk won't work, because the browser blocks loading textures over `file://`.

## Tuning

| Panel section | Highlights |
|---|---|
| **motion** | max skew, scroll / skew smoothing, wheel speed |
| **shader** | bend, ripple, RGB shift, vignette |
| **isometric** | staircase step, card shear and scale, transition time |
| **hover** | lift, hover duration, flip duration / angle / direction / ease, jump height |
| **layout** | rows, gaps, stagger, corner radius, background |

Flip angles that are multiples of 180° land cleanly; other angles snap back at the end.

> Code defaults only apply when nothing is saved. If a change to a default in `index.html` doesn't show up, reset the panel or clear the `dialkit:gallery` key in `localStorage`.

## Project layout

```
index.html        page, shaders and all the gallery logic
photos/           the 14 gallery images (01.jpg – 14.jpg)
vendor/dialkit/   browser build of DialKit (tuning panel)
```

three.js (0.170.0) and GSAP (3.12.5) load from CDNs. `node_modules` is only the source the DialKit build was copied from and isn't needed at runtime.

## Tech

- [three.js](https://threejs.org/): orthographic camera in CSS pixels, one `ShaderMaterial` per card
- [GSAP](https://gsap.com/): scroll smoothing, view transition, hover and flip timelines
- [DialKit](https://www.npmjs.com/package/dialkit): live parameter panel
