## 4.2 Pitch Shifting

Transformacija komplementarna time stretching-u. Njen cilj je da promeni visinu, tj pitch tona audio signala bez promene njegovog trajanja. 

Za pitch shifting možemo koristiti granularnu sintezu ili već pomenuti phase vocoder.

Kod granularne sinteze

1. **Delimo signal na sitne intervale**\
    Dok se krećemo kroz audio signal delimo ga na vrlo kratke *grain*-ove, dužine 1-100ms. Grain-ovi se obično preklapaju (overlap) da bi signal bio kontinualan.

2. **Menjamo gustinu reprodukcije *grain*-ova**\
    Umesto menjanja trajanja samih grain-ova, menjamo **koliko često** ih reprodukujemo. Za viši ton, grain-ove reprodukujemo češće nego što su izvađeni iz originalnog signala. Za niži ton, reprodukujemo ih ređe.

3. **Korišćenje amplitude envelope**\
    Svaki grain dobija amplitude envelope (najčešće Gaussian ili Hanning prozor) koji je nula na krajevima i maksimalan u sredini. Ovo omogućava glatko preklapanje grain-ova bez zvučnih artefakata.

4. **Overlap-add sinteza**\
    Grain-ovi se sabiru (overlap-add) na izlazu, formirajući kontinualan signal. Veći stepen preklapanja daje glađi, prirodniji zvuk, dok manji overlap može dati "granularnu" teksturu.

5. **Održavanje trajanja (opciono)**\
    Ako želimo da zadržimo originalnu dužinu snimka dok menjamo pitch:
    - Za pitch up: neki grain-ovi se dupliraju ili reprodukuju više puta
    - Za pitch down: neki grain-ovi se preskakuju/izbacuju
    
Druga opcija je koristiti phase vocoder kao i kod time stretchinga.

U ovom slučaju 

- Primenimo time stretching za faktor $\alpha\$
- Resamplujemo signal sa faktorom $\frac{1}{\alpha}$
- Rezultat ima originalno trajanje ali promenjen pitch

    \begin{figure}[h]
    \centering
    \includegraphics[width=6cm]{figures/4_time_augm/pitch_shift.png}
    \caption{Pitch shifting}
    \label{fig:pitch}
    \end{figure}
\newpage

Primene pitch shifting-a su sledeće

- Simulacija različitih govornika (muški/ženski glasovi imaju različite fundamentalne
frekvencije)
- Augmentacija za muzičku klasifikaciju (transpozicija)
- Kreiranje sintetičkih glasova
- Korekcija tona kod pevačkih aplikacija


    \begin{table}[h]
    \centering
    \begin{tabular}{|c|c|c|}
        \hline
        Prednosti & Nedostaci \\
        \hline
        Uvodi varijabilnost u tonalitetu bez menjanja sadržaja & Artifakti pri većim shift-ovima \\
        Pomoć pri simuliranju različitih govornika & Može promeniti percepciju pola govornika \\
        Relativno prirodan zvuk u umerenom opsegu & \\
        \hline
    \end{tabular}
    \caption{Prednosti i nedostaci pitch shiftinga}
    \label{tab:pitchshift_procon}
    \end{table}