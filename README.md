# LaTeX Beamer Slides Template

A professional LaTeX Beamer presentation template with clean design, custom styling, and advanced features for academic presentations.

## Features

- **Four switchable font schemes**, each with a *matching* math font
- **Accessibility-checked color palette** with measured contrast ratios
- **Micro-typography** via microtype (protrusion, expansion, tracking)
- **Automated navigation** with table of contents and section dividers
- **Advanced TikZ integration** for overlays and annotations
- **Table highlighting** with row/column animations
- **Custom commands** for consistent formatting
- **Bibliography support** with biblatex
- **Modular structure** for easy customization

## Quick Start

### Prerequisites

You need a LaTeX distribution installed:
- **macOS**: [MacTeX](https://www.tug.org/mactex/)
- **Windows**: [MiKTeX](https://miktex.org/) or [TeX Live](https://www.tug.org/texlive/)
- **Linux**: TeX Live (usually available via package manager)

### Compilation

Compile the main document:

```bash
latexmk slides.tex
```

The bundled `.latexmkrc` sends all intermediate files to `.textmp/`; only
`slides.pdf` (and `slides.synctex.gz`) land in the root. In VS Code, LaTeX
Workshop's default recipe is latexmk, so this works out of the box — don't add
a `% !TEX TS-program` line to `slides.tex`, since that makes LaTeX Workshop
bypass latexmk and run bare pdflatex.

## Customization

### Basic Setup

1. **Edit presentation metadata** in `slides.tex`:
   - Title and subtitle (lines 20-23)
   - Authors and institutions (lines 25-30)
   - Date (line 31)
   - Presenter name in footer (line 10)

2. **Add your content**:
   - Modify or replace the numbered `.tex` files (1-7) in `sections/`
   - Add new sections by creating new `.tex` files and including them in `slides.tex`

3. **Update bibliography**:
   - Add references to `references.bib`

### Advanced Customization

Both settings below live in a single `USER SETTINGS` block at the very top of
`preamble.tex`.

#### Font schemes

Beamer's default is to pair a sans body with whatever math font happens to be
loaded, which is why formulas often look pasted in from another document. Each
scheme here fixes a body face, a display face (title page, frame titles,
section dividers) and a **matching math font** together:

```latex
\def\slidefontscheme{helvetica-garamond}
```

| Scheme | Body | Display | Math |
| --- | --- | --- | --- |
| `helvetica-garamond` | Helvetica | EB Garamond | Palatino (`newpxmath`) |
| `sans` | Helvetica | Helvetica | sans (`newtxsf`) |
| `garamond` | EB Garamond | EB Garamond | EB Garamond |
| `libertinus` | Libertinus | Libertinus | Libertinus |

`helvetica-garamond` is the template's original look and stays the default.
The other three are internally consistent: body, headings and equations all
share one typeface. Use `\displayfamily` if you need the display face directly
— it follows whichever scheme is active, so nothing is hard-coded to
EB Garamond any more. An unrecognized name fails with an explicit error
listing the valid options rather than silently falling back.

#### Micro-typography

```latex
\def\slidemicrotype{1}   % 0 disables
```

Enables microtype's character protrusion and font expansion, plus tracking for
small-caps runs. This matters more on slides than in papers: slide text is
ragged-right and set in short lines, so uneven word spacing and punctuation
hanging off the right edge are much more visible.

#### Colors

The palette in `preamble.tex` is organized into three groups, and every color
carries its **measured** WCAG 2.1 contrast ratio against the white background
as a comment. Thresholds are 4.5 for body text, 3.0 for large text (frame
titles) and for graphical objects such as plot lines.

Prefer the semantic names over raw color names:

| Name | Ratio | Use for |
| --- | --- | --- |
| `ink` | 17.40 | body text |
| `inkmuted` | 7.00 | secondary text |
| `inkfaint` | 5.10 | captions, footline, citations |
| `dimmed` | 3.36 | de-emphasized **large** text only |
| `accent` | 5.50 | primary emphasis |
| `accentalt` | 9.62 | secondary emphasis |
| `rule` / `wash` / `highlight` | — | hairlines / panel fills / row highlight |

`series1`–`series6` are a **suggested palette** for figures (e.g. when exporting
graphs from Stata, R or Python), chosen by exhaustive
search: every entry clears 3.0 against white, and the set stays distinguishable
under normal vision, deuteranopia, protanopia and tritanopia (worst-case
pairwise Lab ΔE = 23.9). The ordering is optimized so any prefix is as
distinct as possible — using just `series1` and `series2` gives the best
possible two-color separation. Past about four series, add direct labels or
distinct markers, since no six-color set separates reliably for every viewer.
`fill1`–`fill6` are matched light tints for shaded areas and bars.

The older color names (`red`, `blue_tol`, `ash`, …) are all retained so
existing decks keep compiling, now annotated with their ratios and flagged
where they are too light for body text.

**Callout box** — a "key takeaway" panel with a soft background and an accent
rule down the left edge:

```latex
\takeaway{\textbf{Key result.} Effects concentrate in the top quartile.}
\takeaway[0.6\textwidth]{Narrower box.}   % optional width argument
```

The appendix contains a **Palette reference** slide showing every swatch with
its name, so you can see what is available while building a deck.

**Custom Commands**:
- `\alertbf{text}` - Accent-colored bold text
- `\takeaway[width]{text}` - Key-takeaway callout panel
- `\showgrid` - Coordinate grid for placing overlay arrows/labels (remove when done)
- `\displayfamily` - The active scheme's display face
- `\cornerlinks{content}` - Add links in bottom corner
- `\cornerinfo{text}` - Add info text in corner
- `\returnbutton{label}` - Navigation back button
- `\myuline{text}` - Custom underline with white contour

## File Structure

```
.
├── slides.tex                          # Main document (entry point)
├── preamble.tex                        # Styling and configuration
├── table_of_contents.tex               # TOC automation
├── references.bib                      # Bibliography
├── figures/                            # Exported figures + the script that makes them
├── sections/1_introduction.tex                  # Introduction slides
├── sections/2_example_math.tex                  # Math examples
├── sections/3_vfill_vspace.tex                  # Spacing examples
├── sections/4_tikz.tex                          # Grid, arrows and boxes with TikZ
├── sections/5_navigation.tex                    # Corner links, back buttons, outline link
├── sections/6_tables.tex                        # Table examples
├── sections/7_figures.tex                       # Figure examples
└── sections/8_appendix.tex                      # Appendix slides
```

## Template Features Demonstrated

Each numbered `.tex` file demonstrates specific features:

1. **Introduction** - Pause animations, citations, itemize bullets
2. **Math** - Display and inline equations
3. **Spacing** - `\vfill` and `\vspace` usage
4. **TikZ** - Overlay text, boxes and arrows, and how to place them with `\showgrid`
5. **Navigation** - Corner links, return buttons, and slide numbers that link to the outline
6. **Tables** - Row/column highlighting with TikZ overlays
7. **Figures** - Side-by-side panel layout, using figures exported from Python
   (`figures/make_figures.py` draws them in the `series`/`fill` palette at
   half-text-width golden-ratio size; re-run it with `python3
   figures/make_figures.py` if you want to tweak them)
8. **Appendix** - Appendix formatting and the palette reference slide

## License

This template is provided as-is for academic and personal use.

## Contributing

Feel free to fork, modify, and share improvements to this template.
