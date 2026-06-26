# Contratto Iniziale (Contract Sketch) - Create Ticket

## Prima Di Compilare

Un contratto iniziale (contract sketch) e' una descrizione leggera di input, output e risposte attese.

Serve a rendere verificabile `create ticket` prima di chiedere codice all'AI.

Compila solo la superficie minima:

- cosa entra;
- cosa esce;
- cosa viene rifiutato;
- quale errore ti aspetti.

Non trasformarlo in una specifica API completa, uno schema di un database o un piano di una patch.

Quando compili, ogni esempio deve rispondere (almeno) a tre domande:

- perche' questo input e' valido o invalido?
- quale risposta mi aspetto?
- quale parte della issue o del fuori scope giustifica la scelta?

## Request

```txt
Serve creare ticket dal supporto.
```

## Boundary Map

| Superficie   | Cosa riguarda                                                                                    | Nota               |
| ------------ | ------------------------------------------------------------------------------------------------ | ------------------ |
| UI           | [cosa inserisce o vede l'utente - vede un form - raccoglie l'input]                              | [nota]             |
| API / azione | [input e output attesi - riceve la richiesta di creazione ticket e risponde con success o error] | [auth - permessi]  |
| Dati         | [campi conservati o generati - definisce i campi minimi per creare un ticket ]                   | [schema data base] |
| Verifica     | [usa payload valido e invalido]                                                                  | [test automatico]  |

## Action

Per questo slice, `create ticket` significa:

```txt
[scrivi una decisione minima e verificabile]
```

## Payload Valido

```json
{
    title: String , Required
    description: String , Required
    category: String , Required
    attachments: document or photos, optional
}

{
    "title": "Problema accesso area cliente",
    "description": "Il cliente segnala che non riesce ad accedere alla propria area personale",
    "category": "support"
}
```

Perche' e' valido:

- [Perche Avere un titolo, description o category mi permette di individuare il perchè? del ticket e il livello d'importanza.
  Senza quello sarebbe un ticket molto vago].

## Risposta Attesa Di Successo

```txt
[status o risultato atteso]
```

Campi attesi:

- [campo generato o restituito]
- [campo confermato]

```json
{
  "ticketId": "ticket_1",
  "status": "created",
  "createdAt": "25/06/2026-22:45"
}
```

## Payload Invalido 1

```json
{
  "description": "Il cliente segnala che non riesce ad accedere alla propria area personale",
  "category": "support"
}
```

Motivo del rifiuto:

```txt
[perche' e' invalido - Mancaza del titolo, anche se posso intuire che sia un problema per accedere all'area personale. Sicuramente con il title posso individuare sin da subito il problema.]
```

Risposta attesa:

```txt
[status o errore atteso ]
```

```json
{
  "error": "validation-error, incomplete-fields",
  "fields": "title"
}
```

## Payload Invalido 2

```json
{
  "title": "Problema accesso area cliente",
  "description": "",
  "category": "support"
}
```

Motivo del rifiuto:

```txt
[perche' e' invalido - Perche non basta sapere il titolo de ticket per avere un quadro generale del problema]
```

Risposta attesa:

```txt
[status o errore atteso]
```

```json
{
  "error": "validation-error, incomplete-fields",
  "fields": "description"
}
```

## Error Model Minimo

| Caso                             | Motivo                           | Risposta attesa                                |
| -------------------------------- | -------------------------------- | ---------------------------------------------- |
| Campo richiesto mancante o vuoto | [avere tutti i campi completati] | [errore - validation-error, incomplete fields] |
| Valore fuori contratto           | [motivo]                         | [errore]                                       |

## Non-Goals Confermati

- [cosa resta fuori scope] - tante cose
- [cosa non chiedere all'AI] - che scriva codice
- [cosa rimandare] - il layout?
