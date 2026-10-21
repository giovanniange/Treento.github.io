# 4. Descrizione testuale degli Use Case – Parte 2 (RF-09 … RF-15)

---

# RF-09 – Calcolo dello stato delle zone

## UC-30 – Aggiornare lo stato delle zone
**Attore principale:** Responsabile (beneficiario) · **Attori secondari:** Servizio meteorologico · **RF collegati:** RF-09, RF-22, RF-23

L'aggiornamento è avviato dal sistema con la periodicità configurata o al verificarsi di un evento rilevante (acquisizione di segnalazioni, cambio di stato di un intervento, registrazione di un'anomalia, approvazione o modifica di una zona); il responsabile è l'attore che beneficia del risultato.

| | |
|---|---|
| **Obiettivo** | Avere per ogni zona uno stato aggiornato e coerente con i dati disponibili. |
| **Precondizioni** | Esiste almeno una zona operativa; pesi e soglie sono configurati (RF-24). |
| **Postcondizioni** | Ogni zona interessata ha uno stato (verde, giallo, rosso, grigio) e un punteggio di criticità aggiornati con i fattori che li determinano; ogni cambio di stato è conservato nella storia della zona; i passaggi allo stato rosso sono notificati. |
| **Use Case inclusi** | Acquisire i dati meteorologici; Calcolare il punteggio di criticità; Registrare il cambio di stato. |
| **Use Case estesi** | UC-83 Ricevere una notifica (zona passata al rosso). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Avvia l'aggiornamento allo scadere del periodo configurato o al verificarsi di un evento rilevante. |
| 2 | Sistema | Acquisisce dal servizio meteorologico i dati recenti su Trento (piogge, siccità, nevicate, allerte per vento o temporali). |
| 3 | Sistema | Per ogni zona interessata calcola il tempo trascorso dall'ultimo intervento verificato rispetto alla frequenza attesa per tipologia e periodo dell'anno. |
| 4 | Sistema | Considera le segnalazioni aperte per numero, gravità e anzianità, le anomalie sugli elementi e gli interventi attesi dal calendario e non eseguiti. |
| 5 | Sistema | Combina i fattori con i pesi configurati in un punteggio di criticità e lo traduce in stato tramite le soglie. |
| 6 | Sistema | Se lo stato è cambiato, lo registra nella storia della zona insieme ai fattori che lo hanno determinato. |
| 7 | Sistema | Aggiorna mappa, elenco delle zone e dashboard; notifica al responsabile le zone passate al rosso (UC-83). |

**Flussi alternativi**
- **A1 – Dati insufficienti.** Al passo 5, se i dati della zona sono insufficienti o non aggiornati oltre il limite configurato, il sistema assegna lo stato grigio indicando i dati mancanti.
- **A2 – Verifica in corso.** Al passo 5, se nella zona c'è un intervento in attesa di verifica, il sistema mantiene lo stato precedente con l'indicatore di verifica in corso.
- **A3 – Programmazione prevale.** Al passo 4, le segnalazioni collegate a un intervento programmato entro l'intervallo configurato non concorrono al peggioramento dello stato (RF-15).
- **A4 – Emergenze.** Le emergenze su singoli elementi non modificano lo stato della zona (RF-15); restano evidenziate in mappa.
- **A5 – Aggiornamento richiesto manualmente.** Il responsabile richiede il ricalcolo dalla scheda di una zona; il sistema esegue i passi 2–7 per quella zona.

**Eccezioni**
- **E1 – Servizio meteorologico non disponibile.** Al passo 2 il sistema usa gli ultimi dati meteo disponibili, segnala nella motivazione che non sono aggiornati e registra l'anomalia; se i dati superano il limite di aggiornamento, il fattore meteo viene escluso e segnalato.
- **E2 – Errore di calcolo.** Se il calcolo non può essere completato per una zona, il sistema mantiene lo stato precedente, lo segnala come non aggiornato e registra l'errore.

---

## UC-31 – Consultare i fattori dello stato di una zona
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-09

