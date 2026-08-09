# Istruzioni operative persistenti

Questo file governa il modo di lavorare sul progetto `fantacalcio-26-27`.

## Scopo

L'utente non deve ricostruire il contesto, ricordare il metodo di lavoro o orchestrare manualmente ogni fase quando cambia chat.

Quando un agente AI riprende il progetto deve:

1. leggere questo file;
2. leggere `PROJECT.md`;
3. ricostruire lo stato reale dagli artefatti presenti nel repository quando necessario;
4. riprendere dal prossimo outcome registrato senza chiedere all'utente di ripetere informazioni già persistite;
5. aggiornare `PROJECT.md` dopo ogni risultato significativo che cambia stato, decisioni, vincoli, incertezze o prossimo lavoro.

## Principi di comportamento

- Mantieni il focus sull'obiettivo finale del progetto: massimizzare la probabilità di vincere la lega Fantacalcio 2026/27 descritta in `PROJECT.md`.
- Lavora su un problema per volta e porta ogni passo a un output concreto prima di aprire il successivo.
- Non trasformare ogni nuovo messaggio dell'utente in un nuovo obiettivo: può essere una correzione, informazione, domanda o modifica locale. L'obiettivo persistente cambia solo quando l'utente lo modifica realmente.
- Non chiedere all'utente di ripetere informazioni già presenti nel repository.
- Non inventare regole della lega, dati, statistiche, prezzi, pesi o soglie mancanti. Se sono materialmente rilevanti, ricavali da fonti affidabili o mantienili esplicitamente aperti.
- Per informazioni temporali o aggiornabili (listone, trasferimenti, infortuni, rigoristi, gerarchie, probabili titolari, allenatori, calendario, quotazioni, FVM, statistiche correnti) usa fonti aggiornate e registra la data/fonte negli output pertinenti.
- Distingui sempre dati osservati, stime, assunzioni e incertezza.
- Non ridurre la valutazione dei giocatori a reputazione, fantamedia o gol dell'ultima stagione.
- Non fissare prematuramente una struttura rigida di rosa o percentuali di budget se i dati e il mercato non le giustificano.
- Non produrre documentazione cerimoniale. Ogni file deve servire alla continuità, alla ricerca, al modello, alla decisione o all'esecuzione dell'asta.
- Se una nuova evidenza invalida una decisione precedente, aggiorna la decisione e gli artefatti dipendenti invece di difendere il lavoro precedente.

## Ciclo operativo

Per ogni passo significativo:

```text
obiettivo persistente + stato corrente
        ↓
gap rilevante
        ↓
prossimo outcome concreto
        ↓
ricerca / dati / analisi / modellazione necessaria
        ↓
output verificabile
        ↓
aggiornamento di PROJECT.md
        ↓
rivalutazione
        ↺
```

Non seguire fasi inutili solo perché compaiono in una roadmap. La roadmap orienta il lavoro, ma il prossimo passo deve derivare dallo stato reale.

## Organizzazione degli artefatti

La struttura va creata progressivamente, solo quando serve realmente.

- `PROJECT.md`: memoria canonica di obiettivo, contesto, decisioni, stato e prossimo outcome.
- `research/`: ricerche e conclusioni durevoli che giustificano il modello.
- `data/raw/`: dati sorgente non modificati.
- `data/processed/`: dataset puliti, normalizzati o arricchiti.
- `models/`: definizioni e implementazioni di scoring, previsioni, slot, incertezza e ottimizzazione.
- `auction/`: strategia d'asta, prezzi, hard cap, alternative, stato live e logica adattiva.
- `outputs/`: prodotti finali destinati all'uso diretto dell'utente.

Non creare directory o file vuoti in anticipo.

## Continuità

`PROJECT.md` è la memoria operativa principale. Deve restare breve abbastanza da poter essere letto all'inizio di una nuova sessione ma completo abbastanza da evitare di ricostruire la conversazione.

Persisti in `PROJECT.md`:

- obiettivo e contesto della lega;
- decisioni stabilizzate;
- principi del modello già accettati;
- evidenza prodotta e output disponibili;
- incertezze ancora aperte che influenzano il lavoro;
- stato corrente;
- prossimo outcome.

Non persistere ragionamenti transitori o l'intera cronologia della chat.

## Regola di ripresa in una nuova chat

Se l'utente indica questo repository o chiede di continuare il progetto, non avviare una nuova discovery generale. Leggi `AGENTS.md` e `PROJECT.md`, poi riprendi dal prossimo outcome salvo che il nuovo messaggio modifichi esplicitamente priorità o obiettivo.
