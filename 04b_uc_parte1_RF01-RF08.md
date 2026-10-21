# 4. Descrizione testuale degli Use Case – Parte 1 (RF-01 … RF-08)

Convenzioni: nel flusso principale «Sistema» indica Treento. I flussi alternativi (A) descrivono scenari validi diversi da quello principale; le eccezioni (E) descrivono errori o condizioni che impediscono di completare lo Use Case. Gli Use Case inclusi/estesi senza identificatore sono sotto-funzionalità che verranno rappresentate nei relativi Use Case Diagram.

---

# RF-01 – Accesso al sistema

## UC-01 – Effettuare il login
**Attore principale:** Utente non autenticato · **Attori secondari:** – · **RF collegati:** RF-01, RF-02

| | |
|---|---|
| **Obiettivo** | Accedere a Treento e alle funzionalità previste per il proprio ruolo. |
| **Precondizioni** | L'utente possiede un account attivo creato dall'amministratore e non è autenticato. |
| **Postcondizioni** | L'utente è autenticato, la sessione è avviata e il sistema mostra la schermata iniziale del suo ruolo. L'accesso è registrato nel registro delle azioni. |
| **Use Case inclusi** | Verificare le credenziali; Verificare lo stato dell'account; UC-05 Visualizzare la schermata iniziale del proprio ruolo. |
| **Use Case estesi** | UC-02 Cambiare la password temporanea; UC-03 Recuperare la password. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Apre l'indirizzo di Treento dal browser. |
| 2 | Sistema | Mostra la schermata di accesso con i campi nome utente e password e il collegamento «Password dimenticata». |
| 3 | Utente | Inserisce nome utente e password e preme «Accedi». |
| 4 | Sistema | Verifica che le credenziali siano corrette. |
| 5 | Sistema | Verifica che l'account sia attivo e non bloccato. |
| 6 | Sistema | Riconosce il ruolo associato all'account e avvia la sessione. |
| 7 | Sistema | Mostra la schermata iniziale del ruolo (UC-05). |

**Flussi alternativi**
- **A1 – Primo accesso con password temporanea.** Al passo 6, se la password utilizzata è temporanea, il sistema avvia UC-02; al termine prosegue dal passo 7.
- **A2 – Password dimenticata.** Al passo 3 l'utente seleziona «Password dimenticata»; si avvia UC-03 e lo Use Case termina.

