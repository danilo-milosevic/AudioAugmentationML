## 4.1 Time Stretching

Time stretching je metoda augmentacije audio podataka kojom se produžava ili skraćuje trajanje audio signala bez promene visine tona.


Među jednostavnijim metodama za time stretching je SOLA - *Synchronous Overlap-Add*. Algoritam funkcioniše tako što
deli audio na preklapajuće segmente, *frame*-ove i rekonstruiše audio signal sa drugačijim rastojanjem između segemenata.
Kod usporenja to znači približavanje segmenata, dok kod produženja se segmenti udaljavaju. Radi na sledećem principu

1. **Deljenje na segmente**\
    Signal se deli na preklapajuće prozore fiksne veličine, oko 10-100ms, zavisno od toga koliko želimo da promenimo dužinu. 
2. **Preklapanje segmenata**\
    Svaki segment se parcijalno prekriva drugim segmentom (izbor segmenta zavisi od sličnosti između njih, tj biramo slične segmente za preklapanje).
    Preklapanje se vrši kako bi ublažili prelaz između segmenata

    \begin{figure}[h]
    \centering
    \includegraphics[width=4cm]{figures/4_time_augm/sola.png}
    \caption{SOLA}
    \label{fig:sola}
    \end{figure}

Ovaj algoritam ima više varijanti kao što su *WSOLA* i *PSOLA*. U praksi, najbolji je kod jednostavnih, periodičnih audio signala.
Nekada daje loše rezultate, kada dođe do lošeg preklapanja segmenata.

Bolja metoda time stretchinga je **Phase vocoder** algoritma koji radi na sledeći način:

1. **Podeli spectrogram na kratke vremenske prozore tj, *frame*-ove**
    Dobijeni *frame*-ovi se preklapaju delom.
2. **Primeni STFT na *frame*-ove**\
    čime dobijamo amplitude i faze za sve frekvencije u svakom od preklapajućih *frame*-ova
3. **Promena rastojanja *frame*-ove**\
    Kod ubrzavana *frame*-ovi se približavaju kreirajući overlap. Kod usporavanja će rastojanje biti veće, pa će nastati prazan
    prostor koji će se popuniti dupliranim *frame*-ovima ili interpolacijom.
4. **Prilagodi fazu svake frekvencije kako bi obezbedio kontinuitet**\
    Kako bi izbegli primetne skokove u zvuku, potrebno je prilagoditi faze frekvencija kako bi se bolje usaglasili 
    *frame*-ovi.
5. **Primeni inverzni STFT**\
    Dobijamo izvorni zvuk ali usporen ili ubrzan.


    \begin{figure}[h]
    \centering
    \includegraphics[width=8cm]{figures/4_time_augm/vocoder.png}
    \caption{Phase vocoder}
    \label{fig:vocoder}
    \end{figure}

Koliko će se promeniti trajanje signala kontroliše se parametrom $\alpha$.

- $\alpha > 1$ - ubrzan snimak
- $\alpha < 1$ - usporen
- $\alpha = 1$ - bez promene

Time stretching je koristan za

- Simulaciju različitih brzina govora
- Augmentaciju podataka za prepoznavanje govora
- Povećanje invarijantnosti na tempo kod muzike
- Prilagođavanje dužine audio snimaka

    \begin{table}[h]
    \centering
    \begin{tabular}{|c|c|c|}
        \hline
        Prednosti & Nedostaci \\
        \hline
        Zadržava visinu i tonalitet & Povećava vremensku raznovrsnost podataka \\
        Prirodno zvuči u razumnom opsegu faktora & Računski zahtevnije nego jednostavnije augmentacije \\
        Povećava vremensku raznovrsnost podataka & Može narušiti prirodnost govora ako se pretera \\
        \hline
    \end{tabular}
    \caption{Prednosti i nedostaci time shiftinga}
    \label{tab:timestretch_procon}
    \end{table}