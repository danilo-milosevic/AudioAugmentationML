## 4.3 Dodavanje nasumičnog šuma

Dodavanje šuma je jedna od najčešćih i najefektivnijih audio augmentacija. Simulira realne
uslove snimanja i čini model robusnijim na različite vrste pozadinskog šuma.

Funkcioniše tako što se čist audio signal $x(t)$ kombinuje sa šumom $n(t)$

$$
y(t) + x(t) + \alpha \dot n(t)
$$

pri čemu je $\alpha$ intenzitet šuma. Često se koristi i SNR, tj *Signal to Noise Ratio*
$$
SNR = 10*log_{10}(P_{signal}/P_{noise})
$$
gde su $P_{signal}$ i $P_{noise}$ prosečne snage signala i šuma.

Postoji više vrsta šuma, tj više distribucija šuma koje se mogu koristiti u augmentaciji.

- **Beli šum**
    - Šum koji ima podjednaku amplitudu među svim frekvencijama.
    - Zbog ovoga ljudskom uhu zvuči kao šuštanje.

    - Sample-ovi belog šuma su međusobno nezavisni i moguće je generisati ga sample-ovanjem bilo koje nezavisne distribucije
        (Gausian, Uniform ...)
- **Roze šum**
    - Šum gde snaga signala opada sa porastom frekvencije.
    - Zato je šum dosta prirodniji za ljudsko uho i češće se javlja u prirodi.
    - Može da se dobije od belog šuma smanjivanjem snage sa porastom frekvencije

- **Brownian šum**
    - Šum gde snaga signala opada proporcionalno kvadratu frekvencije.
    - Još dublji u odnosu na roze šum.

- **Ambijentalni šum**
    - Šum nastao u realnim okruženjima
    - Najrealističniji ali zahteva eksterni skup podataka, teško generisati kao prethodne

    \begin{figure}[h]
    \centering
    \includegraphics[width=7cm]{figures/4_time_augm/noise.png}
    \caption{Vrste šuma}
    \label{fig:noise}
    \end{figure}

    \begin{table}[h]
    \centering
    \begin{tabular}{|c|c|c|}
        \hline
        Prednosti & Nedostaci \\
        \hline
        Izuzetno efikasna za povećanje robusnosti & Previše šuma može narušiti razumljivost govora \\
        Simulira realne uslove korišćenja & Potreban eksterni dataset kod ambijentalnog šuma \\
        Jednostavna implementacija & Može maskirati važne karakteristike signala\\
        \hline
    \end{tabular}
    \caption{Prednosti i nedostaci dodavanja šuma}
    \label{tab:noise_procon}
    \end{table}