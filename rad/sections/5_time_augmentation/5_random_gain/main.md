## 4.5 Random Gain

Random Gain je transformacija koja nasumično povećava amplitudu audio signala.
Cilj ove transformacije je da simulira različite udaljenosti izvora zvuka od mikrofona ili različite postavke
pojačanja tokom snimanja zvuka.

Matematički se definiše kao
$$
y[n] = g \cdot x[n]
$$

gde se $g$ sempluje iz log-uniformne raspodele, s obzirom da ljudsko uho percipira glasnoću logaritamski.

Pritom je promena u decibelima data kao
$$
\Delta dB = 20 \cdot \log_{10}(g)
$$

Primena:

- Simulacija različitih udaljenosti od mikrofona
- Normalizacija varijacija u amplitudi između različitih snimaka
- Robusnost na različite postavke pojačanja

\begin{table}[h]
\centering
\begin{tabular}{|c|c|c|}
    \hline
    Prednosti & Nedostaci \\
    \hline
    Ekstremno jednostavna i brza & Previše pojačanja dovodi do clippinga \\
    Prirodna varijacija koja postoji u realnim podacima & Bolja u kombinaciji sa drugim transformacijama \\
    \hline
\end{tabular}
\caption{Prednosti i nedostaci random gain-a}
\label{tab:randgain_procon}
\end{table}