## 7.3 Validacione strategije

Nakon što smo objasnili metrike i kako balansirati augmentaciju, potrebno je razmotriti kako validirati rezultate.

- **Cross-Validation i Stratified K-fold**

    Standardne validacione strategije koje se mogu koristiti i u drugim domenima, ne samo kod zvuka. Strategija funkcioniše tako što se skup podataka deli na $k$ delova, zatim se $k$ puta ponavlja proces gde se jedan deo ostavlja za validaciju dok se model trenira nad ostalim komponentama. *Stratified* verzija radi na istom principu ali se vodi računa da se zadrži ista raspodela među klasama u svakom od $k$ delova.

- **Speaker-independent splits**

    Ova metoda je kritična kod generalno svih zadataka gde se prepoznaje govornik ili govor. Ideja ove metode je da se trening, validacioni i test organizuju tako da se govornici u test setu nikada ne uključe u trening set. Cilj je postizanje robustnosti modela za prepoznavanje govora čak i za govornike koje model nije čuo prethodno.

- **Temporal split**

    Koristi se kod time-series ili streaming aplikacija. Ideja je da test validation i test set budu odvojeni u vremenu, tj train set sadrži uzorak snimka u intervalu $[0, t_1)$, validation $[t_1, t_2)$ i test u intervalu $[t_2, t_3]$.

- **Domain-based split**

    Kod ove metode se test i train set razlikuju po domenu, tj train set sadrži podatke iz source domena (npr snimci glasova snimljeni u studiju) a test set sadrži podatke iz target domena (npr glasovi snimljeni u realnom svetu, u imperfektnim uslovima).

- **Augmentation-aware validacija**

    Ukoliko se primenjuje augmentacija uvek treba koristiti ovu metodu, potencijalno sa drugim metodama. Ovom metodom se validacija i testiranje vrše na ne-augmentovanim podacima, kako ne bi dobili lažno dobre rezultate.

\begin{figure}[ht]
\centering
\includegraphics[width=8cm]{figures/7_eval_augmentation/cv.png}
\caption{Cross-Validation}
\label{fig:cv}
\end{figure}
