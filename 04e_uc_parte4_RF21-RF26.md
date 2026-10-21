# 4. Descrizione testuale degli Use Case – Parte 4 (RF-21 … RF-26)

---

# RF-21 – Dashboard lavori e indicatori

## UC-76 – Consultare la dashboard lavori
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-21, RF-19

| | |
|---|---|
| **Obiettivo** | Avere sotto controllo l'insieme dei lavori, in particolare quelli in ritardo. |
| **Precondizioni** | L'utente è autenticato come responsabile o dirigente. |
| **Postcondizioni** | È visualizzata la dashboard con l'elenco dei lavori e il loro stato. |
| **Use Case inclusi** | Individuare i lavori in ritardo. |
| **Use Case estesi** | Filtrare i lavori; UC-41 Consultare il dettaglio di un intervento; UC-70 Sollecitare una ditta (solo Responsabile). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Accede alla sezione «Dashboard lavori». |
| 2 | Sistema | Mostra l'elenco dei lavori con zona, tipo, ditta, date, costo e stato (in attesa di assegnazione, in attesa di approvazione, richiesta inviata, accettato, in corso, concluso in attesa di verifica, verificato). |
| 3 | Sistema | Mette in evidenza, in cima e con apposito simbolo, i lavori in ritardo rispetto alla scadenza. |
| 4 | Sistema | Mostra un riepilogo con il numero di lavori per stato. |
| 5 | Utente | Filtra per stato, zona, ditta o periodo, oppure seleziona un lavoro per aprirne il dettaglio. |

**Flussi alternativi**
- **A1 – Sollecito dal ritardo.** Al passo 5 il responsabile seleziona «Sollecita» su un lavoro in ritardo; si avvia UC-70.
- **A2 – Dirigente.** Per il dirigente i comandi operativi non sono mostrati; sono invece evidenziate le richieste in attesa della sua approvazione.

**Eccezioni**
- **E1 – Nessun lavoro.** Al passo 2 il sistema mostra un messaggio informativo.
- **E2 – Errore di caricamento.** Il sistema mostra un messaggio di errore.

---

## UC-77 – Consultare gli indicatori
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-21, RF-11

| | |
|---|---|
| **Obiettivo** | Disporre di dati affidabili per il controllo dell'attività e la rendicontazione. |
| **Precondizioni** | L'utente è autenticato come responsabile o dirigente. |
| **Postcondizioni** | Sono visualizzati gli indicatori calcolati sui dati del periodo predefinito. |
| **Use Case inclusi** | Calcolare gli indicatori. |
| **Use Case estesi** | UC-78 Filtrare gli indicatori; Esportare gli indicatori. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Nella dashboard seleziona la scheda «Indicatori». |
| 2 | Sistema | Calcola e mostra per il periodo predefinito: tempo medio di risposta alle segnalazioni (presa in carico e chiusura), tempo medio di risposta delle ditte, ditte più utilizzate con numero di interventi e spesa, distribuzione delle zone per stato. |
| 3 | Sistema | Mostra la spesa per periodo e per tipologia di lavoro, il numero di interventi programmati rispetto a quelli urgenti, il numero di interventi in ritardo e la percentuale di consigli accettati e giudicati utili. |
| 4 | Utente | Seleziona un indicatore per vederne il dettaglio e i dati da cui è calcolato. |

**Flussi alternativi**
- **A1 – Esportazione.** Al passo 4 l'utente esporta gli indicatori come documento di riepilogo.

**Eccezioni**
- **E1 – Dati insufficienti.** Al passo 2, se per un indicatore non ci sono dati nel periodo, il sistema mostra «dati non disponibili» per quell'indicatore.

---

## UC-78 – Filtrare gli indicatori
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-21

| | |
|---|---|
| **Obiettivo** | Analizzare gli indicatori per un periodo, una zona o una ditta. |
| **Precondizioni** | Sono visualizzati gli indicatori (UC-77). |
| **Postcondizioni** | Gli indicatori sono ricalcolati con i filtri scelti; i filtri attivi sono indicati. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-77). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Imposta periodo, zona e/o ditta. |
| 2 | Sistema | Ricalcola tutti gli indicatori con i filtri scelti e li mostra con l'indicazione dei filtri attivi. |

