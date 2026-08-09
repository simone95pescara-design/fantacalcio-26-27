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

- `AGENTS.md`: istruzioni operative persistenti per continuare il progetto senza ricostruire la chat.
- `data/DATASET_MASTER_SCHEMA.md`: schema iniziale del dataset master e regole di qualità.
- `data/raw/listone-2026-27-source.md`: fonte ufficiale, provenienza e stato di acquisizione del Listone.

## Evidenza sul Listone 2026/27

Verifica 2026-08-09:

- la pagina ufficiale Fantacalcio.it è aggiornata a `Quotazioni e FVM Fantacalcio Serie A 2026/27`;
- la rappresentazione accessibile contiene 502 righe giocatore e 20 squadre;
- per le righe sono disponibili nome, squadra, QI/QA e FVM / 1000 per Classic e Mantra;
- Fantacalcio.it conferma ufficialmente che il Listone 2026/27 contiene ruoli, quotazioni e FVM Classic e Mantra;
- il ruolo Classic non è però serializzato nella rappresentazione testuale accessibile della tabella;
- l'endpoint Excel ufficiale `https://www.fantacalcio.it/api/v1/Excel/prices/21/1` restituisce HTTP 401 nell'ambiente disponibile;
- è stata individuata una fonte secondaria aggiornata (Fantacalcio-Online, stagione 2026/27) che espone un elenco tabellare con ruoli, ma usa propri sistemi di ruolo/configurazioni e presenta classificazioni non coincidenti in modo dimostrabile con il Classic ufficiale Fantacalcio.it; pertanto NON va usata per riempire `role_classic`.

Conclusione qualità dati: non inferire o sostituire il ruolo Classic ufficiale con ruoli di terze parti. La baseline resta bloccata esclusivamente sull'acquisizione del file/lista ufficiale con ruoli.

## Stato corrente

La fase concettuale iniziale è chiusa. Lo schema del dataset master è definito e la fonte ufficiale è verificata. È stato anche verificato che una fonte secondaria facilmente accessibile non è una sostituzione sicura per i ruoli Classic ufficiali. Il blocco concreto è quindi circoscritto: ottenere il Listone ufficiale scaricabile (Excel/PDF o equivalente) con i ruoli.

## Prossimo outcome

Chiudere la **baseline ufficiale Listone Classic 2026/27**.

Percorso preferito: acquisire il file ufficiale tramite il pulsante `Scarica` di Fantacalcio.it in un contesto browser autenticato/accessibile e fornirlo al progetto. Appena disponibile:

1. estrarre automaticamente tutte le righe e il ruolo Classic;
2. preservare snapshot raw datata;
3. verificare duplicati, valori mancanti, 20 squadre, conteggio totale e conteggi per ruolo;
4. produrre dataset strutturato v1 con `player_id, name, team, role_classic, quotation_initial, quotation_current, fvm_1000, source_date, source`;
5. passare immediatamente all'arricchimento storico/statistico.

Non perdere tempo a ricostruire manualmente 502 ruoli o a inferirli da fonti non equivalenti.