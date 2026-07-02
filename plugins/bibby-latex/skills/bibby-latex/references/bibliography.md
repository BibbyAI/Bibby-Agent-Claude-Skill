# Citations & Bibliography

## Decision

- **New standalone doc / thesis / arXiv preprint** → biblatex + biber.
- **Journal/conference template (IEEE, ACM, Springer, Elsevier, NeurIPS/ICML style files)** → whatever the template ships with. Usually natbib + a `.bst` file. Do NOT swap it out; publishers reject biblatex.
- User just says "add citations" with no template → biblatex.

## biblatex setup

```latex
% preamble
\usepackage[backend=biber, style=numeric-comp, sorting=none]{biblatex}
\addbibresource{references.bib}
% body: \cite{key}, \textcite{key}, \parencite{key}
% end of document, before \end{document}:
\printbibliography
```
Common styles: `numeric-comp` ([1–3]), `authoryear` (Smith, 2024), `ieee`, `apa` (needs `biblatex-apa`).
Compile sequence: pdflatex → biber → pdflatex → pdflatex.

## natbib setup

```latex
\usepackage{natbib}
\bibliographystyle{plainnat}   % or the template's .bst
% body: \citep{key} (parenthetical), \citet{key} (textual: "Smith et al. (2024)")
\bibliography{references}      % at end, no .bib extension
```
Compile sequence: pdflatex → bibtex → pdflatex → pdflatex.
`\citep` vs `\citet` is the #1 thing users get wrong — "as shown in \citep{x}" should be `\citet`.

## .bib entries — clean format

```bibtex
@article{vaswani2017attention,
  author  = {Vaswani, Ashish and Shazeer, Noam and Parmar, Niki},
  title   = {Attention Is All You Need},
  journal = {Advances in Neural Information Processing Systems},
  year    = {2017},
  volume  = {30}
}

@inproceedings{key2024,
  author    = {Last, First and Last2, First2},
  title     = {Paper Title},
  booktitle = {Proceedings of the ...},
  year      = {2024},
  pages     = {1--10}
}
```

Rules:
- Keys: `firstauthorYEARkeyword` (lowercase). Never spaces or unicode in keys.
- Protect capitalization the style would lowercase: `title = {The {BERT} Model for {NLP}}`.
- `and` separates authors — never commas between full names, never `et al.` in the .bib.
- Page ranges use `--`.
- arXiv preprints: `@misc` with `eprint`, `archivePrefix = {arXiv}`, `primaryClass`; upgrade to `@inproceedings`/`@article` once published.
- Don't invent bibliographic data. If the user gives a paper title only and you're not certain of the venue/year, leave a `% TODO: verify` comment or ask.

## Cite placement

- Before punctuation, after the claim: `...improves accuracy~\cite{smith2024}.`
- Non-breaking space `~` before every `\cite`/`\citep`.
- Multiple: `\cite{a,b,c}` — one command, not three.