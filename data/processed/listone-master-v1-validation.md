# Validazione baseline Listone 2026/27

Data acquisizione/verifica: 2026-08-09.

## Sorgente

File ufficiale Fantacalcio.it fornito dall'utente: `Quotazioni_Fantacalcio_Stagione_2026_27.xlsx`.

Il workbook contiene i fogli `Tutti`, `Portieri`, `Difensori`, `Centrocampisti`, `Attaccanti`, `Ceduti` e rende finalmente disponibili in modo esplicito sia il ruolo Classic (`R`) sia il ruolo Mantra (`RM`).

## Baseline attiva

Il foglio `Tutti` contiene 496 calciatori attivi, esclusa intestazione/titolo.

Distribuzione Classic verificata:

- P: 60
- D: 175
- C: 174
- A: 87
- Totale: 496

Squadre distinte: 20.

Controlli eseguiti sui campi core (`Id`, `R`, `Nome`, `Squadra`, `Qt.A`, `Qt.I`, `FVM`):

- ID duplicati: 0
- valori core mancanti: 0
- ruoli Classic presenti per tutte le 496 righe: sì

Il workbook contiene inoltre un foglio separato `Ceduti` con 6 calciatori; questi non vengono inclusi nella baseline attiva del dataset master.

## Campi ufficiali disponibili

- Id
- ruolo Classic
- ruolo Mantra
- Nome
- Squadra
- quotazione attuale Classic
- quotazione iniziale Classic
- differenza Classic
- quotazione attuale Mantra
- quotazione iniziale Mantra
- differenza Mantra
- FVM Classic / 1000
- FVM Mantra / 1000

## Decisione

La baseline ufficiale necessaria per il dataset master è ora considerata **VALIDATA**.

Il precedente conteggio web di 502 righe non viene più usato come riferimento di completezza: il file Excel ufficiale fornito direttamente è la fonte canonica per questa snapshot e separa esplicitamente i ceduti.

## Prossimo arricchimento

Passare dalla baseline anagrafico-economica all'arricchimento storico/statistico. Il primo blocco da costruire è lo storico recente per giocatore, mantenendo separati dati osservati, fonte, stagione e disponibilità del campione. Non assegnare ancora score o hard cap d'asta.