---
weight: 600
title: "Classes using/writing"
---
## \(Maybe\) Useful resources

### For using

- [koma script - Regarding the `book`, `report`, and `article` document classes: what are the main differences? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/36989/206709)
- [LaTeX/Document Structure - Wikibooks, open books for an open world](https://en.wikibooks.org/wiki/LaTeX/Document_Structure)
- [Your Guide to documentclass LaTeX: Types and options - LaTeX-Tutorial.com](https://latex-tutorial.com/documentclass-latex/)

### For writing

- [CTAN: Package clsguide](https://ctan.org/pkg/clsguide)


## Classes I like

- [Gijs's Homework Template - Overleaf, Online LaTeX Editor](https://www.overleaf.com/latex/templates/gijss-homework-template/xrhhfgqcfbft) \(Click View Source to see the code.\)
    + Repository of an outdated version: [gijs-pennings/latex-homework: LaTeX class for homework assignments](https://github.com/gijs-pennings/latex-homework)


## Basic class writing

Refs:

- [Gijs's Homework Template - Overleaf, Online LaTeX Editor](https://www.overleaf.com/latex/templates/gijss-homework-template/xrhhfgqcfbft)
- [Writing your own class - Overleaf, Online LaTeX Editor](https://www.overleaf.com/learn/latex/Writing_your_own_class)

```latex
\ProvidesClass{mydoc}

% %%%% If using a parent class, new options
% %%%% must be placed before \PassOptionsToClass

% default false option
\newif\if@optionone
\DeclareOption{optionone}{\@optiononetrue}

% default true option with false counterpart
\newif\if@optiontwo \@optiontwotrue
\DeclareOption{optionthree}{\@optiontwofalse}

% %%%% Load parent class
\DeclareOption*{\PassOptionsToClass{\CurrentOption}{article}}
\ProcessOptions\relax
\LoadClass[12pt, a4paper]{article}

% %%%% Load packages
\RequirePackage[option]{package}

% %%%% Use option to load packages
% https://tex.stackexchange.com/a/1274/206709
\if@optionone
  \RequirePackage{package}
\else
  \RequirePackage{package}
\fi

% %%%% Use option to do other things
\if@optiontwo
  \renewcommand*{...}{...}
\fi

% %%%% Packages that need to be load after others
\RequirePackage[colorlinks,bookmarksnumbered,pdfusetitle]{hyperref}

% load after hyperref
% https://tex.stackexchange.com/a/312661/206709
\RequirePackage[numbered]{bookmark}
\RequirePackage[margin=1in]{geometry}
\RequirePackage[nameinlink]{cleveref}
```
