---
title: Rapporto Stato pagamento ordine
description: Utilizzare il rapporto Stato pagamento ordine per ottenere visibilità sullo stato di pagamento degli ordini e identificare eventuali problemi.
role: User
level: Intermediate
exl-id: 192e47b9-d52b-4dcf-a720-38459156fda4
feature: Payments, Checkout, Orders
source-git-commit: 0dc370409ace6ac6b0a56511cd0071cf525620f1
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 0%

---

# Rapporto Stato pagamento ordine

[!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] offre funzioni di reporting complete per ottenere una visione più chiara delle [transazioni](transactions.md), ordini e pagamenti.

Sono disponibili due visualizzazioni per la generazione di rapporti sullo stato dei pagamenti degli ordini per consentirti di visualizzare rapidamente lo stato dei pagamenti degli ordini:

* **[Visualizzazione stato pagamento ordine](#order-payment-status-data-visualization-view)**- Grafico disponibile nella home di Payment Services che è una rappresentazione visiva degli stati di pagamento aggregati al giorno dalla vista del rapporto Stato pagamento ordine
* **[Visualizzazione report stato pagamento ordine](#order-payment-status-report-view)**- Rapporto disponibile nello stato Pagamento ordine che mostra gli stati dettagliati di pagamento, fatturazione, spedizione, rimborso e controversia per tutte le transazioni

Le visualizzazioni dello stato del pagamento dell&#39;ordine consentono di comprendere facilmente la posizione di un ordine specifico all&#39;interno del flusso di elaborazione del contante dell&#39;ordine. Questi rapporti ti consentono di visualizzare rapidamente gli ordini in base allo stato e alla data di pagamento, identificando eventuali problemi.

È possibile [scarica stati di pagamento ordine](#download-order-payment-statuses) in un formato di file .csv da utilizzare nel software di contabilità o di gestione degli ordini esistente.

>[!NOTE]
>
>Non è possibile visualizzare i rapporti finanziari se non [Modalità Live onboarded e attivata](production.md#enable-live-payments) per [!DNL Payment Services].

## Visualizzazione dati stato pagamento ordine

La visualizzazione dei dati sullo stato del pagamento dell&#39;ordine è disponibile nella Home page di Payment Services. Rappresenta visivamente gli stati dei pagamenti aggregati al giorno dalla tabella dettagliata. [Visualizzazione report stato pagamento ordine](#order-payment-status-report-view).

Il giorno _Amministratore_ barra laterale, vai a **Vendite** > **Servizi di pagamento** > _Ordini_ per visualizzare la visualizzazione dati [stati piano di pagamento](#statuses-information).

![Visualizzazione dei dati di pagamento nell’Amministratore](assets/orderpayment-dataviz.png){width="800" zoomable="yes"}

Clic **[!UICONTROL View Report]** per passare alla tabella dettagliata [Visualizzazione report stato pagamento ordine](#order-payment-status-report-view).

### Personalizzare gli stati nell’arco temporale

Per impostazione predefinita, vengono visualizzati 30 giorni di stato del pagamento.

Nella vista Visualizzazione stato pagamento ordine è possibile personalizzare l&#39;intervallo di tempo per gli stati di pagamento che si desidera visualizzare selezionando un intervallo di date:

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**. La visualizzazione dei dati di stato del pagamento dell&#39;ordine è visibile nella _Ordini_ sezione.
1. Fai clic su **[!UICONTROL Range]** filtro di selezione.
1. Scegliere l&#39;intervallo di date applicabile: 30 giorni, 15 giorni o 7 giorni.
1. Visualizza le informazioni sullo stato per le date specificate.

### Informazioni sugli stati

Gli stati dei pagamenti per un intervallo di date selezionato sono visualizzati a sinistra della visualizzazione dei dati di stato dei pagamenti dell&#39;ordine. Le date per l’intervallo di date selezionato sono visualizzate nella parte inferiore della visualizzazione. Se non vi sono ordini in una data specifica, tale data non viene visualizzata.

La visualizzazione dei dati relativi allo stato del pagamento dell&#39;ordine include le seguenti informazioni.

| Dati | Descrizione |
| ------------ | -------------------- |
| [!UICONTROL Orders] | Intervallo di importi per ordini nell&#39;intervallo di tempo specificato; dati sull&#39;asse Y (a sinistra) |
| Intervallo di date | Intervallo di date per l’intervallo di tempo specificato; dati sull’asse X (in basso) |
| Autorizzato | Ordine autorizzato |
| Acquisizione richiesta | Acquisizione richiesta per l’ordine |
| Acquisizione confermata | Acquisizione ordine completata |
| Acquisizione parziale | Ordine parzialmente acquisito |
| Acquisizione non riuscita | Acquisizione ordine non riuscita |
| Annullato | Ordine annullato |

## Visualizzazione report stato pagamento ordine

La vista del rapporto Stato pagamento ordine è disponibile nella vista Home di Payment Services. Include stati dettagliati (pagamento, fatturazione, spedizione, rimborso, controversia e altro) per tutte le transazioni.

Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**per visualizzare la tabella dettagliata relativa alla visualizzazione del rapporto Stato pagamento ordine.

![Transazioni di stato pagamento ordine nell&#39;amministratore](assets/orders-report-data.png){width="800" zoomable="yes"}

È possibile configurare questa visualizzazione in base alle sezioni di questo argomento per presentare al meglio i dati che si desidera visualizzare.

È possibile [scarica transazioni di pagamento](#download-order-payment-statuses) in un formato di file .csv da utilizzare nel software di contabilità o di gestione degli ordini esistente.

>[!NOTE]
>
>I dati mostrati in questa tabella sono ordinati in ordine decrescente (`DESC`) per impostazione predefinita utilizzando `TRANS DATE`. Il `TRANS DATE` è la data e l’ora in cui è stata avviata la transazione.

### Aggiornamenti dello stato del pagamento

Alcuni metodi di pagamento richiedono un periodo di tempo per l&#39;acquisizione del pagamento. [!DNL Payment Services] ora rileva gli stati in sospeso di una transazione di pagamento in un ordine in base a:

* Rilevamento sincrono `pending capture` transazioni
* Monitoraggio asincrono `pending capture` transazioni

>[!NOTE]
>
>Il rilevamento degli stati in sospeso delle transazioni di pagamento in un ordine impedisce la spedizione accidentale di ordini se il pagamento non è ancora stato ricevuto. Ciò può verificarsi per gli assegni elettronici e le transazioni PayPal.

#### Rilevamento sincrono delle transazioni di acquisizione in sospeso

Rileva automaticamente le transazioni di acquisizione in un `Pending` stato e impedire agli ordini di immettere un `Processing` stato quando viene rilevata una transazione di questo tipo.

Durante il pagamento del cliente o quando un amministratore crea una fattura per un pagamento autorizzato in precedenza, [!DNL Payment Services] rileva automaticamente le transazioni di acquisizione in un `Pending` stato e sposta gli ordini corrispondenti in `Payment Review` stato.

#### Monitoraggio asincrono delle transazioni di acquisizione in sospeso

Rileva quando una transazione di acquisizione in sospeso immette un `Completed` in modo che gli esercenti possano riprendere l’elaborazione dell’ordine interessato.

Per assicurarti che questo processo funzioni come previsto, gli esercenti devono configurare un nuovo processo cron. Una volta configurato il processo per l’esecuzione automatica, non sono previsti altri interventi da parte del commerciante.

Consulta [Configurare i processi cron](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html). Una volta configurato, il nuovo processo viene eseguito ogni 30 minuti per recuperare gli aggiornamenti per gli ordini che si trovano in una `Payment Review` stato.

Gli esercenti possono controllare lo stato aggiornato del pagamento tramite la visualizzazione rapporto Stato pagamento ordine.

### Dati utilizzati nel rapporto

[!DNL Payment Services] utilizza i dati degli ordini e li combina con i dati di pagamento aggregati provenienti da altre fonti (incluso PayPal) per fornire rapporti significativi e molto utili.

I dati dell’ordine vengono esportati e memorizzati nel servizio di pagamento. Quando [modificare o aggiungere stati degli ordini](https://docs.magento.com/user-guide/sales/order-status-custom.html) o [modificare una visualizzazione store](https://docs.magento.com/user-guide/stores/stores-all-view-edit.html), [archiviare](https://docs.magento.com/user-guide/stores/store-information.html), o nome del sito Web, tali dati vengono combinati con i dati di pagamento e il rapporto sullo stato del pagamento dell&#39;ordine viene compilato con le informazioni combinate.

Questo processo prevede due fasi:

1. L’indice viene modificato in base ai dati `ON SAVE` (ogni volta che le informazioni dell&#39;ordine o del negozio vengono modificate) o `BY SCHEDULE` (secondo una pianificazione cron preconfigurata), a seconda di come è configurato in [Gestione indice](https://docs.magento.com/user-guide/system/index-management.html) in Admin.

   Per impostazione predefinita, si verifica l’indicizzazione dei dati `ON SAVE`, il che significa che ogni volta che qualcosa cambia nell’ordine, nello stato dell’ordine, nella visualizzazione del negozio, nel negozio o nel sito web, il processo di reindicizzazione avviene immediatamente.

1. I dati indicizzati vengono inviati al servizio di pagamento, che quindi compila il rapporto Stato pagamento ordine.

Gli unici dati esportati e confrontati a scopo di reporting sono i dati utilizzati dal rapporto Stato pagamento ordine.

>[!NOTE]
>
>I dati mostrati in questa tabella sono ordinati in ordine decrescente (`DESC`) per impostazione predefinita utilizzando `ORDER DATE`. Il `ORDER DATE` è la data e l’ora in cui è stato creato l’ordine.

#### Configurare l’esportazione dei dati

Anche se, per impostazione predefinita, la reindicizzazione si verifica in `ON SAVE` modalità, si consiglia di indicizzare in `BY SCHEDULE` modalità. Il `BY SCHEDULE` L&#39;indice viene eseguito con una pianificazione cron di un minuto e tutti i dati modificati vengono visualizzati nel rapporto sullo stato dell&#39;ordine entro due minuti dalla modifica dei dati. Questa reindicizzazione programmata consente di ridurre qualsiasi tensione sul negozio, soprattutto se si dispone di un grande volume di ordini in entrata, perché avviene secondo un programma (non come ogni ordine viene effettuato).

È possibile modificare la modalità indice:`ON SAVE` o `BY SCHEDULE`—[in Admin](https://docs.magento.com/user-guide/system/index-management.html#change-the-index-mode).

Per informazioni su come configurare l’esportazione dei dati, consulta [Configurazione della riga di comando](configure-cli.md#configure-data-export).

### Seleziona origine dati

Nella vista del rapporto Stato pagamento ordine è possibile selezionare l&#39;origine dati:**[!UICONTROL Live]** _ oppure **[!UICONTROL Sandbox]**- per il quale si desidera visualizzare i risultati del rapporto.

![Selezione di origini dati](assets/datasource.png){width="300" zoomable="yes"}

Se _[!UICONTROL Live]_è l&#39;origine dati selezionata, è possibile visualizzare le informazioni del report per gli archivi che utilizzano [!DNL Payment Services] in modalità di produzione. Se_[!UICONTROL Sandbox]_ è l&#39;origine dati selezionata, è possibile visualizzare le informazioni del rapporto per la modalità sandbox.

Le selezioni delle origini dati funzionano come segue:

* Se non si dispone di negozi che utilizzano [!DNL Payment Services] in modalità Live, la selezione dell’origine dati viene impostata per impostazione predefinita su _[!UICONTROL Sandbox]_.
* Se sono presenti negozi (uno o più) che utilizzano [!DNL Payment Services] in modalità Live, la selezione dell’origine dati viene impostata per impostazione predefinita su _[!UICONTROL Live]_.
* Le esportazioni dei rapporti rispettano sempre la selezione dell’origine dati.

Per selezionare l&#39;origine dati per [!UICONTROL Order Payment Status] rapporto:

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Orders]** > **[!UICONTROL View Report]**.
1. Fai clic su _[!UICONTROL Data source]_filtro di selezione e selezione **[!UICONTROL Live]**o **[!UICONTROL Sandbox]**.

   I risultati del report vengono rigenerati in base all&#39;origine dati selezionata.

### Personalizzare le date dell’ordine nell’arco temporale

Nella visualizzazione del rapporto Stato pagamento ordine è possibile personalizzare l&#39;intervallo temporale dei risultati dello stato che si desidera visualizzare selezionando date specifiche. Per impostazione predefinita, nella griglia sono visualizzati 30 giorni di stato di pagamento dell&#39;ordine.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Fai clic su _[!UICONTROL Order dates]_filtro selettore calendario.
1. Scegli l’intervallo di date applicabile.
1. Visualizza gli stati di pagamento dell&#39;ordine per le date specificate nella griglia.

### Filtrare le informazioni del rapporto

Nella visualizzazione del rapporto Stato pagamento ordine è possibile filtrare i risultati degli stati che si desidera visualizzare selezionando i criteri di filtro.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Fai clic su **[!UICONTROL Filter]** selettore.
1. Attiva/disattiva _Stato pagamento_ opzioni per visualizzare i risultati del rapporto solo per gli stati di pagamento dell&#39;ordine selezionati.
1. Visualizzare i risultati del rapporto all&#39;interno di un intervallo di importi dell&#39;ordine inserendo un _[!UICONTROL Min Order Amount]_o _[!UICONTROL Max Order Amount_].
1. Clic **[!UICONTROL Hide filters]** per nascondere il filtro.

### Mostra e nascondi colonne

Il rapporto Stato pagamento ordine mostra tutte le colonne di informazioni disponibili per impostazione predefinita. È tuttavia possibile personalizzare le colonne visualizzate nel rapporto.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Fai clic su _Impostazioni colonna_ icona (![icona delle impostazioni delle colonne](assets/column-settings.png){width="20" zoomable="yes"}).
1. Per personalizzare le colonne visualizzate nel report, selezionare o deselezionare le colonne nell&#39;elenco.

   Nel rapporto Stato pagamento ordine vengono immediatamente visualizzate le modifiche apportate nel menu Impostazioni colonna. Le preferenze di colonna vengono salvate e rimangono attive se ci si sposta dalla vista del rapporto.

### Stati di visualizzazione

La visualizzazione del rapporto Stato pagamento ordine mostra informazioni complete sullo stato del pagamento per ogni ordine.

Per impostazione predefinita, nella griglia sono visualizzati 30 giorni di stato di pagamento dell&#39;ordine.

Scorri verso sinistra e destra per visualizzare [informazioni stato pagamento ordine](#column-descriptions), inclusa la data dell&#39;ordine, la data autorizzata, fatturata, spedita, lo stato di pagamento e altro ancora.

Il numero di righe restituite in una ricerca o visualizzate negli stati di pagamento dell&#39;ordine predefiniti per 30 giorni viene visualizzato sopra la griglia di visualizzazione dello stato del pagamento dell&#39;ordine insieme al filtro del selettore calendario Date ordine.

#### Stato della retribuzione

La colonna Stato pagamento mostra lo stato corrente di qualsiasi pagamento. A `Capture failed` il pagamento mostra uno stato di avviso rosso e un `Voided` il pagamento mostra uno stato di avviso grigio.

#### Stato rimborso

La colonna Stato rimborso mostra lo stato corrente di qualsiasi rimborso. A `Capture failed` il pagamento mostra uno stato di avviso rosso e un `Voided` il pagamento mostra uno stato di avviso grigio.

### Aggiornare i dati del rapporto

La vista del rapporto Stato pagamento ordine mostra un _[!UICONTROL Last updated]_timestamp che mostra l’ultimo aggiornamento delle informazioni del rapporto. Per impostazione predefinita, i dati del rapporto Stato pagamento ordine vengono aggiornati automaticamente ogni tre ore.

È inoltre possibile forzare manualmente l&#39;aggiornamento dei dati del rapporto Stato pagamento ordine per visualizzare le informazioni più aggiornate.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Fai clic su _Aggiorna_ icona (![icona di aggiornamento](assets/refresh-button-med.png){width="20" zoomable="yes"}).

   I dati del rapporto sullo stato del pagamento dell&#39;ordine vengono aggiornati, *[!UICONTROL Update complete]* viene visualizzata la conferma e nella griglia sono presenti le informazioni più recenti.

### Visualizza controversie

Puoi visualizzare eventuali controversie sugli ordini del tuo Negozio e passare al Centro di risoluzione PayPal per intervenire su di essi, dall&#39;interno del rapporto Stato pagamento ordine.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Accedi a **[!UICONTROL Disputes column]**.
1. Visualizzare eventuali controversie per un ordine specifico e vedere [lo stato della controversia](#order-payment-status-information).
1. Rivedi i dettagli della controversia da [Centro soluzioni PayPal](https://www.paypal.com/us/cshelp/article/what-is-the-resolution-center-help246) facendo clic sul collegamento ID controversia che inizia con _PP-D-_.
1. Adottare le misure appropriate per la controversia, se necessario.

   Per ordinare le controversie in base allo stato, fare clic sul pulsante [!UICONTROL Disputes] intestazione di colonna.

### Scarica stati di pagamento ordine

È possibile scaricare un file .csv con tutti gli stati visibili nella griglia di visualizzazione dello stato del pagamento dell&#39;ordine, sia che si visualizzino gli stati predefiniti di 30 giorni o un intervallo temporale personalizzato.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Se desideri visualizzare gli stati per un intervallo di tempo diverso dagli ultimi 30 giorni, [personalizza l’intervallo di date temporale per i tuoi stati](#customize-dates-timeframe).
1. Fai clic su _Scarica_ (![icona di download](assets/icon-download.png){width="20" zoomable="yes"}).

Gli stati di pagamento dell&#39;ordine vengono scaricati in formato .csv.

### Descrizioni delle colonne

I rapporti sullo stato dei pagamenti degli ordini includono le seguenti informazioni.

| Colonna | Descrizione |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | ID ordine commerce<br> <br>Per visualizzare i [informazioni ordine](https://docs.magento.com/user-guide/sales/orders.html){target="_blank"}, fai clic sull&#39;ID. |
| [!UICONTROL Order Date] | Timestamp data ordine |
| [!UICONTROL Authorized Date] | Data e ora dell’autorizzazione di pagamento |
| [!UICONTROL Order Status] | Commerce corrente [stato ordine](https://docs.magento.com/user-guide/sales/order-status.html){target="_blank"} |
| [!UICONTROL Invoiced] | Stato fattura dell&#39;ordine—*[!UICONTROL No]*, *[!UICONTROL Partial]*, o *[!UICONTROL Yes]* |
| [!UICONTROL Shipped] | Stato spedizione dell&#39;ordine—*[!UICONTROL No]*, *[!UICONTROL Partial]*, o *[!UICONTROL Yes]* |
| [!UICONTROL Order Amt] | Importo totale totale dell’ordine |
| [!UICONTROL Cur] | Tipo di valuta dell’ordine |
| [!UICONTROL Pay Status] | Stato del pagamento per un ordine specifico |
| [!UICONTROL Paid Amt] | Importo pagato su un ordine |
| [!UICONTROL Cur] | Tipo di valuta dell’importo pagato su un ordine |
| [!UICONTROL Refund Status] | Stato di un rimborso su un ordine (ad esempio informazioni da restituzioni, RMA e note di accredito)—   *[!UICONTROL Requires refund]*, *[!UICONTROL Refund requested]*, *[!UICONTROL Refunded]*, *[!UICONTROL Refund failed]*, o *[!UICONTROL Voided]* |
| [!UICONTROL Refund Amount] | Totale dell&#39;importo rimborsato per un ordine |
| [!UICONTROL Cur] | Tipo di valuta dell&#39;importo rimborsato per un ordine |
| [!UICONTROL Disputes] | Stato di qualsiasi controversia relativa a un ordine (informazioni derivanti da controversie e rettifiche)—*[!UICONTROL Open]*, *[!UICONTROL Waiting for buyer response]*, *[!UICONTROL Waiting for seller response]*, *[!UICONTROL Under review]*, *[!UICONTROL Resolved]*, o *[!UICONTROL Other]* |
| [!UICONTROL Payment Method] | Metodo di pagamento utilizzato nella transazione Commerce per un ordine |
| [!UICONTROL Website] | Sito web da cui è stato effettuato l’ordine |
| [!UICONTROL Store] | Archivio da cui è stato effettuato l’ordine |
| [!UICONTROL Store View] | Visualizzazione del Negozio da cui è stato effettuato l&#39;ordine |