**Flussi alternativi**
- **A1 – Confronto tra periodi.** Al passo 1 l'utente sceglie un secondo periodo di confronto; il sistema mostra i due valori affiancati.

**Eccezioni**
- **E1 – Periodo non valido.** Al passo 1, se la data di inizio è successiva a quella di fine, il sistema lo segnala.

---

# RF-22 – Calendario della manutenzione

## UC-79 – Consultare il calendario della manutenzione
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-22

| | |
|---|---|
| **Obiettivo** | Vedere i lavori programmati e le attività stagionali ricorrenti di un periodo. |
| **Precondizioni** | L'utente è autenticato come responsabile o dirigente. |
| **Postcondizioni** | È visualizzato il calendario del periodo scelto. |
| **Use Case inclusi** | Generare le scadenze attese. |
| **Use Case estesi** | UC-81 Consultare le sovrapposizioni; UC-82 Consultare carico di lavoro e spesa prevista; Filtrare il calendario. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Accede alla sezione «Calendario». |
| 2 | Sistema | Mostra il mese corrente con gli interventi programmati e le scadenze attese generate da frequenze e finestre stagionali (sfalci, potature invernali, trattamenti, controlli, spegnimento e riattivazione delle fontane), distinti per tipo. |
| 3 | Utente | Cambia vista (settimana, mese, anno) o periodo, o filtra per zona e tipo di lavoro. |
| 4 | Sistema | Aggiorna il calendario. |
| 5 | Utente | Seleziona una voce. |
| 6 | Sistema | Mostra il dettaglio dell'intervento o della scadenza attesa, con la zona interessata. |

**Flussi alternativi**
- **A1 – Scadenza attesa non coperta.** Al passo 6, se la scadenza attesa non ha ancora un intervento, il responsabile può creare l'intervento (UC-56) o pianificarlo (UC-80).

**Eccezioni**
- **E1 – Errore di caricamento.** Il sistema mostra un messaggio di errore.

---

## UC-80 – Pianificare un intervento nel calendario
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-22, RF-16

| | |
|---|---|
| **Obiettivo** | Fissare il periodo di esecuzione di un intervento. |
| **Precondizioni** | Il responsabile è autenticato; esiste un intervento non concluso o una scadenza attesa. |
| **Postcondizioni** | L'intervento ha un periodo programmato visibile nel calendario; le eventuali sovrapposizioni sono state segnalate. |
| **Use Case inclusi** | Verificare interventi sovrapposti. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona un intervento o una scadenza attesa e sceglie «Pianifica». |
| 2 | Sistema | Mostra il calendario della zona con i lavori già previsti e la finestra stagionale consigliata. |
| 3 | Responsabile | Sceglie il periodo di esecuzione e conferma. |
| 4 | Sistema | Verifica le sovrapposizioni con altri interventi nella stessa zona e nello stesso periodo. |
| 5 | Sistema | Salva la pianificazione e aggiorna calendario e dashboard. |

**Flussi alternativi**
- **A1 – Da scadenza attesa.** Al passo 1, se si parte da una scadenza attesa senza intervento, il sistema crea prima l'intervento (UC-56).
- **A2 – Fuori finestra stagionale.** Al passo 3, se il periodo è fuori dalla finestra stagionale configurata, il sistema lo segnala e chiede conferma.

**Eccezioni**
- **E1 – Sovrapposizione.** Al passo 4 il sistema mostra l'intervento sovrapposto; il responsabile può scegliere un altro periodo o confermare.

---

## UC-81 – Consultare le sovrapposizioni
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-22

