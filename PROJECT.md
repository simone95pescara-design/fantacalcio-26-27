# Stato canonico del progetto

## Obiettivo finale

Massimizzare la probabilità di vincere la lega Fantacalcio 2026/27 costruendo un sistema decisionale completo che supporti preparazione, valutazione dei giocatori, costruzione della rosa, allocazione dei 1000 crediti ed esecuzione/adattamento dell'asta.

L'obiettivo non è creare una semplice lista dei giocatori migliori, ma trasformare dati e ricerca in decisioni operative ripetibili.

## Contesto della lega

- stagione: 2026/27;
- partecipanti: 8;
- budget iniziale: 1000 crediti;
- modalità: Classic, non Mantra;
- modificatore difesa: classico;
- resto del regolamento: sostanzialmente standard, salvo particolarità che emergeranno;
- obiettivo competitivo: vincere la lega, non soltanto massimizzare fantamedia o valore nominale della rosa.

## Output finali attesi

Il progetto deve arrivare almeno a:

1. dataset master 2026/27 con tutti i giocatori del listone ufficiale e informazioni rilevanti;
2. previsioni 2026/27 per giocatore con incertezza esplicita;
3. valore fantacalcistico specifico per la nostra lega;
4. classificazione dei giocatori per slot/funzione nella rosa;
5. valutazione economica con prezzo target, fascia conveniente e hard cap;
6. modello di rosa e allocazione del budget derivati dai dati, non fissati per intuizione;
7. piano d'asta con alternative fungibili e regole condizionali;
8. sistema di aggiornamento durante l'asta in base a prezzi osservati, crediti residui, scarsità e giocatori rimasti.

Dopo l'asta, lo stesso patrimonio informativo potrà essere esteso a formazione settimanale, scambi e mercato di riparazione, ma questi non sono il fronte corrente.

## Principi stabilizzati

- Non esiste al momento evidenza pubblica sufficiente per affermare una composizione universale delle rose vincenti; evitare percentuali o formule inventate.
- La rosa va costruita per funzioni/slot, non soltanto per etichette `top / semitop / scommessa`.
- Ogni slot deve avere più candidati fungibili per evitare dipendenza da singoli nomi.
- Il modificatore difesa rende media voto, disponibilità e profondità difensiva fonti di valore autonome rispetto ai bonus.
- Media voto e fantamedia devono restare distinte.
- Titolarità, minuti e probabilità di voto sono variabili centrali.
- Lo storico deve essere multi-stagione e pesato per recency, non una media piatta.
- Gol/assist osservati devono essere distinti dalle metriche sottostanti (es. xG/xA e altre metriche pertinenti).
- Posizione tattica reale rispetto al ruolo Fantacalcio è rilevante.
- Rigori, punizioni, corner e gerarchie sui piazzati sono fonti di valore.
- Forza della squadra, allenatore, sistema tattico e concorrenza interna devono entrare nella valutazione quando pertinenti.
- Infortuni, ballottaggi, trasferimenti e altri fattori di rischio devono essere espliciti.
- Serie B → Serie A e campionati esteri → Serie A richiedono una traduzione del rendimento; i dati non sono direttamente comparabili.
- Giovani e giocatori con pochi minuti devono avere maggiore incertezza.
- Ogni previsione deve rappresentare anche incertezza/confidence, idealmente con floor, stima centrale e ceiling o distribuzione equivalente.
- Valore sportivo e prezzo d'asta sono problemi distinti.
- FVM/quotazioni sono informazioni sul mercato, non il nostro prezzo massimo.
- Il criterio economico è il rendimento marginale ottenibile per credito, tenendo conto di scarsità, rischio e ruolo nella rosa.
- L'asta deve essere adattiva: prezzo target, fascia accettabile, hard cap, alternative e redistribuzione del budget quando un target salta.
- Non fissare soglie numeriche o pesi prima di osservare distribuzioni e dati 2026/27, salvo che esista evidenza esterna forte.

## Modello concettuale corrente

### Livello giocatore

Feature candidate già identificate:

- storico multi-stagione;
- minuti/presenze/titolarità;
- media voto e fantamedia;
- gol, assist, bonus e malus;
- xG/xA e metriche predittive pertinenti;
- posizione e ruolo tattico reale;
- rigori e piazzati con relativa gerarchia;
- squadra e forza offensiva/difensiva;
- allenatore e sistema;
- concorrenza per il posto;
- storico infortuni/disponibilità;
- età e curva di sviluppo/declino;
- league/promotion translation quando necessaria;
- rischio, floor, ceiling e confidence;
- FVM/quotazione/prezzo di mercato atteso.

Il feature set definitivo non è ancora congelato: deve essere chiuso sulla base di dati disponibili e valore predittivo, evitando variabili decorative.

### Slot funzionali preliminari

La struttura non è ancora congelata economicamente, ma sono emerse funzioni candidate.

**Difesa:** anchor da modificatore, premium ibrido, stabilizzatori ad alta MV/titolarità, profili offensivi/upside, rotazioni/value.

**Centrocampo:** primary scorer, secondary scorer, titolari offensivi/value, floor player, upside e scommesse asimmetriche low-cost.

**Attacco:** primary goal source, seconda fonte forte di gol, titolare ad alto rapporto produzione/prezzo, rotazioni/upside e low-cost funzionali.

**Portieri:** titolarità, forza difensiva, clean-sheet/gol subiti attesi, media voto e complementarità; strategia economica ancora da derivare.

## Pipeline di costruzione

```text
ricerca e definizione delle feature utili
        ↓
dataset master 2026/27
        ↓
previsioni dei giocatori + incertezza
        ↓
valore fantacalcistico specifico per la lega
        ↓
score per slot/funzione
        ↓
valore economico e prezzi d'asta
        ↓
ottimizzazione della rosa sotto 1000 crediti
        ↓
piano d'asta con hard cap e alternative
        ↓
adattamento live durante l'asta
```

Questa è una roadmap, non una pipeline cieca: nuove evidenze possono richiedere correzioni a monte.

## Stato corrente

Completata una prima fase di ricerca concettuale su:

- limiti delle statistiche sulle rose storicamente vincenti;
- importanza del modificatore difesa;
- slot funzionali della rosa;
- titolarità e minuti;
- storico multi-stagione;
- metriche sottostanti;
- rigori/piazzati;
- trasferibilità da Serie B e campionati esteri;
- incertezza delle previsioni;
- rapporto tra valore sportivo e prezzo d'asta;
- necessità di una strategia d'asta adattiva.

La comprensione concettuale è sufficiente per passare alla costruzione; evitare ulteriore teoria generica se non risolve un gap concreto.

## Prossimo outcome

Definire la struttura del **dataset master 2026/27** e acquisire il **listone ufficiale completo**, in modo da iniziare il primo artefatto dati reale del progetto.

Prima di congelare definitivamente tutte le colonne, verificare quali fonti affidabili e aggiornate sono realisticamente acquisibili per ciascuna famiglia di feature e quali dati possono essere storicizzati in modo coerente.
