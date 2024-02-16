---
title: Connettere dati Commerce a Adobe Experience Platform
description: Scopri come collegare i dati di Commerce a Adobe Experience Platform.
exl-id: 87898283-545c-4324-b1ab-eec5e26a303a
feature: Personalization, Integration, Configuration
source-git-commit: 540c423ecf7e50a36c1137f43a9cf9673658c805
workflow-type: tm+mt
source-wordcount: '2501'
ht-degree: 0%

---

# Connettere i dati di Commerce a Adobe Experience Platform

Quando si installa [!DNL Data Connection] , due nuove pagine di configurazione vengono visualizzate nel **Sistema** menu in **Servizi** in Commerce _Amministratore_.

- Connettore Commerce Services
- [!DNL Data Connection]

Per collegare la tua istanza di Adobe Commerce a Adobe Experience Platform, devi configurare entrambi i connettori, partendo dal connettore Commerce Services e terminando con [!DNL Data Connection] estensione.

## Configurare il connettore Commerce Services

Se in precedenza hai installato un servizio Adobe Commerce, probabilmente hai già configurato il connettore Commerce Services. In caso contrario, è necessario completare le seguenti attività nella [Connettore Commerce Services](../landing/saas.md) pagina:

1. Accedi al tuo account Commerce per [recuperare le chiavi API di produzione e sandbox](../landing/saas.md#credentials).
1. Seleziona un [Spazio dati SaaS](../landing/saas.md#saas-configuration).
1. Accedi al tuo account Adobe per [recuperare l’ID organizzazione](../landing/saas.md#ims-organization-optional).

Dopo aver configurato il connettore Commerce Services, puoi quindi configurare [!DNL Data Connection] estensione.

## Configurare [!DNL Data Connection] estensione

In questa sezione imparerai a configurare il [!DNL Data Connection] estensione.

### Aggiungi dettagli account servizio e credenziali

Se prevedi di raccogliere e inviare [dati ordine cronologico](#send-historical-order-data) o [Dati del profilo cliente (Beta)](#send-customer-profile-data), è necessario aggiungere i dettagli dell&#39;account del servizio e delle credenziali. Inoltre, se si sta configurando [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html) devi completare questi passaggi.

Se raccogli e invii solo dati di vetrina o di back office, puoi passare al [generale](#general) sezione.

#### Passaggio 1: creare un progetto nella console Adobe Developer

Crea un progetto nella console di Adobe Developer che autentica Commerce in modo da poter effettuare chiamate API Experienci Platform.

Per creare il progetto, segui i passaggi descritti in [Autenticazione e accesso alle API di Experienci Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html) esercitazione.

Durante l’esercitazione, assicurati che il progetto presenti quanto segue:

- Accedere ai seguenti [profili di prodotto](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#select-product-profiles): **Accesso predefinito per tutti gli elementi di produzione** e **Accesso predefinito AEP**.
- Il corretto [i ruoli e le autorizzazioni sono configurati](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#assign-api-to-a-role).
- Se hai deciso di utilizzare i token web JSON (JWT) come metodo di autenticazione server-to-server, devi caricare anche una chiave privata.

Il risultato di questo passaggio crea un file di configurazione da utilizzare nel passaggio successivo.

#### Passaggio 2: scarica il file di configurazione

Scarica il file [file di configurazione workspace](https://developer.adobe.com/commerce/extensibility/events/project-setup/#download-the-workspace-configuration-file). Copia e incolla il contenuto di questo file in **Dettagli account servizio/credenziali** pagina dell’amministratore di Commerce.

1. Nell’amministrazione di Commerce, passa a **Negozi** > Impostazioni > **Configurazione** > **Servizi** > **[!DNL Data Connection]**.

1. Selezionare il metodo di autorizzazione server-to-server implementato da **Tipo di autorizzazione Adobe Developer** menu. Adobe consiglia di utilizzare OAuth. Il codice JWT è stato dichiarato obsoleto. [Ulteriori informazioni](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

1. (Solo JWT) copia e incolla il contenuto del file `private.key` file in **Segreto client** campo. Utilizza il seguente comando per copiare il contenuto.

   ```bash
   cat config/private.key | pbcopy
   ```

   Consulta [Autenticazione dell’account di servizio (JWT)](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) per ulteriori informazioni su `private.key` file.

1. Copia il contenuto del `<workspace-name>.json` file in **Dettagli account servizio/credenziali** campo.

   ![[!DNL Data Connection] Configurazione amministratore](./assets/epc-admin-config.png){width="700" zoomable="yes"}

1. Clic **Salva configurazione**.

### Generale

1. In Admin (Amministrazione), vai a **Sistema** > Servizi > **[!DNL Data Connection]**.

1. Il giorno **Impostazioni** scheda in **Generale**, verifica l’ID associato al tuo account Adobe Experience Platform, come configurato in [Connettore Commerce Services](../landing/saas.md#organizationid). L’ID organizzazione è globale. È possibile associare un solo ID organizzazione per istanza di Adobe Commerce.

1. In **Ambito** , impostare il contesto su **Sito Web**.

1. (Facoltativo) Se disponi già di un’ [AEP Web SDK (lega)](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html) implementato nel sito, abilita la casella di controllo e aggiungi il nome dell’SDK web AEP. In caso contrario, lasciare vuoti questi campi e il campo [!DNL Data Connection] L&#39;estensione ne distribuisce una per te.

   >[!NOTE]
   >
   >Se specifichi il tuo Web SDK AEP, il [!DNL Data Connection] L&#39;estensione utilizza l&#39;ID dello stream di dati associato all&#39;SDK e non l&#39;ID dello stream di dati specificato in questa pagina (se presente).

### Raccolta dati

In questa sezione si specifica il tipo di dati che si desidera raccogliere e inviare al server Edge di Experienci Platform. Esistono tre tipi di dati:

- **Comportamento** (dati lato client) sono dati acquisiti nella vetrina. Ciò include le interazioni con l’acquirente, come `View Page`, `View Product`, `Add to Cart`, e [elenco richieste di acquisto](events.md#b2b-events) informazioni (per gli esercenti B2B).

- **Back office** (dati lato server) sono dati acquisiti nei server Commerce. Ciò include informazioni sullo stato di un ordine, ad esempio se un ordine è stato effettuato, annullato, rimborsato, spedito o completato. Include inoltre [dati ordine cronologico](#send-historical-order-data).

- (**Beta**) **Profilo** sono dati relativi alle informazioni del profilo dell’acquirente. Scopri [altro](#send-customer-profile-data).

Per garantire che la tua istanza di Adobe Commerce possa iniziare la raccolta dei dati, controlla [prerequisiti](overview.md#prerequisites).

Per ulteriori informazioni sugli eventi, consulta l’argomento [vetrina](events.md#storefront-events), [back office](events.md#back-office-events), e [profilo](events.md#customer-profile-events-server-side) eventi.

>[!NOTE]
>
>Tutti i campi in **Raccolta dati** sezione applicabile al **Sito Web** ambito o superiore.

1. Seleziona **Eventi vetrina** se desideri inviare dati comportamentali della vetrina.

1. Seleziona **Eventi back office** se si desidera inviare informazioni sullo stato dell&#39;ordine, ad esempio se un ordine è stato effettuato, annullato, rimborsato o spedito.

   >[!NOTE]
   >
   >Se si seleziona **Eventi back office**, tutti i dati di back office vengono inviati a Experienci Platform Edge. Se un acquirente sceglie di rinunciare alla raccolta dei dati, devi impostare esplicitamente la preferenza relativa alla privacy dell&#39;acquirente nell&#39;Experience Platform. Questo è diverso dagli eventi di vetrina in cui l’agente di raccolta gestisce già il consenso in base alle preferenze dell’acquirente. Scopri [altro](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html) informazioni sull&#39;impostazione delle preferenze relative alla privacy di un acquirente nell&#39;Experience Platform.

1. (Ignora questo passaggio se utilizzi un tuo AEP Web SDK personale.) [Crea](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html#create) uno stream di dati in Adobe Experience Platform o seleziona uno stream di dati esistente da utilizzare per la raccolta. Immetti l’ID dello stream di dati in **ID flusso di dati** campo.

1. Inserisci il **ID set di dati** che desideri contenere i dati di Commerce. Per trovare l’ID del set di dati:

   1. Apri l’interfaccia utente di Experienci Platform e seleziona **Set di dati** nel menu di navigazione a sinistra per aprire **Set di dati** dashboard. Il dashboard elenca tutti i set di dati disponibili per l’organizzazione. Vengono visualizzati i dettagli di ciascun set di dati elencato, tra cui il nome, lo schema a cui il set di dati aderisce e lo stato dell’esecuzione dell’acquisizione più recente.
   1. Apri il set di dati associato allo stream di dati.
   1. Nel riquadro di destra, visualizzare i dettagli sul set di dati. Copia l’ID del set di dati.

1. Per garantire l&#39;aggiornamento dei dati degli eventi di back office in base a una pianificazione in base a [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html) processo, è necessario modificare il `Sales Orders Feed` indice a `Update by Schedule`.

   1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Index Management]**.

   1. Seleziona la casella di controllo per il `Sales Orders Feed` indicizzatore.

   1. Imposta **[!UICONTROL Actions]** a `Update by Schedule`.

   1. Se si abilitano i dati di back office per la prima volta, eseguire i seguenti comandi per reindicizzare e attivare una risincronizzazione. Le successive risincronizzazioni si verificano automaticamente se il [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html) il processo è configurato correttamente.

      ```bash
      bin/magento index:reindex sales_order_data_exporter_v2
      ```

      ```bash
      bin/magento saas:resync --feed orders
      ```

#### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Ambito | Sito Web specifico in cui desideri applicare le impostazioni di configurazione. |
| ID organizzazione (globale) | ID che appartiene all&#39;organizzazione che ha acquistato il prodotto Adobe DX. Questo ID collega l’istanza di Adobe Commerce a Adobe Experience Platform. |
| AEP Web SDK è già distribuito sul tuo sito? | Seleziona questa casella di controllo se hai implementato il tuo AEP Web SDK sul tuo sito |
| Nome AEP Web SDK (globale) | Se hai già distribuito un Experienci Platform Web SDK sul tuo sito, specifica il nome di tale SDK in questo campo. Questo consente a Storefront Event Collector e Storefront Event SDK di utilizzare l’SDK per web di Experience Platform anziché la versione distribuita da [!DNL Data Connection] estensione. Se non hai implementato un Experienci Platform Web SDK nel tuo sito, lascia vuoto questo campo e il [!DNL Data Connection] L&#39;estensione ne distribuisce una per te. |
| Eventi vetrina | È selezionato per impostazione predefinita, purché l’ID organizzazione e l’ID dello stream di dati siano validi. Gli eventi di vetrina raccolgono dati comportamentali anonimi dai tuoi acquirenti durante la navigazione sul tuo sito. |
| Eventi back office | Se selezionato, il payload dell’evento contiene informazioni anonime sullo stato dell’ordine, ad esempio se un ordine è stato effettuato, annullato, rimborsato o spedito. |
| ID flusso di dati (sito web) | ID che consente il flusso di dati da Adobe Experience Platform ad altri prodotti Adobe DX. Questo ID deve essere associato a un sito web specifico all’interno della tua istanza Adobe Commerce specifica. Se specifichi un Experienci Platform Web SDK personalizzato, non specificare un ID dello stream di dati in questo campo. Il [!DNL Data Connection] L’estensione utilizza l’ID dello stream di dati associato a tale SDK e ignora qualsiasi ID dello stream di dati specificato in questo campo (se presente). |
| ID set di dati (sito web) | ID del set di dati che contiene i dati di Commerce. Questo campo è obbligatorio a meno che tu non abbia deselezionato **Eventi vetrina** o **Eventi back office** caselle di controllo. Inoltre, se utilizzi il tuo Experienci Platform Web SDK e pertanto non hai specificato un ID dello stream di dati, devi comunque aggiungere l’ID del set di dati associato allo stream di dati. In caso contrario, non è possibile salvare il modulo. |

Dopo l’onboarding, i dati della vetrina iniziano a fluire verso il server Edge di Experienci Platform. I dati di back office richiedono circa cinque minuti per essere visualizzati ai margini. Gli aggiornamenti successivi sono visibili sul server Edge in base alla pianificazione cron.

### Inviare dati del profilo cliente

>[!IMPORTANT]
>
>Questa funzione è in versione beta. Se desideri partecipare al programma beta, invia una richiesta a [dataconnection@adobe.com](mailto:dataconnection@adobe.com).

Esistono due tipi di dati di profilo che puoi inviare all’Experience Platform: i record di profilo e gli eventi di profilo della serie temporale.

Un record di profilo contiene dati salvati quando un acquirente crea un profilo nell’istanza Commerce, ad esempio il nome dell’acquirente. Quando lo schema e il set di dati sono [configurato correttamente](profile-data.md), un record di profilo viene inviato all’Experience Platform e inoltrato al servizio di gestione e segmentazione dei profili di Adobe: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html).

Gli eventi di profilo della serie temporale contengono dati sulle informazioni del profilo dell’acquirente, ad esempio se creano, modificano o eliminano un account sul sito. Quando i dati dell’evento profilo vengono inviati all’Experience Platform, risiedono in un set di dati in cui possono essere utilizzati da altri prodotti DX.

1. Assicurati di avere [fornito](#add-service-account-and-credential-details) dettagli dell&#39;account del servizio e delle credenziali.

1. Assicurati di avere uno schema e un set di dati specificati per [acquisizione dei dati del record del profilo](profile-data.md) e [acquisizione dei dati evento profilo serie temporali](update-xdm.md#time-series-profile-event-data).

1. Inserire un segno di spunta nella **Profili cliente** se desideri inviare i dati del profilo all’Experience Platform.

1. Inserisci il **ID del set di dati profilo**.

   I dati del record profilo devono utilizzare un set di dati diverso da quello attualmente in uso per i dati comportamentali e di back office.

1. Se non desideri inviare in streaming gli eventi di profilo attraverso lo stesso ID dello stream di dati utilizzato per i dati comportamentali e di back office, rimuovi il segno di spunta da **Trasmetti i profili cliente attraverso lo stesso ID dello stream di dati** e immetti l’ID dello stream di dati che desideri utilizzare al suo posto.

La disponibilità di un record di profilo in Real-Time CDP può richiedere circa 10 minuti. Lo streaming degli eventi del profilo inizia immediatamente.

#### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Profili cliente | Selezionare questa casella di controllo se si desidera raccogliere e inviare i record del profilo cliente. |
| ID del set di dati profilo | Un record di profilo deve utilizzare un set di dati diverso da quello utilizzato per eventi comportamentali e di back office. |
| Trasmetti i profili cliente attraverso lo stesso ID dello stream di dati | Decidi se utilizzare o meno lo stesso flusso di dati attualmente utilizzato per gli eventi comportamentali e di back office. |
| Stream di dati per i profili cliente | Specifica lo stream di dati specifico per il record del profilo cliente. |

### Inviare dati cronologici degli ordini

Adobe Commerce raccoglie fino a cinque anni di [dati e stato cronologici degli ordini](events.md#back-office-events). È possibile utilizzare [!DNL Data Connection] estensione per inviare i dati storici all’Experience Platform per arricchire i profili dei clienti e personalizzare l’esperienza del cliente in base a tali ordini passati. I dati vengono memorizzati in un set di dati in Experienci Platform.

Anche se Commerce raccoglie già i dati storici dell’ordine, è necessario completare diversi passaggi per inviare tali dati ad Experienci Platform.

Guarda questo video per ulteriori informazioni sugli ordini storici, quindi completa i seguenti passaggi per implementare la raccolta degli ordini storici.

>[!VIDEO](https://video.tv.adobe.com/v/3424672)

#### Impostare il servizio di sincronizzazione ordini

Il servizio di sincronizzazione degli ordini utilizza [Framework coda messaggi](https://developer.adobe.com/commerce/php/development/components/message-queues/) e RabbitMQ. Dopo aver completato questi passaggi, i dati sullo stato dell’ordine possono essere sincronizzati con SaaS, operazione necessaria prima dell’invio all’Experience Platform.

1. Assicurati di avere [fornito](#add-service-account-and-credential-details) dettagli dell&#39;account del servizio e delle credenziali.

1. [Abilita](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq.html) RabbitMQ.

   >[!NOTE]
   >
   >RabbitMQ è già configurato per le versioni Commerce 2.4.7 e successive, ma devi abilitare i consumatori.

1. Abilitare i consumatori della coda di messaggi in base al processo cron in `.magento.env.yaml` utilizzo `CRON_CONSUMERS_RUNNER` variabile di ambiente.

   ```yaml
      stage:
        deploy:
          CRON_CONSUMERS_RUNNER:
            cron_run: true
   ```

   >[!NOTE]
   >
   >Consulta la [documentazione sulle variabili di distribuzione](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#cron_consumers_runner) per scoprire tutte le opzioni di configurazione disponibili.

Con il servizio di sincronizzazione degli ordini abilitato, è possibile specificare l&#39;intervallo di date dell&#39;ordine cronologico nel **[!UICONTROL [!DNL Data Connection]]** pagina.

#### Specifica intervallo date cronologia ordini

Specifica l’intervallo di date per gli ordini storici da inviare all’Experience Platform.

1. In Admin (Amministrazione), vai a **Sistema** > Servizi > **[!DNL Data Connection]**.

1. Seleziona la **Cronologia ordini** scheda.

1. Sotto **Sincronizzazione cronologia ordini**, il **Copia ID set di dati dalle impostazioni** la casella di controllo è già abilitata. In questo modo puoi utilizzare lo stesso set di dati specificato nella **Impostazioni** scheda.

1. In **Da** e **A** , specificare l&#39;intervallo di date per i dati cronologici dell&#39;ordine da inviare. Non puoi selezionare un intervallo di date superiore a cinque anni.

1. Seleziona **[!UICONTROL Start Sync]** per avviare la sincronizzazione. I dati storici dell’ordine sono dati in batch, anziché dati di vetrina e di back office che sono dati in streaming. L’invio dei dati in batch in Experienci Platform richiede circa 45 minuti.

##### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Copia ID set di dati dalle impostazioni | Copia l’ID del set di dati immesso sul **Impostazioni** scheda. |
| ID set di dati (sito web) | ID del set di dati che contiene i dati di Commerce. Questo campo è obbligatorio a meno che tu non abbia deselezionato **Eventi vetrina** o **Eventi back office** caselle di controllo. Inoltre, se utilizzi il tuo Experienci Platform Web SDK e pertanto non hai specificato un ID dello stream di dati, devi comunque aggiungere l’ID del set di dati associato allo stream di dati. In caso contrario, non è possibile salvare il modulo. |
| Da | Data a partire dalla quale si desidera iniziare la raccolta dei dati della cronologia degli ordini. |
| A | Data a partire dalla quale si desidera terminare la raccolta dei dati della cronologia degli ordini. |
| Avvia sincronizzazione | Avvia il processo di sincronizzazione dei dati della cronologia dell&#39;ordine con il server perimetrale Experience Platform. Questo pulsante è disattivato se **[!UICONTROL Dataset ID]** è vuoto o l’ID del set di dati non è valido. |

## Conferma la raccolta dei dati dell’evento

Per confermare che i dati vengono raccolti dal tuo archivio Commerce, utilizza [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html) per esaminare il tuo sito Commerce. Dopo aver confermato che i dati vengono raccolti, è possibile verificare che i dati dell&#39;evento della vetrina e del back office vengano visualizzati nella periferia eseguendo una query che restituisce i dati dalla [set di dati creato](overview.md#prerequisites).

1. Seleziona **Query** nel menu di navigazione a sinistra di Experienci Platform, fai clic su [!UICONTROL Create Query].

   ![Editor query](assets/query-editor.png)

1. All’apertura dell’editor delle query, immetti una query che selezioni i dati dal set di dati.

   ![Crea query](assets/create-query.png)

   Ad esempio, la query potrebbe essere simile alla seguente:

   ```sql
   SELECT * from `your_dataset_name` ORDER by TIMESTAMP DESC
   ```

1. Dopo l’esecuzione della query, i risultati vengono visualizzati nel **Risultati** accanto alla scheda **Console** scheda. Questa vista mostra l’output tabulare della query.

   ![Editor query](assets/query-results.png)

In questo esempio, puoi visualizzare i dati dell’evento dal [`commerce.productListAdds`](events.md#addtocart), [`commerce.productViews`](events.md#productpageview), [`web.webpagedetails.pageViews`](events.md#pageview)e così via. Questa vista ti consente di verificare che i dati di Commerce siano arrivati all’edge.

Se i risultati non sono quelli previsti, apri il set di dati e cerca eventuali importazioni batch non riuscite. Ulteriori informazioni su [risoluzione dei problemi relativi alle importazioni batch](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/troubleshooting.html).

## Passaggi successivi

Quando i dati di Commerce vengono inviati al server Edge di Experienci Platform, altri prodotti Adobe Experience Cloud, come Adobe Journey Optimizer, possono utilizzarli. Ad esempio, puoi configurare Journey Optimizer per l’ascolto di determinati eventi e, in base a tali dati, attivare un’e-mail per il primo utente o se viene abbandonato un carrello. Scopri come estendere la piattaforma Commerce [creazione di percorsi di clienti](using-ajo.md) in Journey Optimizer.
