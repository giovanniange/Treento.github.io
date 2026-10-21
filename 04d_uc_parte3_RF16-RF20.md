# 4. Descrizione testuale degli Use Case – Parte 3 (RF-16 … RF-20)

---

# RF-16 – Creazione di un intervento

## UC-55 – Creare un intervento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-16, RF-26

Use Case generale, specializzato da UC-56 e UC-57 e incluso in UC-36.

| | |
|---|---|
| **Obiettivo** | Registrare un nuovo lavoro su una zona o su specifici elementi. |
| **Precondizioni** | Il responsabile è autenticato; la zona è operativa. |
| **Postcondizioni** | L'intervento esiste nello stato «in attesa di assegnazione» con zona, eventuali elementi, tipo di lavoro, scadenza e richiedente; compare nella dashboard e nel calendario; l'operazione è registrata. |
| **Use Case inclusi** | Verificare interventi sovrapposti. |
| **Use Case estesi** | UC-80 Pianificare un intervento nel calendario; UC-62 Preparare una richiesta alla ditta. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Avvia la creazione di un intervento (da consiglio, manualmente o da emergenza). |
| 2 | Sistema | Mostra il modulo con zona, elementi coinvolti, tipo di lavoro, descrizione, scadenza prevista, segnalazioni collegate e costo stimato. |
| 3 | Responsabile | Compila o verifica i dati e conferma. |
| 4 | Sistema | Verifica i campi obbligatori e la presenza di interventi sovrapposti sulla stessa zona e nello stesso periodo. |
| 5 | Sistema | Salva l'intervento nello stato «in attesa di assegnazione», collega le segnalazioni, aggiorna calendario e dashboard e registra l'operazione. |
| 6 | Sistema | Chiede se preparare subito la richiesta alla ditta (UC-62). |

**Flussi alternativi**
- **A1 – Sovrapposizione rilevata.** Al passo 4, se esiste un intervento sovrapposto, il sistema lo mostra; il responsabile può confermare comunque, modificare il periodo o collegare le segnalazioni all'intervento esistente.

**Eccezioni**
- **E1 – Dati obbligatori mancanti.** Al passo 4 il sistema evidenzia i campi da completare e torna al passo 3.
- **E2 – Errore di salvataggio.** Al passo 5 il sistema mostra un messaggio di errore e non crea l'intervento.

---

## UC-56 – Creare un intervento manualmente
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-16

| | |
|---|---|
| **Obiettivo** | Avviare un lavoro non proposto dal sistema (es. segnalazione telefonica, decisione del responsabile, anomalia rilevata). |
| **Precondizioni** | Quelle di UC-55. |
| **Postcondizioni** | Quelle di UC-55; l'intervento è contrassegnato come creato manualmente (non da consiglio). |
| **Use Case inclusi** | Quelli di UC-55. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Nuovo intervento» dalla dashboard, dalla scheda zona, da una segnalazione o da un'anomalia. |
| 2 | Sistema | Mostra il modulo precompilando i dati disponibili dal punto di partenza (zona, elemento, segnalazione, anomalia). |
| 3 | Responsabile | Indica tipo di lavoro, descrizione, scadenza ed eventuale origine (es. segnalazione telefonica) e conferma. |
| 4 | Sistema | Prosegue come UC-55 dal passo 4. |

**Flussi alternativi**
- **A1 – Consiglio già presente.** Al passo 2, se per la zona esiste un consiglio attivo dello stesso tipo, il sistema lo segnala e propone di avviare i lavori da quel consiglio (UC-36).

**Eccezioni**
- Quelle di UC-55.

---

## UC-57 – Creare un intervento urgente da un'emergenza
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-16, RF-15

