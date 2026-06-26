# Issue: Create ticket with validation

## Request

```txt
Serve creare ticket dal supporto.
```

## Fatti (Facts)

- Il component per gestire / creare / modificare il ticket esiste.
- La richiesta è: permettere al supporto di creare ticket.

## Assunzioni (Assumptions)

- Il flusso di creazione userà il component ticket già esistente.
- Esiste un set minimo di campi obbligatori per creare un ticket, ma va confermato.
- La validazione minima deve impedire l’invio di dati mancanti o non validi.
- Dopo il tentativo di creazione, l’utente deve vedere un esito osservabile.

## Domande Aperte (Questions)

- Quali sono i campi obbligatori minimi per creare un ticket?
- Esiste già un endpoint/API o una funzione esistente per creare il ticket?
- Dopo la creazione, quale esito deve vedere l’utente: messaggio di successo, ticket in lista, oppure apertura del dettaglio?
- Gli errori di creazione lato server devono essere gestiti in questo slice o rimandati a L06?

## Decisione (Decision)

Per questo slice, "creare ticket" significa:

```txt
Dal contesto supporto, l’utente può usare il component ticket esistente per compilare i campi minimi richiesti, inviare solo dati validi e vedere un esito osservabile dopo la creazione.
```

## Fuori Scope / Non-Obiettivi (Non-Goals)

- Non creiamo un nuovo component ticket da zero.
- Non implementiamo modifica, cancellazione o gestione completa del ciclo di vita del ticket.
- Non definiamo un contract tecnico completo, schema database o payload definitivo.
- Non aggiungiamo funzionalità come allegati, notifiche, dashboard, assegnazioni o priorità se non già previste dal flusso esistente.
- Non chiediamo all’AI di inventare campi business non confermati.

## Criteri Di Accettazione (Acceptance Criteria)

1. Dal contesto supporto è possibile avviare la creazione di un ticket usando il component esistente.
2. Se uno o più campi obbligatori sono mancanti o non validi, la creazione viene bloccata e l’utente vede errori chiari.
3. Con dati validi, il ticket viene creato e l’utente vede un esito di successo osservabile.
4. Se la creazione fallisce per un errore gestito nello slice, l’utente vede un messaggio di errore comprensibile.

## Piano Di Verifica Manuale (Manual Test Plan)

- Aprire il contesto supporto e avviare la creazione ticket: il form/component di creazione è accessibile.
- Provare a inviare il form lasciando vuoto almeno un campo obbligatorio: la submit viene bloccata e vengono mostrati errori sui campi.
- Compilare i campi obbligatori con dati validi e inviare: il ticket viene creato e viene mostrato un esito di successo osservabile.
- Se previsto nello slice, simulare un errore di creazione gestito: l’utente vede un messaggio di errore comprensibile.

## Note Per L06

- [quale payload andra' chiarito]
- [quale errore andra' chiarito]
- [quale campo dati andra' deciso]

- Chiarire il payload minimo richiesto per la creazione ticket.
- Chiarire quali errori API/backend devono essere gestiti e come mostrarli in UI.
- Decidere quali campi fanno parte del set minimo obbligatorio.
