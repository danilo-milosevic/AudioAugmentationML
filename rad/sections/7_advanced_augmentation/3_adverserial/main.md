## 6.3 Adverserijalne augmentacije

Kod ove metode augmentacije se u trening skupu dodaju nove instance koje su generisane izmenom originalne instance tako da se obmane model.

Na slici ispod možemo videti primer adverserijalne perturbacije na primeru slika kao i audio podataka. Dodavanjem specifično dizajniranog šuma slici ili audio zapisu model generiše znatno drugačije izlaze.

\begin{figure}[ht]
\centering
\includegraphics[width=8cm]{figures/6_advanced_augm/adverserial.png}
\caption{Primer adverserijalnih perturbacija}
\label{fig:adverserial}
\end{figure}

Međutim ručno definisati adverserijalne perturbacije za svaki trening primer je nepraktično, pogotovo kod većih skupova podataka, tako da je potrebno generisati algoritamske perturbacije. Razmotrićemo ispod dve tehnike.

### 6.3.1 Fast Gradient Sign Method

Fast Gradient Sign Method ili *FGSM* je primer white-box napada, što znači da zahteva znanje arhitekture i parametara modela. Ideja je da se originalnom podatku doda mala količina šuma baziranog na gradientu loss funkcije po ulaznom vektoru.

Princip rada ovakve augmentacije je

1. **Trening modela**

    S obzirom da je potrebno imati definisanu arhitekturu i parametre modela, potrebno je kreirati model i trenirati ga nad datim skupom podataka.

2. **Računanje gradijenta**

    Ako imamo $x$ kao ulazni podatak, $y$ klasu i $J(\theta, x, y)$ kao loss funkciju pri čemu $\theta$ predstavlja parametre modela, onda se gradijent dobija kao
    $$
        \nabla_x J(\theta, x, y) = \dfrac{\partial x}{\partial J}
    $$

3. **Računanje perturbacije**

    Na osnovu dobijenog gradijenta možemo sračunati perturbaciju $\delta$ na sledeći način
    $$
        \delta = \epsilon \cdot sign(\nabla_x J(\theta, x, y))
    $$
    pri čemu $\epsilon$ predstavlja magnitudu perturbacije.

4. **Generisanje adverserijalnih primera**

    Za svaku od instanci $x$ u originalnom trening skupu možemo odrediti gradijent i perturbaciju. Tada se dobija adverserijalni primer na sledeći način
    $$
        x' = x + \delta
    $$

5. **Retreniranje modela**

    Sa tako dobijenim skupom podataka koji sačinjavaju originalne instance i adverserijalni primeri možemo ponovo trenirati model koji će biti otporniji na adverserijalne napade.


\begin{figure}[ht]
\centering
\includegraphics[width=8cm]{figures/6_advanced_augm/fgsm.png}
\caption{Fast Gradient Sign Method}
\label{fig:fgsm}
\end{figure}

\newpage

### 6.3.2 Projected Gradient Descent

Projected Gradient Descent ili *PGD* predstavlja iterativni algoritam za dobijanje adverserijalnih primera i baziran je na sličnim idejama koje imamo kod *FGSD*a, tj koristi računanje gradijenta i perturbacije.
Razlikuje se od *FGSD*a po tome što dodaje perturbaciju iterativno, u više koraka, i to na sledeći način.

1. **Inicijalni uslov i ulazni parametri**

    Na početku biramo broj iteracija $T$, maksimalnu magnitudu perturbacije $\epsilon$ i veličinu koraka $\alpha$. U ovom korako postavljamo incijalno
    $$ x'_0 = x_0 + noise $$
    Šum, tj $noise$ se sample-uje iz uniformne raspodele u dozvoljenoj $\epsilon$-lopti.

2. **Iterativni postupak**

    U svakom koraku $t = 0, 1, \dots, T-1$ računamo gradijent loss funkcije za ulaz $x'_t$, a zatim uzimamo njen znak, slično kao kod *FGSD*a. Zatim se vrši ažuriranje vrednosti na sledeći način
    $$ x'_{t+1} = \Pi (x'_t + \alpha \cdot sign(\nabla_x J(\theta, x'_t, y)))$$
    pri čemu je $\Pi$ **projekciona** funkcija koja ograničava vrednosti sledećeg koraka na validne vrednosti za dati tip podataka - npr kod audio augmentacije ograničava amplitudu signala kako ne bi previše odudarala od početne vrednosti.

3. **Retreniranje modela**

    Kao i kod *FGSD*a, s obzirom da tokom generisanja primera koristimo težine modela, potrebno je izvršiti retreniranje modela korišćenjem augmentovanog skupa podataka.

U odnosu na *FGSD* ova metoda je dosta sporija, s obzirom da se vrši u više iteracija ali zato proizvodi robustnije adverserijalne primere.

\begin{figure}[ht]
\centering
\includegraphics[width=8cm]{figures/6_advanced_augm/pgd.png}
\caption{Projected Gradient descent}
\label{fig:fgsm}
\end{figure}

\begin{table}[h]
\centering
\begin{tabular}{|c|c|c|}
    \hline
    Prednosti & Nedostaci \\
    \hline
    Jednostavna implementacija & Potrebno tuniranje $\epsilon$ parametra \\
    Postiže se robustnost na adverserijalne napade & Računski skupo \\
    Služi kao i regularizacija & Može usporiti konvergenciju \\
    \hline
\end{tabular}
\caption{Prednosti i nedostaci adverserijalne augmentacije}
\label{tab:advers_procon}
\end{table}