| | |
|---|---|
| **Obiettivo** | Intervenire tempestivamente su un'emergenza. |
| **Precondizioni** | Quelle di UC-55; è in gestione un'emergenza (UC-54). |
| **Postcondizioni** | Quelle di UC-55; l'intervento è contrassegnato come urgente, collegato all'emergenza e conteggiato tra gli interventi urgenti negli indicatori. |
| **Use Case inclusi** | Quelli di UC-55. |
| **Use Case estesi** | – (estende UC-54). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Nella gestione dell'emergenza seleziona «Crea intervento urgente». |
| 2 | Sistema | Precompila zona, elemento, posizione, descrizione e fotografie dalla segnalazione, propone il tipo di lavoro e una scadenza ravvicinata. |
| 3 | Responsabile | Verifica e conferma. |
| 4 | Sistema | Prosegue come UC-55 dal passo 4, contrassegnando l'intervento come urgente, e propone subito la preparazione della richiesta alla ditta. |

**Flussi alternativi**
- – 

**Eccezioni**
- Quelle di UC-55.

---

# RF-17 – Approvazione degli interventi

Nota: l'attivazione del passaggio di approvazione, le condizioni e il ruolo competente sono da definire con il Comune (CLAR-01). Gli Use Case seguenti descrivono il comportamento quando il passaggio è attivo.

## UC-58 – Sottoporre una richiesta ad approvazione
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-17, RF-23

| | |
|---|---|
| **Obiettivo** | Ottenere l'autorizzazione del dirigente per una richiesta che soddisfa le condizioni di approvazione. |
| **Precondizioni** | Il responsabile ha preparato una richiesta (UC-62) che soddisfa le condizioni configurate (es. spesa prevista oltre soglia). |
| **Postcondizioni** | L'intervento è «in attesa di approvazione»; la richiesta non può essere inviata; il dirigente ha ricevuto una notifica. |
| **Use Case inclusi** | Verificare le condizioni di approvazione. |
| **Use Case estesi** | – (estende UC-62). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Al termine della preparazione della richiesta verifica le condizioni di approvazione configurate. |
| 2 | Sistema | Informa il responsabile che la richiesta richiede l'approvazione del dirigente e ne mostra il motivo. |
| 3 | Responsabile | Aggiunge eventuali note per il dirigente e seleziona «Invia in approvazione». |
| 4 | Sistema | Porta l'intervento nello stato «in attesa di approvazione», notifica il dirigente (UC-83) e registra l'operazione. |

**Flussi alternativi**
- **A1 – Richiesta modificata dopo il rifiuto.** Se la richiesta era stata respinta (UC-61), il responsabile la modifica e la sottopone di nuovo; il sistema conserva la cronologia delle versioni.

**Eccezioni**
- **E1 – Nessun dirigente attivo.** Al passo 4, se non esiste un dirigente con account attivo, il sistema lo segnala e avvisa l'amministratore.

---

## UC-59 – Consultare le richieste in attesa di approvazione
**Attore principale:** Dirigente · **Attori secondari:** – · **RF collegati:** RF-17

| | |
|---|---|
| **Obiettivo** | Sapere quali richieste attendono la propria approvazione. |
| **Precondizioni** | Il dirigente è autenticato. |
| **Postcondizioni** | È visualizzato l'elenco delle richieste in attesa. |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-60 Approvare una richiesta; UC-61 Respingere una richiesta. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Dirigente | Accede alla sezione «Approvazioni» o apre la notifica ricevuta. |
| 2 | Sistema | Mostra le richieste in attesa con zona, tipo di lavoro, ditta, spesa prevista, data di invio in approvazione e motivo dell'approvazione. |
| 3 | Dirigente | Seleziona una richiesta. |
| 4 | Sistema | Mostra il testo completo della richiesta, l'intervento, il consiglio e le segnalazioni collegate, i documenti allegati e le note del responsabile. |

**Flussi alternativi**
- **A1 – Storico delle approvazioni.** Al passo 2 il dirigente visualizza anche le richieste già approvate o respinte.

**Eccezioni**
- **E1 – Nessuna richiesta in attesa.** Al passo 2 il sistema mostra un messaggio informativo.