| | |
|---|---|
| **Obiettivo** | Capire perché una zona si trova in un determinato stato. |
| **Precondizioni** | L'utente è autenticato e sta consultando la scheda di una zona (UC-29). |
| **Postcondizioni** | Sono visualizzati punteggio, fattori e soglie che determinano lo stato; nessun dato è modificato. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-29). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Nella scheda zona seleziona «Perché questo stato?». |
| 2 | Sistema | Mostra il punteggio di criticità, la soglia raggiunta e il contributo di ciascun fattore (tempo dall'ultimo intervento rispetto alla frequenza attesa, segnalazioni, meteo, anomalie, scadenze non rispettate) espresso in linguaggio comune. |
| 3 | Sistema | Indica la data dell'ultimo aggiornamento dello stato. |

**Flussi alternativi**
- **A1 – Stato grigio.** Al passo 2 il sistema elenca i dati mancanti o non aggiornati.

**Eccezioni**
- **E1 – Dati non disponibili.** Il sistema mostra un messaggio di errore.

---

## UC-32 – Consultare la storia degli stati di una zona
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-09

| | |
|---|---|
| **Obiettivo** | Vedere come lo stato di una zona è cambiato nel tempo. |
| **Precondizioni** | L'utente sta consultando la scheda di una zona (UC-29). |
| **Postcondizioni** | È visualizzata la sequenza degli stati della zona nel periodo scelto. |
| **Use Case inclusi** | – |
| **Use Case estesi** | Filtrare per periodo. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Nella scheda zona seleziona «Storia degli stati». |
| 2 | Sistema | Mostra in ordine cronologico i cambi di stato con data, stato precedente, nuovo stato e causa principale (es. intervento verificato, nuove segnalazioni). |
| 3 | Utente | Seleziona un periodo. |
| 4 | Sistema | Aggiorna la visualizzazione per il periodo scelto. |

**Flussi alternativi**
- **A1 – Nessun cambio di stato.** Al passo 2 il sistema indica che lo stato non è mai cambiato dal momento dell'approvazione della zona.

**Eccezioni**
- **E1 – Errore di caricamento.** Il sistema mostra un messaggio di errore.

---

# RF-10 – Consigli di intervento

## UC-33 – Consultare i consigli di intervento di una zona
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** Servizio meteorologico · **RF collegati:** RF-10

| | |
|---|---|
| **Obiettivo** | Sapere quali lavori il sistema consiglia per una zona, entro quando e con quale gravità. |
| **Precondizioni** | L'utente è autenticato e sta consultando la scheda di una zona (UC-29). |
| **Postcondizioni** | Sono visualizzati i consigli attivi della zona con motivazione; nessuna azione è avviata. |
| **Use Case inclusi** | Generare i consigli della zona. |
| **Use Case estesi** | UC-34 Consultare la motivazione di un consiglio; UC-35 Decidere su un consiglio (solo Responsabile). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Apre la scheda di una zona. |
| 2 | Sistema | Recupera i consigli attivi della zona; se non sono aggiornati, li rigenera sulla base di meteo dei mesi precedenti, ultimi interventi, segnalazioni, tipologia e composizione della zona. |
| 3 | Sistema | Mostra per ogni consiglio: lavori da eseguire, data entro cui eseguirli, livello di gravità e una motivazione breve in linguaggio comune. |
| 4 | Utente | Seleziona un consiglio per leggerne la motivazione completa (UC-34) o, se responsabile, per decidere (UC-35). |

**Flussi alternativi**
- **A1 – Nessun consiglio.** Al passo 3 il sistema comunica che al momento non ci sono interventi consigliati e indica la prossima scadenza attesa dal calendario.
- **A2 – Consiglio rimandato.** Al passo 3, i consigli rimandati sono mostrati separatamente con la data di riesame e la motivazione del rinvio.

**Eccezioni**
- **E1 – Consigli non disponibili.** Al passo 2, se il sistema non riesce a generare i consigli (es. assistenza non disponibile), mostra lo stato della zona e un messaggio che indica che i consigli non sono al momento disponibili; le altre funzioni della scheda restano utilizzabili.

---

## UC-34 – Consultare la motivazione di un consiglio
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-10

| | |
|---|---|
| **Obiettivo** | Capire su quali dati si basa un consiglio, per fidarsi o contraddirlo con cognizione di causa. |
| **Precondizioni** | È visualizzato almeno un consiglio (UC-33). |
| **Postcondizioni** | Sono visualizzati motivazione completa e dati di supporto del consiglio. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-33). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Seleziona «Perché?» su un consiglio. |
| 2 | Sistema | Mostra la motivazione completa (es. «l'ultimo sfalcio risale a oltre due mesi fa, sono pervenute 3 segnalazioni di erba alta, il periodo è stato molto piovoso»). |
| 3 | Sistema | Mostra i dati di supporto con i collegamenti: ultimi interventi, segnalazioni considerate, dati meteo del periodo, frequenza attesa. |
| 4 | Utente | Apre uno dei dati collegati o torna al consiglio. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Dato di supporto non più disponibile.** Se un dato collegato è stato modificato o archiviato, il sistema lo indica.

---

# RF-11 – Decisione sui consigli

## UC-35 – Decidere su un consiglio
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-11, RF-26

Use Case generale, specializzato da UC-36, UC-37 e UC-38.

| | |
|---|---|
| **Obiettivo** | Registrare una decisione consapevole su una proposta del sistema. |
| **Precondizioni** | Il responsabile è autenticato; è visualizzato un consiglio attivo (UC-33). |
| **Postcondizioni** | Il consiglio non è più in attesa di decisione; il sistema conserva proposta e decisione con autore, data e motivazione. |
| **Use Case inclusi** | Registrare proposta e decisione. |
| **Use Case estesi** | UC-39 Valutare l'utilità di un consiglio. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona un consiglio nella scheda della zona. |
| 2 | Sistema | Mostra i comandi «Avvia lavori», «Rimanda», «Non necessario». |
| 3 | Responsabile | Sceglie la decisione (vedi UC-36, UC-37, UC-38). |
| 4 | Sistema | Registra la proposta originaria e la decisione presa, anche se si discosta dalla proposta. |
| 5 | Sistema | Propone di esprimere un giudizio sull'utilità del consiglio (UC-39). |

**Flussi alternativi**
- **A1 – Annullamento.** Al passo 3 il responsabile annulla; il consiglio resta in attesa di decisione.

**Eccezioni**
- **E1 – Consiglio superato.** Al passo 3, se nel frattempo il consiglio è stato aggiornato o è già stata presa una decisione, il sistema lo segnala e mostra il consiglio aggiornato.
- **E2 – Errore di registrazione.** Al passo 4, se la decisione non può essere registrata, il sistema mostra un messaggio di errore e non esegue alcuna azione conseguente.

---

## UC-36 – Avviare i lavori da un consiglio
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-11, RF-16

| | |
|---|---|
| **Obiettivo** | Trasformare un consiglio in un intervento da realizzare. |
| **Precondizioni** | Quelle di UC-35. |
| **Postcondizioni** | È creato un intervento «in attesa di assegnazione» collegato al consiglio, alla zona e alle segnalazioni considerate; la decisione «avviato» è registrata. |
| **Use Case inclusi** | UC-55 Creare un intervento. |
| **Use Case estesi** | UC-62 Preparare una richiesta alla ditta. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Avvia lavori» su un consiglio. |
| 2 | Sistema | Crea la bozza dell'intervento con zona, elementi, lavori, scadenza e segnalazioni del consiglio (UC-55). |
| 3 | Responsabile | Verifica ed eventualmente modifica i dati dell'intervento, poi conferma. |
| 4 | Sistema | Salva l'intervento, collega le segnalazioni, registra la decisione e chiede se preparare subito la richiesta alla ditta. |
| 5 | Responsabile | Sceglie «Prepara richiesta»; si avvia UC-62. |

**Flussi alternativi**
- **A1 – Richiesta preparata in seguito.** Al passo 5 il responsabile sceglie «Più tardi»; l'intervento resta «in attesa di assegnazione» e compare nella dashboard.

**Eccezioni**
- **E1 – Intervento simile già aperto.** Al passo 2, se esiste già un intervento aperto dello stesso tipo sulla zona, il sistema lo segnala e propone di collegare il consiglio a quell'intervento.

---

## UC-37 – Rimandare un consiglio
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-11

| | |
|---|---|
| **Obiettivo** | Posticipare un intervento consigliato indicando perché e quando riesaminarlo. |
| **Precondizioni** | Quelle di UC-35. |
| **Postcondizioni** | Il consiglio è «rimandato» con motivazione e data di riesame; alla data di riesame il sistema lo ripropone. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Rimanda» su un consiglio. |
| 2 | Sistema | Chiede motivazione e data di riesame, proponendo una data coerente con la scadenza consigliata. |
| 3 | Responsabile | Inserisce motivazione e data e conferma. |
| 4 | Sistema | Registra la decisione e pianifica la riproposizione del consiglio alla data indicata. |

**Flussi alternativi**
- **A1 – Data oltre la scadenza consigliata.** Al passo 3, se la data di riesame supera la scadenza consigliata, il sistema lo segnala e chiede conferma.

**Eccezioni**
- **E1 – Dati mancanti.** Al passo 3, se mancano motivazione o data, il sistema non registra la decisione.

---

## UC-38 – Dichiarare non necessario un intervento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-11

| | |
|---|---|
| **Obiettivo** | Scartare un consiglio ritenuto non necessario, lasciandone traccia. |
| **Precondizioni** | Quelle di UC-35. |
| **Postcondizioni** | Il consiglio è «non necessario» con motivazione; non viene più proposto finché i dati della zona non cambiano in modo significativo. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Non necessario» su un consiglio. |
| 2 | Sistema | Chiede la motivazione (es. lavoro già eseguito fuori sistema, situazione verificata sul posto). |
| 3 | Responsabile | Inserisce la motivazione e conferma. |
| 4 | Sistema | Registra la decisione e rimuove il consiglio da quelli attivi. |

**Flussi alternativi**
- **A1 – Lavoro già eseguito.** Al passo 2 il responsabile indica che il lavoro è già stato eseguito; il sistema propone di registrarlo nello storico con la relativa data.

**Eccezioni**
- **E1 – Motivazione mancante.** Al passo 3 il sistema richiede la motivazione e non procede.

---

## UC-39 – Valutare l'utilità di un consiglio
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-11, RF-21

| | |
|---|---|
| **Obiettivo** | Esprimere un giudizio sul consiglio ricevuto, per valutare e migliorare nel tempo la qualità dei consigli. |
| **Precondizioni** | Il responsabile ha preso una decisione su un consiglio (UC-35). |
| **Postcondizioni** | Il giudizio è registrato ed è utilizzato per l'indicatore di qualità dei consigli. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-35). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Chiede se il consiglio è stato utile (utile / poco utile / non utile) con un commento facoltativo. |
| 2 | Responsabile | Seleziona il giudizio ed eventualmente scrive un commento. |
| 3 | Sistema | Registra il giudizio associandolo al consiglio. |

**Flussi alternativi**
- **A1 – Giudizio non espresso.** Al passo 2 il responsabile salta la valutazione; il consiglio resta valutabile in seguito dallo storico delle decisioni.

**Eccezioni**
- – 

---

# RF-12 – Storico degli interventi

## UC-40 – Ricercare gli interventi nello storico
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-12

| | |
|---|---|
| **Obiettivo** | Trovare gli interventi passati e conoscerne i costi complessivi. |
| **Precondizioni** | L'utente è autenticato come responsabile o dirigente. |
| **Postcondizioni** | È visualizzato l'elenco degli interventi che soddisfano i criteri, con i totali di spesa. |
| **Use Case inclusi** | Calcolare i totali di spesa. |
| **Use Case estesi** | UC-41 Consultare il dettaglio di un intervento; UC-42 Esportare lo storico. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Accede alla sezione «Storico interventi». |
| 2 | Sistema | Mostra gli interventi più recenti e i filtri: zona, ditta, periodo, tipologia di lavoro, stato. |
| 3 | Utente | Imposta uno o più filtri e avvia la ricerca. |
| 4 | Sistema | Mostra gli interventi corrispondenti con zona, tipo, ditta, date, costo preventivato e finale, stato. |
| 5 | Sistema | Mostra i totali di spesa (preventivata e finale) dei risultati. |

**Flussi alternativi**
- **A1 – Ricerca testuale.** Al passo 3 l'utente cerca per parola chiave nelle note e descrizioni; il sistema combina il testo con gli altri filtri.

**Eccezioni**
- **E1 – Nessun risultato.** Al passo 4 il sistema mostra un messaggio e propone di modificare i filtri.
- **E2 – Errore di ricerca.** Il sistema mostra un messaggio di errore.

---

## UC-41 – Consultare il dettaglio di un intervento
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-12, RF-19

| | |
|---|---|
| **Obiettivo** | Vedere tutte le informazioni di un intervento. |
| **Precondizioni** | L'utente ha selezionato un intervento (dallo storico, dalla dashboard, dalla scheda zona o da una notifica). |
| **Postcondizioni** | È visualizzata la scheda dell'intervento. |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-67 Consultare la corrispondenza di un intervento; UC-43 Allegare documenti e fotografie (solo Responsabile). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Seleziona un intervento. |
| 2 | Sistema | Mostra zona ed elementi coinvolti, tipo di lavoro, ditta, date di inizio e fine, scadenza, costo preventivato e finale, stato di avanzamento e relativa cronologia. |
| 3 | Sistema | Mostra fotografie prima e dopo, documenti allegati, note, segnalazioni e consiglio collegati, persona che ha richiesto ed eventuale persona che ha approvato il lavoro, esito della verifica. |
| 4 | Utente | Apre un documento, una fotografia o la corrispondenza. |

**Flussi alternativi**
- **A1 – Intervento importato.** Al passo 2, per gli interventi importati dallo storico (RF-13) il sistema indica l'origine dei dati e i campi non disponibili.

**Eccezioni**
- **E1 – Allegato non disponibile.** Al passo 4, se un allegato non può essere aperto, il sistema lo segnala.

---

## UC-42 – Esportare lo storico
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-12

| | |
|---|---|
| **Obiettivo** | Ottenere i risultati di una ricerca in forma tabellare o come documento, per esempio per un riepilogo alla dirigenza. |
| **Precondizioni** | È visualizzato l'elenco dei risultati di una ricerca (UC-40). |
| **Postcondizioni** | L'utente dispone di un file con gli interventi selezionati e i totali; l'esportazione è registrata. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-40). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Seleziona «Esporta». |
| 2 | Sistema | Chiede la forma di esportazione: tabella oppure documento di riepilogo. |
| 3 | Utente | Sceglie la forma e conferma. |
| 4 | Sistema | Genera il file con gli interventi filtrati, i filtri applicati e i totali di spesa, e lo rende disponibile allo scaricamento. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Nessun intervento da esportare.** Al passo 1, se l'elenco è vuoto, il sistema non genera il file e lo segnala.
- **E2 – Errore di generazione.** Al passo 4 il sistema mostra un messaggio di errore.

