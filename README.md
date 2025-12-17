# LaTeX Beamer Slides Template

A professional LaTeX Beamer presentation template with clean design, custom styling, and advanced features for academic presentations.

## Features

- **Clean, modern design** with Helvetica font at 95% scale
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
pdflatex 0_main.tex
bibtex 0_main
pdflatex 0_main.tex
pdflatex 0_main.tex
```

Or use your LaTeX editor's build command (the file headers contain editor hints for proper compilation).

## Customization

### Basic Setup

1. **Edit presentation metadata** in `0_main.tex`:
   - Title and subtitle (lines 20-23)
   - Authors and institutions (lines 25-30)
   - Date (line 31)
   - Presenter name in footer (line 10)

2. **Add your content**:
   - Modify or replace the numbered `.tex` files (1-7)
   - Add new sections by creating new `.tex` files and including them in `0_main.tex`

3. **Update bibliography**:
   - Add references to `references.bib`

### Advanced Customization

**Colors** - Defined in `preamble.tex` (lines 139-155):
```latex
\definecolor{red}{RGB}{209,15,47}
\definecolor{blue_tol}{RGB}{0,119,187}
```

**Custom Commands**:
- `\alertbf{text}` - Red bold text
- `\cornerlinks{content}` - Add links in bottom corner
- `\cornerinfo{text}` - Add info text in corner
- `\returnbutton{label}` - Navigation back button
- `\myuline{text}` - Custom underline with white contour

**Font Configuration** - In `preamble.tex` (lines 54-58):
```latex
\usepackage[scaled=.95]{helvet}
\renewcommand{\familydefault}{\sfdefault}
```

## File Structure

```
.
├── 0_main.tex                          # Main document (entry point)
├── preamble.tex                        # Styling and configuration
├── table_of_contents.tex               # TOC automation
├── references.bib                      # Bibliography
├── 1_introduction.tex                  # Introduction slides
├── 2_example_math.tex                  # Math examples
├── 3_vfill_vspace.tex                  # Spacing examples
├── 4_tables.tex                        # Table examples
├── 5_links.tex                         # Cross-reference examples
├── 6_figures.tex                       # Figure examples
└── 7_appendix.tex                      # Appendix slides
```

## Template Features Demonstrated

Each numbered `.tex` file demonstrates specific features:

1. **Introduction** - Pause animations, citations, itemize bullets
2. **Math** - Display and inline equations
3. **Spacing** - `\vfill` and `\vspace` usage
4. **Tables** - Row/column highlighting with TikZ overlays
5. **Links** - Cross-referencing and corner links
6. **Figures** - Layouts with TikZ annotations
7. **Appendix** - Appendix formatting

## License

This template is provided as-is for academic and personal use.

## Contributing

Feel free to fork, modify, and share improvements to this template.