**Eccezioni**
- **E1 – Credenziali errate.** Al passo 4, se nome utente o password non sono corretti, il sistema mostra un messaggio di errore generico (senza indicare quale dato è errato), registra il tentativo fallito e torna al passo 2.
- **E2 – Account bloccato per troppi tentativi.** Al passo 4, se si raggiunge il numero massimo di tentativi consecutivi falliti (RNF-07), il sistema blocca temporaneamente l'account e informa l'utente. Lo Use Case termina.
- **E3 – Account disattivato.** Al passo 5, se l'account è disattivato, il sistema nega l'accesso, mostra la motivazione di disattivazione (presentata dall'amministratore in UC-09) e informa l'utente di rivolgersi all'amministratore. Lo Use Case termina.

---

## UC-02 – Cambiare la password temporanea
**Attore principale:** Utente non autenticato · **Attori secondari:** – · **RF collegati:** RF-01, RF-03

| | |
|---|---|
| **Obiettivo** | Sostituire la password temporanea ricevuta all'attivazione dell'account con una password personale. |
| **Precondizioni** | L'utente ha inserito credenziali corrette e la password utilizzata è temporanea (UC-01). |
| **Postcondizioni** | La password temporanea è sostituita da quella personale e non è più valida; l'utente prosegue l'accesso. |
| **Use Case inclusi** | Verificare i requisiti della password. |
| **Use Case estesi** | – (estende UC-01). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Informa l'utente che deve definire una nuova password e mostra i requisiti richiesti. |
| 2 | Utente | Inserisce la nuova password e la conferma. |
| 3 | Sistema | Verifica che la password rispetti i requisiti (RNF-07), che le due password coincidano e che sia diversa da quella temporanea. |
| 4 | Sistema | Salva la nuova password, invalida quella temporanea e conferma l'operazione. |
| 5 | Sistema | Restituisce il controllo a UC-01, che prosegue mostrando la schermata iniziale. |

**Flussi alternativi**
- **A1 – Interruzione.** Se l'utente chiude la schermata senza completare il cambio, l'accesso non viene completato; al successivo login il sistema richiede di nuovo il cambio password.

**Eccezioni**
- **E1 – Password non conforme.** Al passo 3, se la password non rispetta i requisiti o le due password non coincidono, il sistema indica il motivo e torna al passo 2.
- **E2 – Errore di salvataggio.** Al passo 4, se il sistema non riesce a salvare la password, mostra un messaggio di errore e la password temporanea resta valida.

---

## UC-03 – Recuperare la password
**Attore principale:** Utente non autenticato · **Attori secondari:** Posta elettronica istituzionale · **RF collegati:** RF-01

| | |
|---|---|
| **Obiettivo** | Ripristinare l'accesso dopo aver dimenticato la password. |
| **Precondizioni** | L'utente non è autenticato e possiede un account associato a un indirizzo email istituzionale. |
| **Postcondizioni** | L'utente ha definito una nuova password valida; il collegamento di ripristino non è più utilizzabile. |
| **Use Case inclusi** | Inviare il collegamento di ripristino; Verificare i requisiti della password. |
| **Use Case estesi** | – (estende UC-01). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Seleziona «Password dimenticata» nella schermata di accesso. |
| 2 | Sistema | Chiede l'indirizzo email associato all'account. |
| 3 | Utente | Inserisce l'indirizzo email e conferma. |
| 4 | Sistema | Se l'indirizzo corrisponde a un account attivo, invia tramite la posta elettronica istituzionale un collegamento di ripristino con validità limitata. |
| 5 | Sistema | Mostra un messaggio che conferma l'invio, senza rivelare se l'indirizzo è registrato. |
| 6 | Utente | Apre il collegamento ricevuto. |
| 7 | Sistema | Mostra la schermata per la nuova password. |
| 8 | Utente | Inserisce e conferma la nuova password. |
| 9 | Sistema | Verifica i requisiti, salva la nuova password, invalida il collegamento e mostra la schermata di accesso. |

**Flussi alternativi**
- **A1 – Indirizzo non registrato o account disattivato.** Al passo 4 il sistema non invia nulla ma, per sicurezza, mostra comunque il messaggio del passo 5. Lo Use Case termina.

**Eccezioni**
- **E1 – Collegamento scaduto o già usato.** Al passo 7, se il collegamento non è più valido, il sistema lo segnala e propone di ripetere la richiesta (passo 2).
- **E2 – Password non conforme.** Al passo 9, se la password non rispetta i requisiti, il sistema indica il motivo e torna al passo 8.
- **E3 – Invio email non riuscito.** Al passo 4, se l'invio non riesce, il sistema mostra un messaggio di errore e invita a riprovare più tardi.

---

## UC-04 – Effettuare il logout
**Attore principale:** Personale comunale · **Attori secondari:** – · **RF collegati:** RF-01

| | |
|---|---|
| **Obiettivo** | Chiudere in modo sicuro la propria sessione di lavoro. |
| **Precondizioni** | L'utente è autenticato. |
| **Postcondizioni** | La sessione è chiusa; per usare di nuovo il sistema è necessario un nuovo login. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Seleziona «Esci» dal menu. |
| 2 | Sistema | Se ci sono modifiche non salvate, chiede conferma. |
| 3 | Utente | Conferma l'uscita. |
| 4 | Sistema | Chiude la sessione e mostra la schermata di accesso. |

**Flussi alternativi**
- **A1 – Uscita annullata.** Al passo 3 l'utente annulla; il sistema mantiene la sessione e la schermata corrente.
- **A2 – Scadenza per inattività.** Se l'utente resta inattivo oltre il limite previsto (RNF-07), il sistema chiude automaticamente la sessione e alla successiva azione mostra la schermata di accesso con un messaggio informativo.

**Eccezioni**
- – 

---

# RF-02 – Funzionalità disponibili per ruolo

## UC-05 – Visualizzare la schermata iniziale del proprio ruolo
**Attore principale:** Personale comunale (Responsabile, Dirigente, Amministratore) · **Attori secondari:** – · **RF collegati:** RF-02, RF-07

| | |
|---|---|
| **Obiettivo** | Avere a disposizione, dopo l'accesso, solo le funzionalità previste per il proprio ruolo. |
| **Precondizioni** | L'utente si è autenticato con successo (UC-01). |
| **Postcondizioni** | È visualizzata la schermata iniziale del ruolo con il menu delle sole funzioni consentite. |
| **Use Case inclusi** | Determinare i permessi del ruolo. |
| **Use Case estesi** | – (incluso in UC-01). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Determina i permessi associati al ruolo dell'utente. |
| 2 | Sistema | Compone il menu con le sole funzionalità consentite. |
| 3 | Sistema | Mostra la schermata iniziale del ruolo: per Responsabile e Dirigente la mappa delle zone (UC-24) con il riepilogo delle notifiche; per l'Amministratore il pannello di amministrazione. |
| 4 | Utente | Sceglie la funzionalità da utilizzare dal menu. |

**Flussi alternativi**
- **A1 – Dirigente.** Al passo 2, per il Dirigente il sistema mostra le sezioni operative in modalità di sola consultazione (senza comandi di creazione, modifica o invio) e aggiunge le sezioni «Approvazioni» e «Registro delle azioni».
- **A2 – Notifiche ad alta priorità in attesa.** Al passo 3, se sono presenti notifiche ad alta priorità non lette, il sistema le mette in evidenza in apertura.

**Eccezioni**
- **E1 – Accesso a una funzione non consentita.** Se l'utente tenta di raggiungere direttamente una funzionalità non prevista per il suo ruolo, il sistema nega l'accesso, mostra un messaggio e registra il tentativo.

---

# RF-03 – Gestione degli account del personale

## UC-06 – Consultare gli account del personale
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-03

| | |
|---|---|
| **Obiettivo** | Avere l'elenco degli utenti con ruolo e stato dell'account. |
| **Precondizioni** | L'amministratore è autenticato. |
| **Postcondizioni** | È visualizzato l'elenco degli account richiesto; nessun dato è modificato. |
| **Use Case inclusi** | – |
| **Use Case estesi** | Filtrare gli account; UC-07 Creare un account; UC-08 Modificare un account; UC-09 Disattivare o riattivare un account. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Accede alla sezione «Gestione account». |
| 2 | Sistema | Mostra l'elenco degli account con nome, cognome, email, ruolo, stato (attivo, disattivato, bloccato) e data dell'ultimo accesso. |
| 3 | Amministratore | Seleziona un account. |
| 4 | Sistema | Mostra il dettaglio dell'account con i comandi disponibili. |

**Flussi alternativi**
- **A1 – Ricerca e filtri.** Al passo 2 l'amministratore filtra per ruolo o stato o cerca per nome o email; il sistema aggiorna l'elenco.
- **A2 – Nessun risultato.** Se nessun account soddisfa i criteri, il sistema mostra un messaggio informativo.

**Eccezioni**
- **E1 – Errore di caricamento.** Se il sistema non riesce a recuperare gli account, mostra un messaggio di errore e propone di riprovare.

---

## UC-07 – Creare un account
**Attore principale:** Amministratore · **Attori secondari:** Posta elettronica istituzionale · **RF collegati:** RF-03, RF-01

| | |
|---|---|
| **Obiettivo** | Abilitare un nuovo membro del personale all'uso del sistema con un ruolo. |
| **Precondizioni** | L'amministratore è autenticato; la persona non possiede già un account. |
| **Postcondizioni** | L'account è creato e attivo con il ruolo assegnato; all'indirizzo email è stata inviata la password temporanea; l'operazione è registrata. |
| **Use Case inclusi** | Verificare l'unicità dell'email; Generare e inviare la password temporanea. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Seleziona «Nuovo account». |
| 2 | Sistema | Mostra il modulo con nome, cognome, email istituzionale e ruolo (Responsabile, Dirigente, Amministratore). |
| 3 | Amministratore | Compila i campi e conferma. |
| 4 | Sistema | Verifica che i campi obbligatori siano compilati e che l'email non sia già associata a un altro account. |
| 5 | Sistema | Crea l'account, genera una password temporanea e la invia all'indirizzo indicato tramite la posta elettronica istituzionale. |
| 6 | Sistema | Registra l'operazione e conferma la creazione mostrando l'account nell'elenco. |

**Flussi alternativi**
- **A1 – Annullamento.** Al passo 3 l'amministratore annulla; nessun account viene creato.

**Eccezioni**
- **E1 – Campi mancanti o non validi.** Al passo 4 il sistema evidenzia i campi da correggere e torna al passo 3.
- **E2 – Email già registrata.** Al passo 4 il sistema segnala che esiste già un account con quell'email e non lo crea, torna al passo 3.
- **E3 – Invio della password non riuscito.** Al passo 5, se l'email non può essere inviata, l'account viene creato ma il sistema lo segnala e consente di ripetere l'invio dal dettaglio dell'account.

---

## UC-08 – Modificare un account
**Attore principale:** Amministratore · **Attori secondari:** Posta elettronica istituzionale · **RF collegati:** RF-03

| | |
|---|---|
| **Obiettivo** | Aggiornare i dati o il ruolo di un utente. |
| **Precondizioni** | L'amministratore è autenticato e ha selezionato un account (UC-06). |
| **Postcondizioni** | I dati dell'account sono aggiornati; un cambio di ruolo ha effetto dal successivo accesso dell'utente; l'operazione è registrata con i valori precedenti. |
| **Use Case inclusi** | Verificare l'unicità dell'email. |
| **Use Case estesi** | Reimpostare la password temporanea. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Seleziona «Modifica» nel dettaglio dell'account. |
| 2 | Sistema | Mostra i dati modificabili (nome, cognome, email, ruolo). |
| 3 | Amministratore | Modifica i dati e conferma. |
| 4 | Sistema | Verifica i dati e l'unicità dell'email. |
| 5 | Sistema | Salva le modifiche, registra l'operazione e conferma. |

**Flussi alternativi**
- **A1 – Reimpostazione della password.** Al passo 1 l'amministratore seleziona «Reimposta password»; il sistema genera una nuova password temporanea, la invia all'utente e invalida quella precedente.
- **A2 – Modifica del proprio account.** Se l'amministratore tenta di togliere a sé stesso il ruolo di amministratore ed è l'unico amministratore attivo, il sistema impedisce l'operazione e lo segnala.
- **A3 – Annullamento.** Al passo 3 l'amministratore annulla; nessun account viene modificato. Lo Use Case termina.

**Eccezioni**
- **E1 – Dati non validi o email già in uso.** Al passo 4 il sistema evidenzia l'errore e torna al passo 3.
- **E2 – Errore di salvataggio.** Al passo 5 il sistema mostra un messaggio di errore; i dati restano invariati.

---

## UC-09 – Disattivare o riattivare un account
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-03, RF-26

| | |
|---|---|
| **Obiettivo** | Togliere o restituire l'accesso a un utente mantenendo la storia delle sue azioni. |
| **Precondizioni** | L'amministratore è autenticato e ha selezionato un account (UC-06). |
| **Postcondizioni** | L'account è disattivato (l'utente non può più accedere e le sessioni aperte sono chiuse) o riattivato; le azioni registrate in precedenza restano consultabili; l'operazione è registrata. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Seleziona «Disattiva» nel dettaglio di un account attivo. |
| 2 | Sistema | Chiede conferma e la motivazione della disattivazione. |
| 3 | Amministratore | Inserisce la motivazione e conferma. |
| 4 | Sistema | Disattiva l'account, chiude le eventuali sessioni aperte, registra l'operazione e conferma. |