---

## UC-43 – Allegare documenti e fotografie a un intervento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-12, RF-20

| | |
|---|---|
| **Obiettivo** | Completare la documentazione di un intervento (preventivi, fatture, fotografie prima e dopo). |
| **Precondizioni** | Il responsabile è autenticato ed è visualizzato il dettaglio di un intervento (UC-41). |
| **Postcondizioni** | I file sono associati all'intervento con tipo, data e autore del caricamento. |
| **Use Case inclusi** | Verificare il tipo di file. |
| **Use Case estesi** | Aggiornare il costo finale. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Aggiungi allegato». |
| 2 | Sistema | Chiede il tipo di allegato (preventivo, fattura, foto prima, foto dopo, altro documento) e il file. |
| 3 | Responsabile | Seleziona tipo e file e conferma. |
| 4 | Sistema | Verifica il tipo e la dimensione del file, lo associa all'intervento e registra l'operazione. |

**Flussi alternativi**
- **A1 – Fattura con costo finale.** Al passo 3, se l'allegato è una fattura, il sistema propone di aggiornare il costo finale dell'intervento.

**Eccezioni**
- **E1 – File non accettato.** Al passo 4, se il file non è di un tipo ammesso o è troppo grande, il sistema lo rifiuta indicandone il motivo.

