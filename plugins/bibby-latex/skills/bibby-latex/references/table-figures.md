# Tables & Figures

## Tables — the only acceptable style

Booktabs. No vertical lines, ever. Caption ABOVE the table.

```latex
\begin{table}[t]
  \centering
  \caption{Results on the benchmark suite.}
  \label{tab:results}
  \begin{tabular}{lcc}
    \toprule
    Method & Accuracy (\%) & Latency (ms) \\
    \midrule
    Baseline       & 84.2 & 120 \\
    Ours           & \textbf{91.7} & \textbf{95} \\
    \bottomrule
  \end{tabular}
\end{table}
```

Rules:
- Column spec: `l` text, `c` centered, `r` numbers-ish; best for numeric columns is `S` from siunitx (`S[table-format=2.1]`) which aligns on decimal point.
- Bold the best result per column with `\textbf`; if using `S` columns, wrap bold entries in `{...}`.
- Multi-row/col: `\multicolumn{2}{c}{...}`, `\multirow{2}{*}{...}` (needs `multirow`).
- Partial rules between column groups: `\cmidrule(lr){2-3}`.
- Wide tables: `\resizebox{\linewidth}{!}{...}` as last resort; prefer `tabularx` with `X` columns or reduce content. Two-column layouts: `table*` for full-width.
- Notes under table: `threeparttable` package.

## Figures

Caption BELOW the figure.

```latex
\begin{figure}[t]
  \centering
  \includegraphics[width=\linewidth]{figures/architecture.pdf}
  \caption{System architecture. The encoder (left) feeds the fusion module.}
  \label{fig:arch}
\end{figure}
```

Rules:
- `width=\linewidth` (not `\textwidth` inside two-column) or a fraction: `width=0.8\linewidth`.
- Vector formats (PDF/EPS) for plots and diagrams; PNG only for photos/screenshots. Never JPG for plots.
- Subfigures — `subcaption` package:
```latex
\begin{figure}[t]
  \centering
  \begin{subfigure}{0.48\linewidth}
    \includegraphics[width=\linewidth]{a.pdf}
    \caption{Condition A}\label{fig:sub-a}
  \end{subfigure}\hfill
  \begin{subfigure}{0.48\linewidth}
    \includegraphics[width=\linewidth]{b.pdf}
    \caption{Condition B}\label{fig:sub-b}
  \end{subfigure}
  \caption{Comparison across conditions.}\label{fig:comparison}
\end{figure}
```
- Never load `subfigure` or `subfig` (deprecated/conflicts); `subcaption` only.

## Placement

- `[t]` is the correct default for papers. `[h]` alone is a lie LaTeX ignores; `[H]` (from `float`) forces exact placement but breaks page flow — use only in theses/reports when the user insists.
- `\label` must come AFTER (or inside) `\caption`, never before — otherwise refs point to the section, a classic silent bug.
- Refer with `\cref{fig:arch}` / `\cref{tab:results}`.

## Algorithms

`algorithm` + `algpseudocode`:

```latex
\begin{algorithm}[t]
  \caption{Training loop}\label{alg:train}
  \begin{algorithmic}[1]
    \Require dataset $\mathcal{D}$, learning rate $\eta$
    \For{each minibatch $B \subset \mathcal{D}$}
      \State $\theta \gets \theta - \eta \nabla_\theta \mathcal{L}(B; \theta)$
    \EndFor
  \end{algorithmic}
\end{algorithm}
```

## Code listings

Short: `\texttt{...}` inline or `verbatim`. Real listings: `listings` (pdflatex-safe, zero setup) or `minted` (prettier, but needs `-shell-escape` + Pygments — warn the user their compiler must support it; Bibby's pipeline runs plain pdflatex, so default to `listings`).