---

## UC-60 – Approvare una richiesta di intervento
**Attore principale:** Dirigente · **Attori secondari:** – · **RF collegati:** RF-17, RF-26

| | |
|---|---|
| **Obiettivo** | Autorizzare l'invio della richiesta alla ditta. |
| **Precondizioni** | Il dirigente sta consultando una richiesta in attesa di approvazione (UC-59). |
| **Postcondizioni** | La richiesta è approvata e può essere inviata; il dirigente risulta come approvatore dell'intervento; il responsabile è notificato; l'operazione è registrata. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Dirigente | Seleziona «Approva». |
| 2 | Sistema | Chiede conferma con una nota facoltativa. |
| 3 | Dirigente | Conferma. |
| 4 | Sistema | Registra l'approvazione con autore e data, rende la richiesta inviabile e notifica il responsabile. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Richiesta modificata nel frattempo.** Al passo 4, se la richiesta è stata modificata dopo l'invio in approvazione, il sistema lo segnala e mostra la versione aggiornata.

---

## UC-61 – Respingere una richiesta di intervento
**Attore principale:** Dirigente · **Attori secondari:** – · **RF collegati:** RF-17, RF-26

| | |
|---|---|
| **Obiettivo** | Bloccare l'invio di una richiesta indicando il motivo. |
| **Precondizioni** | Il dirigente sta consultando una richiesta in attesa di approvazione (UC-59). |
| **Postcondizioni** | La richiesta è respinta e non può essere inviata; l'intervento torna «in attesa di assegnazione»; il responsabile è notificato con la motivazione; l'operazione è registrata. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Dirigente | Seleziona «Respingi». |
| 2 | Sistema | Chiede la motivazione. |
| 3 | Dirigente | Inserisce la motivazione e conferma. |
| 4 | Sistema | Registra il rifiuto, riporta l'intervento allo stato «in attesa di assegnazione» e notifica il responsabile. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Motivazione mancante.** Al passo 3 il sistema richiede la motivazione e non procede.

---

# RF-18 – Preparazione e invio della richiesta alla ditta

## UC-62 – Preparare una richiesta alla ditta
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-18, RF-17

| | |
|---|---|
| **Obiettivo** | Ottenere una richiesta completa e conforme al modello del Comune, pronta per l'invio. |
| **Precondizioni** | Il responsabile è autenticato; esiste un intervento «in attesa di assegnazione». |
| **Postcondizioni** | La richiesta è salvata come pronta per l'invio oppure, se soggetta ad approvazione, è stata sottoposta al dirigente. |
| **Use Case inclusi** | UC-63 Selezionare la ditta; UC-64 Compilare la richiesta con il supporto del sistema; Verificare la completezza della richiesta. |
| **Use Case estesi** | UC-58 Sottoporre una richiesta ad approvazione; UC-65 Inviare la richiesta alla ditta. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Dall'intervento seleziona «Prepara richiesta». |
| 2 | Sistema | Avvia la selezione della ditta (UC-63). |
| 3 | Sistema | Precompila la richiesta con il modello della tipologia di lavoro (UC-64). |
| 4 | Responsabile | Verifica e modifica la richiesta, allega i documenti richiesti dal modello e seleziona «Salva». |
| 5 | Sistema | Verifica che i campi obbligatori siano compilati e che siano allegati i documenti previsti. |
| 6 | Sistema | Verifica le condizioni di approvazione. |
| 7 | Sistema | Salva la richiesta come pronta per l'invio e propone di inviarla (UC-65). |

**Flussi alternativi**
- **A1 – Approvazione necessaria.** Al passo 6, se le condizioni di approvazione sono soddisfatte, si avvia UC-58.
- **A2 – Salvataggio in bozza.** Al passo 4 il responsabile salva la richiesta incompleta come bozza; il sistema non esegue le verifiche e la richiesta resta modificabile.

