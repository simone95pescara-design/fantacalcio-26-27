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

## Modello concettuale corrente

Feature candidate: storico multi-stagione, minuti/titolarità, MV/FM, bonus/malus, xG/xA e metriche predittive, posizione tattica, rigori/piazzati, forza squadra, allenatore/sistema, concorrenza, infortuni, età, league/promotion translation, rischio/floor/ceiling/confidence, FVM/quotazioni/prezzo atteso.

Slot preliminari:

- difesa: anchor modificatore, premium ibrido, stabilizzatori, offensivi/upside, rotazioni/value;
- centrocampo: primary/secondary scorer, titolari offensivi/value, floor, upside, low-cost asimmetrici;
- attacco: primary goal source, seconda fonte gol, value scorer, rotazioni/upside, low-cost;
- portieri: titolarità, forza difensiva, clean sheet/gol subiti attesi, MV, complementarità.

## Pipeline di costruzione

```text
fonti e dataset master
        ↓
previsioni + incertezza
        ↓
valore fantacalcistico
        ↓
score per slot
        ↓
valore economico
        ↓
ottimizzazione rosa / 1000 crediti
        ↓
piano d'asta
        ↓
adattamento live
```

La roadmap non è cieca: evidenze nuove possono correggere decisioni a monte.

## Artefatti disponibili

- `AGENTS.md`: istruzioni operative persistenti.
- `data/DATASET_MASTER_SCHEMA.md`: schema iniziale del dataset master e regole di qualità.
- `data/raw/listone-2026-27-source.md`: provenienza e storia dell'acquisizione del Listone.
- `data/processed/listone-master-v1-validation.md`: validazione della baseline ufficiale ottenuta dal workbook Fantacalcio.it.
- `data/processed/listone-master-v1-portieri.csv`: prima persistenza tabellare della baseline ufficiale (portieri; il resto della baseline resta verificato nel workbook sorgente/validation).
- `research/data-sources-v1.md`: fonti candidate e regole di provenienza per storico Fantacalcio, statistiche cross-league e xG/xA.

## Baseline ufficiale Listone 2026/27 — CHIUSA

Il 2026-08-09 l'utente ha fornito il workbook ufficiale `Quotazioni_Fantacalcio_Stagione_2026_27.xlsx`.

Il foglio `Tutti` contiene 496 calciatori attivi con ruolo Classic ufficiale e 20 squadre. Distribuzione verificata: P=60, D=175, C=174, A=87. Nessun ID duplicato e nessun valore mancante nei campi core controllati. Il workbook contiene separatamente 6 calciatori nel foglio `Ceduti`, esclusi dalla baseline attiva.

La precedente osservazione web di 502 righe non è più il criterio canonico: la snapshot Excel ufficiale fornita direttamente prevale e rende esplicita la separazione dei ceduti.

## Fonti storiche già verificate

- Fantacalcio.it espone per la Serie A 2025/26 PV, MV, FM, gol, gol subiti, rigori segnati/tirati, rigori parati, assist, ammonizioni ed espulsioni. Questa è la fonte primaria per le metriche direttamente fantacalcistiche.
- FBref espone statistiche 2025/26 per Serie A, Serie B e numerosi campionati esteri con schema comparabile (minuti, presenze/starts, gol, assist, rigori, cartellini e metriche per90). È la fonte candidata per lo strato calcistico cross-league.
- Non combinare xG/xA di provider diversi senza definizione esplicita; la fonte expected definitiva deve ancora essere scelta in base alla copertura effettiva.

## Stato corrente

La fase concettuale iniziale e la baseline anagrafico-economica ufficiale sono chiuse. È stata definita anche la politica di provenienza dei dati storici. Non assegnare ancora score, fasce o prezzi massimi: manca il primo dataset storico collegato al master.

## Prossimo outcome

Costruire la **tabella storica 2025/26** e collegarla alla baseline 2026/27.

Ordine operativo:

1. acquisire dalla fonte Fantacalcio.it le metriche 2025/26 dei giocatori con storico Serie A (`PV, MV, FM, Gol, GS, Rig segnati/tirati, RP, Ass, Amm, Esp`);
2. conservare nome e squadra della fonte e fare matching al `player_id` 2026/27 con confidence esplicita;
3. classificare i giocatori non coperti dalla Serie A 2025/26 in `Serie B`, `estero`, `altro/pochi dati`;
4. acquisire per questi ultimi statistiche native del campionato di origine senza applicare ancora coefficienti di translation;
5. solo dopo estendere a stagioni precedenti e metriche xG/xA.

Il primo gate è una tabella 2025/26 tracciabile e validata; nessuna previsione 2026/27 prima di questo gate.