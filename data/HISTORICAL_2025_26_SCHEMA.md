# Schema storico 2025/26

Questo file definisce il primo blocco storico da collegare alla baseline ufficiale 2026/27.

## Unità osservativa

Una riga rappresenta una stagione/competizione di un giocatore. Lo storico non viene fuso subito nel master 2026/27: resta in formato long per preservare provenienza, campionato e comparabilità.

## Campi minimi

- `player_id_2026_27`: ID Fantacalcio del master quando il matching è risolto;
- `source_player_name`: nome esattamente come compare nella fonte storica;
- `source_team`: squadra nella stagione storica;
- `season`: `2025/26`;
- `country`;
- `competition`;
- `tier`: livello del campionato, es. 1 per Serie A, 2 per Serie B;
- `appearances_fantacalcio` (`PV`) quando disponibile;
- `starts`: titolarità/partenze quando disponibile;
- `minutes`;
- `mv`;
- `fm`;
- `goals`;
- `goals_conceded`;
- `penalties_scored`;
- `penalties_taken`;
- `penalties_saved`;
- `assists`;
- `yellow_cards`;
- `red_cards`;
- `xg`;
- `xa`;
- `npxg` quando disponibile;
- `source_provider`;
- `source_url`;
- `source_date`;
- `match_method`: `exact_id`, `exact_name_team`, `normalized_name`, `manual_review`, `unmatched`;
- `match_confidence`: `high`, `medium`, `low`;
- `comparability_class`: `serie_a_fantacalcio`, `serie_b_native`, `foreign_native`, `other`, `insufficient_data`.

## Regole

1. Non convertire Serie B o campionati esteri in equivalenti Serie A in questa fase.
2. `MV` e `FM` sono ammesse solo se provengono da una fonte Fantacalcio comparabile; non sostituirle con rating di altri provider.
3. Non mescolare xG/xA di provider diversi nella stessa serie senza registrare il provider.
4. Il matching al master 2026/27 deve essere tracciabile e la confidence deve restare esplicita.
5. Trasferimenti tra squadre nella stessa stagione non devono causare perdita di informazione: se la fonte offre righe separate, conservarle oppure aggregarle solo con regola documentata.
6. Campioni piccoli o assenza di dati devono restare espliciti; non imputare valori medi per riempire celle.

## Gate di qualità

Il blocco 2025/26 è pronto per la fase successiva solo quando:

- ogni riga storica conserva fonte e competizione;
- i match automatici ad alta confidence sono distinguibili dai casi manuali;
- i giocatori del master non coperti sono classificati per motivo (`Serie B`, `estero`, `altro/pochi dati`);
- nessun valore cross-league è già tradotto arbitrariamente;
- sono prodotti conteggi di copertura e casi non risolti.
