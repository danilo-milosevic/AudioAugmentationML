# 3. Osnove augmentacije audio signala

Augmentacija podataka je tehnika u mašinskom učenju koja uključuje kreiranje novih trening
primera primenom transformacija na postojeće podatke. Metode augmentacije podataka su dizajnirane
tako da uvedu dovoljno varijacije u skupu trening podataka tako da održe realističnost i semantički sadržaj
ali i poboljšaju sposobnost modela da generalizuje.

Postoji više podela augmentacija audio podataka

1. Po domenu primen
    - **Augmentacije u vremenskom domenu** \
        Primenjuju se direktno na waveform audio zapisa
    - **Augmentacije u frekventnom domenu**\
        Primenjuju se na spectrogram audio zapisa
    - **Augmentacije u feature prostoru**\
        Primenjuju se na ekstrakovnim feature-ima
2. Po složenosti
    - **Jednostavne transformacije**\
        Dodavanje šuma, promena pitch-a
    - **Kompozitne transformacije**\
        Nastaju kombinaciju više jednostavnih transformacija
    - **Naučene transformacije**\
        Transformacije primenom treniranih modela kao što su GAN ili varijacioni auto-enkoderi
3. Po determinističnosti
    - **Determinističke**\
        Ista transformacija daje iste rezultate
    - **Stohastičke**\
        Uvode nasumičnost tokom tranformacija

Ciljevi augmentacije podataka su

- **Povećanje veličine trening skupa**\
    Osnovni cilj je kreiranje većeg i raznovrsnijeg trening skupa bez skupljanja novih podataka.
    Duboke neuronske mreže, posebno konvolucione mreže i transformeri, zahtevaju velike
    količine podataka da bi efikasno naučile reprezentacije podataka.

- **Regularizacija i smanjenje overfitting-a**\
    Uvođenjem varijacije u trening podatke, sprečavamo model da "zapamti" specifične detalje trening skupa. Umesto toga,
    model mora naučiti robusnije feature-e koji generalizuju na varijacije. 

- **Simulacija realnih varijacija**\
    U produkciji, model će često morati da koristi zvukove koji se razlikuju od trening podataka po
    kvalitetu snimanja, pozadinskom šumu, akustici prostorije, karakteristikama govornika, itd.
    Augmentacijom možemo da simuliramo ove varijacije tokom treninga, čineći model otpornijim na
    realne uslove korišćenja.

- **Balansiranje skupa podataka**\
    U mnogim scenarijima, dostupni podaci nisu ravnomerno distribuirani kroz klase. Na primer,
    u skupu podataka za klasifikaciju emocija govornika, normalan govor može biti mnogo češći od ljutitog ili
    tužnog govora. Selektivnom augmentacijom manje zastupljenih klasa možemo poboljšati balans skupa podataka.