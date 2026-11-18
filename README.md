# Il catalogo Netflix: una dashboard con Quarto

Materiale del corso **R Lab** (Università di Napoli Federico II): una dashboard
[Quarto](https://quarto.org) costruita passo passo, dalla progettazione alla
versione completa, sui dati del catalogo di film e serie TV di Netflix.

Il repository contiene il file dei dati e tutto il necessario per produrre:

- lo **scheletro** della dashboard, con le card numerate, per controllare la
  struttura prima di inserire i contenuti
- la **dashboard completa**, con grafici e tabelle interattivi e una pagina
  esplorabile con Observable JS

Il tutorial che spiega ogni passaggio è pubblicato sul sito del corso.

## Contenuto

```
.
├── dati/
│   └── netflix_titles.csv            i dati: 6.234 titoli, 12 variabili
├── immagini/
│   └── logo.svg                      il logo della dashboard
├── netflix-legenda.qmd               la descrizione dei dati (legenda delle variabili)
├── netflix-analisi.R                 il codice R: un blocco "## @knitr" per ogni contenuto
├── netflix-dashboard-scheletro.qmd   lo scheletro della dashboard
├── netflix-dashboard.qmd             la dashboard completa
├── netflix.scss                      i colori e lo stile della dashboard
└── dashboard-netflix.zip             tutti i file precedenti in un unico archivio
```

## Come usarlo

1. Scarica i file: pulsante verde **Code** → **Download ZIP** (oppure scarica
   solo `dashboard-netflix.zip`) ed estrai l'archivio.
2. Apri la cartella come progetto: in RStudio *File* → *New Project* →
   *Existing Directory*; in Positron *File* → *Open Folder*.
3. Installa, se necessario, i package **dalla console**:

   ```r
   install.packages(c("tidyverse", "highcharter", "plotly", "dygraphs", "xts",
                      "ggridges", "gt", "gtExtras", "formattable", "DT"))
   ```

   La versione di `dplyr` deve essere almeno la 1.2 (per la funzione
   `recode_values`).
4. Apri un file `.qmd` e premi **Render**, oppure scrivi nel Terminale:

   ```bash
   quarto render netflix-dashboard-scheletro.qmd
   quarto render netflix-dashboard.qmd
   quarto render netflix-legenda.qmd
   ```

Il file `netflix-analisi.R` si può eseguire anche da solo, con **Source**, per
provare il codice prima di inserirlo nella dashboard.

## La dashboard

| Pagina | Contenuti | Package |
|--------|-----------|---------|
| Panoramica | quattro value box; titoli aggiunti per anno e per mese; film e serie TV; titoli per pubblico | highcharter, dygraphs, plotly |
| Generi e paesi | i generi più frequenti; i paesi di produzione | plotly, highcharter, gt, gtExtras |
| Durata e pubblico | la durata dei film e le stagioni delle serie; i titoli per fascia di pubblico | ggridges, highcharter, formattable |
| Catalogo | tutti i titoli, con ricerca e filtri | DT |
| Esplora | grafici e tabella che reagiscono ai controlli | Observable JS |

Il codice di ogni contenuto è nello script `netflix-analisi.R`; la dashboard
lo richiama con `knitr::read_chunk()` e l'opzione `ref.label`.

> La pagina **Esplora** carica le librerie di Observable JS da internet: per
> vederla serve una connessione.

## I dati

Il file `dati/netflix_titles.csv` è una versione del dataset
[Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows)
di Shivam Bansal, pubblicato su Kaggle: contiene i titoli aggiunti al catalogo
tra il 2008 e il gennaio 2020. Per le condizioni d'uso dei dati si rimanda alla
pagina del dataset. La descrizione delle variabili è nel documento
`netflix-legenda.qmd`.

Netflix è un marchio registrato di Netflix, Inc.: questo materiale ha scopo
esclusivamente didattico e non è affiliato a Netflix.