**Flussi alternativi**
- **A1 – Riattivazione.** Al passo 1, su un account disattivato o bloccato, l'amministratore seleziona «Riattiva»; il sistema riattiva l'account, gli assegna una nuova password temporanea e la invia all'utente.
- **A2 – Interventi in carico.** Al passo 2, se l'utente è indicato come referente di interventi aperti, il sistema lo segnala, affinché vengano assegnati gli interventi aperti ad altri responsabili presenti nel sistema.

**Eccezioni**
- **E1 – Ultimo amministratore.** Se l'account è l'unico amministratore attivo, il sistema impedisce la disattivazione.
- **E2 – Errore di salvataggio.** Al passo 4 il sistema mostra un messaggio di errore e lo stato dell'account resta invariato.

---

# RF-04 – Costruzione iniziale delle zone

## UC-10 – Caricare le fonti dei dati iniziali
**Attore principale:** Amministratore · **Attori secondari:** Servizio cartografico · **RF collegati:** RF-04

| | |
|---|---|
| **Obiettivo** | Rendere disponibili al sistema le fonti necessarie per proporre le zone: storico dei lavori, eventuale censimento del verde, cartografia. |
| **Precondizioni** | L'amministratore è autenticato e dispone dei file forniti dal Comune (CLAR-05, CLAR-06). |
| **Postcondizioni** | Le fonti sono caricate e validate; il sistema indica quali fonti sono disponibili e con quale completezza. |
| **Use Case inclusi** | Verificare il formato delle fonti; Acquisire la cartografia. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Accede alla sezione «Costruzione zone» e seleziona «Carica fonti». |
| 2 | Sistema | Mostra le tipologie di fonte previste: storico dei lavori, censimento degli elementi, cartografia comunale. |
| 3 | Amministratore | Carica i file disponibili per ciascuna tipologia. |
| 4 | Sistema | Verifica il formato e il contenuto minimo di ciascun file. |
| 5 | Sistema | Acquisisce dal servizio cartografico le basi cartografiche aperte (parchi, giardini, strade, piazze) relative al territorio comunale. |
| 6 | Sistema | Mostra un riepilogo delle fonti caricate con numero di record e completezza. |

**Flussi alternativi**
- **A1 – Censimento non disponibile.** Al passo 3 l'amministratore indica che il censimento non esiste; il sistema prosegue e segnala nel riepilogo che le zone avranno una composizione sintetica.

