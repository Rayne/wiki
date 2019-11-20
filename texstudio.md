# TeXStudio

## Mehrere Instanzen

```bash
texstudio --start-always main.tex & texstudio --start-always cheat-sheet.tex &
```

## Makros

### Operator-Auszeichnung

**Trigger**: `OP`

```tex
\operatorname{%|}
```

### Aufzählung mit Einrückung

**Trigger**: `ITEMIZE`

```tex
\begin{itemize}

	\item
		%|

	\item

	\item

	\item

\end{itemize}
```

### Subfigures 2

**Trigger**: `FIG2`

```tex
\begin{figure}[H]
	\centering
	\begin{subfigure}[b]{0.33\linewidth}
		\includegraphics[width=\linewidth]{res/%|}
	\end{subfigure}
	\qquad
	\begin{subfigure}[b]{0.33\linewidth}
		\includegraphics[width=\linewidth]{res/}
	\end{subfigure}
\end{figure}
```

### Subfigures 2x2

**Trigger**: `FIG4`

```tex
\begin{figure}[H]
	\centering
	\begin{subfigure}[b]{0.33\linewidth}
		\includegraphics[width=\linewidth]{res/%|}
	\end{subfigure}
	\qquad
	\begin{subfigure}[b]{0.33\linewidth}
		\includegraphics[width=\linewidth]{res/}
	\end{subfigure}

	\bigskip

	\begin{subfigure}[b]{0.33\linewidth}
		\includegraphics[width=\linewidth]{res/}
	\end{subfigure}
	\qquad
	\begin{subfigure}[b]{0.33\linewidth}
		\includegraphics[width=\linewidth]{res/}
	\end{subfigure}
\end{figure}
```
