# Square Kufic Plate

A single-page web app that sets Arabic text, typically Quran verses, in square Kufic (كوفي مربع) on a square plate, then exports it for 3D printing.

Open `index.html` in a browser. There is no build step and nothing to install.

## What it does

The letters and line rules are copied from a reference plate of إن مع العسر يسرا (a 17 × 17 grid), which the generator reproduces square for square when that verse is set bottom to top.

- **Grid:** every stroke and every gap is one square.
- **Letter heights:** short letters (teeth, the ع head, م, the ن bowl) stand two squares above the baseline; alef, lam, ك, ط, ه and و stand five rows.
- **Line heights:** each line is only as tall as its letters need. A roof row is added only when the line has a tall letter or a dot or hamza above; a row under the baseline only for dots or hamza below. Lines sit one square apart, and spare rows make some lines one or two squares taller so the lines fill the square exactly.
- **Rising stems:** alef and lam that open a line rise to the top edge; the lines above step in beside them.
- **Roof:** alef/lam heads bend over the short letters beside them, leaving a one-square gap.
- **Kashida:** joins and the tails and bowls of letters (the wide ن, the long ع tail) stretch so every line is flush on both sides.
- **ر and ع:** ر is one stroke through the baseline and drops two squares below it; the tail of a final ع drops and runs back right under the line.
- **ع / غ and ك:** they face right; the ع head is a small C opening right and never stretches.
- **Dots:** every dot is drawn, at most one square from its letter: above on the roof row, inside the bowl for ن, under the baseline for dots below.
- **Hamza:** one square under the alef for إ, a small mark beside the top for أ ؤ ئ, a bar for آ.
- **Hand editing:** "Edit squares" lets you click or drag on the plate to add or remove squares, with undo and reset. Every export uses the edited plate.

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
