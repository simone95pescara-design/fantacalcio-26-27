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

Workbook ufficiale `Statistiche_Fantacalcio_Stagione_2025_26.xlsx`: 663 giocatori con i campi ufficiali `Id, R, Rm, Nome, Squadra, Pv, Mv, Fm, Gf, Gs, Rp, Rc, R+, R-, Ass, Amm, Esp, Au`.

Matching esatto tramite ID tra baseline 2026/27 e storico Serie A 2025/26:

- totale: 384/496 = 77,42%; unmatched 112;
- P: 43/60, unmatched 17;
- D: 130/175, unmatched 45;
- C: 142/174, unmatched 32;
- A: 69/87, unmatched 18.

L'assenza dallo storico Serie A non va corretta con fuzzy matching: è un segnale da classificare (Serie B, estero, rientro, giovane/pochi dati, altro).

## Provenienza 2025/26 degli unmatched — IN CORSO

Categorie operative: `SERIE_B_2025_26`, `FOREIGN_LEAGUE_2025_26`, `YOUTH_RESERVE_2025_26`, `RETURN_OTHER_2025_26`, `UNRESOLVED`.

Prima tranche verificata con fonti primarie/strutturate:

- AC Monza 2025/26: rosa/convocazioni ufficiali del club confermano numerosi unmatched attuali come giocatori di Serie B 2025/26;
- Venezia FC 2025/26: numeri di maglia e convocazioni ufficiali confermano numerosi unmatched attuali come giocatori di Serie B 2025/26;
- Frosinone 2025/26: FBref espone statistiche Serie B strutturate per diversi unmatched attuali, tra cui Palmisani, Calò, Ghedjemis, Anthony Oyono, Kvernadze, Calvani, Koutsoupias, Raimondo, Bracaglia, Monterisi e Chichella.

Persistito `data/processed/historical-2025-26-provenance-v1.csv` con la prima tranche ad alta confidenza. Non trattare il file come classificazione completa dei 112 finché i residui non sono risolti.

## Artefatti principali

- `AGENTS.md`: istruzioni operative persistenti.
- `data/DATASET_MASTER_SCHEMA.md`: schema dataset master.
- `data/HISTORICAL_2025_26_SCHEMA.md`: schema storico 2025/26.
- `data/raw/listone-2026-27-source.md`: provenienza Listone.
- `data/raw/statistiche-serie-a-2025-26-source.md`: provenienza storico 2025/26.
- `data/processed/listone-master-v1-validation.md`: validazione baseline.
- `data/processed/historical-2025-26-validation.md`: validazione matching storico.
- `data/processed/historical-2025-26-unmatched.csv`: working list dei 112 unmatched.
- `data/processed/historical-2025-26-provenance-v1.csv`: prima classificazione verificata della provenienza 2025/26.
- `research/data-sources-v1.md`: politica fonti.
- `research/unmatched-provenance-2025-26-v1.md`: ricerca e criteri di classificazione della provenienza.

## Stato corrente

Baseline 2026/27 chiusa; storico Serie A 2025/26 acquisito; 112 unmatched identificati; classificazione di provenienza avviata e prima tranche ad alta confidenza persistita. Non costruire ancora score, fasce, prezzi massimi o previsioni.

## Prossimo outcome

Completare la classificazione dei 112 unmatched, concentrandosi sui residui non già verificati delle tre neopromosse e poi sui trasferimenti esteri/rientri/giovani. Per ogni giocatore registrare almeno `provenance_2025_26`, club/competizione 2025/26, confidence ed evidenza.

Dopo la classificazione completa, acquisire statistiche native 2025/26 per tutti i gruppi non-Serie A e consolidare una tabella storica 2025/26 unificata. Non applicare ancora coefficienti Serie B→A o cross-league: la metodologia di translation verrà costruita e validata separatamente.