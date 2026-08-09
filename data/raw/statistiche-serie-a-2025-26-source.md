# Statistiche Fantacalcio Serie A 2025/26 — fonte

## Fonte primaria

Pagina ufficiale Fantacalcio.it:

`https://www.fantacalcio.it/statistiche-serie-a/2025-26/fantacalcio/medie`

Verificata il 2026-08-09.

La pagina espone per i calciatori Serie A 2025/26 almeno:

`Calciatore, Sq, PV, MV, FM, Gol, GS, Rig, RP, Ass, Amm, Esp`.

La pagina è leggibile via web e contiene l'intera tabella storica. Il download ufficiale individuato dal pulsante `Scarica` punta a:

`https://www.fantacalcio.it/api/v1/Excel/stats/20/1`

Nell'ambiente corrente l'endpoint diretto restituisce HTTP 401, quindi non dichiarare acquisito il workbook Excel finché non viene fornito/scaricato in modo effettivo.

## Stato acquisizione

- schema e campi verificati;
- contenuto tabellare web verificato;
- workbook ufficiale non acquisito per 401;
- nessuna previsione o imputazione eseguita;
- il matching completo ai 496 giocatori del master resta il prossimo gate dati.

## Regola di precedenza

Se viene fornito il workbook ufficiale delle statistiche 2025/26, esso prevale sulla rappresentazione web come snapshot raw canonica, analogamente a quanto fatto con il Listone 2026/27.
