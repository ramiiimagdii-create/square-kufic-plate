# Square Kufic Plate

A single-page web app that sets Arabic text, typically Quran verses, in square Kufic (كوفي مربع) on a square plate, then exports it for 3D printing.

Open `index.html` in a browser. There is no build step and nothing to install.

## What it does

The letters were chosen square by square with the owner, starting from a reference plate of إن مع العسر يسرا (a 17 × 17 grid). `letter-sheet.png` shows every letter in every form.

- **Grid:** every stroke and every gap is one square.
- **Heights:** every letter reaches the top and the baseline of its line, so lines align on all four sides. Short letters get there through a stem (teeth lengthen, ع grows a stem under its head, م و ف ق are boxes on a stem, ه has an ear); a head, mouth or loop never stretches. A letter stops one square under a dot or hamza above it.
- **Shapes:** ع / غ a small C opening right; ك a tall stem with its bar reaching right; ص a wide loop with a tooth; final ب ت ث a tooth plus a long tail; final ل a stretching bowl; د a small hook that stretches.
- **Tails:** ر drops and sweeps left; و drops its tail; final ي returns right under the line; final ع runs right under the line.
- **Dots:** every dot is drawn, one square, right above or below its letter with a one-square gap (inside the bowl for ن); three dots in a row.
- **Hamza:** one square with a notch, as in the plate, always directly above or below its letter: under إ (the alef stops short), above أ (the alef starts lower), above ؤ ئ; a short bar over آ. It is drawn notched in the preview, SVG, PNG and STL.
- **Lines:** each line is only as tall as its letters need, one gap row apart. Lines interlock as in the plate: dots below and tails drop into free space in the line underneath, and a line only gets rows of its own when a dot finds no room. The square is chosen so the lines fill it exactly, with no stretched letters. Alef and lam that open a line rise to the top edge, and alef/lam heads bend over the short letters beside them.
- **Kashida:** joins, tails and bowls stretch so every line is flush on both sides.
- **Reading order:** top to bottom or bottom to top, or let the tool pick whichever fills the square better.
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
