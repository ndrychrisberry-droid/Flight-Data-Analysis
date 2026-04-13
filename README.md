Analisi e Predizione dei Ritardi dei Voli (2024)
Progetto di analisi dati e machine learning su un campione di voli statunitensi del 2024.
L'obiettivo è costruire un classificatore binario che preveda se un volo arriverà in ritardo
di oltre 15 minuti.

Dataset
Il file sorgente è data/flight_data_2024_sample.csv, con 35 colonne originali in inglese.
Tutte le colonne vengono rinominate in italiano all'inizio del notebook.


Struttura del notebook
1. Caricamento e traduzione
Il dataset viene letto con pandas e le 35 colonne vengono rinominate secondo la convenzione
italiana definita nel dizionario traduzione_totale.
2. Pulizia dei dati
Prima della pulizia viene prodotto un report diagnostico che mostra il numero di voli
cancellati, dirottati e i valori nulli per colonna.
Le operazioni eseguite sono:

rimozione dei voli con cancellato == 1 o dirottato == 1
eliminazione delle colonne a varianza zero (anno), ridondanti (citta_orig,
stato_orig, citta_dest, stato_dest), identificatori non generalizzabili
(num_volo) e colonne quasi interamente nulle (codice_cancellazione,
cancellato, dirottato)

3. Feature engineering
Vengono create le seguenti variabili:

rotta: concatenazione di aeroporto di origine e destinazione (es. JFK-LAX)
ora_partenza: ora estratta dal formato HHMM dell'orario previsto
fascia_partenza: categoria temporale basata sull'ora di partenza
(mattina 5-12, pomeriggio 12-18, sera 18-22, notte altrimenti)
media_meteo_orig: media storica del ritardo meteo per aeroporto di origine
media_ritardo_compagnia: media storica del ritardo vettore per compagnia
media_traffico_orig: media storica del ritardo traffico per aeroporto di origine
media_sicurezza_orig: media storica del ritardo sicurezza per aeroporto di origine
media_ritardo_prec: media del ritardo da aereo precedente per aeroporto
media_durata_rotta: durata media storica della rotta

4. Definizione del target
Dopo aver eliminato le righe senza ritardo_arrivo registrato, viene creata la
variabile target:
pythondf['in_ritardo'] = (df['ritardo_arrivo'] > 15).astype(int)
5. Rimozione delle variabili future
Prima della modellazione vengono rimosse tutte le colonne che sarebbero note
solo a volo completato (ritardi effettivi, orari reali, tempi di rullaggio, ecc.),
per evitare data leakage. Vengono anche rimossi gli identificatori non utili al
modello (aeroporto_orig_cod, aeroporto_dest_cod, ora_part_prevista,
ora_arr_prevista, data_volo).
6. Analisi esplorativa (EDA)
Vengono prodotti grafici con seaborn e matplotlib su:

probabilità di ritardo per mese
probabilità di ritardo per giorno della settimana (1 = lunedì, 7 = domenica)
probabilità di ritardo per fascia oraria
analisi delle medie storiche a confronto tra voli puntuali e in ritardo

7. Preparazione per il modello
Le variabili categoriche (compagnia, rotta, fascia_partenza) vengono
codificate numericamente con LabelEncoder. Le colonne fascia_distanza e
media_sicurezza_orig vengono escluse da X.
Il dataset viene diviso in train (80%) e test (20%) con split stratificato
(random_state=42), poi scalato con StandardScaler.
8. Addestramento e valutazione
Vengono addestrati due modelli, entrambi con class_weight='balanced':

LogisticRegression con max_iter=1000
RandomForestClassifier con n_estimators=100

La valutazione include accuratezza, classification_report (precision, recall, F1)
e matrici di confusione affiancate per i due modelli.