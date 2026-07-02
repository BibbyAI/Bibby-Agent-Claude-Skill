# LaTeX Symbols & Commands Cheatsheet

All math-mode unless noted. Requires `amsmath` + `amssymb` (assume loaded).

## Greek
`\alpha \beta \gamma \delta \epsilon (\varepsilon) \zeta \eta \theta (\vartheta) \iota \kappa \lambda \mu \nu \xi \pi \rho (\varrho) \sigma (\varsigma) \tau \upsilon \phi (\varphi) \chi \psi \omega`
Uppercase: `\Gamma \Delta \Theta \Lambda \Xi \Pi \Sigma \Upsilon \Phi \Psi \Omega`
Variants: `\varepsilon` and `\varphi` are the ones people usually want, not `\epsilon`/`\phi`.

## Sets & logic
| Meaning | Command |
|---|---|
| ℝ ℕ ℤ ℚ ℂ | `\mathbb{R}` etc. |
| ∈ ∉ ⊂ ⊆ ⊃ ⊇ | `\in \notin \subset \subseteq \supset \supseteq` |
| ∪ ∩ ∖ ∅ | `\cup \cap \setminus \emptyset` (nicer: `\varnothing`) |
| ∀ ∃ ∄ | `\forall \exists \nexists` |
| ∧ ∨ ¬ | `\land \lor \neg` |
| ⇒ ⇐ ⇔ | `\implies \impliedby \iff` (spaced) or `\Rightarrow \Leftarrow \Leftrightarrow` |
| → ↦ | `\to \mapsto` |

## Relations
| Meaning | Command |
|---|---|
| ≤ ≥ ≠ ≈ ≡ ∼ ≃ ≅ ∝ | `\leq \geq \neq \approx \equiv \sim \simeq \cong \propto` |
| ≪ ≫ | `\ll \gg` |
| ≜ / := | `\triangleq` / `\coloneqq` (needs `mathtools`) |

## Operators
| Meaning | Command |
|---|---|
| × ÷ ± ∓ ⋅ | `\times \div \pm \mp \cdot` |
| ⊗ ⊕ ⊙ ∘ ∗ | `\otimes \oplus \odot \circ \ast` |
| ∑ ∏ ∫ ∮ ∬ | `\sum \prod \int \oint \iint` |
| ∂ ∇ | `\partial \nabla` |
| √ | `\sqrt{x}`, `\sqrt[n]{x}` |
| min/max/argmin | `\min \max`; `\operatorname*{arg\,min}_{x}` or define `\DeclareMathOperator*{\argmin}{arg\,min}` |
| custom operator | `\DeclareMathOperator{\tr}{tr}` (preamble) |

## Accents & decorations
`\hat{x} \bar{x} \tilde{x} \vec{x} \dot{x} \ddot{x} \mathbf{x} \boldsymbol{\theta} \mathcal{L} \mathrm{d} \mathsf{T} \mathfrak{g}`
Wide versions: `\widehat{ABC} \widetilde{ABC} \overline{ABC} \underbrace{...}_{n\text{ terms}}`

## Brackets — always auto-size
`\left( ... \right)`, `\left[ ... \right]`, `\left\{ ... \right\}`, `\left| ... \right|`, `\left\lVert ... \right\rVert`, `\left\langle ... \right\rangle`, `\left\lfloor ... \right\rfloor`, `\left\lceil ... \right\rceil`
Manual sizes when `\left/\right` misbehaves across line breaks: `\big \Big \bigg \Bigg`.

## Fractions, binomials, cases
- `\frac{a}{b}`, inline-friendly `\tfrac{a}{b}`, display-forced `\dfrac{a}{b}`
- `\binom{n}{k}`
- Cases:
```latex
f(x) = \begin{cases} 1 & x > 0 \\ 0 & \text{otherwise} \end{cases}
```

## Matrices
`pmatrix` (parens), `bmatrix` [brackets], `vmatrix` |det|, `Vmatrix` ‖ ‖, `smallmatrix` for inline:
```latex
A = \begin{bmatrix} a & b \\ c & d \end{bmatrix}
```

## Multi-line equations
- Aligned at `=`: `align` environment, `&` before alignment point, `\\` between lines. `align*` for no numbers, `\notag` per line, `\nonumber` also works.
- One number for a group: `split` inside `equation`.
- Long single equation broken across lines: `multline`.
- Never `eqnarray`.

## Probability / ML / stats (common in Bibby users' papers)
```latex
\newcommand{\E}{\mathbb{E}}
\newcommand{\Prob}{\mathbb{P}}
\newcommand{\Var}{\operatorname{Var}}
\newcommand{\KL}[2]{D_{\mathrm{KL}}\!\left(#1 \,\|\, #2\right)}
\newcommand{\given}{\mid}
\newcommand{\norm}[1]{\left\lVert #1 \right\rVert}
\newcommand{\abs}[1]{\left\lvert #1 \right\rvert}
\newcommand{\inner}[2]{\left\langle #1, #2 \right\rangle}
```
- Conditional: `p(y \mid x)` — `\mid`, not `|` (spacing).
- Distributions: `x \sim \mathcal{N}(\mu, \sigma^2)`
- Gradient of loss: `\nabla_\theta \mathcal{L}(\theta)`

## Text inside math
`\text{...}` (from amsmath), never `\mbox`. Spacing tweaks: `\,` thin, `\;` medium, `\quad`, `\qquad`, negative `\!`.
Differential: `\int f(x)\, \mathrm{d}x` — upright d with thin space.

## Units (siunitx)
`\SI{3.5}{\milli\second}`, `\SI{95.2}{\percent}`, `\num{1.2e-4}`, ranges `\SIrange{10}{20}{\kelvin}`.

## Arrows & misc
`\leftarrow \rightarrow \leftrightarrow \Longrightarrow \hookrightarrow \rightharpoonup \uparrow \downarrow`
`\infty \aleph \hbar \ell \Re \Im \angle \perp \parallel \therefore \because \dots \cdots \vdots \ddots`
Degree: `45^\circ`. Prime: `x'` or `x^{\prime\prime}`.