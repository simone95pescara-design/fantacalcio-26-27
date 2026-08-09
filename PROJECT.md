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
- Con modificatore difesa, MV, disponibilità e profondità hanno valore autonomo dai bonus.
- Titolarità/minuti/probabilità di voto sono centrali.
- Storico multi-stagione con recency, non media piatta.
- Distinguere risultati osservati da metriche sottostanti come xG/xA.
- Considerare ruolo tattico, rigori/piazzati, squadra, allenatore, sistema e concorrenza.
- Serie B→A ed estero→A richiedono traduzione del rendimento; non assumere comparabilità diretta.
- Giovani e campioni piccoli devono avere più incertezza.
- Separare valore sportivo e prezzo d'asta; FVM e' informazione di mercato, non hard cap.
- Non fissare pesi/soglie numeriche prima di osservare distribuzioni e copertura dei dati.

## Pipeline

fonti e dataset master → storico multi-stagione → previsioni + incertezza → valore fantacalcistico → score per slot → valore economico → ottimizzazione rosa / 1000 crediti → piano d'asta → adattamento live

## Baseline ufficiale 2026/27 — CHIUSA

Workbook ufficiale `Quotazioni_Fantacalcio_Stagione_2026_27.xlsx`: 496 giocatori attivi, 20 squadre, P=60 D=175 C=174 A=87; 6 ceduti separati. ID Fantacalcio usato come chiave primaria.

## Storico Fantacalcio 2025/26 — ACQUISITO E MATCHATO

Workbook ufficiale `Statistiche_Fantacalcio_Stagione_2025_26.xlsx`: 663 giocatori. Matching esatto ID con baseline 2026/27: 384/496 = 77,42%; unmatched 112. Per ruolo: P 43/60, D 130/175, C 142/174, A 69/87.

## Ricerca unmatched — IN CORSO

Ricerca web 2026-08-09 conferma che una parte consistente degli unmatched ha storico nativo Serie B 2025/26. FBref offre tabelle strutturate per Frosinone, Venezia e Monza con presenze, starts, minuti, gol, assist, rigori, cartellini e per-90. Sono gia' verificati esempi come Palmisani, Calo, Ghedjemis, Oyono, Kvernadze, Calvani, Stankovic, Busio, Schingtienne e Kike Perez.

Classi di provenienza adottate: `SERIE_B_2025_26`, `FOREIGN_LEAGUE_2025_26`, `YOUTH_RESERVE_2025_26`, `RETURN_OTHER_2025_26`, `UNRESOLVED`.

Non applicare ancora coefficienti Serie B→A/cross-league. I dati devono essere prima acquisiti nella scala nativa e accompagnati da provenienza e confidence.

## Artefatti principali

- `AGENTS.md`: istruzioni operative persistenti.
- `data/DATASET_MASTER_SCHEMA.md`: schema dataset master.
- `data/HISTORICAL_2025_26_SCHEMA.md`: schema storico 2025/26.
- `data/processed/historical-2025-26-unmatched.csv`: working list unmatched.
- `research/data-sources-v1.md`: politica fonti.
- `research/unmatched-provenance-2025-26-v1.md`: ricerca e protocollo di classificazione unmatched.

## Stato corrente

Baseline 2026/27 chiusa; storico Serie A 2025/26 matchato al 77,42%; ricerca provenienza unmatched avviata e fonti Serie B validate. Non costruire ancora score, fasce, prezzi massimi o previsioni.

## Prossimo outcome

Costruire `historical-2025-26-provenance.csv` per tutti i 112 unmatched. Risolvere prima in blocco i giocatori provenienti da Frosinone/Venezia/Monza attraverso le statistiche Serie B 2025/26, poi i trasferimenti da campionati esteri, infine giovani/riserve e casi residui. Dopo la classificazione completa, acquisire le statistiche native e consolidare lo storico 2025/26.
