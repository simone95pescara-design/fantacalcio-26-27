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

## Pipeline

fonti e dataset master → storico multi-stagione → previsioni + incertezza → valore fantacalcistico → score per slot → valore economico → ottimizzazione rosa / 1000 crediti → piano d'asta → adattamento live

## Baseline ufficiale 2026/27 — CHIUSA

Workbook ufficiale `Quotazioni_Fantacalcio_Stagione_2026_27.xlsx`: 496 giocatori attivi, 20 squadre, P=60 D=175 C=174 A=87; 6 ceduti separati. ID Fantacalcio usato come chiave primaria.

## Storico Fantacalcio 2025/26 — ACQUISITO E MATCHATO

Workbook ufficiale `Statistiche_Fantacalcio_Stagione_2025_26.xlsx`: 663 giocatori. Matching esatto tramite ID: 384/496 = 77,42%; unmatched 112 (P=17, D=45, C=32, A=18).

## Provenienza 2025/26 unmatched — GATE CHIUSO

Tutti i 112 unmatched sono classificati. Persistenza evidenze:
- `historical-2025-26-provenance-v1.csv`: 77;
- `provenance-batch-078-087.csv`: 10;
- `provenance-batch-088-097.csv`: 10;
- `provenance-batch-098-112.csv`: 15.

Controllo aritmetico: 77+10+10+15 = 112. Working population canonica: 112. Residui classificazione: 0.

Creato `data/processed/provenance-master-2025-26.csv` come control record del consolidamento. I quattro source batch restano i record canonici dell'evidenza e della confidence. Nei casi multi-stint le esperienze devono restare separate nella fase statistica.

## Acquisizione quantitativa nativa 2025/26 — AVVIATA

Creato `data/processed/native-stats-2025-26-serie-b-batch-01.csv` con il primo batch quantitativo Serie B, ricavato da tabelle strutturate FBref 2025/26 per Frosinone, Venezia e Monza.

Campi target: `MP, Starts, Min, Gls, Ast, PK, PKatt, CrdY, CrdR`, mantenuti nella scala nativa della competizione. Il batch contiene 20 giocatori; per alcune righe la copertura è completa, per altre sono disponibili soltanto playing time o subset di output. I campi mancanti restano esplicitamente vuoti e sono marcati in `coverage_note`: non vengono imputati.

Esempi ad alta copertura già acquisiti:
- Palmisani 38/38, 3410';
- Calò 37/37, 3173', 10 gol, 15 assist, 5 rigori, 7 gialli;
- Ghedjemis 37 presenze, 36 start, 3009', 15 gol;
- Kvernadze 36 presenze, 2495', 5 gol, 5 assist;
- Stankovic (Venezia) 38/38, 3420';
- Busio 37/37, 3196';
- Pessina 33/33, 2904', 5 gol, 3 rigori su 3;
- Birindelli 33 presenze, 29 start, 2627', 5 gol.

## Regole dati stabilizzate

- non tradurre ancora Serie B/estero/Serie C/youth in equivalenti Serie A;
- mantenere campionato e club nativi;
- mantenere stint multipli separati;
- non alzare artificialmente la confidence;
- non imputare statistiche non osservate: campo vuoto + `coverage_note`;
- MV e fantamedia distinte;
- titolarità/minuti/probabilità di voto centrali;
- storico multi-stagione con recency;
- distinguere output osservati e metriche sottostanti xG/xA;
- giovani e campioni piccoli devono portare incertezza esplicita;
- nessuno score/prezzo/hard cap prima della chiusura dei dati e della metodologia di translation.

## Stato corrente

Baseline 2026/27 chiusa; storico Serie A 2025/26 acquisito; provenienza 112/112 chiusa; acquisizione quantitativa nativa avviata con primo batch Serie B di 20 giocatori.

## Prossimo outcome

1. completare i restanti giocatori Serie B 2025/26 con gli stessi campi target;
2. fare QA della copertura Serie B;
3. passare ai campionati esteri, mantenendo stint e competizione espliciti;
4. acquisire Serie C / seconde squadre / youth con flag qualità/copertura;
5. unire i dati nativi non-Serie A con i 384 Serie A per costruire la prima tabella storica 2025/26 dei 496.

Solo dopo: stagioni precedenti, xG/xA e metodologia di translation cross-league.