**Eccezioni**
- **E1 – File non valido.** Al passo 4, se un file ha un formato non riconosciuto o è privo dei dati minimi, il sistema lo scarta indicandone il motivo; gli altri file restano caricati.
- **E2 – Servizio cartografico non raggiungibile.** Al passo 5 il sistema segnala l'errore e consente di ripetere l'acquisizione in un secondo momento.

---

## UC-11 – Generare la proposta di suddivisione in zone
**Attore principale:** Amministratore · **Attori secondari:** Servizio cartografico · **RF collegati:** RF-04, RF-06

| | |
|---|---|
| **Obiettivo** | Ottenere una prima suddivisione del verde in zone candidate, con perimetro, nome e composizione. |
| **Precondizioni** | Le fonti sono state caricate (UC-10); almeno la cartografia è disponibile. |
| **Postcondizioni** | Esiste un insieme di zone in stato «proposta», non ancora operative, consultabili dal responsabile; l'operazione è registrata. |
| **Use Case inclusi** | UC-10 Caricare le fonti dei dati iniziali; Individuare le aree delimitate; Raggruppare gli elementi puntuali; Proporre il nome delle zone; UC-20 Assegnare automaticamente un elemento a una zona. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Seleziona «Genera proposta di zone». |
| 2 | Sistema | Individua le aree verdi già delimitate in cartografia e le trasforma in zone candidate con il loro perimetro. |
| 3 | Sistema | Raggruppa gli elementi puntuali (es. alberate) per prossimità e per appartenenza alla stessa via o piazza, creando ulteriori zone candidate. |
| 4 | Sistema | Propone per ogni zona un nome derivato dal toponimo della via, del parco o della piazza. |
| 5 | Sistema | Assegna gli elementi censiti alle zone secondo la regola a priorità (UC-20) e ricostruisce dallo storico l'elenco delle aree oggetto di manutenzione. |
| 6 | Sistema | Mostra il riepilogo della proposta (numero di zone, elementi assegnati, zone senza elementi) e la rende consultabile al responsabile. |
| 7 | Sistema | Notifica al responsabile che la proposta è pronta per la validazione. |

**Flussi alternativi**
- **A1 – Assenza di censimento.** Al passo 5, se non esistono elementi censiti, il sistema crea zone con il solo perimetro e una composizione sintetica stimata dallo storico (es. numero approssimativo di alberi), segnalandola come da completare.
- **A2 – Proposta già esistente.** Al passo 1, se esiste una proposta non ancora validata, il sistema chiede se sostituirla; le zone già approvate non vengono modificate.

**Eccezioni**
- **E1 – Fonti insufficienti.** Al passo 2, se manca la cartografia, il sistema non genera la proposta e indica le fonti mancanti.
- **E2 – Errore di elaborazione.** Se l'elaborazione si interrompe, il sistema annulla la proposta parziale e mostra un messaggio di errore.

---

## UC-12 – Consultare le zone proposte
**Attore principale:** Responsabile · **Attori secondari:** Servizio cartografico · **RF collegati:** RF-04, RF-05

| | |
|---|---|
| **Obiettivo** | Esaminare la bozza di suddivisione prima di validarla. |
| **Precondizioni** | Il responsabile è autenticato; esiste almeno una zona in stato «proposta». |
| **Postcondizioni** | Il responsabile ha visualizzato le zone proposte; nessun dato è modificato. |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-13 Modificare una zona; UC-18 Approvare una zona. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Accede alla sezione «Validazione zone». |
| 2 | Sistema | Mostra la mappa con le zone proposte, distinte da quelle già approvate, e il relativo elenco. |
| 3 | Responsabile | Seleziona una zona proposta. |
| 4 | Sistema | Mostra perimetro, nome proposto, elementi assegnati o composizione sintetica, fonti da cui deriva e lavori storici associati. |

**Flussi alternativi**
- **A1 – Filtro delle zone da completare.** Al passo 2 il responsabile filtra le zone con composizione sintetica o senza elementi; il sistema aggiorna mappa ed elenco.

**Eccezioni**
- **E1 – Nessuna zona da validare.** Al passo 2, se non ci sono zone proposte, il sistema lo comunica.
- **E2 – Cartografia non disponibile.** Se la base cartografica non può essere caricata, il sistema mostra l'elenco delle zone senza mappa e segnala il problema.

---

# RF-05 – Validazione e modifica delle zone

## UC-13 – Modificare una zona
**Attore principale:** Responsabile · **Attori secondari:** Servizio cartografico · **RF collegati:** RF-05, RF-26

Use Case generale, specializzato da UC-14, UC-15, UC-16 e UC-17, che ne ereditano precondizioni, postcondizioni ed eccezioni.

| | |
|---|---|
| **Obiettivo** | Correggere la suddivisione in zone affinché rispecchi l'organizzazione reale della manutenzione. |
| **Precondizioni** | Il responsabile è autenticato e ha selezionato una zona (proposta o approvata). |
| **Postcondizioni** | La zona risulta modificata; gli elementi coinvolti sono riassegnati; per una zona già approvata lo stato viene ricalcolato; la modifica è registrata con autore, data e valori precedenti. |
| **Use Case inclusi** | Registrare la modifica della zona; UC-20 Assegnare automaticamente un elemento a una zona (per gli elementi interessati). |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona una zona e sceglie «Modifica». |
| 2 | Sistema | Mostra gli strumenti di modifica: unire, dividere, modificare perimetro, rinominare e classificare. |
| 3 | Responsabile | Sceglie il tipo di modifica ed esegue l'operazione (vedi UC-14…UC-17). |
| 4 | Sistema | Mostra un'anteprima con gli effetti (elementi spostati, interventi e segnalazioni collegati). |
| 5 | Responsabile | Conferma. |
| 6 | Sistema | Applica la modifica, riassegna gli elementi, registra l'operazione e conferma. |

**Flussi alternativi**
- **A1 – Annullamento.** Ai passi 3–5 il responsabile annulla; la zona resta invariata.

