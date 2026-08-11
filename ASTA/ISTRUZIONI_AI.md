# ASTA FANTACALCIO 2026/27 — ISTRUZIONI OPERATIVE PER L'AI

## Scopo
Questa cartella è la fonte operativa dell'asta. Ogni AI/chat che gestisce l'asta deve leggere questo file prima di registrare o modificare dati.

## Principi obbligatori
1. Ogni partecipante parte da **1000 crediti**, salvo modifica esplicita dell'utente.
2. Non inventare mai nomi di squadre, partecipanti, giocatori, prezzi o ruoli.
3. Ogni acquisto deve essere registrato solo sulla base di un messaggio dell'utente.
4. Un acquisto già registrato non va modificato o cancellato senza una correzione esplicita dell'utente.
5. Dopo ogni operazione ricalcolare sempre crediti spesi, crediti residui, numero di giocatori e rosa del partecipante.
6. I crediti residui non possono diventare negativi. Se un'operazione produrrebbe saldo negativo, segnalarla e non registrarla finché l'utente non corregge o conferma una regola diversa.
7. Lo stesso giocatore non può essere assegnato due volte. Se compare già nel registro, fermare la registrazione e segnalare il conflitto.
8. In caso di nome ambiguo o dato incompleto, non indovinare. Conservare lo stato esistente e chiedere/attendere il dato mancante.
9. I file sotto `ASTA/` rappresentano lo stato ufficiale dell'asta. Prima di rispondere su budget, rose o acquisti, leggere lo stato corrente.
10. I file di ruolo presenti nella root del repository possono essere usati come riferimento, ma non prevalgono mai sul registro ufficiale dell'asta.
11. **REGOLA LIVE OBBLIGATORIA:** dopo OGNI acquisto valido, correzione o annullamento, la risposta all'utente DEVE includere immediatamente la tabella completa e aggiornata dei crediti di TUTTE le squadre. Non è sufficiente confermare l'operazione.
12. La tabella live deve essere prodotta usando i dati appena persistiti nei file dell'asta, non affidandosi soltanto alla memoria della conversazione.

## Formato rapido dei comandi dell'utente
L'utente può comunicare un acquisto in linguaggio naturale o in forma sintetica, ad esempio:
`Lautaro, Boston, 135`
`Lautaro a Boston per 135`
`Boston prende Lautaro 135`
`Lautaro 135 Boston`

I tre dati essenziali sono: **giocatore, squadra/partecipante, prezzo**. Se uno manca o è ambiguo, non registrare e chiedere soltanto il dato necessario.

## Procedura obbligatoria per ogni acquisto
1. Leggere lo stato corrente dell'asta.
2. Verificare che squadra/partecipante esista in `PARTECIPANTI.md`.
3. Verificare che il giocatore non sia già in `REGISTRO_ASTA.csv`.
4. Verificare che il prezzo sia un intero positivo.
5. Calcolare il nuovo saldo e verificare che non sia negativo.
6. Aggiungere l'acquisto a `REGISTRO_ASTA.csv`.
7. Aggiornare `ROSE.md`.
8. Aggiornare `PARTECIPANTI.md`.
9. Ricontrollare per ogni squadra: `1000 - crediti_spesi = crediti_residui`.
10. Solo dopo la persistenza dei dati, rispondere mostrando la tabella live completa.

## OUTPUT LIVE OBBLIGATORIO
Dopo ogni operazione valida mostrare SEMPRE, nello stesso messaggio:

**Operazione registrata:** `Giocatore → Squadra | X crediti`

| Squadra | Spesi | 💰 Disponibili | Giocatori |
|---|---:|---:|---:|
| tutte le squadre | valore aggiornato | valore aggiornato | valore aggiornato |

La tabella deve includere **tutte le 8 squadre**, anche quelle non coinvolte nell'ultimo acquisto. I crediti disponibili sono `1000 - totale speso`. Evidenziare chiaramente il saldo disponibile. Mantenere l'ordine ufficiale di `PARTECIPANTI.md`, salvo richiesta diversa.

Subito sotto, mostrare una riga compatta con gli ultimi acquisti utili alla verifica. Non sostituire mai la tabella completa con una risposta tipo «registrato» o con il solo saldo della squadra coinvolta.

## Correzioni e annullamenti
Per una correzione, modificare l'acquisto interessato nel registro e ricalcolare da zero i totali sulla base del registro completo. Per un annullamento, eliminare la relativa registrazione e ricalcolare completamente lo stato. In entrambi i casi aggiornare `PARTECIPANTI.md` e `ROSE.md` e mostrare nuovamente la **tabella live completa di tutte le squadre**.

## Fonte di verità
`REGISTRO_ASTA.csv` è la **fonte primaria di verità**. Se esiste una discrepanza tra file, ricostruire rose, spese e saldi dal registro e riallineare gli altri file prima di proseguire.

## Persistenza tra chat
Una nuova chat/agente deve, prima di gestire l'asta:
1. leggere `ASTA/ISTRUZIONI_AI.md`;
2. leggere `ASTA/PARTECIPANTI.md`;
3. leggere `ASTA/REGISTRO_ASTA.csv`;
4. leggere `ASTA/ROSE.md`;
5. verificare matematicamente i saldi;
6. applicare il workflow live definito sopra.

Non affidarsi alla memoria di chat precedenti quando i file sono disponibili.

## Stato iniziale ufficiale
L'asta è composta da **8 squadre**, ciascuna con **1000 crediti iniziali**. I nomi ufficiali sono quelli contenuti in `PARTECIPANTI.md`.