---

# RF-13 – Importazione dei dati storici

## UC-44 – Importare i dati storici
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-13, RF-12

| | |
|---|---|
| **Obiettivo** | Portare nel sistema i lavori già eseguiti in possesso del Comune, associati alle zone. |
| **Precondizioni** | L'amministratore è autenticato; le zone sono state approvate (almeno in parte); è disponibile il file dei lavori storici (CLAR-06). |
| **Postcondizioni** | I lavori importati sono presenti nello storico e associati alle zone; i record non associabili sono in attesa di correzione; lo stato delle zone è ricalcolato; l'importazione è registrata. |
| **Use Case inclusi** | Verificare il formato del file; Normalizzare i record; Associare i lavori alle zone; UC-30 Aggiornare lo stato delle zone. |
| **Use Case estesi** | UC-45 Correggere i record non associati. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Accede a «Importazione storico» e carica il file dei lavori. |
| 2 | Sistema | Verifica il formato e mostra la corrispondenza proposta tra le colonne del file e i campi dello storico. |
| 3 | Amministratore | Conferma o corregge la corrispondenza dei campi. |
| 4 | Sistema | Normalizza i record (date, importi, tipologie di lavoro, nomi delle ditte). |
| 5 | Sistema | Propone per ogni lavoro la zona sulla base delle indicazioni testuali di luogo. |
| 6 | Sistema | Mostra il riepilogo: record associati, record con associazione incerta, record non associati o non validi. |
| 7 | Amministratore | Conferma il consolidamento dei record associati. |
| 8 | Sistema | Inserisce i lavori nello storico, ricalcola lo stato delle zone interessate (UC-30) e registra l'importazione. |