**Eccezioni**
- **E1 – Geometria non valida.** Al passo 4, se il perimetro risultante si sovrappone a un'altra zona o non è chiuso, il sistema lo segnala e torna al passo 3.
- **E2 – Errore di salvataggio.** Al passo 6 il sistema mostra un messaggio di errore e annulla l'intera modifica.

---

## UC-14 – Unire zone
**Attore principale:** Responsabile · **Attori secondari:** Servizio cartografico · **RF collegati:** RF-05

| | |
|---|---|
| **Obiettivo** | Accorpare due o più zone confinanti troppo piccole in un'unica zona. |
| **Precondizioni** | Quelle di UC-13; sono selezionate almeno due zone confinanti. |
| **Postcondizioni** | Esiste una sola zona con perimetro unito, elementi, storico e segnalazioni di tutte le zone di origine; le zone di origine sono archiviate e la loro storia resta consultabile. |
| **Use Case inclusi** | Quelli di UC-13. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona sulla mappa due o più zone confinanti e sceglie «Unisci». |
| 2 | Sistema | Calcola il perimetro unito e chiede nome e tipologia della nuova zona, proponendo quelli della zona più estesa. |
| 3 | Responsabile | Conferma o modifica nome e tipologia. |
| 4 | Sistema | Mostra l'anteprima con elementi, interventi e segnalazioni che confluiranno nella nuova zona. |
| 5 | Responsabile | Conferma l'unione. |
| 6 | Sistema | Crea la zona unita, sposta elementi e collegamenti, archivia le zone di origine e registra l'operazione. |

**Flussi alternativi**
- **A1 – Tipologie diverse.** Al passo 2, se le zone hanno tipologie diverse, il sistema lo segnala e chiede di scegliere la tipologia della zona risultante.

**Eccezioni**
- **E1 – Zone non confinanti.** Al passo 2 il sistema segnala che le zone non sono confinanti e non procede.
- **E2 – Contratti diversi.** Al passo 4, se le zone sono coperte da contratti di manutenzione diversi, il sistema lo segnala e chiede una conferma esplicita.

---

## UC-15 – Dividere una zona
**Attore principale:** Responsabile · **Attori secondari:** Servizio cartografico · **RF collegati:** RF-05, RF-06

| | |
|---|---|
| **Obiettivo** | Separare una zona troppo grande in due o più zone. |
| **Precondizioni** | Quelle di UC-13. |
| **Postcondizioni** | Esistono le nuove zone con i rispettivi perimetri ed elementi; lo storico della zona originaria resta associato a essa (archiviata) e consultabile dalle nuove zone. |
| **Use Case inclusi** | Quelli di UC-13. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona una zona e sceglie «Dividi». |
| 2 | Sistema | Permette di tracciare sulla mappa una o più linee di divisione. |
| 3 | Responsabile | Traccia le linee di divisione. |
| 4 | Sistema | Calcola le nuove zone, assegna a ciascuna gli elementi che vi ricadono (UC-20) e propone un nome per ognuna. |
| 5 | Responsabile | Verifica e modifica nomi e tipologie, poi conferma. |
| 6 | Sistema | Crea le nuove zone, archivia quella originaria, redistribuisce le segnalazioni aperte in base alla posizione e registra l'operazione. |

**Flussi alternativi**
- **A1 – Interventi aperti sulla zona.** Al passo 4, se sulla zona ci sono interventi non conclusi, il sistema chiede a quale nuova zona associarli.

**Eccezioni**
- **E1 – Linea di divisione non valida.** Al passo 4, se la linea non divide la zona in parti chiuse, il sistema lo segnala e torna al passo 3.

---

## UC-16 – Modificare il perimetro di una zona
**Attore principale:** Responsabile · **Attori secondari:** Servizio cartografico · **RF collegati:** RF-05, RF-06

| | |
|---|---|
| **Obiettivo** | Spostare un confine per far coincidere la zona con l'area effettivamente gestita. |
| **Precondizioni** | Quelle di UC-13. |
| **Postcondizioni** | Il perimetro è aggiornato; gli elementi entrati o usciti dal perimetro sono riassegnati; le zone confinanti interessate sono aggiornate. |
| **Use Case inclusi** | Quelli di UC-13. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona una zona e sceglie «Modifica perimetro». |
| 2 | Sistema | Mostra il perimetro con i punti modificabili. |
| 3 | Responsabile | Sposta, aggiunge o rimuove punti del perimetro. |
| 4 | Sistema | Mostra l'anteprima degli elementi che cambierebbero zona. |
| 5 | Responsabile | Conferma. |
| 6 | Sistema | Salva il nuovo perimetro, riassegna gli elementi (UC-20) e registra l'operazione. |

**Flussi alternativi**
- **A1 – Confine condiviso.** Al passo 4, se la modifica interessa una zona confinante, il sistema propone di aggiornare anche il suo perimetro in modo coerente.

**Eccezioni**
- **E1 – Sovrapposizione.** Al passo 4, se il nuovo perimetro si sovrappone a un'altra zona senza aggiornarla, il sistema lo segnala e torna al passo 3.

---

## UC-17 – Rinominare e classificare una zona
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-05, RF-09, RF-22

| | |
|---|---|
| **Obiettivo** | Assegnare alla zona un nome chiaro e la tipologia che ne determina la manutenzione attesa. |
| **Precondizioni** | Quelle di UC-13. |
| **Postcondizioni** | Nome, tipologia e quartiere della zona sono aggiornati; se la tipologia è cambiata, le scadenze attese nel calendario e lo stato della zona sono ricalcolati. |
| **Use Case inclusi** | Quelli di UC-13. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona una zona e sceglie «Rinomina e classifica». |
| 2 | Sistema | Mostra nome, tipologia (es. parco, viale alberato, piazza) e quartiere correnti. |
| 3 | Responsabile | Modifica i dati e conferma. |
| 4 | Sistema | Verifica che il nome non sia già usato da un'altra zona. |
| 5 | Sistema | Salva i dati; se la tipologia è cambiata ricalcola le scadenze attese e lo stato della zona; registra l'operazione. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Nome già esistente.** Al passo 4 il sistema segnala il conflitto e torna al passo 3.

---

## UC-18 – Approvare una zona
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-04, RF-05, RF-09

