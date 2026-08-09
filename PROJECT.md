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

Gestione settimanale/scambi/riparazione potranno essere estensioni successive, non sono il fronte corrente.

## Principi stabilizzati

- Evitare statistiche inventate sulle rose vincenti: non esiste evidenza pubblica sufficiente per una composizione universale.
- Costruire la rosa per funzioni/slot, non solo top/semitop/scommessa.
- Ogni slot deve avere alternative fungibili.
- Con modificatore difesa, MV, disponibilità e profondità hanno valore autonomo dai bonus.
- MV e fantamedia restano distinte.
- Titolarità/minuti/probabilità di voto sono centrali.
- Storico multi-stagione con recency, non media piatta.
- Distinguere gol/assist osservati da metriche sottostanti come xG/xA.
- Considerare ruolo tattico reale, rigori/piazzati, squadra, allenatore, sistema e concorrenza.
- Rendere espliciti infortuni, ballottaggi, trasferimenti e rischio.
- Serie B→A ed estero→A richiedono traduzione del rendimento; non assumere comparabilità diretta.
- Giovani e campioni piccoli devono avere più incertezza.
- Ogni previsione deve rappresentare floor/stima centrale/ceiling o distribuzione equivalente e confidence.
- Separare valore sportivo e prezzo d'asta; FVM è informazione di mercato, non hard cap.
- Ottimizzare rendimento marginale per credito tenendo conto di scarsità, rischio e funzione nella rosa.
- L'asta deve essere adattiva con target, fascia, hard cap, alternative e redistribuzione del budget.
- Non fissare pesi/soglie numeriche prima di osservare distribuzioni e copertura dei dati, salvo evidenza forte.

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

## Provenienza 2025/26 degli unmatched — CLASSIFICAZIONE COMPLETATA

Categorie operative: `SERIE_B_2025_26`, `FOREIGN_LEAGUE_2025_26`, `YOUTH_RESERVE_2025_26`, `RETURN_OTHER_2025_26`, `UNRESOLVED`.

La working list contiene esattamente i 112 unmatched canonici. Tutti i **112/112** sono ora classificati con provenienza 2025/26 persistita nei file di lavoro; non restano casi da classificare. Le confidence restano associate all'evidenza e non vanno alzate artificialmente.

### Persistenza batch

- primi 77: `data/processed/historical-2025-26-provenance-v1.csv`;
- 78–87: `data/processed/provenance-batch-078-087.csv`;
- 88–97: `data/processed/provenance-batch-088-097.csv`;
- 98–112: `data/processed/provenance-batch-098-112.csv`.

Per i giocatori non-Serie A conservare club, competizione e statistiche nella scala nativa. Non tradurre ancora in equivalenti Serie A. Nei casi con più club/competizioni nella stessa stagione conservare gli stint separati.

### Note finali di classificazione

- Franz Stolz: stagione 2025/26 multi-stint estera (Rapid Bucuresti → Grazer AK), da conservare separatamente.
- Davide Renzetti: prestito al Bra, Serie C.
- Wisdom Amey: prestito alla Pianese, Serie C.
- Redouane Halhal: KV Mechelen, Belgio.
- Anouar El Azzouzi: Fortuna Düsseldorf, 2. Bundesliga.
- Luis Milla: Getafe, LaLiga.
- Alessandro Romano: stint Roma + Spezia Serie B; conservare separatamente.

## Artefatti principali

- `AGENTS.md`: istruzioni operative persistenti.
- `data/DATASET_MASTER_SCHEMA.md`: schema dataset master.
- `data/HISTORICAL_2025_26_SCHEMA.md`: schema storico 2025/26.
- `data/processed/historical-2025-26-unmatched.csv`: lista completa dei 112 unmatched.
- `data/processed/historical-2025-26-provenance-v1.csv`: primi 77 classificati.
- `data/processed/provenance-batch-078-087.csv`: batch 78–87.
- `data/processed/provenance-batch-088-097.csv`: batch 88–97.
- `data/processed/provenance-batch-098-112.csv`: batch finale 98–112.
- `research/data-sources-v1.md`: politica fonti.
- `research/unmatched-provenance-2025-26-v1.md`: criteri di classificazione.

## Stato corrente

Baseline 2026/27 chiusa; storico Serie A 2025/26 acquisito; **provenienza dei 112 unmatched completata 112/112**. Non costruire ancora score, fasce, prezzi massimi o previsioni.

## Prossimo outcome

1. consolidare i quattro file di provenienza in un unico provenance master e verificare automaticamente 112 righe / 112 ID unici / zero mancanti;
2. acquisire statistiche native 2025/26 per ogni gruppo non-Serie A, mantenendo stint separati;
3. consolidare una tabella storica 2025/26 unificata per i 496 giocatori;
4. misurare qualità/copertura e campioni piccoli;
5. solo dopo estendere lo storico alle stagioni precedenti e alle metriche xG/xA.

Non applicare ancora coefficienti Serie B→A o cross-league: la metodologia di translation verrà costruita e validata separatamente.