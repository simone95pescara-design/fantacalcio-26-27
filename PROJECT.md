# Stato canonico del progetto

## Obiettivo finale

Massimizzare la probabilità di vincere la lega Fantacalcio 2026/27 costruendo un sistema decisionale completo per valutazione giocatori, rosa, allocazione dei 1000 crediti ed esecuzione/adattamento dell'asta.

Non costruire una semplice lista di nomi: trasformare dati, ricerca e incertezza in decisioni operative ripetibili.

## Contesto della lega

- stagione 2026/27;
- 8 partecipanti;
- 1000 crediti;
- Classic, non Mantra;
- modificatore difesa classico;
- resto del regolamento sostanzialmente standard salvo particolarità future.

## Output finali attesi

1. dataset master 2026/27;
2. previsioni per giocatore con incertezza esplicita;
3. valore fantacalcistico specifico per la lega;
4. classificazione per slot/funzione;
5. prezzo target, fascia conveniente e hard cap;
6. modello di rosa e budget derivati dai dati;
7. piano d'asta con alternative fungibili;
8. aggiornamento live in base a prezzi, crediti, scarsità e giocatori rimasti.

## Principi stabilizzati

- Costruire la rosa per funzioni/slot, non solo top/semitop/scommessa.
- MV e fantamedia restano distinte; titolarità/minuti/probabilità di voto sono centrali.
- Storico multi-stagione con recency; distinguere output osservati e metriche sottostanti.
- Serie B→A ed estero→A richiedono traduzione separata e validata.
- Giovani e campioni piccoli devono avere più incertezza.
- Separare valore sportivo e prezzo d'asta; FVM non è hard cap.
- Non fissare pesi/soglie numeriche prima di osservare distribuzioni e copertura.

## Pipeline

```text
fonti e dataset master
→ storico multi-stagione
→ previsioni + incertezza
→ valore fantacalcistico
→ score per slot
→ valore economico
→ ottimizzazione rosa / 1000 crediti
→ piano d'asta
→ adattamento live
```

## Baseline ufficiale 2026/27 — CHIUSA

Workbook ufficiale `Quotazioni_Fantacalcio_Stagione_2026_27.xlsx`: 496 giocatori attivi, 20 squadre, P=60 D=175 C=174 A=87; 6 ceduti separati. ID Fantacalcio usato come chiave primaria.

## Storico Fantacalcio 2025/26 — ACQUISITO E MATCHATO

Workbook ufficiale `Statistiche_Fantacalcio_Stagione_2025_26.xlsx`: 663 giocatori. Matching esatto tramite ID: 384/496 = 77,42%; unmatched 112 (P=17, D=45, C=32, A=18).

## Provenienza 2025/26 degli unmatched — IN CORSO

Categorie: `SERIE_B_2025_26`, `FOREIGN_LEAGUE_2025_26`, `YOUTH_RESERVE_2025_26`, `RETURN_OTHER_2025_26`, `UNRESOLVED`.

La classificazione procede in batch da 10 quando l'evidenza lo consente, senza forzare confidence alta.

### Stato

- classificati: **97/112**;
- residui: **15**;
- primi 77 consolidati in `historical-2025-26-provenance-v1.csv`;
- batch 78–87 in `provenance-batch-078-087.csv`;
- batch 88–97 in `provenance-batch-088-097.csv`.

### Batch 88–97

- Alessio Cacciamani → Juve Stabia, Serie B, high;
- Aleksandar Stankovic → Club Brugge, Belgio, high;
- Abdoulaye Camara → sviluppo Udinese/settore giovanile con debutto Serie A finale, high;
- Elias Havel → Hartberg, Austria, high;
- Kingstone Mutandwa → SV Ried, Austria, high;
- Gustavo Varela → Gil Vicente, Portogallo, high;
- Willem Geubbels → Paris FC, Ligue 1, high;
- Hamed Junior Traorè → Olympique Marseille, Francia, medium;
- Jay Robinson → Southampton, Inghilterra, medium;
- O. Diallo → youth/reserve provenance, medium e da rafforzare nella fase di acquisizione statistiche.

Per i non-Serie A conservare club, competizione e statistiche nella scala nativa. Non tradurre ancora in equivalenti Serie A. Confidence medium resta esplicita e dovrà essere rafforzata quando raccogliamo le statistiche native.

## Artefatti principali

- `AGENTS.md`
- `data/processed/historical-2025-26-unmatched.csv`
- `data/processed/historical-2025-26-provenance-v1.csv`
- `data/processed/provenance-batch-078-087.csv`
- `data/processed/provenance-batch-088-097.csv`
- `research/data-sources-v1.md`

## Stato corrente

Baseline chiusa; storico Serie A acquisito; **97/112 unmatched classificati**, 15 residui. Non costruire ancora score, fasce, prezzi massimi o previsioni.

## Prossimo outcome

1. classificare i 15 residui finali, idealmente 10 + 5;
2. consolidare tutti i batch nel provenance master e verificare 112/112, duplicati e confidence;
3. acquisire statistiche native 2025/26 per ogni gruppo non-Serie A;
4. costruire tabella storica 2025/26 unificata;
5. solo dopo estendere lo storico alle stagioni precedenti e xG/xA.

Non applicare ancora coefficienti Serie B→A o cross-league.