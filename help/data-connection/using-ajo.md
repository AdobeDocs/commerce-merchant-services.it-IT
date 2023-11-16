---
title: Utilizza Adobe Journey Optimizer per inviare un’e-mail con carrello abbandonato
description: Scopri come utilizzare Adobe Journey Optimizer per inviare un’e-mail con carrello abbandonato.
role: Admin, Developer
feature: Personalization, Integration
exl-id: 5e4e7c0a-c00b-4278-bd73-6b6f2fcbe770
source-git-commit: f90ef4d2732a0b0676e0899712f94b41a1c2d85a
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%

---

# Utilizzare Adobe Journey Optimizer per inviare un messaggio e-mail per carrello abbandonato

[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html) ti consente di personalizzare l’esperienza di e-commerce per i tuoi acquirenti. Ad esempio, puoi utilizzare Journey Optimizer per creare e distribuire campagne di marketing pianificate, come le promozioni settimanali di un negozio al dettaglio, o generare un’e-mail abbandonato nel carrello se un cliente ha aggiunto un prodotto a un carrello ma non lo ha completato.

Seguendo questi passaggi, puoi imparare ad ascoltare un `checkout` generato dalla tua istanza Commerce e rispondere a tale evento in Journey Optimizer per generare un’e-mail del carrello abbandonata.

>[!IMPORTANT]
>
>A scopo dimostrativo, assicurati di utilizzare il tuo ambiente sandbox Commerce. In questo modo, i dati dell’evento di vetrina e di back office inviati ad Experienci Platform non diluiscono i dati dell’evento di produzione.

## Prerequisiti

Prima di iniziare con questi passaggi, assicurati:

