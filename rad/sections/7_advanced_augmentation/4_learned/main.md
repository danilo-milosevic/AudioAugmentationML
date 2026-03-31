## 6.4 Naučene augmentacije korišćenjem neuronskih mreža

Problem kod svih prethodnih metoda augmentacije je bila potreba za ručnim definisanjem pravila kako augmentisati podatke. Umesto ručne augmentacije, moguće je naučiti modele da generišu nove podatke (generativni modeli kao što su GAN-ovi, autoencoderi itd.) ili definisanjem mogućih augmentacija nakon čega model uči kako kombinovati augmentacije da bi model ostvario bolje rezultate preko reinforcement learning-a

### 6.4.1 AutoAugment

Opisan u Google-ovom radu iz 2019 godine, predstavlja reinforcement learning metodu koja uči kako kombinovati augmentacije tako da model ostvari bolje performanse. Iako prvenstveno razvijan za slike, moguće je primeniti i na audio podacima.

Princip rada je sledeći

1. **Inicijalizacija**

    U prvom koraku se incijalizuje, odnosno definiše *search space* augmentacija što predstavlja sve moguće augmentacije koje agent može primeniti nad podacima kao i njihove parametre. Cilj agenta je pronaći u tom prostoru augmentacija najbolje kombinacije.

2. **Predlaganje politike**

    U sledećem koraku reinforcement learning agent predlaže *augmentation policy*, tj politiku augmentacije, što predstavlja kombinaciju augmentacija i parametara.

3. **Trening modela**

    Koristeći predloženu politiku augmentacije, model se trenira sa augmentisanim skupom podataka i mere se performanse tako dobijenog modela.

4. **Ažuriranje agenta**

    Mere se performanse modela treniranog sa primenjenom politikom i rezultati se koriste kao nagrade (*reward*) za reinforcement learning agenta. Na ovaj način, kroz iteracije, agent uči koje augmentacije najbolje utiču na performanse modela-


\begin{figure}[ht]
\centering
\includegraphics[width=8cm]{figures/6_advanced_augm/autoaugment.jpg}
\caption{AutoAugment kod slika}
\label{fig:autoaugment}
\end{figure}

\newpage

### 6.4.2 Augmentacija generativnim modelima

Generativnim modelima je moguće generisati nove instance podataka nad kojima se kasnije može model trenirati. Postoji više tipova generativnih modela, međutim ovde ćemo razmotriti način rada *GAN*-ova odnosno generativnih adverserijalnih mreža i njihovu upotrebu za augmentaciju podataka.

Generativne adverserijalne mreže se sastoje od dve komponente - **generatora** i **diskriminatora** i rade na sledećem principu

1. **Generator generiše *fake* podatke**

    Generator dobija na ulaz-u šum koji zatim pretvara u izlaz koji treba biti što uverljiviji.

2. **Diskriminator predviđa da li je ulaz lažan ili pravi podatak**

    Diskriminator se trenira da prepozna da li je podatak pravi ili lažan, tako što se na ulaz dovodi podatak, on generiše predviđanje a zatim se težine koriguju u zavisnosti da li je predviđanje tačno.

3. **Generator se ažurira**

    Na osnovu rezultata diskriminatora se nagrađuje ili kažnjava generator. Ako je diskriminator prepoznao lažan podatak, generator se kažnjava a suprotnom nagrađuje i težine generatorske mreže se koriguju.

4. **Kraj treninga**

    Trening se završava kada tačnost predviđanja diskriminatora dođe do 50%, tj kada disktriminator više ne može sa sigurnošću da razlikuje prave i lažne podatke.

\begin{figure}[ht]
\centering
\includegraphics[width=8cm]{figures/6_advanced_augm/gan.jpeg}
\caption{Princip rada $GAN$a}
\label{fig:gan}
\end{figure}

Kod augmentacije audio podataka možemo koristi GAN-ove za generisanje novih primera i to pomoću

- **WaveGan** koji služi za generisanje zvuka u wave formatu
- **SpecGAN** koji služi za generisanje spektrograma

Prednost ove metode je što može lako generisati nove primere pa time pomoći kada nemamo puno primera ili kod nebalansiranih klasa, međutim treniranje *GAN*-ova je dugo i može biti teško podesiti parametre kako bi dobili dobre rezultate.

\newpage


\begin{table}[h]
\centering
\begin{tabular}{|c|c|c|}
    \hline
    Prednosti & Nedostaci \\
    \hline
    Može otkriti nove, efikasne augmentacije & Ekstremno računski skupo \\
    Automatizuje augmentaciju & Treniranje $GAN$a može biti dugo \\
    Visoko realistični primeri kod $GAN$a & \\
    \hline
\end{tabular}
\caption{Prednosti i nedostaci naučenih augmentacija}
\label{tab:learned_procon}
\end{table}