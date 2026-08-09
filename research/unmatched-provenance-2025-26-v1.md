# Ricerca provenienza unmatched 2025/26 — v1

Data ricerca: 2026-08-09.

## Scopo

Classificare i 112 giocatori del Listone 2026/27 senza match ID nello storico Fantacalcio Serie A 2025/26, senza confondere `assenza dallo storico Fantacalcio` con `assenza di dati calcistici`.

## Risultato strutturale emerso

Una quota importante degli unmatched non e' un vero caso di dati mancanti: proviene dalle squadre promosse dalla Serie B 2025/26 oppure da trasferimenti esteri. Per questi giocatori va acquisito lo storico nativo della competizione 2025/26 e solo successivamente applicata una metodologia di league translation.

## Serie B 2025/26: fonti verificate

FBref espone tabelle 2025/26 per Frosinone, Venezia e Monza con MP, starts, minuti, gol, assist, rigori, cartellini e statistiche per 90. Le tabelle permettono quindi di recuperare direttamente gran parte degli unmatched appartenenti alle neopromosse.

Esempi verificati Frosinone:
- Lorenzo Palmisani: 38 presenze, 38 starts, 3410 minuti;
- Giacomo Calo: 37 presenze, 3173 minuti, 10 gol, 15 assist, 5 rigori segnati;
- Fares Ghedjemis: 37 presenze, 3009 minuti, 15 gol, 3 assist;
- Anthony Oyono: 34 presenze, 2750 minuti, 1 gol, 4 assist;
- Giorgi Kvernadze: 36 presenze, 2495 minuti, 5 gol, 5 assist;
- Gabriele Calvani: 35 presenze, 2790 minuti, 1 gol, 1 assist.

Esempi verificati Venezia:
- Filip Stankovic: 38 presenze, 3420 minuti;
- Gianluca Busio: 37 presenze, 3196 minuti, 7 gol, 4 assist, 1 rigore;
- Joel Schingtienne: 35 presenze, 3038 minuti, 1 gol, 2 assist;
- Kike Perez: 35 presenze, 2735 minuti, 3 gol, 7 assist;
- Andrea Adorante e John Yeboah risultano inoltre nelle tabelle individuali della stagione.

Monza dispone della stessa struttura FBref 2025/26 Serie B; la stagione si e' chiusa con 61 gol fatti e 32 subiti in 38 partite.

## Implicazione metodologica

Non utilizzare MV/FM Fantacalcio Serie A per questi giocatori, perche' non esistono sulla stessa scala/competizione nella stagione 2025/26. Conservare invece statistiche native Serie B con `source_competition=Serie B` e `translation_status=not_applied`.

## Classi di provenienza da usare

- `SERIE_B_2025_26`: giocatore osservato in Serie B 2025/26;
- `FOREIGN_LEAGUE_2025_26`: giocatore osservato in un campionato estero;
- `YOUTH_RESERVE_2025_26`: settore giovanile/riserve o campione senior insufficiente;
- `RETURN_OTHER_2025_26`: rientro/prestito/altra competizione italiana non Serie A/B;
- `UNRESOLVED`: provenienza non ancora verificata.

Ogni classificazione deve avere almeno `source_competition`, `source_team`, `source_url/reference`, `confidence`.

## Regola di acquisizione

1. Match esatto per nome normalizzato + squadra/storia trasferimento, mai solo fuzzy name.
2. Salvare dati grezzi nella scala della competizione originale.
3. Non confrontare direttamente gol/90 o assist/90 di campionati diversi come se fossero equivalenti.
4. Non applicare coefficienti di conversione in questa fase.
5. Mantenere esplicita l'incertezza per giovani e campioni piccoli.

## Prossimo batch

Costruire `historical-2025-26-provenance.csv` per tutti i 112 unmatched. Prima risolvere in blocco i giocatori 2026/27 di Frosinone, Venezia e Monza usando le tabelle Serie B 2025/26; successivamente ricercare individualmente i trasferimenti esteri e infine i giovani/reserve.