**Eccezioni**
- **E1 – Richiesta incompleta.** Al passo 5 il sistema indica i campi e i documenti mancanti e torna al passo 4.
- **E2 – Modello non configurato.** Al passo 3, se per la tipologia di lavoro non esiste un modello, il sistema usa il modello generico e avvisa l'amministratore.

---

## UC-63 – Selezionare la ditta
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-18, RF-25

| | |
|---|---|
| **Obiettivo** | Scegliere una ditta competente per il lavoro e, se presente, titolare del contratto attivo per la zona. |
| **Precondizioni** | È in corso la preparazione di una richiesta (UC-62). |
| **Postcondizioni** | La ditta e il contatto di riferimento sono associati alla richiesta. |
| **Use Case inclusi** | Filtrare le ditte per competenza e contratto. |
| **Use Case estesi** | Consultare il dettaglio di una ditta. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Mostra le ditte attive competenti per il tipo di lavoro, mettendo per prima quella con contratto o appalto attivo per la zona. |
| 2 | Sistema | Per ogni ditta mostra contatti, competenze, contratto e numero di interventi aperti. |
| 3 | Responsabile | Seleziona la ditta e il contatto. |
| 4 | Sistema | Associa la ditta alla richiesta. |

**Flussi alternativi**
- **A1 – Ditta diversa da quella del contratto.** Al passo 3, se il responsabile sceglie una ditta diversa da quella del contratto attivo per la zona, il sistema chiede una motivazione e la registra.

**Eccezioni**
- **E1 – Nessuna ditta competente.** Al passo 1, se nessuna ditta attiva è competente per il lavoro, il sistema lo segnala e suggerisce di contattare l'amministratore per aggiornare l'anagrafica.

---

## UC-64 – Compilare la richiesta con il supporto del sistema
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-18, RF-10

| | |
|---|---|
| **Obiettivo** | Ottenere rapidamente una descrizione completa dell'intervento, controllandone e correggendone il contenuto. |
| **Precondizioni** | È in corso la preparazione di una richiesta e la ditta è stata scelta (UC-63). |
| **Postcondizioni** | La richiesta contiene dati della zona, lavorazioni, scadenza, descrizione e riferimenti, verificati dal responsabile; il sistema conserva la proposta originaria e le modifiche. |
| **Use Case inclusi** | Applicare il modello di richiesta; Proporre lavorazioni e descrizione. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Applica il modello configurato per la tipologia di lavoro (campi obbligatori, documenti, passaggi). |
| 2 | Sistema | Inserisce dati della zona, elementi, lavori consigliati, scadenza proposta e riferimenti (contratto, intervento). |
| 3 | Sistema | Propone le lavorazioni principali e una descrizione dell'intervento sulla base delle segnalazioni e delle previsioni, indicando su quali dati si basa. |
| 4 | Responsabile | Controlla, modifica, aggiunge o elimina lavorazioni e testo. |
| 5 | Sistema | Aggiorna la richiesta e conserva sia la proposta sia la versione modificata. |

**Flussi alternativi**
- **A1 – Proposta rifiutata.** Al passo 4 il responsabile scarta la proposta del sistema e compila la descrizione manualmente.

**Eccezioni**
- **E1 – Proposta non disponibile.** Al passo 3, se il sistema non riesce a generare la proposta, lo segnala e lascia la richiesta con i soli dati del modello, compilabile manualmente.

---

## UC-65 – Inviare la richiesta alla ditta
**Attore principale:** Responsabile · **Attori secondari:** Posta elettronica istituzionale · **RF collegati:** RF-18, RF-19

