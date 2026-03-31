## 5.3 Filtering

Filtriranje je metoda augmentacije audio podataka kao i tehnika obrade signala gde se određene frekvencije (audio ili slike) zadržavaju dok se određene frekvencije izbacuju ili atenuiraju, odnosno umanjuju određenim faktorom.

Frekvencija nakon koje kreće atenuacija ili odbacivanje se zove **cutoff** frekvencija. 

Postoji više različitih vrsta filtera, zavisno od toga koje frekvencije filtriraju

### 5.3.1 Low-pass filter

Low-pass filter atenuira odnosno oslabljuje frekvencije iznad datog cutoff-a. Koristi se prvenstveno za redukciju šuma kako u audio snimcima tako i u slikama, s obzirom da je šum najčešće signal visoke frekvence kao što je pozadinski ili električni šum kod mikrofona.

\begin{figure}[ht]
\centering
\includegraphics[width=7cm]{figures/5_freq_augm/lpf.jpg}
\caption{Low-pass filter}
\label{fig:lpf}
\end{figure}

### 5.3.2 High-pass filter

High-pass filter predstavlja komplement low-pass filtera, odnosno atenuira frekvencije ispod zadatog cutoff frekvencije. Najčešće se koristi za redukciju šuma niskih frekvencija (kao što je šum nastao dodirivanjem mikrofona, pozadinskog šuma nastalog klima uređajima itd.) kao i za poboljšanje jasnoće ljudskog govora.

\begin{figure}[ht]
\centering
\includegraphics[width=7cm]{figures/5_freq_augm/hpf.jpg}
\caption{High-pass filter}
\label{fig:hpf}
\end{figure}

### 5.3.3 Band-pass filter

Nastaje kombinacijom low-pass i high-pass filtera, odnosno atenuira frekvencije ispod zadate frekvencije $f_L$ i iznad frekvencije $f_H$. Kod audio augmentacije koristi se za uklanjanje istovremeno nisko frekventnog i visoko frekventnog šuma.

\begin{figure}[ht]
\centering
\includegraphics[width=7cm]{figures/5_freq_augm/bpf.jpg}
\caption{Band-pass filter}
\label{fig:bpf}
\end{figure}

\newpage

### 5.3.4 Band-stop filter

Takođe poznat kao i band-reject filter, predstavlja komplement band-pass filter-a. Ovde se filtriraju frekvencije u opsegu $[f_L, f_H]$. Primer primene kod audio obrade je uklanjanje mikrofonije kod muzike.

\begin{figure}[ht]
\centering
\includegraphics[width=7cm]{figures/5_freq_augm/bsf.jpg}
\caption{Band-stop filter}
\label{fig:bsf}
\end{figure}

### 5.3.5 Comb filter

Nastaje atenuacijom više različitih raspona frekvencija
$$
{[f_{L_1}, f_{H_1}], [f_{L_2}, f_{H_2}], [f_{L_3}, f_{H_3}], \dots [f_{L_n}, f_{H_n}]}
$$
zbog čega signal dobija izgled češlja. U praksi se comb filter implementira dodavanjem signala koji je pomeren vremenski originalnom signalu, tj formulom

$$
y[n] = x[n] + \alpha x[n-K]
$$
gde je $\alpha$ parametar koji kontroliše koliko se dodaje vremenski pomeren signal a $K$ predstavlja zakašnjenje, tj *delay*.

\begin{figure}[ht]
\centering
\includegraphics[width=7cm]{figures/5_freq_augm/comb.jpg}
\caption{Comb filter}
\label{fig:comb}
\end{figure}

\begin{table}[h]
\centering
\begin{tabular}{|c|c|c|}
    \hline
    Prednosti & Nedostaci \\
    \hline
    Precizna kontrola frekvencijskog sadržaja & Može poremetiti faze \\
    Simulacija različitih prenosnih medijuma & Može ukloniti važne informacije \\
    \hline
\end{tabular}
\caption{Prednosti i nedostaci filtering-a}
\label{tab:filter_procon}
\end{table}