# Criterio reale di scelta all'asta

Questo file corregge la direzione della FAST pipeline.

## Il prodotto NON e una lista di top

Per ogni ruolo il risultato deve essere una **lista di acquisto ordinata per quanto vorremmo realmente il giocatore al suo probabile prezzo**, includendo nomi noti, value, poco pubblicizzati e scommesse.

Ogni giocatore importante deve avere:
- `DESIDERABILITA`: quanto lo vogliamo realmente (5/5 → 1/5);
- `TIPO`: target forte / value / upside / floor / solo sconto / evita;
- `PREVISIONE MV 26/27`: intervallo, non falsa precisione;
- `TITOLARITA`: alta / media / bassa;
- `BONUS`: profilo atteso;
- `RISCHIO`: cosa puo rompere la previsione;
- `PREZZO BUONO`: fascia in cui siamo contenti di comprarlo;
- `HARD CAP`: oltre il quale il valore sparisce;
- `PERCHE`: evidenza storica + ruolo + contesto 26/27;
- `CONFIDENCE`: alta/media/bassa.

## Principio di ranking

Non ordinare per fama o per punti assoluti. Ordinare per:

`valore fantacalcistico atteso - costo atteso - rischio + utilita per la struttura della rosa`.

Quindi un giocatore da MV prevista 6.10 a 12 crediti puo essere un acquisto migliore di uno da 6.25 a 55.

## Uso del lavoro precedente

Il lavoro dati NON viene buttato:
- FVM 26/27 = prior del prezzo/consenso di mercato;
- storico 25/26 = base quantitativa per MV/FM/bonus/disponibilita;
- provenienza = confidence per nuovi arrivi;
- modificatore = aumenta il valore di MV e disponibilita;
- ricerca live = usata solo per verificare ruolo, gerarchie, infortuni, piazzati e cambi di contesto dei profili che possono essere acquistati.

## Output d'asta finale

Per ogni ruolo servono quattro liste leggibili in chat e nel repository:
1. `LI PRENDEREI FORTE` — profili su cui siamo disposti a costruire il reparto;
2. `VALUE CHE VOGLIO` — nomi meno contesi con rapporto prezzo/rendimento superiore;
3. `SCOMMESSE CON UPSIDE` — costo basso, rischio noto, ceiling reale;
4. `SOLO A SCONTO / EVITA` — giocatori validi ma probabilmente pagati troppo o con rischio sfavorevole.

L'asta deve essere eseguibile partendo da queste liste, non dalla conoscenza dei nomi piu famosi.
