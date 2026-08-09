# Fonte ufficiale Listone Fantacalcio 2026/27

## Fonte primaria

Pagina ufficiale Fantacalcio.it `Quotazioni e FVM Fantacalcio Serie A 2026/27`.

URL sorgente: `https://www.fantacalcio.it/quotazioni-fantacalcio`

Ultima verifica: 2026-08-09.

Fantacalcio.it ha annunciato il Listone 2026/27 per il 4 agosto 2026, specificando che contiene ruoli, quotazioni e FVM per Classic e Mantra.

## Stato di acquisizione verificato

La pagina ufficiale è ora indicizzata con intestazione esplicita `Quotazioni e FVM Fantacalcio Serie A 2026/27` e rende consultabile l'elenco corrente.

Nella rappresentazione testuale verificata sono presenti 502 righe giocatore consecutive (dalla prima voce Martinez L. all'ultima Satalino), appartenenti alle 20 squadre mostrate dalla pagina.

Per ogni riga la rappresentazione accessibile espone almeno:

- nome giocatore;
- abbreviazione squadra;
- QI Classic;
- QA Classic;
- FVM / 1000 Classic;
- QI Mantra;
- QA Mantra;
- FVM / 1000 Mantra.

Esempi osservati il 2026-08-09: Martinez L. (INT) QI/QA Classic 35/35, FVM 370; Malen (ROM) 34/34, FVM 365; Dimarco (INT) 32/32, FVM 265.

## Limite ancora aperto

La rappresentazione testuale della tabella non espone in modo affidabile la colonna del ruolo Classic, anche se il sito dichiara la visualizzazione Classic/Mantra e il Listone ufficiale comprende i ruoli.

Il pulsante `Scarica` è presente. In una verifica precedente il relativo endpoint Excel era stato identificato come `https://www.fantacalcio.it/api/v1/Excel/prices/21/1`, ma l'accesso diretto dall'ambiente aveva restituito HTTP 401. Non dichiarare quindi ancora acquisito l'Excel ufficiale.

## Controlli di qualità richiesti prima del dataset master v1

1. ottenere il ruolo Classic ufficiale per tutte le 502 righe, preferibilmente dal file ufficiale o da una rappresentazione ufficiale equivalente;
2. verificare che non vi siano duplicati di identità e che tutte le 20 squadre siano rappresentate;
3. preservare una snapshot raw datata;
4. produrre il dataset strutturato v1 con almeno `player`, `team`, `role_classic`, `qi`, `qa`, `fvm_1000`, `source_date`;
5. mantenere separati i dati Mantra perché il progetto corrente usa Classic.

## Regola di provenienza

I dati del listone devono restare riconducibili alla fonte ufficiale e alla data di acquisizione. Aggiornamenti successivi di mercato o quotazione non devono sovrascrivere silenziosamente la snapshot iniziale: creare snapshot datate o una cronologia equivalente.