| | |
|---|---|
| **Obiettivo** | Trasmettere alla ditta la richiesta confermata attraverso il canale ufficiale del Comune. |
| **Precondizioni** | La richiesta è pronta per l'invio; se soggetta ad approvazione, è stata approvata (UC-60). |
| **Postcondizioni** | La richiesta è inviata dalla casella istituzionale; l'intervento è nello stato «richiesta inviata» con data di invio; la richiesta è visibile nella corrispondenza dell'intervento; l'operazione è registrata. |
| **Use Case inclusi** | Verificare la completezza della richiesta; Verificare l'approvazione. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Invia» sulla richiesta pronta. |
| 2 | Sistema | Mostra l'anteprima dell'email con destinatario, oggetto con il riferimento dell'intervento, testo e allegati e chiede la conferma esplicita. |
| 3 | Responsabile | Conferma l'invio. |
| 4 | Sistema | Verifica completezza e, se necessaria, approvazione. |
| 5 | Sistema | Invia la richiesta tramite la posta elettronica istituzionale. |
| 6 | Posta elettronica istituzionale | Conferma l'avvenuto invio. |
| 7 | Sistema | Porta l'intervento nello stato «richiesta inviata», archivia il messaggio nella corrispondenza e registra l'operazione. |

**Flussi alternativi**
- **A1 – Invio annullato.** Al passo 3 il responsabile annulla; la richiesta resta pronta per l'invio.

**Eccezioni**
- **E1 – Approvazione mancante.** Al passo 4, se l'approvazione è necessaria ma non è stata concessa, il sistema blocca l'invio e lo segnala.
- **E2 – Invio non riuscito.** Al passo 6, se la posta non conferma l'invio, il sistema lo segnala, lascia l'intervento nello stato precedente e consente di riprovare.

---

# RF-19 – Corrispondenza e avanzamento dell'intervento

## UC-66 – Ricevere una risposta della ditta
**Attore principale:** Posta elettronica istituzionale · **Attori secondari:** – · **RF collegati:** RF-19, RF-23

| | |
|---|---|
| **Obiettivo** | Rendere disponibile nella scheda dell'intervento la risposta inviata da una ditta. |
| **Precondizioni** | Il collegamento con la casella istituzionale è configurato; è arrivata un'email da una ditta in anagrafica. |
| **Postcondizioni** | La risposta è collegata all'intervento corrispondente e visibile nella corrispondenza, oppure è in attesa di associazione manuale; il responsabile è notificato. |
| **Use Case inclusi** | Riconoscere l'intervento di riferimento. |
| **Use Case estesi** | UC-68 Associare manualmente una risposta a un intervento. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Posta elettronica istituzionale | Rende disponibile al sistema un nuovo messaggio ricevuto da una ditta. |
| 2 | Sistema | Riconosce l'intervento di riferimento (riferimento nell'oggetto, mittente, conversazione). |
| 3 | Sistema | Collega il messaggio e gli allegati all'intervento. |
| 4 | Sistema | Notifica il responsabile della risposta ricevuta (UC-83), suggerendo l'eventuale aggiornamento di stato (es. «accettato dalla ditta»). |

**Flussi alternativi**
- **A1 – Intervento non riconosciuto.** Al passo 2, se l'intervento non può essere individuato con certezza, il sistema pone il messaggio tra le risposte da associare e notifica il responsabile (UC-68).

**Eccezioni**
- **E1 – Mittente sconosciuto.** Al passo 1, se il mittente non appartiene a nessuna ditta in anagrafica, il messaggio non viene acquisito dal sistema e resta nella casella istituzionale.
- **E2 – Casella non raggiungibile.** Il sistema registra l'errore, ritenta e, se persiste, avvisa l'amministratore.

---

## UC-67 – Consultare la corrispondenza di un intervento
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-19

| | |
|---|---|
| **Obiettivo** | Leggere in un unico punto tutte le comunicazioni relative a un lavoro. |
| **Precondizioni** | È visualizzato il dettaglio di un intervento (UC-41). |
| **Postcondizioni** | È visualizzata la corrispondenza dell'intervento. |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-70 Sollecitare una ditta (solo Responsabile). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Seleziona la scheda «Corrispondenza» dell'intervento. |
| 2 | Sistema | Mostra in ordine cronologico richieste, solleciti e risposte con data, mittente, destinatario, testo e allegati. |
| 3 | Utente | Apre un messaggio o un allegato. |

