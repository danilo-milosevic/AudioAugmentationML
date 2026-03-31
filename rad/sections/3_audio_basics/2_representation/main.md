## 2.2 Reprezentacije audio signala

Audio signali se mogu predstaviti i analizirati na više načina, pri čemu se uglavnom predstavljaju u vremenskom ili u frekventnom domenu.

- **Vremenski domen**
    
    Najjednostavnija reprezentacija audio signala - prikaz amplitude signala kroz vreme. 


    \begin{figure}[h]
    \centering
    \includegraphics[width=7cm]{figures/3_audio_basics/waveform.png}
    \caption{Prikaz audio signala u vremenskom domenu}
    \label{fig:time_domain}
    \end{figure}

    \begin{table}[h]
    \centering
    \begin{tabular}{|c|c|}
        \hline
        Prednosti & Nedostaci \\
        \hline
        Vremenske informacije su očuvane & Nepogodno za analizu frekvencija \\
        Nema gubitaka tokom konverzije & Zahteva duže sekvence za neuronske mreže \\
        Lako za razumevanje i prikaz & \\

        \hline
    \end{tabular}
    \caption{Prednosti i nedostaci prikaza audio signala u vremenskom domenu}
    \label{tab:time_procon}
    \end{table}

- **Frekventni domen** 

    Furijeovom transformacijom je moguće izvršiti dekompoziciju audio signala na njegove frekvencije. Analiza signala korišćenjem
    Furijeove transformacije je pogodna za slučajeve kada frekvencije signala ne variraju vremenom. U realnosti je ovo retkost,
    s obzirom da ljudski govor i muzika variraju vremenom, tj oni su aperiodični signali.

    Zato umesto direktnog vršenja Furijeove transformacije nad signalom, možemo ulazni signal da podelimo na preklapajuće segmente a zatim
    nad njima vršiti FFT.
    Podelom audio signala na kratke preklapajuće segmente, a zatim primenom Furijeove transformacije dobijamo STFT - *Short Time Fourier Transform*.

    Matematički STFT se može definisati kao
    \begin{equation}
    \mathrm{STFT}\{x[n]\}(m,\omega)
    = \sum_{n=-\infty}^{\infty} x[n]\; w[n - m]\; e^{-j \omega n}
    \end{equation}
    pri čemu je $x[n]$ ulazni signal u trenutku $n$, dok je $w$ window funkcija i $m$ vreme u okviru kog analiziramo frekvence.

    \newpage

    \begin{figure}[h]
    \centering
    \includegraphics[width=5cm]{figures/3_audio_basics/stft_exp.png}
    \includegraphics[width=5cm]{figures/3_audio_basics/stft.png}
    \caption{Levo - Proces dobijanja STFT reprezentacije. Desno - STFT reprezentacija. X osa predstavlja vreme, Y osa frekvence a boja intenzitet.}
    \label{fig:stft_exp}
    \end{figure}
    
    
    Postoji više window funkcija, ispod je dat primer Hann-ove window funkcije

    \begin{equation}
    w[n] =
    \begin{cases}
    \displaystyle
    \frac{1}{2}
    \left(
    1 - \cos\!\left(\frac{2\pi n}{N-1}\right)
    \right),
    & 0 \le n < N, \\[8pt]
    0, & \text{u suprotnom.}
    \end{cases}
    \end{equation}

    STFT reprezentacija međutim ne opisuje najbolje kako ljudsko uho percipira zvuk. Na osnovu istraživanja je zaključeno
    da ljudi najbolje registruju i razlikuju zvukove u rasponu frekvenci od 500 do 1000Hz, dok teško razlikuju više frekvence
    npr 1-1.5kHz.
    Upravo zato je osmišljena mel skala. Mel skala se dobija pretvaranjem linearnog spektrograma u logaritamski na sledeći način
    $$
    m = 2595 \cdot \log_{10}\Big(1 + \frac{f}{700}\Big)
    $$
    pri čemu je $m$ rezultujuća vrednost a $f$ ulazna frekvenca.

    \begin{figure}[h]
    \centering
    \includegraphics[width=5cm]{figures/3_audio_basics/mel.png}
    \caption{Mel spektrogram}
    \label{fig:mel}
    \end{figure}

    Mel spektrogram je pogotovo koristan kod zadataka prepoznavanja govora i muzike.