**Flussi alternativi**
- **A1 – Record da correggere.** Al passo 6, se ci sono record incerti o non associati, l'amministratore avvia UC-45 prima di consolidare.
- **A2 – Record duplicati.** Al passo 4, se un lavoro risulta già presente nello storico, il sistema lo segnala come duplicato e non lo importa salvo conferma.

**Eccezioni**
- **E1 – File non leggibile.** Al passo 2 il sistema rifiuta il file indicando il motivo.
- **E2 – Errore durante il consolidamento.** Al passo 8 il sistema annulla l'intera importazione e mostra un messaggio di errore; lo storico resta invariato.

---

## UC-45 – Correggere i record non associati
**Attore principale:** Amministratore · **Attori secondari:** – · **RF collegati:** RF-13

| | |
|---|---|
| **Obiettivo** | Associare a una zona o normalizzare i record che il sistema non è riuscito a trattare automaticamente. |
| **Precondizioni** | È in corso un'importazione con record incerti o non associati (UC-44). |
| **Postcondizioni** | Ogni record corretto è pronto per il consolidamento; i record scartati sono esclusi con motivazione. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – (estende UC-44). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Amministratore | Apre l'elenco dei record da correggere. |
| 2 | Sistema | Mostra per ciascun record il testo originale, l'eventuale zona proposta e il problema riscontrato. |
| 3 | Amministratore | Sceglie la zona corretta e/o corregge i campi non validi. |
| 4 | Sistema | Valida il record e lo segna come pronto. |
| 5 | Amministratore | Ripete i passi 3–4 e torna a UC-44 per il consolidamento. |

**Flussi alternativi**
- **A1 – Record scartato.** Al passo 3 l'amministratore scarta il record indicandone il motivo.
- **A2 – Correzione multipla.** Al passo 3 l'amministratore applica la stessa zona a tutti i record con la stessa descrizione di luogo.

**Eccezioni**
- **E1 – Dati ancora non validi.** Al passo 4 il sistema segnala i campi ancora non validi.

---

# RF-14 – Acquisizione delle segnalazioni

## UC-46 – Acquisire le segnalazioni
**Attore principale:** Responsabile (beneficiario) · **Attori secondari:** Portale segnalazioni · **RF collegati:** RF-14, RF-15

L'acquisizione è avviata dal sistema con il periodo configurato (ipotesi: ogni 2 giorni, massimo 7 – CLAR-04); il responsabile è l'attore che ne beneficia.