**Flussi alternativi**
- **A1 – Nessuna comunicazione.** Al passo 2 il sistema indica che non sono ancora presenti comunicazioni.

**Eccezioni**
- **E1 – Allegato non disponibile.** Al passo 3 il sistema lo segnala.

---

## UC-68 – Associare manualmente una risposta a un intervento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-19

| | |
|---|---|
| **Obiettivo** | Collegare all'intervento corretto una risposta che il sistema non ha riconosciuto. |
| **Precondizioni** | Il responsabile è autenticato; esiste almeno una risposta da associare. |
| **Postcondizioni** | La risposta è collegata all'intervento scelto ed è visibile nella sua corrispondenza; l'operazione è registrata. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-66). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Apre l'elenco «Risposte da associare». |
| 2 | Sistema | Mostra le risposte con mittente, data, oggetto e gli interventi aperti più probabili per quella ditta. |
| 3 | Responsabile | Seleziona una risposta e l'intervento corretto. |
| 4 | Sistema | Collega la risposta all'intervento e registra l'operazione. |

**Flussi alternativi**
- **A1 – Risposta non pertinente.** Al passo 3 il responsabile indica che la risposta non riguarda alcun intervento; il sistema la archivia fra i messaggi non pertinenti.

**Eccezioni**
- – 

---

## UC-69 – Aggiornare lo stato di un intervento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-19, RF-20

| | |
|---|---|
| **Obiettivo** | Registrare l'avanzamento comunicato dalla ditta (accettazione, inizio, conclusione). |
| **Precondizioni** | Il responsabile è autenticato; l'intervento è almeno nello stato «richiesta inviata». |
| **Postcondizioni** | L'intervento è nel nuovo stato con data e riferimento alla comunicazione; dashboard e calendario sono aggiornati; se concluso, l'intervento è «concluso in attesa di verifica». |
| **Use Case inclusi** | Verificare la transizione di stato. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Nel dettaglio dell'intervento seleziona «Aggiorna stato». |
| 2 | Sistema | Mostra gli stati successivi ammessi (richiesta inviata → accettato dalla ditta → in corso → concluso in attesa di verifica). |
| 3 | Responsabile | Seleziona il nuovo stato, indica la data ed eventualmente collega la comunicazione della ditta. |
| 4 | Sistema | Verifica che la transizione sia ammessa, aggiorna lo stato e registra l'operazione. |
| 5 | Sistema | Se il nuovo stato è «concluso in attesa di verifica», mantiene la zona nello stato precedente con l'indicatore di verifica in corso e notifica il responsabile della verifica da eseguire. |

**Flussi alternativi**
- **A1 – Rifiuto della ditta.** Al passo 3, se la ditta ha rifiutato la richiesta, il responsabile lo indica; l'intervento torna «in attesa di assegnazione» per la scelta di un'altra ditta.
- **A2 – Aggiornamento di date e costi.** Al passo 3 il responsabile aggiorna anche le date effettive di inizio e fine e il costo preventivato comunicato dalla ditta.

**Eccezioni**
- **E1 – Transizione non ammessa.** Al passo 4, se lo stato scelto non è ammesso dallo stato corrente, il sistema lo segnala e non aggiorna l'intervento.

---

## UC-70 – Sollecitare una ditta
**Attore principale:** Responsabile · **Attori secondari:** Posta elettronica istituzionale · **RF collegati:** RF-19, RF-20

