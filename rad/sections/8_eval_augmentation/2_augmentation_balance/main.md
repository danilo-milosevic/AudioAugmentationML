## 7.2 Balans između količine augmentacije i performansi

Veliki problem kod augmentacije podataka jeste koliko augmentacije primeniti.

**Premalo** augmentacije može izazvati

- Overfitting modela na trening podacima
- Loša generalizacija na test podacima

dok **previše** augmentacije može izazvati

- Gubitak važnih informacija
- Podaci mogu postati nerealistični
- Sporija konvergencija

Postoji nekoliko načina za pronalaženje balansa u augmentaciji

1. **Ablation study**

    Ovom metodom se sistematski testira efekat svake augmentacije pojedinačno kao i u kombinaciji.
    Prvi korak je izmeriti performanse bez ikakvih augmentacija, odnosno *baseline* a zatim primeniti svaku augmentaciju odvojeno kao i njihove kombinacije. Na osnovu skupljenih metrika (npr preciznost) možemo zaključiti koja je najbolja kombinacija metrika

2. **Parameter sweep**

    Može se koristiti i u kombinaciji sa *ablation study*. Cilj je varirati intenzitet augmentacija dok ne zaključimo najbolje parametre za augmentacije.

3. **Nadgledati krive metrika**

    Kod ove metode potrebno je nadgledati krive trening i validacionih metrika.
    Ukoliko je gap veliki potrebno je više augmentacije, ukoliko su metrike loše onda je potrebno smanjiti augmentacije ili promeniti model, dok ako je konvergencija spora moguće je da imamo previše augmentacije.

4. **Progresivna augmentacija**

    Umesto primenjivanja pune augmentacije vršimo postepeno povećanje augmentacija tokom treninga.

5. **Validacija u različitim uslovima**

    Dobra ideja je evaluirati model na više različitih test setova - na čistom setu, test setu sa dodatim šumom, test setu sa dodatom reverbacijom itd.

Generalni saveti tokom augmentacija koje ćemo primeniti i tokom evaluacije u praktičnom delu rada su

- Početi sa manjom augmentacijom a zatim dodavati postepeno
- Augmentaciju vršiti na 40-70% trening primera, ne na svim
- Validaciju i testiranje vršiti bez primenjenih augmentacija
