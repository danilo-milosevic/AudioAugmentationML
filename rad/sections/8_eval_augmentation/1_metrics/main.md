## 7.1 Metrike performansi

Kao i kod ostalih domena, za merenje performansi kod klasifikacionije audio podataka možemo koristiti standardne metrike, kao što su

- **Konfuzione matrice** koje upoređuju predviđene i prave klase, što se kod binarne klasifikacije svodi na 4 vrednosti - true positive, true negative, false positive i false negative.
- **Accuracy** koji se računa kao

    $$Accuracy = \dfrac{TP + TN}{TP + TN + FP + FN}$$
- **Precision** koji se računa kao 
    
    $$Precision = \dfrac{TP}{TP + FP}$$
- **Recall** koji se računa kao 
    
    $$Recall = \dfrac{TP}{TP + FN}$$
- **F1-Score** koji se dobija na osnovu precision i recall-a
    
    $$F1 = 2 \dfrac{Precision \cdot Recall}{Precision + Recall}$$
    
    F1 je pogotovo korisna metrika kod neujednačenih skupova i može se računati na dva načina
    - *Macro F1*

        Računa se kao prosek F1 za svaku od klasa, gde se svaka klasa tretira podjednako
    
    - *Micro F1*

        Računa se globalno, preko svih instanci, time favorizujući većinske klase
- **Mathews korelacioni koeficijent** računa se na sledeći način

    $$MCC = \dfrac{TP\cdot TN - FP \cdot FN}{\sqrt{(TP+FP)(TP+FN)(TN+FP)(TN+FN)}}$$

Pored standardnih metrika postoje i metrike specifične kod audio problema

- **Word Error Rate**
    
    Koristi se kod *ASR - Automatic Speech Recognition* i računa se na sledeći način
    $$
        WER = \dfrac{S + D + I}{N}
    $$
    pri čemu je $S$ broj pogrešno prepoznatih reči, $D$ broj reči koje fale, $I$ broj dodatih reči koje nisu u snimku dok je $N$ ukupan broj reči u snimku.

- **Character Error Rate**

    Računa se isto kao *WER* ali na nivou karaktera. Ova metrika je korisna kod jezika sa složenim karakterima kao što su japanski, arapski i drugi.

- **Event-Based i Segment-Based F1**

    F1 metrike karakteristične za audio domen. *Event-Based F1* se računa na nivou event-a, događaja u audio zapisu, dok *Segment-Based F1* deli snimak na kratke segmente (oko 1s) i računa F1 na svakom segmentu.