| | |
|---|---|
| **Obiettivo** | Disporre delle segnalazioni sul verde provenienti dal portale del Comune, senza inserirle a mano. |
| **Precondizioni** | Il collegamento con il portale delle segnalazioni è configurato. |
| **Postcondizioni** | Le nuove segnalazioni sul verde sono presenti in stato «nuova», associate alla zona, classificate e raggruppate; le emergenze sono state notificate; lo stato delle zone è aggiornato; l'acquisizione è registrata. |
| **Use Case inclusi** | Filtrare le segnalazioni sul verde; Associare la segnalazione alla zona; Classificare tipologia e urgenza; Riconoscere i duplicati; Applicare la regola «la programmazione prevale»; UC-30 Aggiornare lo stato delle zone. |
| **Use Case estesi** | Notificare un'emergenza (UC-83). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Sistema | Allo scadere del periodo configurato richiede al portale le segnalazioni pervenute dall'ultima acquisizione. |
| 2 | Portale segnalazioni | Restituisce le segnalazioni. |
| 3 | Sistema | Seleziona quelle relative al verde e ne conserva solo i dati necessari (testo, fotografia, posizione, data) (RNF-09). |
| 4 | Sistema | Associa ogni segnalazione alla zona in base alla posizione e, se possibile, all'elemento interessato. |
| 5 | Sistema | Stima tipologia e urgenza e raggruppa le segnalazioni che riguardano lo stesso problema. |
| 6 | Sistema | Collega a un intervento già programmato entro l'intervallo configurato le segnalazioni sullo stesso problema («la programmazione prevale»). |
| 7 | Sistema | Aggiorna lo stato delle zone interessate (UC-30). |
| 8 | Sistema | Registra l'acquisizione con il numero di segnalazioni acquisite e notifica al responsabile le nuove segnalazioni. |

**Flussi alternativi**
- **A1 – Emergenza.** Al passo 5, se una segnalazione è classificata come emergenza, il sistema notifica subito il responsabile con priorità alta e contrassegna in emergenza l'elemento interessato o la posizione segnalata, senza modificare lo stato della zona (RF-15); il responsabile la gestisce con UC-54.
- **A2 – Nessuna nuova segnalazione.** Al passo 2, se non ci sono nuove segnalazioni, il sistema registra l'acquisizione e termina.
- **A3 – Posizione esterna alle zone.** Al passo 4, se la posizione non ricade in alcuna zona, la segnalazione resta «nuova» senza zona e viene evidenziata al responsabile per l'associazione manuale (UC-50).

**Eccezioni**
- **E1 – Portale non raggiungibile.** Al passo 2 il sistema registra l'errore, ritenta secondo la configurazione e, se l'errore persiste, avvisa il responsabile e l'amministratore; l'acquisizione successiva recupera tutte le segnalazioni non ancora acquisite.
- **E2 – Segnalazione non leggibile.** Al passo 3, se una segnalazione è incompleta o non interpretabile, il sistema la acquisisce come «da classificare» e la segnala al responsabile.

---

## UC-47 – Richiedere un'acquisizione immediata
**Attore principale:** Responsabile · **Attori secondari:** Portale segnalazioni · **RF collegati:** RF-14

| | |
|---|---|
| **Obiettivo** | Aggiornare le segnalazioni fuori dal ciclo periodico (es. dopo un temporale). |
| **Precondizioni** | Il responsabile è autenticato; non è in corso un'altra acquisizione. |
| **Postcondizioni** | Quelle di UC-46; il ciclo periodico riparte dalla data di questa acquisizione. |
| **Use Case inclusi** | UC-46 Acquisire le segnalazioni. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Nella sezione «Segnalazioni» seleziona «Aggiorna ora». |
| 2 | Sistema | Mostra la data dell'ultima acquisizione e chiede conferma. |
| 3 | Responsabile | Conferma. |
| 4 | Sistema | Esegue UC-46 e mostra al termine il numero di nuove segnalazioni, evidenziando le eventuali emergenze. |

**Flussi alternativi**
- – 

**Eccezioni**
- **E1 – Acquisizione già in corso.** Al passo 2 il sistema informa che è già in corso un'acquisizione e mostra l'avanzamento.
- **E2 – Portale non raggiungibile.** Come UC-46 E1; il sistema informa il responsabile dell'esito negativo.

---

# RF-15 – Gestione e classificazione delle segnalazioni

## UC-48 – Consultare le segnalazioni
**Attore principale:** Responsabile, Dirigente · **Attori secondari:** – · **RF collegati:** RF-15

| | |
|---|---|
| **Obiettivo** | Sapere quali problemi segnalano i cittadini, dove e con quale urgenza. |
| **Precondizioni** | L'utente è autenticato come responsabile o dirigente. |
| **Postcondizioni** | È visualizzato l'elenco delle segnalazioni richieste. |
| **Use Case inclusi** | – |
| **Use Case estesi** | Filtrare le segnalazioni; Visualizzare il dettaglio di una segnalazione; UC-49 … UC-53 (solo Responsabile). |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Utente | Accede alla sezione «Segnalazioni». |
| 2 | Sistema | Mostra l'elenco delle segnalazioni con data, zona, tipologia stimata, urgenza, stato (nuova, presa in carico, collegata a un intervento, chiusa) e indicazione dei gruppi di duplicati; le emergenze sono in evidenza. |
| 3 | Utente | Filtra per zona, stato, tipologia, urgenza o periodo. |
| 4 | Sistema | Aggiorna l'elenco. |
| 5 | Utente | Seleziona una segnalazione. |
| 6 | Sistema | Mostra testo, fotografia, posizione sulla mappa, data, classificazione, segnalazioni dello stesso gruppo ed eventuali interventi collegati. |