| | |
|---|---|
| **Obiettivo** | Individuare lavori in conflitto, ad esempio ditte diverse nella stessa zona nello stesso periodo. |
| **Precondizioni** | È visualizzato il calendario (UC-79). |
| **Postcondizioni** | Sono visualizzate le sovrapposizioni del periodo. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-79). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Attiva la vista «Sovrapposizioni». |
| 2 | Sistema | Evidenzia nel calendario gli interventi sovrapposti e ne mostra l'elenco con zona, periodo e ditte coinvolte. |
| 3 | Responsabile | Seleziona una sovrapposizione e, se necessario, ripianifica uno degli interventi (UC-80). |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Nessuna sovrapposizione.** Al passo 2 il sistema indica che nel periodo non ci sono sovrapposizioni.

---

## UC-82 – Consultare carico di lavoro e spesa prevista
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-22, RF-21

| | |
|---|---|
| **Obiettivo** | Valutare quanto lavoro e quanta spesa sono previsti in un periodo, anche per la pianificazione del budget. |
| **Precondizioni** | È visualizzato il calendario (UC-79). |
| **Postcondizioni** | Sono visualizzati numero di interventi e spesa prevista per il periodo. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-79). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Seleziona «Carico e spesa» per il periodo visualizzato. |
| 2 | Sistema | Mostra per ogni mese del periodo il numero di interventi programmati e di scadenze attese, suddivisi per tipo di lavoro, e la spesa prevista sulla base dei costi preventivati. |

**Flussi alternativi**
- **A1 – Costi non disponibili.** Al passo 2, per gli interventi senza costo preventivato, il sistema li conteggia separatamente come «costo non stimato».

**Eccezioni**
- – 

---

# RF-23 – Notifiche e scadenze

## UC-83 – Ricevere una notifica
**Attore principale:** Responsabile, Dirigente (beneficiari) · **Attori secondari:** Posta elettronica istituzionale · **RF collegati:** RF-23

La notifica è generata dal sistema al verificarsi di un evento; l'attore principale è chi la riceve.

| | |
|---|---|
| **Obiettivo** | Essere avvisato di ciò che richiede attenzione, distinguendo ciò che è urgente. |
| **Precondizioni** | Si è verificato un evento previsto: per il responsabile intervento prossimo alla scadenza o scaduto, zona passata al rosso, segnalazione di emergenza, risposta di una ditta, lavoro concluso in attesa di verifica, inizio di una finestra stagionale; per il dirigente approvazione in attesa o ritardo significativo. |
| **Postcondizioni** | La notifica è presente nel centro notifiche del destinatario con il livello di importanza; se ad alta priorità è stata evidenziata nell'applicazione e inviata per email. |
| **Use Case inclusi** | Determinare destinatari e livello di importanza. |
| **Use Case estesi** | Inviare la notifica per email. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Rileva un evento previsto. |
| 2 | Sistema | Determina i destinatari in base al ruolo e il livello di importanza secondo la configurazione. |
| 3 | Sistema | Crea la notifica con descrizione dell'evento e collegamento all'oggetto (zona, intervento, segnalazione, richiesta). |
| 4 | Sistema | Inserisce la notifica nel centro notifiche e aggiorna il contatore delle notifiche non lette. |
| 5 | Utente | Visualizza l'avviso nell'applicazione. |

**Flussi alternativi**
- **A1 – Alta priorità.** Al passo 4, se la notifica è ad alta priorità (es. emergenza), il sistema la mostra in evidenza a tutto schermo nell'applicazione e la inoltra anche per email tramite la posta elettronica istituzionale.
- **A2 – Utente non collegato.** Al passo 5, se l'utente non è collegato, troverà la notifica al successivo accesso (UC-05 A2); le notifiche ad alta priorità gli arrivano comunque per email.

**Eccezioni**
- **E1 – Invio email non riuscito.** Nell'A1, se l'email non può essere inviata, il sistema registra l'errore, ritenta e mantiene la notifica in evidenza nell'applicazione.

---

## UC-84 – Consultare il centro notifiche
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-23