| | |
|---|---|
| **Obiettivo** | Sollecitare la ditta per un lavoro in ritardo o per le correzioni richieste dopo una verifica negativa. |
| **Precondizioni** | Il responsabile è autenticato; l'intervento è in ritardo, senza risposta oppure respinto in verifica. |
| **Postcondizioni** | Il sollecito è inviato e archiviato nella corrispondenza dell'intervento; l'operazione è registrata. |
| **Use Case inclusi** | Precompilare il sollecito. |
| **Use Case estesi** | – (estende UC-67 e UC-75). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Sollecita» su un intervento (dalla dashboard, dalla corrispondenza o dopo una verifica negativa). |
| 2 | Sistema | Precompila il sollecito con riferimento all'intervento, scadenza superata o correzioni richieste. |
| 3 | Responsabile | Modifica il testo se necessario e conferma l'invio. |
| 4 | Sistema | Invia il sollecito tramite la posta elettronica istituzionale. |
| 5 | Sistema | Archivia il sollecito nella corrispondenza, registra l'operazione e aggiorna il numero di solleciti dell'intervento. |

**Flussi alternativi**
- **A1 – Nuova scadenza.** Al passo 3 il responsabile indica una nuova scadenza concordata; il sistema la aggiorna conservando quella originaria.

**Eccezioni**
- **E1 – Invio non riuscito.** Al passo 4 il sistema lo segnala e consente di riprovare.

---

# RF-20 – Verifica di fine lavori

## UC-71 – Consultare gli interventi in attesa di verifica
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-20

| | |
|---|---|
| **Obiettivo** | Sapere quali lavori conclusi devono essere verificati. |
| **Precondizioni** | Il responsabile è autenticato. |
| **Postcondizioni** | È visualizzato l'elenco degli interventi «concluso in attesa di verifica». |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-72 Registrare l'esito della verifica. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Accede alla sezione «Verifiche» o apre la notifica di lavoro concluso. |
| 2 | Sistema | Mostra gli interventi in attesa di verifica con zona, tipo, ditta, data di conclusione e giorni di attesa. |
| 3 | Responsabile | Seleziona un intervento. |
| 4 | Sistema | Mostra il dettaglio dell'intervento con le comunicazioni della ditta e le eventuali foto inviate. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Nessuna verifica in attesa.** Al passo 2 il sistema mostra un messaggio informativo.

---

## UC-72 – Registrare l'esito della verifica
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-20, RF-26

Use Case generale, specializzato da UC-73, UC-74 e UC-75. La verifica sul posto può essere eseguita dal responsabile o da un tecnico incaricato; l'esito è sempre registrato dal responsabile.

| | |
|---|---|
| **Obiettivo** | Documentare l'esito del controllo dei lavori conclusi. |
| **Precondizioni** | Il responsabile è autenticato; l'intervento è «concluso in attesa di verifica». |
| **Postcondizioni** | L'esito della verifica è registrato con data, autore, esecutore del sopralluogo, fotografie e note; l'intervento e la zona sono aggiornati secondo l'esito. |
| **Use Case inclusi** | UC-43 Allegare documenti e fotografie; Registrare l'esito. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Registra verifica» sull'intervento. |
| 2 | Sistema | Mostra il modulo con data del sopralluogo, esecutore (responsabile o tecnico incaricato), esito, note e caricamento delle fotografie. |
| 3 | Responsabile | Compila il modulo, allega le fotografie scattate in loco e sceglie l'esito (vedi UC-73, UC-74, UC-75). |
| 4 | Sistema | Verifica i dati obbligatori e registra la verifica. |

**Flussi alternativi**
- **A1 – Verifica senza fotografie.** Al passo 3, se non vengono allegate fotografie, il sistema chiede conferma e una nota esplicativa.

**Eccezioni**
- **E1 – Dati mancanti.** Al passo 4 il sistema indica i dati mancanti e torna al passo 3.
- **E2 – Errore di salvataggio.** Al passo 4 il sistema mostra un messaggio di errore; l'intervento resta in attesa di verifica.

---

## UC-73 – Approvare i lavori
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-20, RF-09, RF-12