**Flussi alternativi**
- **A1 – Dirigente.** Al passo 6, per il dirigente non sono mostrati i comandi di gestione.
- **A2 – Dati personali.** Al passo 6, gli eventuali dati personali del segnalante sono mostrati solo ai ruoli autorizzati (RNF-09).

**Eccezioni**
- **E1 – Nessuna segnalazione.** Al passo 4 il sistema mostra un messaggio informativo.

---

## UC-49 – Prendere in carico una segnalazione
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-15, RF-21

| | |
|---|---|
| **Obiettivo** | Indicare che una segnalazione è in gestione. |
| **Precondizioni** | Il responsabile è autenticato ed è visualizzata una segnalazione in stato «nuova». |
| **Postcondizioni** | La segnalazione è «presa in carico» con data e autore; la data concorre al calcolo del tempo di risposta. |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-52 Collegare una segnalazione a un intervento. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Prendi in carico» sulla segnalazione. |
| 2 | Sistema | Aggiorna lo stato, registra data e autore e lo applica all'intero gruppo di duplicati, se presente. |
| 3 | Sistema | Propone di collegare la segnalazione a un intervento esistente o di crearne uno nuovo. |

**Flussi alternativi**
- **A1 – Presa in carico multipla.** Al passo 1 il responsabile seleziona più segnalazioni; il sistema le prende in carico tutte.

**Eccezioni**
- **E1 – Segnalazione già presa in carico.** Il sistema lo segnala indicando da chi e quando.

---

## UC-50 – Correggere la classificazione di una segnalazione
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-15, RF-09

| | |
|---|---|
| **Obiettivo** | Correggere zona, elemento, tipologia o urgenza stimate dal sistema. |
| **Precondizioni** | Il responsabile è autenticato ed è visualizzata una segnalazione non chiusa. |
| **Postcondizioni** | La classificazione è aggiornata e registrata insieme a quella proposta dal sistema; lo stato della zona è ricalcolato. |
| **Use Case inclusi** | UC-30 Aggiornare lo stato delle zone. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Modifica classificazione». |
| 2 | Sistema | Mostra zona, elemento, tipologia e urgenza correnti. |
| 3 | Responsabile | Modifica i valori e conferma. |
| 4 | Sistema | Salva la classificazione, conserva la proposta originaria, ricalcola lo stato delle zone interessate e registra l'operazione. |

**Flussi alternativi**
- **A1 – Classificata come emergenza.** Al passo 3, se il responsabile imposta l'urgenza a «emergenza», il sistema contrassegna l'elemento o la posizione come in emergenza e propone UC-54.
- **A2 – Segnalazione non pertinente.** Al passo 3 il responsabile indica che la segnalazione non riguarda il verde; il sistema propone di chiuderla (UC-53).

**Eccezioni**
- **E1 – Zona non valida.** Al passo 4, se la posizione non è compatibile con la zona scelta, il sistema chiede conferma.

---

## UC-51 – Gestire un gruppo di segnalazioni duplicate
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-15

| | |
|---|---|
| **Obiettivo** | Evitare di gestire più volte lo stesso problema segnalato da più cittadini. |
| **Precondizioni** | Il responsabile è autenticato; esistono segnalazioni raggruppate dal sistema o simili tra loro. |
| **Postcondizioni** | Il gruppo è confermato o modificato; le segnalazioni dello stesso gruppo condividono stato e interventi collegati. |
| **Use Case inclusi** | – |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Apre un gruppo proposto dal sistema. |
| 2 | Sistema | Mostra le segnalazioni del gruppo con testo, foto e posizione sulla mappa e il motivo del raggruppamento. |
| 3 | Responsabile | Conferma il gruppo. |
| 4 | Sistema | Registra il gruppo; da questo momento stato e collegamenti sono condivisi dalle segnalazioni del gruppo. |

**Flussi alternativi**
- **A1 – Separazione.** Al passo 3 il responsabile esclude una o più segnalazioni dal gruppo; il sistema le rende indipendenti.
- **A2 – Unione manuale.** Il responsabile seleziona segnalazioni non raggruppate e sceglie «Unisci»; il sistema crea il gruppo.

**Eccezioni**
- **E1 – Stati incompatibili.** Al passo 4, se le segnalazioni sono collegate a interventi diversi, il sistema chiede quale intervento mantenere.

---

## UC-52 – Collegare una segnalazione a un intervento
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-15, RF-16, RF-21

