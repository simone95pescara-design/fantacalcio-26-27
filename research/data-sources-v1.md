# Fonti dati candidate per l'arricchimento storico/statistico

Data verifica: 2026-08-09.

## Obiettivo

Arricchire la baseline ufficiale 2026/27 senza confondere dati Fantacalcio, statistiche calcistiche generali e stime. Ogni famiglia di feature deve conservare provenienza, stagione e campionato.

## 1. Fantacalcio.it — storico fantacalcistico Serie A

Fonte primaria per le metriche direttamente legate al gioco quando il calciatore ha militato in Serie A.

URL base 2025/26:
`https://www.fantacalcio.it/statistiche-serie-a/2025-26/statistico/medie`

Campi esposti dalla pagina ufficiale: partite valutate (PV), media voto (MV), fantamedia (FM), gol, gol subiti, rigori segnati/tirati, rigori parati, assist, ammonizioni, espulsioni.

Regola: MV/FM e bonus/malus Fantacalcio vanno presi dalla fonte Fantacalcio quando disponibili; non sostituirli con rating o voti di provider diversi.

Limite osservato: il download Excel storico ufficiale individuato (`/api/v1/Excel/stats/20/4` per 2025/26) restituisce HTTP 401 dall'ambiente automatico. La pagina web resta consultabile.

## 2. FBref — statistiche calcistiche comparabili tra campionati

Fonte candidata per minuti, presenze, partenze, gol, assist, rigori, cartellini e statistiche per 90; utile soprattutto per confrontare Serie A, Serie B e campionati esteri con schema omogeneo.

Serie A 2025/26:
`https://fbref.com/en/comps/11/2025-2026/stats/2025-2026-Serie-A-Stats`

Serie B 2025/26:
`https://fbref.com/en/comps/18/stats/Statistiques-Serie-B`

FBref copre anche molte leghe estere e consente di conservare il campionato originario del giocatore.

Regola: i dati grezzi di campionati diversi non vanno trasformati subito in equivalenti Serie A. Prima si preservano come osservazioni native con `competition`, `season` e `source`, poi si costruirà separatamente il modello di league/promotion translation.

## 3. Metriche xG/xA

Le metriche expected devono provenire da una fonte con definizione coerente e copertura sufficiente. Non combinare xG/xA di provider diversi come se fossero perfettamente equivalenti. La fonte definitiva va scelta dopo verifica di copertura per Serie A, Serie B e principali campionati di provenienza dei 496 giocatori.

## Modello dati storico minimo

Ogni record stagione-giocatore deve conservare almeno:

- `player_id_master` (quando il matching è certo);
- `player_name_source`;
- `season`;
- `competition`;
- `team_source`;
- `appearances` / `minutes` quando disponibili;
- `fantacalcio_pv`, `mv`, `fm`, `goals`, `assists`, `yellow`, `red`, `penalties_scored`, `penalties_attempted` quando provenienti da Fantacalcio;
- statistiche calcistiche/per90 da provider generalista in colonne separate;
- eventuali `xg`, `xa` con provider esplicito;
- `source_url`;
- `source_date`;
- `match_confidence` per il collegamento al master 2026/27.

## Regole di qualità

1. Non fare join solo sul cognome quando esistono omonimie o abbreviazioni.
2. Conservare il nome originale della fonte e il metodo di matching.
3. Non imputare zero quando il dato è assente: assente e zero hanno significati diversi.
4. Non confrontare MV/FM con rating di altri provider.
5. Non convertire ancora Serie B/estero in Serie A: prima acquisizione e validazione, poi traduzione.
6. Per giocatori senza storico sufficiente aumentare successivamente l'incertezza invece di inventare una previsione precisa.

## Prossimo passo dati

Costruire la prima tabella storica 2025/26 partendo da Fantacalcio.it per i giocatori con esperienza Serie A, e in parallelo classificare i giocatori del master 2026/27 in base al tipo di storico disponibile: Serie A, Serie B, estero, campione piccolo/nuovo.