| | |
|---|---|
| **Obiettivo** | Chiudere un intervento eseguito correttamente e aggiornare lo stato reale della zona. |
| **Precondizioni** | Quelle di UC-72. |
| **Postcondizioni** | L'intervento è «verificato» e chiuso, inserito nello storico; la data di fine lavori è il nuovo riferimento per la frequenza di manutenzione; lo stato della zona è ricalcolato; le segnalazioni collegate sono proposte per la chiusura; l'eventuale emergenza collegata è chiusa. |
| **Use Case inclusi** | Quelli di UC-72; UC-30 Aggiornare lo stato delle zone. |
| **Use Case estesi** | UC-53 Chiudere una segnalazione. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Nel modulo di verifica sceglie l'esito «Approvato». |
| 2 | Sistema | Chiede conferma della data di fine lavori e del costo finale. |
| 3 | Responsabile | Conferma o corregge data e costo. |
| 4 | Sistema | Porta l'intervento a «verificato», lo chiude e lo inserisce nello storico. |
| 5 | Sistema | Aggiorna il riferimento per la frequenza di manutenzione, ricalcola lo stato della zona (UC-30) e rimuove l'indicatore di verifica in corso. |
| 6 | Sistema | Propone la chiusura delle segnalazioni collegate (UC-53) e chiude l'eventuale emergenza collegata. |

**Flussi alternativi**
- – 

**Eccezioni**
- Quelle di UC-72.

---

## UC-74 – Approvare i lavori con riserva
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-20

| | |
|---|---|
| **Obiettivo** | Chiudere un intervento sostanzialmente eseguito, annotando le carenze non bloccanti. |
| **Precondizioni** | Quelle di UC-72. |
| **Postcondizioni** | Quelle di UC-73; l'intervento riporta la riserva, visibile nello storico e nel dettaglio. |
| **Use Case inclusi** | Quelli di UC-73. |
| **Use Case estesi** | UC-56 Creare un intervento manualmente (per le carenze). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Nel modulo di verifica sceglie l'esito «Approvato con riserva». |
| 2 | Sistema | Richiede la descrizione della riserva. |
| 3 | Responsabile | Descrive la riserva e conferma. |
| 4 | Sistema | Prosegue come UC-73 dal passo 2, registrando la riserva. |

**Flussi alternativi**
- **A1 – Intervento integrativo.** Al termine il responsabile sceglie di creare un intervento per le carenze rilevate (UC-56).

**Eccezioni**
- **E1 – Riserva non descritta.** Al passo 3 il sistema richiede la descrizione e non procede.

---

## UC-75 – Respingere i lavori
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-20, RF-19

| | |
|---|---|
| **Obiettivo** | Riaprire un intervento non eseguito correttamente e richiedere le correzioni alla ditta. |
| **Precondizioni** | Quelle di UC-72. |
| **Postcondizioni** | L'intervento torna «in corso» con l'esito negativo e le correzioni richieste registrati; la zona mantiene lo stato precedente; la ditta può essere sollecitata. |
| **Use Case inclusi** | Quelli di UC-72. |
| **Use Case estesi** | UC-70 Sollecitare una ditta. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Nel modulo di verifica sceglie l'esito «Respinto». |
| 2 | Sistema | Richiede la descrizione delle correzioni da eseguire e una nuova scadenza. |
| 3 | Responsabile | Descrive le correzioni, indica la scadenza e conferma. |
| 4 | Sistema | Registra l'esito, riporta l'intervento allo stato «in corso» e mantiene la zona nello stato precedente. |
| 5 | Sistema | Propone di inviare subito un sollecito alla ditta con le correzioni richieste (UC-70). |

**Flussi alternativi**
- **A1 – Sollecito rimandato.** Al passo 5 il responsabile rinvia il sollecito; l'intervento compare in dashboard come «correzioni richieste».

**Eccezioni**
- **E1 – Correzioni non descritte.** Al passo 3 il sistema richiede la descrizione e non procede.
