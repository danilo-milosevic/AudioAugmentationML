## 2.1 Digitalni audio signal

Zvuk je mehanički talas koji se prostire kroz neku sredinu kao rezultat vibracija. Kako bi se
zvuk sačuvao na računaru on se zapisuje u digitalnom obliku, gde je predstavljen diskretizovanom verzijom
kontinualnog zvučnog talasa. Proces digitalizacije se sastoji od semplovanja (sampling) i kvantizacije.

- **Sampling**
    - Proces merenja amplitude zvučnog talasa u regularnim vremenskim intervalima. Frekvencija *sampling*-a  određuje koliko puta u sekundi ćemo meriti amplitudu zvučnog signala. Po Nyquist-Shannon-ovoj teoremi semplovanja signala, potrebno je semplovati sa bar duplo manjom frekvencijom od izvorne frekvencije signala. U suprotnom dolazi do *aliasing*a

    \begin{figure}[h]
    \centering
    \includegraphics[width=5cm]{figures/3_audio_basics/sampling.png}
    \caption{Semplovanje audio signala}
    \label{fig:sampling}
    \end{figure}

    \begin{table}[h]
    \centering
    \begin{tabular}{|c|c|c|}
        \hline
        Standardne frekvencije semplovanja (kHz) & Upotreba \\
        \hline
        8 & telefonski govor \\
        44.1 & CD kvalitet \\
        48 & profesionalni audio \\
        96 ili 192 & high-res audio \\

        \hline
    \end{tabular}
    \caption{Broj vrednosti amplituda u zavisnosti od broja bitova}
    \label{tab:frequencies}
    \end{table}

- **Kvantizacija**
    - Kako su računari digitalni uređaji konačne preciznosti, potrebno je vrednosti amplitude signala mapirati na jednu od $2^n$ vrednosti, pri čemu $n$ predstavlja broj bitova kojim možemo predstaviti vrednosti amplitude.

    \begin{table}[h]
    \centering
    \begin{tabular}{|c|c|c|}
        \hline
        Broj bitova & Broj mogućih vrednosti amplitude \\
        \hline
        8 & 256 \\
        16 & 65,536 (CD) \\
        24 & 16,777,216 (profesionalni audio) \\
        32 & 4,294,967,296 (digitalna obrada signala) \\

        \hline
    \end{tabular}
    \caption{Broj vrednosti amplituda u zavisnosti od broja bitova}
    \label{tab:quantization}
    \end{table}

Audio signal se zatim predstavlja kao diskretan niz vrednosti $x[n]$. Kod mono signala to je jednodimenzionalni niz, dok stereo signal ima dva kanala.