| | |
|---|---|
| **Obiettivo** | Rivedere tutte le notifiche ricevute. |
| **Precondizioni** | L'utente è autenticato come responsabile o dirigente. |
| **Postcondizioni** | Le notifiche consultate risultano lette. |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-85 Aprire l'oggetto di una notifica; Filtrare le notifiche. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Apre il centro notifiche. |
| 2 | Sistema | Mostra le notifiche in ordine di importanza e data, distinguendo con icona e testo il livello di importanza e lo stato letta/non letta. |
| 3 | Utente | Filtra per livello di importanza, tipo di evento o stato, oppure segna una o più notifiche come lette. |
| 4 | Sistema | Aggiorna l'elenco e il contatore. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Nessuna notifica.** Al passo 2 il sistema mostra un messaggio informativo.

---

## UC-85 – Aprire l'oggetto di una notifica
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-23

| | |
|---|---|
| **Obiettivo** | Raggiungere direttamente la zona, l'intervento, la segnalazione o la richiesta a cui la notifica si riferisce. |
| **Precondizioni** | È visualizzata una notifica (UC-83 o UC-84). |
| **Postcondizioni** | È aperta la schermata dell'oggetto della notifica; la notifica è letta. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-84). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Seleziona una notifica. |
| 2 | Sistema | Segna la notifica come letta e apre la schermata dell'oggetto collegato (es. UC-29, UC-41, UC-54, UC-59). |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Oggetto non più disponibile o non consentito.** Al passo 2, se l'oggetto è stato archiviato o non è accessibile al ruolo, il sistema lo segnala.

---

# RF-24 – Configurazione dei parametri

## UC-86 – Configurare il calcolo dello stato delle zone
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-24, RF-09

