## 2.3 Izazovi u radu sa audio podacima

Rad sa audio podacima kod mašinskog učenja donosi nekoliko specifičnih izazova

- **Promenljivo trajanje zvučnih zapisa**

    Za razliku od slika koje imaju fiksne dimenzije, audio snimci mogu biti proizvoljnog trajanja. Model mora biti u stanju da procesira signale različite dužine što može da uradi
    - Korekcijom dužine snimka, skraćivanjem ili padd-ovanjem signala
    - Korišćenjem arhitektura koje primaju ulaze različitih dužina (rekurentne mreže, transformeri)

- **Velika dimenzionalnost**
    
    Audio sa frekvencijom semplovanja od 16kHz ima 16000 vrednosti u sekundi. Za snimak od 10 sekundi, to je 160000 vrednosti. Zbog toga se često koriste kompresovane reprezentacije.

- **Osetljivost na šum**

    Zvukovi snimljeni u realnim uslovima često sadrže različite vrste šuma kao što su pozadinski šum, električni šum mikrofona, odjek prostorija, zvukove iz više različitih izvora koji se prepliću (govor više ljudi u isto vreme) itd.

- **Nedostatak label-ovanih podataka**

    Kvalitetni, labelovani audio skupovi podataka su relativno mali i skupi. Problem je u tome što je za govor potrebno ručno izvršiti transkripciju sa preciznom vremenskom anotacijom, dok je za muziku potrebna kategorizacija žanrova, instrumenata, takta itd.

- **Varijabilnost govora**

    Kod prepoznavanja govora mnogo faktora utiče na audio signal - jezik, akcenat, pol, emotivno stanje, brzina govora, artikulacija, pozadinski šum itd.

Baš zbog ovih izazova je augmentacija audio podataka ključna za treniranje modela koji će imati dobre performanse u realnim uslovima.

\begin{figure}[h]
\centering
\includegraphics[width=7cm]{figures/3_audio_basics/augment.png}
\caption{Nekoliko vrsta augmentacija audio signala}
\label{fig:augmentation_sample}
\end{figure}