| | |
|---|---|
| **Obiettivo** | Rendere operativa una zona proposta. |
| **Precondizioni** | Il responsabile è autenticato; la zona è in stato «proposta» e ha nome, perimetro e tipologia. |
| **Postcondizioni** | La zona è operativa: compare nella mappa e nelle aree verdi, il sistema ne calcola lo stato e genera le scadenze attese; l'approvazione è registrata. |
| **Use Case inclusi** | Verificare la completezza della zona; UC-30 Aggiornare lo stato delle zone. |
| **Use Case estesi** | Approvare più zone insieme. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona una zona proposta e sceglie «Approva». |
| 2 | Sistema | Verifica che la zona abbia nome, perimetro e tipologia. |
| 3 | Sistema | Chiede conferma mostrando un riepilogo della zona. |
| 4 | Responsabile | Conferma. |
| 5 | Sistema | Rende la zona operativa, ne calcola lo stato (UC-30), genera le scadenze attese nel calendario e registra l'approvazione. |

**Flussi alternativi**
- **A1 – Approvazione multipla.** Al passo 1 il responsabile seleziona più zone proposte; il sistema esegue i passi 2–5 per ciascuna e mostra quali sono state approvate e quali no.
- **A2 – Composizione sintetica.** Al passo 2, se la zona ha solo una composizione sintetica, il sistema lo segnala ma consente l'approvazione; lo stato potrà risultare grigio finché i dati non vengono completati.

**Eccezioni**
- **E1 – Zona incompleta.** Al passo 2, se mancano nome, perimetro o tipologia, il sistema indica cosa manca e non approva la zona.

---

# RF-06 – Gestione degli elementi e assegnazione alle zone

## UC-19 – Inserire un elemento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-06

| | |
|---|---|
| **Obiettivo** | Aggiungere un nuovo elemento al patrimonio verde (es. un albero piantato, una nuova fontana). |
| **Precondizioni** | Il responsabile è autenticato; esiste almeno una zona operativa. |
| **Postcondizioni** | L'elemento è registrato con i suoi dati e assegnato a una sola zona; la composizione della zona è aggiornata; l'operazione è registrata. |
| **Use Case inclusi** | UC-20 Assegnare automaticamente un elemento a una zona. |
| **Use Case estesi** | UC-22 Correggere l'assegnazione di un elemento. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Nuovo elemento» dalla mappa o dalla scheda di una zona. |
| 2 | Sistema | Mostra il modulo con categoria (albero, fontana, aiuola, panchina, gioco…), specie o tipologia, posizione e note. |
| 3 | Responsabile | Compila i dati e indica la posizione sulla mappa. |
| 4 | Sistema | Verifica i campi obbligatori. |
| 5 | Sistema | Assegna l'elemento a una zona secondo la regola a priorità (UC-20) e mostra la zona assegnata con il criterio utilizzato. |
| 6 | Responsabile | Conferma l'inserimento. |
| 7 | Sistema | Salva l'elemento, aggiorna la composizione della zona e registra l'operazione. |

**Flussi alternativi**
- **A1 – Assegnazione non condivisa.** Al passo 6 il responsabile non condivide la zona proposta e avvia UC-22.
- **A2 – Inserimento dalla scheda di una zona.** Al passo 1, se l'inserimento parte dalla scheda di una zona e la posizione ricade in essa, il sistema propone direttamente quella zona.

**Eccezioni**
- **E1 – Dati mancanti.** Al passo 4 il sistema evidenzia i campi mancanti e torna al passo 3.
- **E2 – Posizione fuori dal territorio comunale.** Al passo 5, se la posizione non ricade in nessuna zona né in prossimità di una zona, il sistema lo segnala e chiede di correggere la posizione.

---

## UC-20 – Assegnare automaticamente un elemento a una zona
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-06

| | |
|---|---|
| **Obiettivo** | Ottenere l'assegnazione dell'elemento alla zona corretta secondo la regola a priorità decrescente, senza ambiguità. |
| **Precondizioni** | È disponibile la posizione dell'elemento; esistono zone. È incluso in UC-19, UC-11, UC-13…UC-16. |
| **Postcondizioni** | L'elemento è associato a una sola zona e il sistema conserva il criterio utilizzato. |
| **Use Case inclusi** | Verificare l'appartenenza geometrica; Confrontare via, parco e contratto; Confrontare gli elementi simili vicini; Calcolare la zona con il centro più vicino. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Verifica in quali perimetri di zona ricade la posizione dell'elemento. |
| 2 | Sistema | Se ricade nel perimetro di una sola zona, assegna l'elemento a quella zona (criterio 1). |
| 3 | Sistema | Restituisce zona e criterio allo Use Case chiamante. |

**Flussi alternativi**
- **A1 – Elemento sul confine o entro la tolleranza.** Al passo 2, se l'elemento è sul confine di più zone o entro la tolleranza, il sistema sceglie la zona con cui condivide il nome della via o del parco oppure il contratto di manutenzione (criterio 2).
- **A2 – Criterio 2 non decisivo.** Se A1 non individua una sola zona, il sistema sceglie la zona che nelle vicinanze contiene più elementi simili per tipologia e specie (criterio 3).
- **A3 – Parità.** Se anche A2 non individua una sola zona, il sistema sceglie la zona con il centro geometrico più vicino (criterio 4).

**Eccezioni**
- **E1 – Nessuna zona vicina.** Al passo 1, se l'elemento non ricade in alcuna zona né entro la tolleranza, il sistema non assegna l'elemento e lo segnala allo Use Case chiamante.

---

## UC-21 – Modificare o rimuovere un elemento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-06, RF-26

