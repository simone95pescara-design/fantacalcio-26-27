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

## Formato rapido dei comandi dell'utente
L'utente può comunicare un acquisto in linguaggio naturale oppure in forma sintetica, per esempio:

`Lautaro, Simone, 135`

Interpretazione:
- Giocatore: Lautaro
- Partecipante/squadra: Simone
- Prezzo: 135 crediti

Sono validi anche messaggi come:
- `Lautaro a Simone per 135`
- `Simone prende Lautaro 135`
- `Lautaro 135 Simone`

Registrare l'operazione solo quando i tre campi essenziali — giocatore, partecipante, prezzo — sono identificabili con sufficiente certezza.

## Procedura per ogni acquisto
Prima della registrazione:
1. Verificare che il partecipante esista in `PARTECIPANTI.md`.
2. Verificare che il giocatore non sia già presente in `REGISTRO_ASTA.csv`.
3. Verificare che il prezzo sia un numero intero positivo.
4. Calcolare `nuovo_residuo = residuo_attuale - prezzo`.
5. Verificare che il nuovo residuo sia >= 0.

Se i controlli passano:
1. Aggiungere una riga a `REGISTRO_ASTA.csv`.
2. Aggiornare la rosa in `ROSE.md`.
3. Aggiornare spesi/residui/numero giocatori in `PARTECIPANTI.md`.
4. Ricontrollare matematicamente che per ogni partecipante valga:
   `crediti_iniziali - crediti_spesi = crediti_residui`.
5. Mostrare all'utente la situazione aggiornata.

## Output da mostrare dopo ogni acquisto
Mostrare in modo compatto:

### Operazione registrata
`Giocatore → Squadra | prezzo X`

### Situazione crediti
Tabella con almeno:
- Squadra/Partecipante
- Crediti iniziali
- Spesi
- Residui
- N. giocatori

### Ultimi acquisti
Mostrare almeno gli ultimi acquisti utili a verificare che l'operazione sia stata inserita correttamente.

Su richiesta mostrare anche la rosa completa di una o di tutte le squadre.

## Correzioni
Se l'utente dice, per esempio, `correggi Lautaro: 125 e non 135`:
1. Trovare l'acquisto originale.
2. Modificare il prezzo nel registro.
3. Ricalcolare da zero i totali del partecipante sulla base del registro completo, evitando correzioni aritmetiche cumulative che possano introdurre errori.
4. Aggiornare `PARTECIPANTI.md` e `ROSE.md`.
5. Mostrare il risultato corretto.

Se l'utente annulla un acquisto, eliminare la relativa riga dal registro e ricalcolare completamente lo stato della squadra interessata.

## Fonte di verità e ricostruzione
`REGISTRO_ASTA.csv` è la **fonte primaria di verità** per tutti gli acquisti effettuati.

Se esiste una discrepanza tra file:
1. ricostruire spese e rose partendo da `REGISTRO_ASTA.csv`;
2. aggiornare gli altri file per riallinearli;
3. segnalare brevemente la correzione all'utente.

## Classifica operativa
La "classifica" dell'asta non è una classifica sportiva: è il riepilogo gestionale delle squadre. Per impostazione predefinita ordinarla secondo l'ordine dei partecipanti in `PARTECIPANTI.md`, non in base ai crediti residui, salvo richiesta diversa.

## Persistenza tra chat
Una nuova chat o un nuovo agente che interviene sull'asta deve:
1. leggere `ASTA/ISTRUZIONI_AI.md`;
2. leggere `ASTA/PARTECIPANTI.md`;
3. leggere `ASTA/REGISTRO_ASTA.csv`;
4. leggere `ASTA/ROSE.md`;
5. ricostruire mentalmente/verificare i saldi prima di effettuare nuove registrazioni.

Non affidarsi alla memoria di una chat precedente quando i file sono disponibili.

## Stato iniziale
Budget standard per ogni partecipante: **1000 crediti**.
I partecipanti verranno inseriti quando comunicati dall'utente.
