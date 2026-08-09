# Fonte ufficiale Listone Fantacalcio 2026/27

## Fonte primaria

Pagina ufficiale Fantacalcio.it `Quotazioni e FVM Fantacalcio Serie A 2026/27`.

URL sorgente: `https://www.fantacalcio.it/quotazioni-fantacalcio`

Data verifica: 2026-08-09.

La pagina ufficiale espone il Listone 2026/27 con giocatore, squadra, quotazione iniziale/corrente e FVM su base 1000, con visualizzazione Classic e Mantra.

Fantacalcio.it ha annunciato il Listone 2026/27 per il 4 agosto 2026, specificando che contiene ruoli, quotazioni e FVM per Classic e Mantra.

## Acquisizione

La pagina web è consultabile e mostra i dati 2026/27. Il pulsante `Scarica` punta al momento della verifica all'endpoint:

`https://www.fantacalcio.it/api/v1/Excel/prices/21/1`

L'accesso diretto tramite l'ambiente di ricerca ha restituito HTTP 401, quindi il file Excel ufficiale non è stato ancora acquisito direttamente.

Questo non invalida la fonte web, ma significa che il dataset raw completo non deve essere dichiarato acquisito finché non viene ottenuto in forma riproducibile o estratto dalla pagina ufficiale con controllo di completezza.

## Evidenza osservata

La pagina verificata riporta esplicitamente l'intestazione `Quotazioni e FVM Fantacalcio Serie A 2026/27` e contiene già l'elenco dei giocatori 2026/27.

## Prossimo controllo

1. acquisire l'intero listone Classic in forma tabellare;
2. verificare numero totale di giocatori e ruoli;
3. preservare una copia raw datata;
4. produrre il primo dataset strutturato con identità, squadra, ruolo, quotazioni e FVM.
