# ✈️ Flight Delay Prediction 2024: Data Analysis & Machine Learning

![Data Science](https://img.shields.io/badge/Data%20Science-EDA%20%7C%20Feature%20Engineering-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Classification-orange)
![Python](https://img.shields.io/badge/Python-Pandas%20%7C%20Scikit--Learn-green)

## 📌 Panoramica del Progetto
Questo progetto analizza e modella un campione di dati del traffico aereo statunitense del 2024 con l'obiettivo di sviluppare un **classificatore binario**. Il modello predice proattivamente se un volo subirà un ritardo significativo (superiore ai 15 minuti) all'arrivo. 

L'obiettivo di business è fornire uno strumento di supporto decisionale per ottimizzare la logistica aeroportuale, migliorare le comunicazioni ai passeggeri e mitigare i costi legati alle inefficienze operative.

---

## 🛠️ Pipeline dei Dati e Architettura

Il flusso di lavoro segue le best practice del ciclo di vita del Machine Learning:

### 1. Data Cleaning & Preprocessing
* **Traduzione e Standardizzazione:** Parsing del dataset `flight_data_2024_sample.csv` (35 feature originali) con mappatura e rinominazione automatica delle colonne per una gestione standardizzata in italiano.
* **Data Quality:** Generazione di report diagnostici per l'identificazione di valori nulli. Filtraggio sistematico dei "rumori" statistici (voli cancellati o dirottati) ed eliminazione delle feature a varianza zero, ridondanti o non generalizzabili (es. `num_volo`).

### 2. Feature Engineering Avanzata
Per aumentare il potere predittivo del modello, i dati grezzi sono stati trasformati in feature analitiche e storiche:
* **Feature Temporali/Spaziali:** Estrazione di `fascia_partenza` (mattina, pomeriggio, sera, notte) e creazione dell'identificativo `rotta` univoco.
* **Ingegneria dei Dati Storici:** Calcolo delle medie storiche (aggregazioni) per aeroporto e per compagnia aerea al fine di isolare le cause latenti di ritardo:
  * `media_meteo_orig` e `media_traffico_orig`
  * `media_ritardo_compagnia` e `media_sicurezza_orig`
  * `media_durata_rotta` e `media_ritardo_prec`

### 3. Prevenzione del Data Leakage ⚠️
*(Critical Step)* Prima della fase di addestramento, è stata applicata una rigorosa pulizia delle **variabili future**. Tutte le colonne note solo a volo completato (orari reali, tempi di rullaggio, ritardi effettivi) sono state rimosse per evitare dispersioni di dati (*Data Leakage*) e garantire che il modello valuti solo le informazioni disponibili al momento della previsione. Il target è stato binarizzato: `in_ritardo` (`ritardo_arrivo` > 15 min).

### 4. Exploratory Data Analysis (EDA)
Indagine visiva multivariata (Seaborn/Matplotlib) per individuare pattern nascosti:
* Mappatura probabilistica dei ritardi per mese, giorno della settimana e fascia oraria.
* Confronto statistico delle medie storiche tra voli puntuali e voli in ritardo.

### 5. Modellazione Predittiva e Valutazione
Le feature categoriche sono state processate tramite `LabelEncoder`, mentre i dati numerici sono stati normalizzati con `StandardScaler`. Il dataset è stato suddiviso con **split stratificato** (80/20) per mantenere le proporzioni del target.

Sono stati addestrati e messi in competizione due algoritmi, entrambi bilanciati (`class_weight='balanced'`) per gestire l'asimmetria delle classi:
* **Logistic Regression:** Algoritmo interpretabile di baseline.
* **Random Forest Classifier:** Modello d'insieme non lineare per catturare relazioni complesse (100 stimatori).

**Metriche di Valutazione Estratte:** Accuratezza, Classification Report (Precision, Recall, F1-Score) e Matrici di Confusione comparative.

---

## 💻 Stack Tecnologico
* **Linguaggio:** Python
* **Data Manipulation:** Pandas, NumPy
* **Data Visualization:** Matplotlib, Seaborn
* **Machine Learning:** Scikit-Learn (Classificazione, Preprocessing, Model Evaluation)