| | |
|---|---|
| **Obiettivo** | Aggiornare i dati di un elemento o dismetterlo (es. albero abbattuto, gioco rimosso). |
| **Precondizioni** | Il responsabile è autenticato e ha selezionato un elemento. |
| **Postcondizioni** | I dati dell'elemento sono aggiornati oppure l'elemento è dismesso (non più conteggiato nella zona ma presente nello storico); l'operazione è registrata. |
| **Use Case inclusi** | Registrare la modifica dell'elemento. |
| **Use Case estesi** | UC-20 Assegnare automaticamente un elemento a una zona (se cambia la posizione). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona un elemento dalla mappa o dalla scheda zona e sceglie «Modifica». |
| 2 | Sistema | Mostra i dati dell'elemento. |
| 3 | Responsabile | Modifica i dati e conferma. |
| 4 | Sistema | Verifica i dati; se la posizione è cambiata riesegue l'assegnazione alla zona (UC-20). |
| 5 | Sistema | Salva le modifiche, aggiorna la composizione delle zone interessate e registra l'operazione. |

**Flussi alternativi**
- **A1 – Dismissione.** Al passo 1 il responsabile sceglie «Dismetti» e indica motivo e data (es. abbattimento con riferimento all'intervento); il sistema marca l'elemento come dismesso e aggiorna la composizione della zona.

**Eccezioni**
- **E1 – Dati non validi.** Al passo 4 il sistema evidenzia l'errore e torna al passo 3.
- **E2 – Interventi aperti sull'elemento.** Nell'A1, se l'elemento è coinvolto in interventi non conclusi, il sistema lo segnala e chiede conferma.

---

## UC-22 – Correggere l'assegnazione di un elemento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-06, RF-26

| | |
|---|---|
| **Obiettivo** | Spostare manualmente un elemento nella zona corretta quando l'assegnazione automatica non è adeguata. |
| **Precondizioni** | Il responsabile è autenticato e ha selezionato un elemento assegnato a una zona. |
| **Postcondizioni** | L'elemento appartiene alla nuova zona; l'assegnazione manuale è registrata con la motivazione e non viene più modificata automaticamente; le composizioni delle due zone sono aggiornate. |
| **Use Case inclusi** | Registrare la modifica dell'elemento. |
| **Use Case estesi** | – (estende UC-19). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Cambia zona» nel dettaglio dell'elemento. |
| 2 | Sistema | Mostra la zona corrente con il criterio usato e l'elenco delle zone vicine. |
| 3 | Responsabile | Sceglie la nuova zona e inserisce una motivazione. |
| 4 | Sistema | Sposta l'elemento, aggiorna le composizioni delle zone e registra l'operazione. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Motivazione mancante.** Al passo 3 il sistema richiede la motivazione e non procede.

---

## UC-23 – Registrare un'anomalia su un elemento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-06, RF-09

| | |
|---|---|
| **Obiettivo** | Segnalare un problema su un singolo elemento (es. fontana guasta, controllo di stabilità scaduto) affinché concorra allo stato della zona. |
| **Precondizioni** | Il responsabile è autenticato e ha selezionato un elemento. |
| **Postcondizioni** | L'anomalia è registrata sull'elemento ed è visibile in mappa e nella scheda zona; lo stato della zona è ricalcolato. |
| **Use Case inclusi** | UC-30 Aggiornare lo stato delle zone. |
| **Use Case estesi** | Risolvere un'anomalia; UC-56 Creare un intervento manualmente. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona un elemento e sceglie «Registra anomalia». |
| 2 | Sistema | Mostra il modulo con tipo di anomalia, gravità, descrizione ed eventuali fotografie. |
| 3 | Responsabile | Compila e conferma. |
| 4 | Sistema | Registra l'anomalia, aggiorna lo stato della zona (UC-30) e conferma. |

**Flussi alternativi**
- **A1 – Risoluzione dell'anomalia.** Su un elemento con anomalia aperta il responsabile sceglie «Risolvi» indicando l'eventuale intervento che l'ha risolta; il sistema chiude l'anomalia e ricalcola lo stato.
- **A2 – Creazione immediata di un intervento.** Al termine il responsabile sceglie «Crea intervento»; si avvia UC-56 con elemento e anomalia precompilati.

**Eccezioni**
- **E1 – Dati mancanti.** Al passo 3, se mancano tipo o gravità, il sistema lo segnala e non registra l'anomalia.

---

# RF-07 – Mappa delle zone

## UC-24 – Visualizzare la mappa delle zone
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** Servizio cartografico · **RF collegati:** RF-07

| | |
|---|---|
| **Obiettivo** | Avere una visione d'insieme dello stato del verde di Trento. |
| **Precondizioni** | L'utente è autenticato come responsabile o dirigente; esiste almeno una zona operativa. |
| **Postcondizioni** | È visualizzata la mappa con le zone colorate per stato e le eventuali emergenze; nessun dato è modificato. |
| **Use Case inclusi** | Caricare la base cartografica; Rappresentare lo stato delle zone. |
| **Use Case estesi** | UC-25 Filtrare la mappa; UC-26 Visualizzare gli elementi di una zona sulla mappa; UC-27 Visualizzare la scheda sintetica di una zona. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Accede alla sezione «Mappa» (schermata iniziale). |
| 2 | Sistema | Carica la base cartografica di Trento dal servizio cartografico. |
| 3 | Sistema | Rappresenta ogni zona con il suo nome e con colore, icona e motivo del suo stato (verde, giallo, rosso, grigio). |
| 4 | Sistema | Evidenzia in rosso, con il simbolo di emergenza, gli elementi o le posizioni in emergenza. |
| 5 | Sistema | Mostra la legenda degli stati e dei simboli. |
| 6 | Utente | Sposta e ingrandisce la mappa per esplorarla. |

**Flussi alternativi**
- **A1 – Verifica in corso.** Al passo 3, le zone con un intervento in attesa di verifica mostrano anche l'indicatore di verifica in corso.

**Eccezioni**
- **E1 – Cartografia non disponibile.** Al passo 2, se il servizio cartografico non risponde, il sistema mostra un messaggio e propone l'elenco delle zone (UC-28).
- **E2 – Nessuna zona operativa.** Al passo 3 il sistema comunica che non ci sono zone approvate.

---

## UC-25 – Filtrare la mappa
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-07

| | |
|---|---|
| **Obiettivo** | Restringere la mappa alle zone e agli elementi di interesse. |
| **Precondizioni** | La mappa è visualizzata (UC-24). |
| **Postcondizioni** | La mappa mostra solo zone ed elementi che soddisfano i filtri; i filtri attivi sono indicati. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-24). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Apre il pannello dei filtri. |
| 2 | Sistema | Mostra i filtri: stato, quartiere, tipo di elemento, tipo di lavoro in corso. |
| 3 | Utente | Seleziona uno o più valori. |
| 4 | Sistema | Aggiorna la mappa mostrando solo zone ed elementi corrispondenti e indica i filtri attivi. |

