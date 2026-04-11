# progetto

abbiamo preso il dataset de i voli 
facciamo il progetto EDA + Addestramento dei modelli. 

1. Inziamo, traducendo tutte le colonne del dataset

2. poi abbiamo analizzato i dati mancanti con il grafico dei dati mancanti

3. abbiamo eliminato la colonna "numero volo" che non ci serve all'analisi del dataset e all'implemnentazione di algoritmi predittivi

4. quindi ora facciamo la pulizia del dataset
Le dimensioni del dataset: Vedrai che il numero di righe scenderà un pochino (perché abbiamo tolto i voli cancellati) e il numero di colonne si ridurrà drasticamente, lasciando solo le informazioni essenziali.

La distribuzione del Target: Il comando value_counts() ti dirà esattamente quanti voli nel tuo dataset sono puntuali (0) e quanti sono in ritardo (1). Fai molta attenzione a questi due numeri: se i voli in orario sono tantissimi e quelli in ritardo pochissimi, avremo un dataset "sbilanciato" (ma ce ne occuperemo più avanti!).

5. L'Analisi Esplorativa dei Dati (EDA) serve a farti scoprire i "segreti" nascosti nel tuo dataset prima di passare l'informazione all'intelligenza artificiale.
In questa fase risponderemo a tre domande fondamentali usando proprio i grafici chiesti dalla tua professoressa:
Quale compagnia aerea fa più ritardi? (Useremo un Barplot)
Qual è il giorno peggiore per volare? (Useremo un Barplot)

6. 
