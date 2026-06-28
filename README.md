# CV — Esau Salvador Martinez Lopez

Personal CV written in LaTeX, designed for AI/Software Engineer roles.

## Setup

### Prerequisites

```bash
brew install --cask mactex
brew install tex-fmt
```

### VS Code

Install [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) and add to your settings:

```json
{
  "latex-workshop.formatting.latex": "tex-fmt",
  "[latex]": {
    "editor.defaultFormatter": "James-Yu.latex-workshop"
  }
}
```

## Build

```bash
pdflatex -interaction=nonstopmode en-cv-esau-martinez.tex
```

Output: `en-cv-esau-martinez.pdf`

## Project Structure

```
.
├── .agents/skills/cv-guide/   # CV optimization skill (design, ATS, HR guidelines)
├── .gitignore                 # Ignores everything except .tex, .pdf, .agents, .gitignore
├── en-cv-esau-martinez.tex    # CV source (English)
└── en-cv-esau-martinez.pdf    # Compiled PDF
```

## Conventions

- Commits follow [Conventional Commits](https://www.conventionalcommits.org/)
- Only `.tex`, `.pdf`, `.agents`, and `.gitignore` are tracked
- LaTeX build artifacts (`.aux`, `.log`, `.out`, `.fdb_latexmk`, `.fls`) are ignored