**Flussi alternativi**
- **A1 – Rimozione dei filtri.** L'utente seleziona «Azzera filtri»; il sistema torna alla vista completa.

**Eccezioni**
- **E1 – Nessun risultato.** Al passo 4, se nessuna zona corrisponde, il sistema mostra un messaggio e propone di modificare i filtri.

---

## UC-26 – Visualizzare gli elementi di una zona sulla mappa
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** Servizio cartografico · **RF collegati:** RF-07

| | |
|---|---|
| **Obiettivo** | Vedere i singoli elementi aumentando il livello di dettaglio. |
| **Precondizioni** | La mappa è visualizzata (UC-24). |
| **Postcondizioni** | Sono visualizzati gli elementi dell'area inquadrata con simboli per categoria. |
| **Use Case inclusi** | – |
| **Use Case estesi** | Visualizzare il dettaglio di un elemento. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Ingrandisce la mappa su un'area. |
| 2 | Sistema | Superato il livello di dettaglio previsto, mostra i singoli elementi con simboli e colori diversi per categoria (alberi, fontane, aiuole, giochi…). |
| 3 | Utente | Seleziona un elemento. |
| 4 | Sistema | Mostra categoria, specie, zona di appartenenza, anomalie ed eventuale emergenza. |

**Flussi alternativi**
- **A1 – Zona con composizione sintetica.** Al passo 2, se la zona non ha elementi censiti, il sistema mostra la composizione sintetica nella zona.

**Eccezioni**
- **E1 – Errore di caricamento.** Se gli elementi non possono essere caricati, il sistema mostra solo le zone e un messaggio.

---

## UC-27 – Visualizzare la scheda sintetica di una zona
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-07, RF-08

| | |
|---|---|
| **Obiettivo** | Leggere in sintesi la situazione di una zona direttamente dalla mappa. |
| **Precondizioni** | La mappa è visualizzata (UC-24). |
| **Postcondizioni** | È visualizzata la scheda sintetica della zona. |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-29 Consultare la scheda completa di una zona. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Seleziona una zona sulla mappa. |
| 2 | Sistema | Mostra la scheda sintetica: nome, tipologia, stato con motivazione breve, composizione, ultimi interventi, segnalazioni aperte ed eventuali emergenze. |
| 3 | Utente | Seleziona «Apri scheda completa». |
| 4 | Sistema | Avvia UC-29. |

**Flussi alternativi**
- **A1 – Chiusura.** Al passo 3 l'utente chiude la scheda e torna alla mappa.

**Eccezioni**
- **E1 – Dati non disponibili.** Se i dati della zona non possono essere caricati, il sistema mostra un messaggio di errore.

---

# RF-08 – Consultazione delle aree verdi

## UC-28 – Consultare l'elenco delle zone
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-08

| | |
|---|---|
| **Obiettivo** | Trovare le zone ordinandole per gravità, quartiere o data dell'ultimo intervento. |
| **Precondizioni** | L'utente è autenticato come responsabile o dirigente. |
| **Postcondizioni** | È visualizzato l'elenco delle zone nell'ordine scelto. |
| **Use Case inclusi** | – |
| **Use Case estesi** | Ordinare l'elenco; Cercare una zona per nome; UC-29 Consultare la scheda completa di una zona. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Accede alla sezione «Aree verdi». |
| 2 | Sistema | Mostra l'elenco delle zone con nome, quartiere, tipologia, stato (colore e icona) e data dell'ultimo intervento, ordinato per gravità. |
| 3 | Utente | Sceglie un diverso ordinamento (quartiere, data dell'ultimo intervento) o cerca una zona per nome. |
| 4 | Sistema | Aggiorna l'elenco. |
| 5 | Utente | Seleziona una zona; si avvia UC-29. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Nessuna zona trovata.** Al passo 4 il sistema mostra un messaggio informativo.
- **E2 – Errore di caricamento.** Il sistema mostra un messaggio e propone di riprovare.

---

## UC-29 – Consultare la scheda completa di una zona
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-08, RF-09, RF-10

| | |
|---|---|
| **Obiettivo** | Disporre di tutte le informazioni necessarie per decidere su una zona. |
| **Precondizioni** | L'utente è autenticato come responsabile o dirigente e ha selezionato una zona. |
| **Postcondizioni** | È visualizzata la scheda completa della zona; nessun dato è modificato. |
| **Use Case inclusi** | UC-33 Consultare i consigli di intervento di una zona. |
| **Use Case estesi** | UC-31 Consultare i fattori dello stato; UC-32 Consultare la storia degli stati; UC-35 Decidere su un consiglio (solo Responsabile); UC-41 Consultare il dettaglio di un intervento. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Apre la scheda di una zona dall'elenco o dalla mappa. |
| 2 | Sistema | Mostra in apertura stato, gravità e consigli di intervento correnti con la loro motivazione (UC-33). |
| 3 | Sistema | Per il responsabile, mostra sotto i consigli i comandi decisionali «Avvia lavori», «Rimanda», «Non necessario». |
| 4 | Sistema | Mostra la composizione completa con specie e quantità, lo storico degli interventi della zona, le segnalazioni della zona e gli altri elementi presenti. |
| 5 | Utente | Consulta le sezioni di interesse. |

**Flussi alternativi**
- **A1 – Dirigente.** Al passo 3, per il dirigente i comandi decisionali non sono mostrati.
- **A2 – Nessun consiglio attivo.** Al passo 2 il sistema indica che per la zona non ci sono interventi consigliati.
- **A3 – Stato grigio.** Al passo 2, se la zona è grigia, il sistema indica quali dati mancano o non sono aggiornati.

**Eccezioni**
- **E1 – Errore di caricamento.** Se la scheda non può essere caricata, il sistema mostra un messaggio di errore.
