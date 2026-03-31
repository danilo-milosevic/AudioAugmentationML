## 5.2 Loudness kontrola

Loudness kontrola je metoda augmentacije podataka koja se primenjuje u frekventnom domenu i omogućava manipulaciju percipirane glasnoće zvuka, za razliku od random gain-a. 

Kod random gain-a smo nasumično pojačavali amplitude nekim faktorom $g$, semplovanim korišćenjem uniformne raspodele. Međutim ova metoda ne uzima u obziru percepciju ljudskog uha. Ljudsko uho je najosetljivije na frekvence u opsegu od 2kHz do 5kHz (sa vrhom oko 3.5-4kHz) i poklapa se sa frekvencom rezonance kanala ljudskog uha.

\begin{figure}[ht]
\centering
\includegraphics[width=5cm]{figures/5_freq_augm/hearing.png}
\caption{Osetljivost ljudskog uha na različite frekvencije}
\label{fig:freq_ear}
\end{figure}

Kontrola glasnoće, odnosno *loudness control* uzima u obzir osetljivost ljudskog uha i skalira spektar prema perceptualnim krivama.

Primenjuje se na spektrogramu zvuka:
$$
S^\prime\left[f, t\right] = S\left[f, t\right] \cdot L\left(f\right) \cdot g
$$
pri čemu je 

- $L\left(f\right)$ frekvencijski zavisna težina bazira na perceptualnim modelima i data je kao funkcija frekvence. Ona određuje koliko će se skalirati svaka frekvenca.
- $g$ je skalar kojim se određuje koliko primeniti kontrolu glasnoće

Najčešće se za $L\left(f\right)$ koristi *A-weighting* koja je data kao
\setcounter{equation}{0}
\begin{align}
R_{A}(f) &= \frac{12194^2 f^4}{\left(f^2 + 20.6^2\right)\sqrt{\left(f^2 + 107.7^2\right)\left(f^2 + 737.9^2\right)\left(f^2 + 12194^2\right)}} \\
A(f) &= 20\log_{10}\left(R_{A}(f)\right) - 20\log_{10}\left(R_{A}(1000)\right)
\end{align}

Ova metoda se primenjuje za

- Normalizaciju glasnoće između različitih snimaka
- Simulaciju različitih slušnih uslova
- Povećanje konzistentnosti trening podataka

\newpage

\begin{figure}[ht]
\centering
\includegraphics[width=7cm]{figures/5_freq_augm/aweight.jpg}
\caption{A-weighting kriva}
\label{fig:aweight}
\end{figure}

\begin{table}[h]
\centering
\begin{tabular}{|c|c|c|}
    \hline
    Prednosti & Nedostaci \\
    \hline
    Bolje odgovara ljudskoj percepciji & Kompleksnija implementacija \\
    Korisna za normalizaciju dataset-a & Sporije nego random gain \\
    \hline
\end{tabular}
\caption{Prednosti i nedostaci loudness kontrole}
\label{tab:loudcontroll_procon}
\end{table}