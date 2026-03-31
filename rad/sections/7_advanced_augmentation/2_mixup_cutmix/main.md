## 6.2 MixUp i CutMix

MixUp i CutMix su metode augmentacije koje kombinuju dva podatka iz trening skupa kako bi se dobile nove instance. Prvenstveno su razvijene za augmentaciju podataka u domenu računarskog vida ali su kasnije prilagođene za augmentaciju audio podataka.

### 6.2.1 MixUp

MixUp funkcioniše tako što na osnovu dva audio signala $(x_1, y_1)$ i $(x_2, y_2)$ formira novi primer $(x_{mix}, y_{mix})$ linearnom kombinacijom prva dva signala na sledeći način

\setcounter{equation}{0}
\begin{align}
x_{mix} &= \lambda \cdot x_1 + (1 - \lambda) \cdot x_2 \\
y_{mix} &= \lambda \cdot y_1 + (1 - \lambda) \cdot y_2
\end{align}

Na slici ispod možemo da vidimo efekat MixUp augmentacije na mel spektrogramima dva uzorka

\begin{figure}[ht]
\centering
\includegraphics[width=8cm]{figures/6_advanced_augm/mixup.png}
\caption{MixUp}
\label{fig:mixup}
\end{figure}

### 6.2.2 CutMix

CutMix takođe formira na osnovu dva audio signala treći kombinovanjem, ali nema interpolacije, već se deo prvog signala menja delom drugog signala.

Postoje više vrste CutMix-a, zavisno od toga na kojim se primerima u trening skupu primenjuje i nad kojom reprezentacijom audio signala.

- **Between-Class**

    Meša signale instanci iz različitih klasa.
- **Within-Class**

    Meša primere isključivo iz iste klase.
- **SpecMix**
    
    Primenjuje mixup na mel spektrogramu umesto na waveform.
- **PatchMix**

    Primenjuje mixup tako što menja nasumične patch-eve spektrograma između dve izabrane instance.


\begin{figure}[ht]
\centering
\includegraphics[width=8cm]{figures/6_advanced_augm/specmix.png}
\caption{SpecMix}
\label{fig:specmix}
\end{figure}

\begin{table}[h]
\centering
\begin{tabular}{|>{\centering\arraybackslash}p{8cm}|>{\centering\arraybackslash}p{8cm}|}
    \hline
    \textbf{Prednosti} & \textbf{Nedostaci} \\
    \hline
    Jednostavna augmentacija za razumevanje i implementaciju &
    Ne čini model robustnijim na kompleksnije adverserijalne primere \\

    Služi kao i regularizacija &
    Računski skupo, s obzirom da vršimo trening dva puta \\
    \hline
\end{tabular}
\caption{Prednosti i nedostaci MixUp-a i CutMix-a}
\label{tab:mixup_procon}
\end{table}