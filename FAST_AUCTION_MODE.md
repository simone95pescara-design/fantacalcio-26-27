# FAST AUCTION MODE — 2026/27

Attivato perché l'asta è imminente. Da questo punto il progetto ottimizza per **decisioni utili in tempo**, non per completezza preventiva del dataset.

## Regola operativa

1. Congelare temporaneamente l'arricchimento storico esaustivo.
2. Usare subito Listone/FVM 2026/27 + storico Fantacalcio 2025/26 già disponibile + provenance/confidence per i nuovi arrivi.
3. Costruire una board completa dei 496 con score provvisorio e confidence esplicita.
4. Ricercare in profondità solo i giocatori che possono cambiare una decisione d'asta: target, top di fascia, rigoristi, titolari incerti, nuovi arrivi, possibili mispricing.
5. Tradurre la board in piano d'asta: scenari di budget, slot, target, alternative, hard cap condizionali.
6. Durante l'asta aggiornare prezzi e budget residuo; il mercato reale prevale sulle stime pre-asta.

## Cosa NON fare ora

- non completare 3-4 stagioni di storico per tutti i 496 prima di produrre la board;
- non imputare dati mancanti come se fossero osservati;
- non trattare FVM come verità o hard cap universale;
- non bloccare l'operatività in attesa di un modello predittivo completo.

## Board v0

La board v0 deve combinare:
- FVM 2026/27 come prior di mercato/valore corrente;
- MV/FM/PV 2025/26 dove disponibili;
- penalità/flag di incertezza per chi non ha storico Serie A direttamente comparabile;
- ranking e tier per ruolo;
- scenari di allocazione 1000 crediti compatibili con lega Classic a 8 e modificatore difesa.

La board v0 è uno strumento tattico da migliorare rapidamente, non il modello definitivo del progetto.