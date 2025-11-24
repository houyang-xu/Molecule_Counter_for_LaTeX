# Molecule Counter

A LaTeX package for automatically numbering molecules in chemistry documents.

**Author:** H. Xu
**Version:** 1.1  
**Date:** July 2025

## Features

- Automatic molecule numbering with bold formatting
- Sequential or chapter-based numbering (depends on which file you use)
- Forward and backward references
- Invisible molecule registration for document organisation

## Installation

Copy `moleculecounter.sty` or `moleculecounterbych.sty` to your project directory. Works for Overleaf and texlive. I think it's possible to copy it to the texlive installation and make it work as a built-in package but somehow when I do put it in a folder under *texlive\texmf-local\tex\latex* it just doesnt work. Happy to take advice.

## Usage

### Choose Your Package
```latex
\usepackage{moleculecounter}        % Sequential: 1, 2, 3...
% OR 
\usepackage{moleculecounterbych}    % By chapter: 1.1, 1.2, 2.1...
```

### Commands

**`\newmol{label}`** - Define and display a new molecule
```latex
The synthesis of paclitaxel (\newmol{taxol}) was performed...
% Output: "The synthesis of paclitaxel (**1**) was performed..."
```

**`\invmol{label}`** - Register a molecule invisibly (nothing printed. I prefer this one as it'd good for managing all molecules of the same section. Also if you have molecule names in floats e.g. tables or figures and sometimes you have *\newmol* before *\usemol*, which causes issues. *Update*: with the new forward-referencing function in v1.1 it doesn't seem to be an issue anymore!
)
```latex
\invmol{howeveryoucallyourmolecule}
\invmol{howeveryoucallyourmolecule2}
```

**`\usemol{label}`** - Reference a molecule
```latex
Compound \usemol{taxol} was treated with...
% Output: "Compound **1** was treated with..."
```

### Example
```latex
\documentclass{report}
\usepackage{moleculecounterbych}

\begin{document}

% Pre-register molecules
\invmol{catalyst}
\invmol{substrate}

\chapter{Introduction}
To a solution of \usemol{substrate} was added \usemol{catalyst}...

\chapter{Results}
We synthesised \newmol{product} in 79\% yield...
\end{document}
```

## Forward References

The package supports using `\usemol{}` before `\newmol{}` or `\invmol{}`. Requires **two compilation passes**. If references fail, delete `.aux` and `.moldata` files and recompile twice.

## Version History

- **v1.1** (July 2025): Forward reference support
- **v1.0**: Initial release

