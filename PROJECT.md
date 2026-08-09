# Stato canonico del progetto

## Obiettivo finale

Massimizzare la probabilità di vincere la lega Fantacalcio 2026/27 costruendo un sistema decisionale completo per valutazione giocatori, rosa, allocazione dei 1000 crediti ed esecuzione/adattamento dell'asta.

## Contesto

- 8 partecipanti
- 1000 crediti
- Classic
- modificatore difesa classico

## Modalità corrente — FAST AUCTION MODE

L'asta è imminente: il progetto ottimizza ora per **decisioni operative disponibili in tempo**, non per completezza preventiva del dataset. Le istruzioni sono in `FAST_AUCTION_MODE.md`.

Il lavoro storico esaustivo è temporaneamente congelato. Non è eliminato: verrà ripreso dopo l'asta o solo sui target dove può cambiare concretamente una decisione.

## Baseline disponibile

- Listone ufficiale Fantacalcio 2026/27: 496 giocatori attivi, P=60 D=175 C=174 A=87.
- FVM ufficiale 2026/27 disponibile per tutti i 496.
- Storico Fantacalcio Serie A 2025/26 matchato direttamente per 384/496.
- Provenienza 2025/26 dei 112 non matchati classificata 112/112.
- Acquisizione quantitativa nativa non-Serie A avviata ma non più bloccante per l'asta.

## Board tattica v0 — CREATA

Creato workbook `Fantacalcio_2026_27_FAST_AUCTION_BOARD_v0.xlsx` nella conversazione.

Contenuto:
- `LEGGIMI`: metodologia, limiti e fonti;
- `PIANO_1000`: tre scenari di budget e slot base;
- `BOARD_496`: tutti i 496 giocatori;
- fogli separati P/D/C/A.

La board combina:
- FVM 2026/27 come prior dominante;
- PV/MV/FM 2025/26 per rifinire il ranking quando direttamente comparabili;
- score v0 per ruolo;
- tier S/A/B/C/D;
- confidence esplicita;
- `Cap v0` indicativo derivato da FVM+tier.

ATTENZIONE: `Cap v0` NON è ancora l'hard cap definitivo. Serve come filtro tattico immediato. Il vero hard cap deve essere contestualizzato rispetto a scenario di budget, slot ancora aperti e prezzi reali dell'asta.

## Scenari budget v0

- BALANCED: P 70 / D 170 / C 250 / A 510
- ATTACCO PREMIUM: P 60 / D 145 / C 205 / A 590
- MODIFICATORE+C: P 80 / D 215 / C 285 / A 420

Lo scenario non è scelto una volta per tutte: l'asta reale determina quale ramo usare.

## Regole operative stabilizzate

- non inseguire un singolo nome oltre il valore solo perché era target;
- usare alternative fungibili per slot;
- FVM è un prior, non verità né hard cap universale;
- sui giocatori senza storico Serie A direttamente comparabile mantenere confidence più bassa;
- ricerca approfondita solo su target/top/mispricing/titolarità-rigori che possono cambiare una decisione;
- con modificatore difesa, MV e disponibilità mantengono valore specifico;
- mercato reale e crediti residui prevalgono sul piano pre-asta.

## Stato corrente

La board operativa v0 è disponibile. Il prossimo fronte non è completare il dataset: è **trasformare la board in una shortlist operativa d'asta per slot e prezzi**, concentrando la ricerca aggiornata sui giocatori che contano davvero.

## Prossimo outcome

1. selezionare per ruolo le fasce realmente acquistabili/strategiche dalla board v0;
2. fare ricerca aggiornata mirata su titolarità, ruolo tattico, rigori/piazzati, infortuni e gerarchie soltanto sui target prioritari;
3. produrre target / alternative / evita / cap contestualizzato per ciascuno slot;
4. definire lo scenario di partenza e le regole di switch durante l'asta;
5. usare prezzi reali dell'asta per adattare budget e cap live.
