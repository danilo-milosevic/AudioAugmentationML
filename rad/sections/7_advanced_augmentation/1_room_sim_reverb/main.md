## 6.1 Simulacija prostorija i reverberacije

Reverbacija, odnosno odjek, je akustički fenomen koji nastaje kao posledica refleksije zvuka od površina u prostoriji i zato zavisi od geometrije prostorije i predmeta u njoj. Zbog ovoga je simuliranje reverbacija veoma korisna metoda augmentacije audio podataka, s obzirom da dodaje raznovrsnost i realizam među audio podacima.

Kada se zvuk emituje u prostoriji, slušalac čuje taj zvuk na više načina

- **Direktno od izvora**

    Zvuk koji stiže od izvora do slušaoca najkraćim, direktnim putem.
    S obzirom da se zvuk emituje podjednako u svim pravcima, samo mali deo energije zvučnog talasa dolazi do slušaoca, dok većina predstavlja indirektni zvuk koji se dalje deli na kategorije ispod.

- **Rane refleksije**

    Ostatak zvuka koji ne dolazi do slušaoca direktno od izvora se odbija od zidova, prozora, kao i svih predmeta u prostoriji. Zvuk koji nakon odbijanja dolazi do slušaoca u roku od 0-50$ms$ predstavlja ranu refleksiju.
    Rane refleksije su veoma bitne za razumevanje ljudskog govora. Ukoliko se izvor i slušalac nalaze u otvorenoj ravnoj prostoriji (ravnica, pustinja...) jedini zvuk koji dolazi do slušaoca je direktan zvuk, pa će se zvuk slabo čuti već posle nekoliko metara.

- **Kasne refleksije**

    Kasne refleksije su jasno odvojene od originalnog signala i lako primetne ljudskom uhu kao zakašnjenja. Primer ovoga je eho. Kasne refleksije nastaju odbijanjem zvuka i dolaska do slušaoca nakon 50$ms$ do 250$ms$.

- **Reverberacija**

    Zvuk koji nastaje odbijanjem originalnog signala od zidova i predmeta u prostoriji i dolazi do slušaoca nakon 250$ms$ i više se ne prepoznaje kao zakasneli originalni zvuk, već kao relativno tih zvuk koji dolazi iz svih smerova. Reverberacija može da traje oko 2-5$s$ nakon čega zvuk potpuno nestaje.

\begin{figure}[ht]
\centering
\includegraphics[width=4.5cm]{figures/6_advanced_augm/reflections.png}
\includegraphics[width=4.5cm]{figures/6_advanced_augm/reverb.png}
\caption{Izvori zvuka}
\label{fig:rev_ref}
\end{figure}

Za predstavljanje reverbacije u nekom prostoru koristi se **Room Impulse Response** koji predstavlja funkciju koja opisuje kako se u okviru prostorije prostiru direktni zvukovi, rane i kasne refleksije kao i reverberacija.

Kako bi se dobio reverberiran signal primenjuje se konvolucija izvornog zvuka i *RIR*a.
$$
y(t) = x(t) \otimes h(t)
$$

Bitan parametar reverbacije je **RT60**, odnosno vreme u sekundama potrebno da zvuk oslabi za 60$dB$ nakon što izvor prestane da emituje zvuk, time opisujući reverbaciju prostorije. Za standardne prostorije (sobe u kući) *RT60* je 0.2-0.4 sekunde, dok je na primer kod katedrala oko 5-10s. Ovo vreme zavisi od veličine i oblika prostorije kao i od materijala zidova - neki materijali više ili manje apsorbuju zvuk.

Postoji nekoliko metoda primene reverbacije

1. **Konvolucija sa snimljenim RIR-om**

    Predstavlja najrealističniji pristup. Prvo se snimi room impulse response u više različitih prostorija a zatim se primenjuje konvolucija RIR-a i originalnog signala. Postoje više javno dostupnih RIR dataset-ova kao što su *MIT Acoustical Reverbation Scene Statistics Survey*, *OpenAIR*, *BIRD* i mnogi drugi.

2. **Algoritamska reverbacija**

    Umesto snimanja RIR-a za različite prostorije moguće je algoritamski simulirati reverbaciju različitih prostorija.
    Neki od najpoznatijih algoritama su *Schroeder*-ov reverb, *Freeverb* (baziran na *Schroeder*-ovom reverbu), *Dattorro* reverb i mnogi drugi.
    
    *Schroeder*-ov reverb radi na osnovu više paralelnih comb filtera i više serijskih allpass filtera koji puštaju sve frekvence ali menjaju faze signala. Izlazi paralelnih comb filter-a se sekvencijalno propuštaju kroz allpass filtere i na kraju se dobija signal sa reverberacijom.


\begin{figure}[ht]
\centering
\includegraphics[width=5cm]{figures/6_advanced_augm/schroeder.png}
\caption{$Schroeder$ reverbacija}
\label{fig:schroeder}
\end{figure}

3. **Parametarski pristup**

    Koristi parametre kao što su pre-delay, decay time, diffusion da generiše reverbaciju bez fizičke simulacije.

\begin{table}[h]
\centering
\begin{tabular}{|c|c|c|}
    \hline
    Prednosti & Nedostaci \\
    \hline
    Visoko realistična augmentacija & Računski skupa \\
    Poboljšava robusnost na različite akustičke uslove & Računski skuplja \\
    \hline
\end{tabular}
\caption{Prednosti i nedostaci simulacije reverbacije}
\label{tab:reverb_procon}
\end{table}