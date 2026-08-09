# Stato canonico del progetto

## Obiettivo finale
Massimizzare la probabilità di vincere la lega Fantacalcio 2026/27 costruendo un sistema decisionale completo per valutazione giocatori, rosa, allocazione dei 1000 crediti ed esecuzione/adattamento dell'asta.

## Contesto
- 8 partecipanti
- 1000 crediti
- Classic
- modificatore difesa classico

## Modalità corrente — FAST AUCTION MODE
L'asta è imminente: il progetto ottimizza per decisioni operative disponibili in tempo. Il lavoro storico esaustivo è congelato salvo ricerca mirata che possa cambiare una decisione d'asta.

## Baseline disponibile
- Listone ufficiale Fantacalcio 2026/27: 496 giocatori attivi.
- FVM ufficiale 2026/27 disponibile per tutti.
- Storico Fantacalcio Serie A 2025/26 matchato per 384/496.
- Provenienza dei 112 non matchati chiusa 112/112.
- FAST AUCTION BOARD v0 disponibile nella conversazione.

## Cartella operativa
`AUCTION/` è il nuovo punto di ingresso. Gli artefatti precedenti restano temporaneamente solo come evidenza/supporto e verranno rimossi o archiviati quando AUCTION sarà autosufficiente.

File operativi già persistiti:
- `AUCTION/README.md`
- `AUCTION/01_BUDGET.md`
- `AUCTION/02_PORTIERI.md`
- `AUCTION/03_DIFENSORI.md`

## Difesa — v1 CHIUSA operativamente
Scenario balanced: target 150–180 crediti.

Principio: 4–5 difensori realmente schierabili da modificatore + profili bonus + low-cost, senza dipendere da un singolo nome.

Strategia preferita: anchor tra Bremer/Mancini/Pavlovic/Akanji sotto cap, poi Solet/Kalulu/Bastoni/Rrahmani/Ostigard e stabilizzatori MV. Dimarco trattato come eccezione: prezzo massimo operativo 95 nello scenario balanced; oltre si passa alla strategia modificatore efficiente.

I cap individuali e le switch rule sono in `AUCTION/03_DIFENSORI.md`.

## Regole operative stabilizzate
- non inseguire un singolo nome oltre il cap;
- alternative fungibili per slot;
- FVM è prior, non hard cap;
- confidence inferiore sui giocatori non direttamente comparabili;
- ricerca solo dove può cambiare una decisione;
- con modificatore, MV e disponibilità hanno valore autonomo;
- prezzi reali e crediti residui prevalgono sul piano pre-asta.

## Stato corrente
Portieri strategicamente impostati; difensori operativi v1 completati. Non tornare alla raccolta storica massiva.

## Prossimo outcome
**CENTROCAMPISTI FAST AUCTION**:
1. estrarre shortlist dalla board;
2. verificare solo target prioritari per ruolo tattico, titolarità, rigori/piazzati e gerarchie aggiornate;
3. produrre C1–C8 con target, alternative, prezzo e hard cap;
4. poi attaccanti;
5. infine regole live e pulizia repository, mantenendo soltanto ciò che serve all'asta.
