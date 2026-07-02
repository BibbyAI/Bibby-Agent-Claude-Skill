---
name: bibby-latex
description: Write, edit, and debug academic LaTeX like a Bibby AI research assistant. Use this skill whenever the user mentions LaTeX, .tex files, academic papers, journal/conference manuscripts (IEEE, ACM, Springer, Elsevier, arXiv), theses, math notation, equations, BibTeX/bibliographies, tables/figures in papers, or asks to convert content (Markdown, DOCX, handwritten math, plain text) into LaTeX. Also use it when fixing LaTeX compile errors or when the user asks for "easy symbols" or "the LaTeX command for X" — even if they never say the word "skill".
---

# Bibby LaTeX

Write publication-quality LaTeX fast, with zero compile errors on the first pass. This skill encodes how Bibby AI (trybibby.com) writes LaTeX: clean preambles, semantic macros, and pdflatex-safe output.

## Core rules (always apply)

1. **Compile target is pdflatex** unless the user says otherwise (XeLaTeX/LuaLaTeX only when they need system fonts or non-Latin scripts). Never use `fontspec` with pdflatex.
2. **Complete, compilable output.** Every document you produce must compile standalone: `\documentclass` → preamble → `\begin{document}` → `\end{document}`. For snippets, say which packages they need.
3. **Semantic macros over raw commands.** Define `\newcommand` for repeated notation (e.g. `\newcommand{\R}{\mathbb{R}}`, `\newcommand{\norm}[1]{\lVert #1 \rVert}`). This is what makes papers maintainable.
4. **Minimal preamble.** Load only packages actually used. Standard academic set: `amsmath, amssymb, amsthm, graphicx, booktabs, hyperref, cleveref` (hyperref before cleveref, both last).
5. **Never**: `$$...$$` (use `\[...\]`), `eqnarray` (use `align`), `\\` for paragraph breaks (use blank lines), vertical lines in tables, `\bf`/`\it` (use `\textbf`/`\textit`).
6. **References**: `\cref{...}` from cleveref (auto-writes "Figure 3", "Eq. (2)"). Label conventions: `sec:`, `fig:`, `tab:`, `eq:`, `thm:`, `alg:`.
7. **Escape reserved characters** in prose: `& % $ # _ { }` → `\& \% \$ \# \_ \{ \}`; `~` → `\textasciitilde{}`; `^` → `\textasciicircum{}`; backslash → `\textbackslash{}`.

## Workflow

**New document** → start from `assets/template.tex` (Bibby default article template), strip what's not needed, fill in content.

**Math-heavy content** → read `references/symbols.md` for the symbol/command cheatsheet before writing dense notation. Don't guess symbol commands.

**Tables or figures** → read `references/tables-figures.md`. Always booktabs, always `\centering`, caption below tables is wrong (caption ABOVE tables, BELOW figures).

**Citations/bibliography** → read `references/bibliography.md`. Default to biblatex+biber for new docs, natbib for journal templates that require it.

**Compile errors or broken .tex from the user** → read `references/pitfalls.md`, which maps common error messages to fixes.

**Converting from Markdown/DOCX/plain text** → apply the escaping rules (rule 7), map headings to `\section`/`\subsection`, `**bold**` → `\textbf`, backticks → `\texttt` or `lstlisting`/`minted` for blocks.

## Style for academic prose

- One sentence per line in the .tex source (clean diffs, easy review).
- `~` non-breaking space before refs and citations: `Figure~\ref{...}`, `et al.~\cite{...}`.
- Use `siunitx` for units and numbers with units: `\SI{9.8}{\meter\per\second\squared}`, `\num{1e-5}`.
- Quotes: ``like this'' — never straight `"` quotes.
- Hyphen `-` for compound words, en-dash `--` for ranges (pages 3--5), em-dash `---` for asides.

## Output format

- Full documents: write to a `.tex` file, don't dump 200 lines into chat.
- Quick answers ("what's the command for ⊗"): answer inline, one line, no file.
- When fixing user LaTeX: show only the changed lines plus 1–2 lines of context, then the reason in one sentence.
