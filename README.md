# Square Kufic Plate

A single-page web app that sets Arabic text, typically Quran verses, in square Kufic (كوفي مربع) on a square plate, then exports it for 3D printing.

Open `index.html` in a browser. There is no build step and nothing to install.

## What it does

The letters follow a square Kufic letter chart (each letter's start, middle, end and isolated forms) and the owner's reference plate of إن مع العسر يسرا, a 17 × 17 grid.

- **Grid:** every stroke and every gap is one square, and strokes sit on every other row and column, so all spacing is even.
- **Lines:** a line is three squares high. Ascenders, dots and hamza sit in the two rows above it; tails and dots below sit in the two rows under it. These rows are shared with the neighbouring line, so lines interlock.
- **Filling the square:** the line breaks are chosen so lines are about the same length. A short line is filled by widening boxes, bowls and joins. If the lines are too low for the widest one, a line grows taller instead of being stretched thin.
- **Rule check:** every layout is checked before it is shown. Letters never touch unless they are joined on the baseline, dots and hamza stand clear of everything, and no stroke is two squares thick. Every distinct word in the Quran and a sample of whole verses pass this check.
- **Reference pictures:** a few verses are stored square by square from pictures and come out exactly as drawn: إن مع العسر يسرا (the reference plate), وفي السماء رزقكم وما توعدون, ذلك فضل الله يؤتيه من يشاء والله ذو الفضل العظيم, and وجعل بينكم مودة ورحمة.
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