- È stato eseguito il provisioning per utilizzare Adobe Journey Optimizer
- Tu [configurato](connect-data.md) il [!DNL Data Connection] estensione
- Tu [confermato](connect-data.md#confirm-that-event-data-is-collected) che i dati dell’evento Commerce arrivino al server Edge di Experienci Platform

## Passaggio 1: creare un utente nell’ambiente sandbox di Commerce

Crea un utente nell’ambiente sandbox e verifica che le informazioni sull’account utente siano visualizzate in Experience Platform. Verifica che l’e-mail specificata sia valida, poiché verrà utilizzata più avanti in questa sezione per inviare l’e-mail del carrello abbandonato.

1. Accedi o crea un account nell’ambiente sandbox di Commerce.

   ![Accedi al tuo account di prova](assets/sign-in-account.png){width="700" zoomable="yes"}

   Con il [!DNL Data Connection] installata e configurata, queste informazioni sull’account vengono inviate all’Experience Platform come profilo.

1. Conferma che le informazioni sull’account utente vengano visualizzate nel **[!UICONTROL Profile]** Experience Platform.

   Vai a **[!UICONTROL Profiles]** in Adobe Experience Platform. Clic **[!UICONTROL Detail]** nel profilo per visualizzare il profilo creato.

   ![Conferma profilo](assets/check-event-profile.png){width="700" zoomable="yes"}

## Passaggio 2: visualizzare gli eventi in Journey Optimizer

Nell’ambiente sandbox di Commerce, puoi visualizzare le pagine dei prodotti, aggiungere articoli al carrello e varie altre attività che un acquirente eseguirebbe. Queste attività attivano gli eventi sulla vetrina. Ora puoi confermare che questi eventi fluiscono in Journey Optimizer.

1. Launch [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html).
1. Seleziona **[!UICONTROL Profiles]**.
1. Imposta **[!UICONTROL Identity namespace]** a `Email`.
1. Imposta il **[!UICONTROL Identity value]** al tuo indirizzo e-mail.
1. Seleziona il tuo profilo, quindi fai clic su **[!UICONTROL Events]** scheda.

   ![Controlla dettagli evento](assets/check-event-details.png){width="700" zoomable="yes"}

   Cerca `commerce.checkouts` ed esaminare il payload dell’evento:

   ```json
   "personID": "84281643067178465783746543501073369488", 
   "eventType": "commerce.checkouts", 
   "_id": "4b41703f-e42e-485b-8d63-7001e3580856-0", 
   "commerce": { 
       "cart": {}, 
       "checkouts": { 
           "value": 1 
       } 
   ```

   Come puoi vedere, il payload completo dell’evento contiene dati dettagliati sull’evento. Nella sezione successiva, configurerai gli eventi in Journey Optimizer per l’ascolto e la risposta al `commerce.checkouts` evento generato dalla vetrina Commerce.

## Passaggio 3: configurare gli eventi in Journey Optimizer

Configura due eventi in Journey Optimizer: un evento è in ascolto del `commerce.checkouts` l’altro è un evento di timeout di base che attende un periodo di tempo specifico prima di attivare un’e-mail del carrello abbandonata.

### Creare un evento listener

1. Launch [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html).

1. Clic **[!UICONTROL Configurations]** sotto **[!UICONTROL Administration]** sezione del riquadro sinistro.

1. In **[!UICONTROL Events]** riquadro, fai clic su **[!UICONTROL Manage]**.

   ![Configurazione evento Journey Optimizer](assets/ajo-config.png){width="700" zoomable="yes"}

1. Il giorno **[!UICONTROL Events]** pagina, fai clic su **[!UICONTROL Create Event]**.

1. Nella navigazione corretta, imposta l’evento come segue:

   1. Imposta il **[!UICONTROL Name]** a: `firstname_lastname_checkout`.
   1. Imposta **[!UICONTROL Type]** a **[!UICONTROL Unitary]**.
   1. Imposta **[!UICONTROL Event id typ]e** a **[!UICONTROL Rule based]**.
   1. Imposta **[!UICONTROL Schema]** al tuo Commerce [schema](update-xdm.md).
   1. Seleziona **[!UICONTROL Fields]** e nella **[!UICONTROL Fields]** nella pagina visualizzata, seleziona i campi utili per l’evento. Ad esempio, seleziona tutti i campi sotto il **[!UICONTROL Product list items]**, **[!UICONTROL Commerce]**, **[!UICONTROL eventType]**, e **[!UICONTROL Web]**.
   1. Clic **[!UICONTROL OK]** per salvare i campi selezionati.
   1. Fai clic all’interno del **[!UICONTROL Event id condition]** e crea una condizione di `eventType` è uguale a `commerce.checkouts` E `personalEmail.address` è uguale all’indirizzo e-mail utilizzato al momento della creazione del profilo nella sezione precedente.

      ![Imposta condizione Journey Optimizer](assets/ajo-set-condition.png){width="700" zoomable="yes"}

   1. Clic **[!UICONTROL OK]**.
   1. Clic **[!UICONTROL Save]** per salvare l’evento.

### Creare un evento di timeout

1. Crea un evento in Journey Optimizer come hai fatto in precedenza.

1. Nella navigazione corretta, imposta l’evento come segue:

   1. Imposta il **[!UICONTROL Name]** a: `firstname_lastname_timeout`.
   1. Imposta **[!UICONTROL Type]** a **[!UICONTROL Unitary]**.
   1. Imposta **[!UICONTROL Event id typ]e** a **[!UICONTROL Rule based]**.
   1. Imposta **[!UICONTROL Schema]** al tuo Commerce [schema](update-xdm.md).
   1. Imposta il **[!UICONTROL Schema]**, **[!UICONTROL Fields]**, e **[!UICONTROL Event id condition]** come sopra.
   1. Clic **[!UICONTROL Save]** per salvare l’evento.

Con questi due eventi configurati, crea un percorso che invia un’e-mail del carrello abbandonata.

## Passaggio 4: creare un percorso di pagamento

Creare un percorso che ascolti `commerce.checkouts` e invia un’e-mail del carrello abbandonato dopo un determinato periodo di tempo.

1. In Journey Optimizer, seleziona **[!UICONTROL Journeys]** in **J[!UICONTROL OURNEY MANAGEMENT]**.
1. Clic **[!UICONTROL Create Journey]**.
1. Specifica il nome del percorso.
1. Clic **[!UICONTROL OK]** per salvare il percorso.
1. Nella barra di navigazione a sinistra sotto **[!UICONTROL EVENTS]** , cerca l’evento di estrazione creato in precedenza: `firstname_lastname_checkout` e trascinalo sull’area di lavoro.

   >[!TIP]
   >
   >Facendo doppio clic sull’evento, questo viene aggiunto automaticamente all’area di lavoro.

1. Cerca l’evento timeout e aggiungilo all’area di lavoro.
1. Fare doppio clic sull&#39;evento di timeout.

   1. In **[!UICONTROL Timeout]** , seleziona la sezione **[!UICONTROL Define the event time]** casella di controllo.
   1. In **[!UICONTROL Wait for]** immissione campo `1` e `Minute`.
   1. Seleziona la **[!UICONTROL Set a timeout path]** casella di controllo.

   Con questa configurazione di timeout, un acquirente che esegue un pagamento ma non completa l’ordine entro un minuto attiva questo ramo di timeout. In un ambiente di produzione effettivo, imposterai questo valore per un periodo più lungo, ad esempio 24 ore.

1. Nella barra di navigazione a sinistra sotto **[!UICONTROL ACTIONS]**, aggiungi **[!UICONTROL Email]** azione al ramo timeout. Il percorso deve essere simile al seguente:

   ![Area di lavoro Journey Optimizer](assets/ajo-canvas.png){width="700" zoomable="yes"}

### Creare un messaggio e-mail per carrello abbandonato

Crea un’e-mail carrello abbandonata che viene inviata quando viene rilevato un carrello abbandonato.

1. Nel percorso creato in precedenza, fare doppio clic su **[!UICONTROL Email]** nell’area di lavoro.

1. Segui le [passaggi](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/personalization/personalization-use-cases/personalization-use-case-helper-functions.html#configure-email) nella guida di Journey Optimizer per creare l’e-mail del carrello abbandonato.

Ora disponi di un percorso in Journey Optimizer che ascolta `commerce.checkouts` dal tuo punto vendita Commerce e un’e-mail del carrello abbandonata, inviata dopo un certo periodo di tempo. Nella sezione successiva verrà eseguito il test del percorso.

## Passaggio 5: attivare l’evento di pagamento in tempo reale

In questa sezione l’evento viene testato in tempo reale.

1. In Journey Optimizer, attiva la modalità di test.

   ![Abilita modalità di test](assets/ajo-enable-test.png){width="700" zoomable="yes"}

1. Per testare questo percorso in tempo reale, apri un’altra scheda del browser e passa al sito web di Commerce sandbox.

   1. Aggiungi un prodotto al carrello.
   1. Passa alla pagina di pagamento.
   1. Dalla pagina di pagamento, abbandona il carrello tornando alla pagina principale o chiudendo la scheda.

      Il percorso è ora attivato. Per confermare, apri la scheda con il percorso in Journey Optimizer. Dovresti trovare una freccia verde che mostra il percorso attraversato dall’utente.

1. Controlla la casella in entrata dell’e-mail.
