# Square Kufic Plate

A single-page web app that sets Arabic text, typically Quran verses, in square Kufic (كوفي مربع) on a square plate, then exports it for 3D printing.

Open `index.html` in a browser. There is no build step and nothing to install.

## What it does

- **Grid lettering:** every stroke and every gap is exactly one cell.
- **Cleans the text:** harakat, Quranic annotation marks and verse numbers are removed automatically.
- **Flush edges:** every line is stretched with kashida (joins, bowls and tails) until it touches both sides of the square.
- **Rising stems:** alef and lam at the start of a lower line rise to the top edge.
- **Filled space:** short letters grow to fill the line, and alef/lam bend over short neighbours.
- **No filler:** only written words appear, never decoration.

### Arrangements

| Arrangement | Description |
| --- | --- |
| **Stacked** | Lines fill the square edge to edge. The first line can sit at the bottom or at the top. |
| **Spiral** | Text runs upright along the bottom and turns 90° at each corner, winding inward. The last words fill the centre. |
| **Four-fold** | The phrase is written on all four sides and again in the centre. |

Any arrangement can be turned 45° into a diamond.

## Plate and export

- **Plate:** 195 × 195 mm by default, with an adjustable margin and an optional border.
- **SVG:** true-size vector, in millimetres.
- **PNG:** 150, 300 or 600 dpi, with the physical size stored in the file.
- **STL:** a closed solid, with one of three model styles:

| Style | Result |
| --- | --- |
| Raised | Letters stand on the plate (5 mm plate and 2 mm relief by default). |
| Engraved | Letters are cut into the plate. |
| Letters only | Only the letters, extruded to the plate thickness. |

## Code layout

Everything is in `index.html`:

- `RAW`: the glyph patterns, one string per letter form (`#` stroke, `.` empty).
- `renderBand`: lays one line on the grid (kashida, bent stems, letter growth, dots).
- `stackFit` / `layoutStacked`: the stacked composition.
- `layoutRings`: the spiral and four-fold compositions.
- `makeSVG`, `makePNG`, `makeSTL`: the exports.
