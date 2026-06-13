# 🛒 Retail Sales Analytics: Advanced Wrangling, KPI, Segmentazione RFM e Analisi delle Coorti con Python

## 🎯 Obiettivi Specifici
* **Data Cleaning & Advanced Curation** — Gestione avanzata di un dataset reale da 1 milione di righe: isolamento delle transazioni stornate (resi con codice "C"), gestione dei `CustomerID` nulli tramite flag `is_anonymous`, trattamento degli outlier con metodo IQR e Feature Engineering.
* **Analisi Esplorativa (EDA) & Trend** — Studio delle distribuzioni delle vendite per prodotto e analisi geografica per Paese; individuazione dei pattern di stagionalità tramite aggregazioni temporali con `pd.Grouper(freq='M')`.
* **KPI di Business** — Calcolo programmatico delle metriche chiave: Fatturato Netto, Average Order Value (AOV), Purchase Frequency e Repeat Purchase Rate.
* **Segmentazione Clienti (Modello RFM)** — Classificazione empirica dei clienti in segmenti commerciali (Champions, Loyal, At Risk, Hibernating) tramite scoring a quintili con `pd.qcut()` e mappatura con dizionari Python.
* **Analisi della Retention (Cohort Retention)** — Matrice di fidelizzazione mensile per analizzare il ciclo di vita e il Churn Rate dei clienti nel tempo.

## 🛠️ Strumenti e Librerie

| Strumento | Ruolo nel progetto |
| :--- | :--- |
| **Python 3.x** | Linguaggio di programmazione principale |
| **Pandas** | Data Wrangling, aggregazioni temporali (`pd.Grouper`), calcolo KPI, Pivot delle Coorti e scoring RFM |
| **NumPy** | Operazioni vettoriali, logica condizionale e calcolo degli outlier con percentili |
| **Matplotlib** | Struttura dei grafici e personalizzazione avanzata dei layout (assi, titoli, salvataggio) |
| **Seaborn** | Visualizzazioni statistiche ad alto impatto (Heatmap coorti, grafici distribuzione segmenti) |
| **Jupyter** | Ambiente interattivo — codice, output e grafici inline su `.ipynb` |
| **GitHub** | Versioning del codice e pubblicazione del portfolio |

## 📂 Dataset
* **Nome**: Online Retail II Dataset (UCI Machine Learning Repository)
* **Contenuto**: Transazioni e-commerce di un retailer globale UK (2009–2011)
* **Dimensione**: ~1.067.371 righe
* **Formato**: CSV (preferito rispetto a .xlsx per velocità di caricamento in Pandas)
* **Variabili**: `Invoice`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `Price`, `CustomerID`, `Country`

## 📁 Struttura Cartelle

```text
retail_sales_analytics/
│
├── data/
│   └── online_retail_II.csv             # Dataset originale (non modificare)
│
├── 01_data_cleaning.ipynb               # Notebook 1: Pulizia e Feature Engineering
├── 02_eda.ipynb                         # Notebook 2: EDA e trend temporali
├── 03_kpi_calculations.ipynb            # Notebook 3: Metriche di business
├── 04_rfm_and_cohorts.ipynb             # Notebook 4: Segmentazione RFM e Retention
│
├── output/
│   ├── dati_puliti/                     # cleaned_retail.csv generato dal Notebook 1
│   └── grafici/                         # PNG esportati dai notebook
│
├── requirements.txt
└── README.md
```
## 📊 Dettaglio Fasi di Lavoro

### Fase 1 — Data Cleaning & Feature Engineering (`01_data_cleaning.ipynb`)
* Caricamento efficiente del file CSV con ottimizzazione dei tipi di dato (`dtypes`)
* Identificazione e separazione dei resi (`Invoice` con prefisso "C") dal fatturato lordo
* Gestione dei `CustomerID` nulli: flag `is_anonymous` — mantenuti per KPI aggregati, esclusi dall'RFM
* Trattamento Outlier: valori anomali su `Quantity` e `Price` tramite metodo IQR con `np.percentile()`
* Feature Engineering: colonna `TotalPrice` = `Quantity` × `Price` — base per tutte le metriche successive
* Salvataggio del dataset pulito in `output/dati_puliti/cleaned_retail.csv`

### Fase 2 — EDA & Aggregazioni Temporali (`02_eda.ipynb`)
* Analisi della concentrazione del fatturato per Paese (Top 10, UK separato per scala)
* Trend mensile vendite con `pd.Grouper(freq='M')` su `InvoiceDate`
* Top 10 prodotti per volume e per fatturato complessivo (due classifiche distinte, risultati spesso divergenti)
* Analisi temporale: giorni della settimana e fasce orarie di picco degli ordini
* Salvataggio grafici in `output/grafici/`

### Fase 3 — KPI di Business (`03_kpi_calculations.ipynb`)
* Fatturato Netto Globale dalla colonna `TotalPrice`
* AOV (Average Order Value) a livello mensile e geografico
* Repeat Purchase Rate (clienti con più di 1 acquisto ÷ clienti totali)
* Report tabellare riassuntivo dei KPI da inserire nel README

### Fase 4 — RFM & Analisi delle Coorti (`04_rfm_and_cohorts.ipynb`)
* **Segmentazione RFM**:
  * Calcolo Recency, Frequency e Monetary per cliente tramite `groupby()` + `agg()`
  * Scoring 1–5 con `pd.qcut()` per ogni dimensione
  * Mappatura segmenti (Champions, Loyal, At Risk, Hibernating) con dizionari Python e logica condizionale
  * `sns.countplot` e grafici a barre per composizione volumetrica della customer base
* **Analisi delle Coorti — Cohort Retention**:
  * Estrazione `CohortMonth` = mese di primo acquisto per cliente
  * Calcolo `CohortIndex` = mesi di attività successivi al primo acquisto
  * `pivot_table()` → Cohort Retention Matrix
  * `sns.heatmap(annot=True, fmt='.0%')` per percentuali di retention visibili mese su mese

## 📝 Struttura del README.md
* Titolo del Progetto & Pitch Aziendale (il problema di business risolto dall'analisi)
* Quick Start: istruzioni per clonare la repository e consultare i 4 notebook in ordine
* Executive Summary dei Risultati:
  * I macro KPI emersi dall'analisi
  * Evidenza visiva del trend mensile e della Heatmap delle Coorti
  * Distribuzione percentuale dei clienti nei segmenti RFM
* Raccomandazioni Strategiche: 3 azioni data-driven per il team Marketing

## 📈 Output Finale
* **4 Notebook Jupyter .ipynb** — codice, grafici e insight visibili inline su GitHub
* **`cleaned_retail.csv`** in `output/dati_puliti/`
* **Grafici .png** in `output/grafici/`: heatmap coorti, trend mensili, distribuzione RFM, analisi geografica
* **README aggiornato** con Executive Summary e raccomandazioni strategiche