| | |
|---|---|
| **Obiettivo** | Associare la segnalazione al lavoro che la risolve. |
| **Precondizioni** | Il responsabile è autenticato ed è visualizzata una segnalazione non chiusa. |
| **Postcondizioni** | La segnalazione (o il suo gruppo) è «collegata a un intervento»; alla verifica positiva dell'intervento potrà essere chiusa. |
| **Use Case inclusi** | – |
| **Use Case estesi** | UC-56 Creare un intervento manualmente. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Collega a intervento». |
| 2 | Sistema | Mostra gli interventi aperti o programmati sulla stessa zona, a partire da quelli dello stesso tipo. |
| 3 | Responsabile | Seleziona l'intervento e conferma. |
| 4 | Sistema | Collega la segnalazione, aggiorna lo stato e registra l'operazione. |

**Flussi alternativi**
- **A1 – Nessun intervento adatto.** Al passo 2 il responsabile sceglie «Crea nuovo intervento»; si avvia UC-56 con la segnalazione precompilata.

**Eccezioni**
- **E1 – Intervento non più aperto.** Al passo 4, se l'intervento è stato chiuso nel frattempo, il sistema lo segnala.

---

## UC-53 – Chiudere una segnalazione
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-15, RF-21

| | |
|---|---|
| **Obiettivo** | Concludere la gestione di una segnalazione. |
| **Precondizioni** | Il responsabile è autenticato ed è visualizzata una segnalazione non chiusa. |
| **Postcondizioni** | La segnalazione (o il gruppo) è «chiusa» con motivazione e data; la data concorre al tempo di risposta; lo stato della zona è ricalcolato. |
| **Use Case inclusi** | UC-30 Aggiornare lo stato delle zone. |
| **Use Case estesi** | – |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Seleziona «Chiudi segnalazione». |
| 2 | Sistema | Chiede la motivazione: risolta da intervento, non pertinente, già risolta, duplicata. |
| 3 | Responsabile | Sceglie la motivazione ed eventualmente aggiunge una nota. |
| 4 | Sistema | Chiude la segnalazione, ricalcola lo stato della zona e registra l'operazione. |

**Flussi alternativi**
- **A1 – Chiusura automatica.** Quando un intervento collegato viene verificato con esito positivo (UC-73, UC-74), il sistema propone la chiusura delle segnalazioni collegate con motivazione «risolta da intervento».

**Eccezioni**
- **E1 – Intervento collegato non concluso.** Al passo 3, se si sceglie «risolta da intervento» ma l'intervento non è verificato, il sistema lo segnala e chiede conferma.

---

## UC-54 – Gestire un'emergenza
**Attore principale:** Responsabile · **Attori secondari:** – · **RF collegati:** RF-15, RF-07, RF-23

| | |
|---|---|
| **Obiettivo** | Valutare rapidamente un'emergenza segnalata (es. albero pericolante, ramo caduto) e decidere come intervenire. |
| **Precondizioni** | Il responsabile è autenticato; esiste una segnalazione classificata come emergenza, notificata con priorità alta. |
| **Postcondizioni** | L'emergenza è presa in carico e gestita con un intervento urgente oppure chiusa con motivazione; l'evidenza in mappa è rimossa alla chiusura; ogni decisione è registrata. Lo stato della zona non viene modificato automaticamente dall'emergenza. |
| **Use Case inclusi** | UC-49 Prendere in carico una segnalazione. |
| **Use Case estesi** | UC-57 Creare un intervento urgente da un'emergenza; Chiudere l'emergenza. |

**Flusso principale**

| # | Attore | Azione |
|---|---|---|
| 1 | Responsabile | Apre la notifica di emergenza o seleziona il simbolo di emergenza sulla mappa. |
| 2 | Sistema | Mostra la segnalazione con testo, foto, posizione, elemento interessato, eventuali segnalazioni dello stesso gruppo e interventi già aperti sull'elemento. |
| 3 | Responsabile | Prende in carico l'emergenza (UC-49). |
| 4 | Sistema | Registra la presa in carico e la indica sulla mappa. |
| 5 | Responsabile | Decide di intervenire e avvia UC-57. |
| 6 | Sistema | Collega l'intervento urgente all'emergenza e mantiene l'evidenza in mappa fino alla chiusura dell'intervento. |

**Flussi alternativi**
- **A1 – Emergenza non confermata.** Al passo 5 il responsabile, dopo una verifica, ritiene che non si tratti di un'emergenza: chiude l'emergenza indicando il motivo oppure la riclassifica come segnalazione ordinaria (UC-50); il sistema rimuove l'evidenza in mappa.
- **A2 – Intervento già in corso.** Al passo 2, se esiste già un intervento aperto sull'elemento, il responsabile collega l'emergenza a quell'intervento (UC-52).

**Eccezioni**
- **E1 – Emergenza già gestita.** Al passo 3, se l'emergenza è già stata presa in carico da un altro responsabile, il sistema lo segnala indicando chi la sta gestendo.
