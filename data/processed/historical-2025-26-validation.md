# Validazione storico Fantacalcio 2025/26

Fonte: workbook ufficiale `Statistiche_Fantacalcio_Stagione_2025_26.xlsx` fornito dall'utente il 2026-08-09.

## Struttura sorgente

Il workbook contiene i fogli `Tutti`, `Portieri`, `Difensori`, `Centrocampisti`, `Attaccanti`.

Il foglio `Tutti` contiene 663 righe giocatore e 18 campi: `Id, R, Rm, Nome, Squadra, Pv, Mv, Fm, Gf, Gs, Rp, Rc, R+, R-, Ass, Amm, Esp, Au`.

## Matching con baseline 2026/27

Matching primario effettuato tramite `Id` Fantacalcio, non tramite nome.

Baseline attiva 2026/27: 496 giocatori.

Match esatti per ID con storico 2025/26: **384 / 496 = 77,42%**.

Unmatched: **112 / 496 = 22,58%**.

Copertura per ruolo:

- P: 43 / 60 = 71,67%; unmatched 17.
- D: 130 / 175 = 74,29%; unmatched 45.
- C: 142 / 174 = 81,61%; unmatched 32.
- A: 69 / 87 = 79,31%; unmatched 18.

## Interpretazione

Un unmatched non significa automaticamente "nuovo dall'estero": può essere neopromosso dalla Serie B, rientro da prestito, nuovo acquisto estero, giovane senza storico Serie A, giocatore proveniente da altra competizione o altro caso di assenza dal dataset Serie A 2025/26.

Non applicare fuzzy matching ai 112 unmatched per forzare una copertura: l'ID Fantacalcio è la chiave primaria e l'assenza dal dataset è informazione utile sulla provenienza/campione disponibile.

## Gate successivo

Classificare i 112 unmatched per provenienza 2025/26 (`Serie B`, `estero`, `altro/pochi dati`) e acquisire le statistiche native della competizione di origine. Nessuna league translation e nessuna previsione 2026/27 prima di aver reso esplicita questa provenienza.
