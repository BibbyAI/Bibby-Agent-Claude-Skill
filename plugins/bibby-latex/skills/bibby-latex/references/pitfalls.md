# Compile Errors → Fixes

Map the error message to the fix. Errors report the line where LaTeX *noticed*, not where the mistake is — look at that line and upward.

## Error message table

| Error | Cause | Fix |
|---|---|---|
| `Undefined control sequence` | Typo'd command or missing package | Check spelling; identify the package that defines it and add `\usepackage` |
| `Missing $ inserted` | Math command in text mode (`\alpha`, `_`, `^` outside math) or unclosed `$` | Wrap in `$...$`, or escape `_` as `\_` if literal |
| `Missing } inserted` / `Too many }'s` | Unbalanced braces | Count braces on the reported line and above; check `\left(` without `\right)` |
| `! LaTeX Error: \begin{X} ended by \end{Y}` | Mismatched/crossed environments | Fix nesting order |
| `Runaway argument?` | Unclosed brace in a command argument, often spans lines | Find the `{` never closed |
| `File 'X.sty' not found` | Package not installed | Install (`tlmgr install X`) or remove the package |
| `Option clash for package X` | Package loaded twice with different options | Load once with merged options, or pass options via `\PassOptionsToPackage` before documentclass |
| `Command \X already defined` | `\newcommand` on existing name | Use `\renewcommand`, or rename |
| `Undefined citation` / `Citation 'x' undefined` warnings | bib not compiled or bad key | Run full sequence (pdflatex → biber/bibtex → pdflatex ×2); check key spelling |
| `LaTeX Error: There's no line here to end` | `\\` after empty line or in wrong place | Delete the `\\`; paragraph breaks are blank lines |
| `Float(s) lost` | Figure/table inside a box/minipage without `[H]` | Move float out, or use `[H]` from `float` |
| `Dimension too large` | Usually giant image or TikZ coordinate overflow | Scale down |
| `Paragraph ended before \X was complete` | Blank line inside a command argument | Remove blank line or use a `long`-capable macro |
| `Unicode character not set up` (pdflatex) | Pasted unicode (—, ", α, emoji) | Replace with LaTeX equivalents; add `\usepackage[utf8]{inputenc}` (pre-2018 distros) |
| `Package hyperref Warning: Token not allowed` | Math/fragile command in `\section` heading | `\texorpdfstring{$\alpha$}{alpha}` |
| Hyperref refs point to wrong place | `\label` before `\caption` | `\label` goes after `\caption` |
| `Extra alignment tab` (`&`) | More `&` than columns in tabular/align | Fix column count or escape literal `&` as `\&` |

## Silent bugs (compiles, but wrong output)

- `\label` before `\caption` → wrong ref numbers.
- `$$...$$` → wrong vertical spacing, breaks `fleqn`.
- `\ref` without `~` → line break between "Figure" and "3".
- `|` in math for norms/conditionals → bad spacing; use `\lvert`, `\mid`, `\lVert`.
- Loading `hyperref` early → half the packages break. hyperref second-to-last, `cleveref` last.
- Straight quotes `"word"` → both render as closing quotes. Use ``word''.
- `\it`/`\bf` → no italic correction and doesn't nest. Use `\textit`/`\textbf`.

## Overfull hbox warnings

Not errors, but reviewers see black boxes in draft mode. Fixes in order of preference:
1. Reword the sentence.
2. `\usepackage{microtype}` (should be in every preamble anyway — free 90% reduction in overfull boxes).
3. Allow hyphenation of a stubborn word: `\hyphenation{hy-phen-ation}`.
4. Never `\sloppy` globally; `\begin{sloppypar}` locally if desperate.

## Debug procedure for "it won't compile and I don't know why"

1. Read the FIRST error in the log, not the last — errors cascade.
2. If the error is opaque: bisect. Comment out the second half of the document (`\end{document}` early), recompile, narrow down.
3. Check for the usual suspects: unescaped `%` (eats rest of line — text mysteriously missing is almost always this), unescaped `&`, `_` in text mode (common in file names and URLs — use `\url{}` from hyperref for URLs).
4. Clean aux files (`.aux .toc .bbl .out`) when refs/TOC behave inexplicably.