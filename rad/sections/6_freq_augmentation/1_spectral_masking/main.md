## 5.1 Spectral masking (SpecAugment)

Spectral masking ili *SpecAugment* je napredna tehnika augmentacije audio podataka, prvi put opisana u radu Google Brain-a tima iz 2019. pod naslovom *SpecAugment: A Simple Data Augmentation Method for Automatic Speech Recognition*. Ova metoda je pokazala dosta dobre rezultate kod automatskog prepoznavanje ljudskog govora (ASR).

Metoda je bazirana na augmentaciji log mel spektrograma ulaznog audio signala i inspirisana je maskiranjem kod augmentacije u vizuelnom domenu. Tehnika je komputaciono jeftina i primenjuje se direktno na log mel spektrogramu, kao da je spektrogram slika. Zbog ovoga je moguće primeniti spectral masking online, tokom treninga.

SpecAugment se sastoji od tri transformacije nad log mel spektrogramom

- Time warping
- Time masking
- Frequency masking

**Time warping**

Ukoliko imamo log mel spektrogram sa $\tau$ vremenskih koraka, mi ga posmatramo kao sliku gde je vreme horizontalna osa a frekvenca vertikalna osa. Nasumična tačka duž horizontalne linije koja prolazi kroz centar slike u okviru vremena $(W, \tau - W)$ će se *warp*-ovati ulevo ili udesno za distancu $w$ koja se uzima iz uniformne raspodele u opsegu $[0, W]$. Deo signala levo od izabrane tačne se razvlači dok se desni deo skuplja.


\begin{figure}[ht]
\centering
\includegraphics[width=6cm]{figures/5_freq_augm/spec_timewarp.png}
\caption{SpecAugment - Time warping}
\label{fig:spec-timewarp}
\end{figure}

\newpage

**Frequency masking**

Frequency masking se primenjuje tako da se $f$ uzastopnih mel frequency kanala $[f_0, f_0 + f]$ maskiraju, pri čemu se $f$ bira iz uniformne rapsodele u opsegu $[0, F]$ ($F$ je parametar) a $f_0$ se bira iz raspona $[0, \nu - f]$, gde je $\nu$ broj mel frequency kanala.

\begin{figure}[ht]
\centering
\includegraphics[width=7cm]{figures/5_freq_augm/spec_freqmask.png}
\caption{SpecAugment - Frequency masking}
\label{fig:spec-freqmask}
\end{figure}

**Time masking**

Time masking se primenjuje tako da se $t$ vremenskih koraka $[t_0, t_0 + t]$ maskiraju, pri čemu se $t$ bira iz uniformne rapsodele u opsegu $[0, T]$ ($T$ je parametar) a $t_0$ se bira iz raspona $[0, \tau - t]$, gde je $\tau$ broj vremenskih koraka signala.

\begin{figure}[ht]
\centering
\includegraphics[width=7cm]{figures/5_freq_augm/spec_timemask.png}
\caption{SpecAugment - Time masking}
\label{fig:spec-timemask}
\end{figure}

\newpage

Moguće je definisati polise - kombinacije ove 3 metode, sa različitim vrednostima za $W$, $F$, i $T$, kao i primeniti ih na više raspona frekvenci ili više raspona vremenskih koraka. Neki od primera takvih polisa su iz orginalnog rada - $LB$, $LD$, $SM$ i $SS$ koji (izuzev $LB$) primenjuju transformacije nad 2 odvojena raspona frekvencija i 2 raspona vremenskih koraka, sa različitim $W$, $F$ i $T$ parametrima.

\begin{figure}[ht]
\centering
\includegraphics[width=6cm]{figures/5_freq_augm/spec_policies.png}
\includegraphics[width=6cm]{figures/5_freq_augm/policies.png}
\caption{SpecAugment - Policies}
\label{fig:spec-policies}
\end{figure}

Pored klasičnog SpecAugmenta, postoji i druge varijante koje su nastale iz ove metode. Prvi nedostatak kod SpecAugment-a je što se augmentacija podataka vrši samo nad ulaznim podacima neuronske mreže, što propušta priliku za augmentacijom mel spektrograma *hidden state*-a neuronske mreže. Upravo ovo je ideja algoritma *SpecAugment++*.

Pored toga, ova tehnika uvodi i mogućnost maskiranja frekvenci i vremena, ali ne striktno anuliranjem, već i dodeljivanjem druge vrednosti. Konkretno, rad je opisao 3 metoda augmentacije.

- **ZM - Zero Value Masking**\
    Klasična transformacija, kao i kod *SpecAugment*a. Deo frekvencija i deo vremenskih koraka se postavlja na 0.

- **MM - Mini-batch based mixture masking**\
    Kod ove metode se uzimaju mini-batch-evi audio signala nad kojima se primenjuje augmentacija. Tada se hidden state trenutnog *sample*-a $x \in \mathbb{R}^{T \times X}$ menja tako što se uzima hidden state nekog drugog *sample*-a iz istog mini-batcha $y \in \mathbb{R}^{T \times X}$ i u okviru odabranog raspona frekvenci i odabranog raspona vremenskog intervala se računa vrednost mel spektrograma uzorka $x$ kao prosek vrednosti $x$ i $y$.

- **MM - Mini-batch based mixture masking**\
    Kod ove metode se uzimaju mini-batch-evi audio signala nad kojima se primenjuje augmentacija. Tada se hidden state trenutnog *sample*-a $x \in \mathbb{R}^{T \times X}$ menja tako što se uzima hidden state nekog drugog *sample*-a iz istog mini-batcha $y \in \mathbb{R}^{T \times X}$ i u okviru odabranog raspona frekvenci i odabranog raspona vremenskog intervala mel spektrogramu uzorka $x$ se dodeljuje vrednost spektrograma $y$.

\newpage

\begin{figure}[ht]
\centering
\includegraphics[width=5cm]{figures/5_freq_augm/spec_pp.png}
\caption{SpecAugment++}
\label{fig:spec-pp}
\end{figure}

Najveći nedostatak ove metode je potreba za pažljivi tune-ovanjem parametara augmentacije. Zbog toga je nastala varijacija ovih metoda koja pokušava da automatski odredi najbolje parametre - *Policy-SpecAugment*.

Neka su moguće augmentacije $\{A_1, A_2, A_3\} = \{TimeWarp, FreqMask, TimeMask\}$ i neka je u epohi $j$, prosečan validation loss primenom samo $i$-te augmentacije $\mathcal{L}_i^j$.

Zatim se ti validation loss-ovi koriste kako bi se dobio vektor verovatnoća
$$
\begin{equation}
P_i^{(j)} = \frac{\mathcal{L}_i^{(j)}}{\sum_{k=1}^{3} \mathcal{L}_k^{(j)}}
\end{equation}
$$

Ovako dobijenim vektorima verovatnoće moguće je dalje usmeriti augmentaciju tako da se primenjuju one transformacije koje će poboljšati performanse.


\begin{table}[h]
\centering
\begin{tabular}{|c|c|c|}
    \hline
    Prednosti & Nedostaci \\
    \hline
    Izuzetno efikasna za ASR zadatke & Može maskirati kritične informacije \\
    Može maskirati kritične informacije & Potrebno pažljivo tune-ovanje parametara za specifične zadatke \\
    Brza jer radi direktno na spektrogramu & \\
    \hline
\end{tabular}
\caption{Prednosti i nedostaci SpecAugment-a}
\label{tab:specaug_procon}
\end{table}