# Data Sketch - Create Ticket

## Prima Di Compilare

Un data sketch e' una classificazione dei campi prima dello schema definitivo.

Serve a decidere quali dati sono accettati, generati, respinti o ancora mancanti.

Il Mermaid finale visualizza solo campi e relazioni gia' motivati nella tabella.

Non usare questo file per progettare tutto il database o accettare campi non collegati a issue e contract.

## Come Scegliere Lo Stato Del Campo

| Stato     | Usalo quando                                      | Domanda di controllo      |
| --------- | ------------------------------------------------- | ------------------------- |
| accettato | il campo arriva dall'input e serve al primo slice | chi lo inserisce?         |
| generato  | il sistema crea il valore                         | quando viene creato?      |
| respinto  | il campo e' fuori scope o non motivato            | quale vincolo lo esclude? |
| mancante  | il campo potrebbe servire, ma manca una decisione | chi deve chiarirlo?       |

Se non sai motivare un campo, non metterlo nel Mermaid: lascialo `mancante` o `respinto`.

## Scopo

Classificare i dati prima di chiedere codice.

## Campi

| Campo         | Stato     | Motivo                                                                                                         | Fonte                                    |
| ------------- | --------- | -------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| `title`       | accettato | [senza il title è difficile capire il problema]                                                                | contract                                 |
| `description` | accettato | [senza la descrpiton è difficile capire il problema']                                                          | contract                                 |
| `priority`    | accettato | [senza il priority non posso sapere l'urgenza del ticket]                                                      | contract                                 |
| `area`        | mancante  | [perche']                                                                                                      | issue / contract / decisione / inferenza |
| `status`      | generato  | [se tutti i campi sono completati, come risposta avro uno status "created"]                                    | contract                                 |
| `id`          | generato  | [se tutti i campi sono compilati, l'id verrà creato automaticamente come risposta di creazione ticket success] | contract                                 |
| `attachments` | optional  | [avere un documento o uno screenshot del problema può essere più comodo e veloce per individuare il problema]  | issue / contract / decisione / inferenza |
| `owner`       | mancante  | [perche']                                                                                                      | issue / contract / decisione / inferenza |
| `createdAt`   | generato  | [Per individuare e avere un registro dei ticket creati, risposta ad un ticket creato con success]              | contract                                 |

## Mermaid Leggero

Usa Mermaid solo per visualizzare la relazione minima. Non trasformarlo in schema DB definitivo.

```mermaid
erDiagram
  SUPPORT_USER ||--o TICKET : creates

  TICKET {
    string ticketId
    string title
    string description
    attachments documents or photos
    string category
    string status
    string createdAt
  }
```

Campi mostrati nel diagramma:

- [campo] - [accettato/generato/respinto/mancante]
- [campo] - [accettato/generato/respinto/mancante]

## Campi Scartati O Rimandati

| Campo         | Decisione | Motivo                                                                    |
| ------------- | --------- | ------------------------------------------------------------------------- |
| [area]        | rimandato | [sarebbe comodo capire l'area del support, magari lo aggiungo più avanti] |
| [attachments] | rimandato | [potrei aggiungerlo in un secondo momento]                                |
| [owner]       | rimandato | [potrei aggiungere in un secondo momento questa opzione]                  |

## Domande Per L07

- [quale file potrebbe contenere questi dati?] -
- [quale naming andra' verificato nella repo?]
- [quale campo dipende da una decisione non presa?]
