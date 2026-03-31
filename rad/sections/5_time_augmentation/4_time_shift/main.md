## 4.4 Time Shifting

Predstavlja jednostavnu transformaciju gde se audio signal pomera unapred ili unazad u vremenu.
Na početku ili kraju se zato dodaje tišina ili se cirkularno rotira signal. 

Primena time shiftinga
- Simulacija različitih početnih tačaka detekcije
- Augmentacija za sound event detection
- Povećanje robusnosti na poziciju događaja u snimku

\begin{table}[h]
\centering
\begin{tabular}{|c|c|c|}
    \hline
    Prednosti & Nedostaci \\
    \hline
    Ekstremno brza transformacija & Može obrisati važan sadržaj na početku ili kraju \\
    Ne menja akustički sadržaj & Manje korisna kada je temporalna struktura važna \\
    \hline
\end{tabular}
\caption{Prednosti i nedostaci time shiftinga}
\label{tab:timeshift_procon}
\end{table}