# Dataset master 2026/27 — schema iniziale

## Scopo

Definire il primo artefatto dati reale del progetto. Il dataset master deve permettere di passare dal listone ufficiale a previsioni, slot funzionali, valore economico e decisioni d'asta.

Lo schema è volutamente diviso in famiglie di campi. Non tutte le colonne devono essere disponibili subito: i campi osservati, derivati e stimati devono restare distinguibili.

## 1. Identità e listone ufficiale

Campi minimi:

- `player_id` — identificatore stabile interno;
- `name` — nome listone;
- `team` — squadra Serie A 2026/27;
- `role_classic` — P/D/C/A;
- `quotation_initial` — quotazione iniziale ufficiale;
- `quotation_current` — quotazione ufficiale corrente;
- `fvm_1000` — FVM ufficiale su base 1000;
- `listone_source_date` — data acquisizione;
- `listone_source` — fonte ufficiale.

## 2. Storico prestazionale

Per ciascuna stagione utile e, dove possibile, normalizzato per 90 minuti:

- presenze;
- minuti;
- titolarità;
- media voto;
- fantamedia;
- gol;
- assist;
- ammonizioni;
- espulsioni;
- autogol;
- rigori segnati/sbagliati;
- altri bonus/malus rilevanti.

Lo storico non va aggregato subito in una media piatta: mantenere le stagioni separate per consentire pesi di recency.

## 3. Metriche sottostanti

Candidate, solo se acquisibili in modo coerente:

- xG;
- npxG;
- xA;
- tiri e tiri in area;
- tocchi in area;
- key passes/chance creation;
- partecipazione offensiva;
- clean sheet/gol subiti per portieri e difensori;
- altre metriche dimostrate utili per ruolo.

## 4. Disponibilità e ruolo

- minuti attesi 2026/27;
- probabilità di titolarità;
- concorrenza interna;
- ruolo tattico reale;
- posizione media/compiti offensivi quando disponibili;
- rischio turnover;
- storico infortuni e indisponibilità;
- stato fisico corrente.

## 5. Responsabilità sui piazzati

- gerarchia rigori;
- probabilità di essere rigorista;
- punizioni dirette;
- corner;
- altri piazzati rilevanti.

## 6. Contesto squadra

- allenatore;
- sistema tattico;
- forza offensiva squadra;
- forza difensiva squadra;
- qualità attesa della squadra;
- eventuale cambio squadra/allenatore/ruolo rispetto allo storico.

## 7. Trasferibilità dello storico

Per giocatori non direttamente comparabili con Serie A recente:

- campionato precedente;
- livello/forza del campionato precedente;
- flag `promotion_from_serie_b`;
- flag `foreign_league_transfer`;
- coefficiente/modello di traduzione, se derivato;
- qualità/confidenza della traduzione.

Non usare un coefficiente arbitrario unico se i dati non lo giustificano.

## 8. Profilo anagrafico e sviluppo

- età;
- curva di sviluppo/declino stimata;
- esperienza Serie A;
- campione storico disponibile.

## 9. Previsione 2026/27

Campi derivati futuri:

- minuti previsti;
- presenze previste;
- MV prevista;
- FM prevista;
- gol previsti;
- assist previsti;
- bonus/malus previsti;
- floor;
- stima centrale;
- ceiling;
- confidence/incertezza.

## 10. Valore fantacalcistico e slot

- score complessivo per la nostra lega;
- score specifico modificatore difesa quando pertinente;
- slot funzionali candidati;
- ranking nello slot;
- rischio specifico dello slot.

## 11. Economia d'asta

- FVM ufficiale;
- prezzo di mercato atteso;
- prezzo target nostro;
- fascia conveniente;
- hard cap;
- valore marginale per credito;
- alternative fungibili;
- stato disponibilità durante l'asta.

## Regole di qualità

- distinguere sempre osservato / derivato / stimato;
- conservare fonte e data per dati aggiornabili;
- non riempire campi mancanti con zero se zero non significa realmente assenza;
- mantenere stagioni e campionati di origine separati prima della traduzione;
- non congelare pesi e soglie prima di osservare distribuzioni e copertura dei dati;
- ogni nuova colonna deve avere una funzione concreta nel modello o nella decisione d'asta.

## Stato

Schema iniziale definito. Prossimo passo: popolare il nucleo ufficiale del listone 2026/27 e verificare copertura/qualità delle fonti per le famiglie di feature successive.