| | |
|---|---|
| **Obiettivo** | Adattare il calcolo dello stato alle regole concordate con il Comune. |
| **Precondizioni** | L'amministratore è autenticato. |
| **Postcondizioni** | Pesi dei fattori, soglie di stato e limite dei dati non aggiornati sono aggiornati; lo stato delle zone è ricalcolato; la modifica è registrata con i valori precedenti. |
| **Use Case inclusi** | Verificare la coerenza dei parametri; UC-30 Aggiornare lo stato delle zone. |
| **Use Case estesi** | Simulare l'effetto della modifica. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Accede a «Configurazione → Stato delle zone». |
| 2 | Sistema | Mostra i pesi dei fattori, le soglie verde/giallo/rosso e il limite oltre il quale i dati sono considerati non aggiornati. |
| 3 | Amministratore | Modifica i valori. |
| 4 | Sistema | Verifica la coerenza (es. soglie crescenti, pesi nell'intervallo ammesso). |
| 5 | Amministratore | Conferma. |
| 6 | Sistema | Salva i parametri, ricalcola lo stato delle zone (UC-30) e registra la modifica. |

**Flussi alternativi**
- **A1 – Simulazione.** Al passo 5 l'amministratore seleziona «Simula»; il sistema mostra quante zone cambierebbero stato senza salvare.
- **A2 – Ripristino.** L'amministratore ripristina una configurazione precedente dallo storico delle modifiche.

**Eccezioni**
- **E1 – Valori incoerenti.** Al passo 4 il sistema indica i valori non validi e torna al passo 3.

---

## UC-87 – Configurare tipologie, frequenze e finestre stagionali
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-24, RF-22, RF-05, RF-06

| | |
|---|---|
| **Obiettivo** | Definire le tipologie di zona e di elemento e le manutenzioni attese per ciascuna. |
| **Precondizioni** | L'amministratore è autenticato. |
| **Postcondizioni** | Tipologie, frequenze e finestre stagionali sono aggiornate; le scadenze attese nel calendario e lo stato delle zone interessate sono ricalcolati; la modifica è registrata. |
| **Use Case inclusi** | Verificare la coerenza dei parametri. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Accede a «Configurazione → Tipologie e manutenzioni». |
| 2 | Sistema | Mostra le tipologie di zona e di elemento con, per ciascun tipo di lavoro, frequenza attesa e finestra stagionale (es. spegnimento fontane: dal … al …). |
| 3 | Amministratore | Aggiunge una tipologia o modifica frequenze e finestre e conferma. |
| 4 | Sistema | Verifica i dati, salva, rigenera le scadenze attese, ricalcola lo stato delle zone interessate e registra la modifica. |

**Flussi alternativi**
- **A1 – Tipologia in uso.** Al passo 3, se si tenta di eliminare una tipologia assegnata a zone o elementi, il sistema lo impedisce e propone di disattivarla.

**Eccezioni**
- **E1 – Dati non validi.** Al passo 4 (es. finestra con fine precedente all'inizio) il sistema lo segnala e torna al passo 3.

---

## UC-88 – Configurare i modelli di richiesta
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-24, RF-18, RF-17

| | |
|---|---|
| **Obiettivo** | Definire una sola volta, per ciascuna tipologia di lavoro, la forma della richiesta secondo le procedure del Comune. |
| **Precondizioni** | L'amministratore è autenticato. |
| **Postcondizioni** | Il modello è salvato e viene utilizzato per le nuove richieste; le richieste già inviate non cambiano; la modifica è registrata. |
| **Use Case inclusi** | Verificare la completezza del modello. |
| **Use Case estesi** | Configurare le condizioni di approvazione (CLAR-01). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Accede a «Configurazione → Modelli di richiesta» e seleziona una tipologia di lavoro. |
| 2 | Sistema | Mostra il modello con testo base, campi obbligatori, documenti da allegare e passaggi di approvazione. |
| 3 | Amministratore | Modifica il modello e conferma. |
| 4 | Sistema | Verifica che il modello contenga almeno i campi minimi (zona, lavori, scadenza, riferimenti) e lo salva come nuova versione. |

**Flussi alternativi**
- **A1 – Nuovo modello.** Al passo 1 l'amministratore crea un modello per una tipologia che non ne ha, partendo dal modello generico.
- **A2 – Condizioni di approvazione.** Al passo 3 l'amministratore imposta le condizioni (es. soglia di spesa) che attivano l'approvazione del dirigente.

**Eccezioni**
- **E1 – Modello incompleto.** Al passo 4 il sistema indica i campi minimi mancanti.

---

## UC-89 – Configurare acquisizione segnalazioni e notifiche
**Attore principale:** Amministratore · **Attori secondari:** Portale segnalazioni · **RF collegati:** RF-24, RF-14, RF-15, RF-23

| | |
|---|---|
| **Obiettivo** | Impostare periodicità dell'acquisizione, intervallo entro cui la programmazione prevale e livelli di importanza delle notifiche. |
| **Precondizioni** | L'amministratore è autenticato. |
| **Postcondizioni** | I parametri sono aggiornati e si applicano dalle successive acquisizioni e notifiche; la modifica è registrata. |
| **Use Case inclusi** | Verificare la coerenza dei parametri. |
| **Use Case estesi** | Verificare il collegamento con il portale. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Accede a «Configurazione → Segnalazioni e notifiche». |
| 2 | Sistema | Mostra periodo di acquisizione, intervallo di prevalenza della programmazione e, per ogni tipo di evento, il livello di importanza della notifica. |
| 3 | Amministratore | Modifica i valori e conferma. |
| 4 | Sistema | Verifica che il periodo di acquisizione non superi i sette giorni, salva i parametri e registra la modifica. |

**Flussi alternativi**
- **A1 – Verifica del collegamento.** Al passo 3 l'amministratore seleziona «Verifica collegamento»; il sistema interroga il portale delle segnalazioni e ne mostra l'esito.

**Eccezioni**
- **E1 – Periodo non ammesso.** Al passo 4, se il periodo supera i sette giorni, il sistema lo segnala e non salva.

---

## UC-90 – Modificare i parametri operativi consentiti
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-24

| | |
|---|---|
| **Obiettivo** | Adeguare i parametri operativi a lui consentiti senza dover passare dall'amministratore. |
| **Precondizioni** | Il responsabile è autenticato; l'amministratore ha reso modificabili dal responsabile alcuni parametri (insieme da definire – CLAR-03). |
| **Postcondizioni** | I parametri consentiti sono aggiornati con gli stessi effetti delle modifiche dell'amministratore; la modifica è registrata. |
| **Use Case inclusi** | Verificare la coerenza dei parametri. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Accede a «Impostazioni operative». |
| 2 | Sistema | Mostra solo i parametri che il responsabile può modificare, con i valori correnti. |
| 3 | Responsabile | Modifica i valori e conferma. |
| 4 | Sistema | Verifica la coerenza, salva, applica gli effetti (es. ricalcolo delle scadenze o dello stato) e registra la modifica. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Valori non validi.** Al passo 4 il sistema lo segnala e torna al passo 3.

---

# RF-25 – Anagrafica delle ditte

## UC-91 – Consultare l'anagrafica delle ditte
**Attore principale:** Responsabile, Amministratore · **Attori secondari:** – · **RF collegati:** RF-25

| | |
|---|---|
| **Obiettivo** | Conoscere le ditte incaricate dal Comune, i loro contatti, competenze e contratti. |
| **Precondizioni** | L'utente è autenticato come responsabile o amministratore. |
| **Postcondizioni** | È visualizzato l'elenco o il dettaglio delle ditte. |
| **Use Case inclusi** | – |
| **Use Case estesi** | Filtrare le ditte; UC-92, UC-93, UC-94 (solo Amministratore). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Accede alla sezione «Ditte». |
| 2 | Sistema | Mostra l'elenco con ragione sociale, competenze, stato (attiva/disattivata) e contratti attivi. |
| 3 | Utente | Filtra per competenza o cerca per nome e seleziona una ditta. |
| 4 | Sistema | Mostra contatti, competenze, contratti con zone e periodo di validità, interventi aperti e conclusi. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Nessuna ditta.** Al passo 2 il sistema indica che l'anagrafica è vuota.

---

## UC-92 – Inserire o modificare una ditta
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-25

| | |
|---|---|
| **Obiettivo** | Registrare o aggiornare i dati di una ditta incaricata dal Comune. |
| **Precondizioni** | L'amministratore è autenticato; dispone dei dati della ditta (individuata dal Comune, es. tramite bando – CLAR-02). |
| **Postcondizioni** | La ditta è registrata o aggiornata ed è selezionabile per le richieste compatibili con le sue competenze; l'operazione è registrata. |
| **Use Case inclusi** | Verificare l'unicità della ditta. |
| **Use Case estesi** | UC-93 Gestire i contratti di una ditta. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Seleziona «Nuova ditta» o «Modifica» su una ditta esistente. |
| 2 | Sistema | Mostra il modulo con ragione sociale, partita IVA, contatti (email per le richieste, telefono, referente) e competenze (tipologie di lavoro). |
| 3 | Amministratore | Compila i dati e conferma. |
| 4 | Sistema | Verifica i campi obbligatori e che non esista già una ditta con la stessa partita IVA. |
| 5 | Sistema | Salva la ditta e registra l'operazione. |

**Flussi alternativi**
- **A1 – Cambio dell'email di contatto.** Al passo 3, se cambia l'email per le richieste, il sistema la usa per i nuovi invii e continua a riconoscere anche l'indirizzo precedente per le risposte già in corso.

**Eccezioni**
- **E1 – Dati mancanti o ditta già presente.** Al passo 4 il sistema lo segnala e torna al passo 3.

---

## UC-93 – Gestire i contratti di una ditta
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-25, RF-18

| | |
|---|---|
| **Obiettivo** | Associare a una ditta gli appalti o contratti attivi, con zone e periodo di validità. |
| **Precondizioni** | L'amministratore è autenticato ed è selezionata una ditta. |
| **Postcondizioni** | Il contratto è registrato; per le zone coperte la ditta viene proposta per prima nelle richieste del tipo di lavoro previsto; l'operazione è registrata. |
| **Use Case inclusi** | Verificare sovrapposizioni tra contratti. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Nel dettaglio della ditta seleziona «Aggiungi contratto». |
| 2 | Sistema | Mostra il modulo con riferimento del contratto, tipologie di lavoro coperte, zone, data di inizio e di fine. |
| 3 | Amministratore | Compila i dati, seleziona le zone e conferma. |
| 4 | Sistema | Verifica che le date siano coerenti e che le stesse zone e tipologie non siano già coperte da un altro contratto nello stesso periodo. |
| 5 | Sistema | Salva il contratto e registra l'operazione. |

**Flussi alternativi**
- **A1 – Modifica o chiusura anticipata.** Al passo 1 l'amministratore modifica un contratto esistente o ne anticipa la scadenza.

**Eccezioni**
- **E1 – Contratti sovrapposti.** Al passo 4 il sistema mostra il contratto in conflitto e chiede di correggere i dati o confermare esplicitamente.
- **E2 – Date non valide.** Al passo 4 il sistema lo segnala.

---

## UC-94 – Disattivare una ditta
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-25

| | |
|---|---|
| **Obiettivo** | Escludere una ditta dalle nuove richieste mantenendone lo storico. |
| **Precondizioni** | L'amministratore è autenticato ed è selezionata una ditta attiva. |
| **Postcondizioni** | La ditta è disattivata: non compare tra le ditte selezionabili, ma resta associata agli interventi registrati; l'operazione è registrata. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Seleziona «Disattiva» sulla ditta. |
| 2 | Sistema | Chiede conferma e motivazione, segnalando gli eventuali interventi aperti affidati alla ditta. |
| 3 | Amministratore | Inserisce la motivazione e conferma. |
| 4 | Sistema | Disattiva la ditta e registra l'operazione. |

**Flussi alternativi**
- **A1 – Riattivazione.** Su una ditta disattivata l'amministratore seleziona «Riattiva»; il sistema la rende di nuovo selezionabile.

**Eccezioni**
- **E1 – Interventi aperti.** Al passo 2, se la ditta ha interventi non conclusi, il sistema lo segnala; gli interventi restano affidati alla ditta finché il responsabile non li riassegna.

---

# RF-26 – Registro delle azioni

## UC-95 – Consultare il registro delle azioni
**Attore principale:** Dirigente, Amministratore · **Attori secondari:** – · **RF collegati:** RF-26

| | |
|---|---|
| **Obiettivo** | Sapere chi ha fatto cosa e quando, per trasparenza e in caso di contestazioni. |
| **Precondizioni** | L'utente è autenticato come dirigente o amministratore. |
| **Postcondizioni** | Sono visualizzate le voci del registro; nessuna voce può essere modificata o cancellata. |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-96 Filtrare il registro; Esportare il registro. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Accede alla sezione «Registro delle azioni». |
| 2 | Sistema | Mostra le voci più recenti con data e ora, autore, tipo di azione e oggetto (zona, elemento, intervento, segnalazione, account, configurazione). |
| 3 | Utente | Seleziona una voce. |
| 4 | Sistema | Mostra il dettaglio dell'azione, inclusi i valori precedenti e successivi quando applicabile, e il collegamento all'oggetto. |

**Flussi alternativi**
- **A1 – Dall'oggetto al registro.** L'utente apre il registro filtrato su un oggetto specifico dalla sua scheda (es. «Cronologia» di una zona).

**Eccezioni**
- **E1 – Errore di caricamento.** Il sistema mostra un messaggio di errore.

---

## UC-96 – Filtrare il registro
**Attore principale:** Dirigente, Amministratore · **Attori secondari:** – · **RF collegati:** RF-26

| | |
|---|---|
| **Obiettivo** | Restringere il registro alle azioni di interesse. |
| **Precondizioni** | È visualizzato il registro (UC-95). |
| **Postcondizioni** | Sono visualizzate solo le voci che soddisfano i filtri. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-95). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Imposta i filtri: autore, periodo, tipo di azione, oggetto. |
| 2 | Sistema | Mostra le voci corrispondenti con l'indicazione dei filtri attivi. |

**Flussi alternativi**
- **A1 – Esportazione.** Al passo 2 l'utente esporta le voci filtrate in forma tabellare; il sistema registra anche l'esportazione.

**Eccezioni**
- **E1 – Nessuna voce.** Al passo 2 il sistema mostra un messaggio informativo.
