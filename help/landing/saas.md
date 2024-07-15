---
title: Connettore servizi Commerce
description: Scopri come integrare la tua istanza di Adobe Commerce o di Magento Open Source nei servizi utilizzando le chiavi API di produzione e sandbox.
exl-id: 28027a83-449b-4b96-b926-a7bfbfd883d8
feature: Services, Saas
role: Admin, User
source-git-commit: 3eb873c84edb56d2fc399c72296f2b545a78064e
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Alcune funzionalità di Adobe Commerce e Magento Open Source sono basate su [!DNL Commerce Services] e distribuite come SaaS (software as a service). Per utilizzare questi servizi, è necessario connettere l&#39;istanza [!DNL Commerce] utilizzando le chiavi API di produzione e sandbox e specificare lo spazio dati nella [configurazione](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html). È necessario configurarlo una sola volta.

## Servizi disponibili {#availableservices}

Di seguito sono elencate le funzionalità di [!DNL Commerce] a cui è possibile accedere tramite [!DNL Commerce Services Connector]:

| Servizio | Disponibilità |
| ---|--- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) con tecnologia Adobe Sensei | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) con tecnologia Adobe Sensei | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/overview.md) | ADOBE COMMERCE e MAGENTO OPEN SOURCE |
| [[!DNL Channel Manager]](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/intro-to-channel-manager/overview.html) | ADOBE COMMERCE e MAGENTO OPEN SOURCE |
| [[!DNL Site-Wide Analysis Tool]](https://experienceleague.adobe.com/docs/commerce-operations/tools/site-wide-analysis-tool/intro.html) | Adobe Commerce |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## Architettura

A un livello avanzato, [!DNL Commerce Services Connector] è costituito dai seguenti elementi principali:

![Architettura di Commerce Services Connector](assets/saas-config-sync-workflow.png)

Le sezioni seguenti descrivono ciascuno di questi elementi in modo più dettagliato.

## Credenziali {#apikey}

Le chiavi API di produzione e sandbox sono generate dall&#39;account [!DNL Commerce] del [proprietario licenza](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding) identificato da un ID [!DNL Commerce] univoco (MageID). Per superare la convalida dei diritti per servizi come [!DNL Product Recommendations] o [!DNL Live Search], il proprietario della licenza per l&#39;organizzazione del commerciante può generare il set di chiavi API, purché l&#39;account sia in buono stato.

Le chiavi possono essere condivise in base alla necessità di sapere con l&#39;integratore di sistemi o il team di sviluppo che gestisce progetti e ambienti per conto del titolare della licenza. Gli sviluppatori a cui il proprietario della licenza ha concesso [!DNL Shared Access] non possono generare le chiavi per loro conto anche se l&#39;organizzazione del commerciante è presente nel menu a discesa [!DNL Switch Accounts] sul loro account.

Inoltre, gli integratori di soluzioni sono anche autorizzati a utilizzare [!DNL Commerce Services]. Se sei un integratore di soluzioni, il firmatario del contratto partner [!DNL Commerce] deve generare le chiavi API.

>[!NOTE]
>
>Il proprietario della licenza è in genere il contatto principale sull’account Adobe Commerce e non è sempre lo stesso del proprietario del progetto di infrastruttura cloud Adobe Commerce on.

### Generare le chiavi API di produzione e sandbox {#genapikey}

1. Accedi al tuo account [!DNL Commerce] all&#39;indirizzo [https://account.magento.com](https://account.magento.com/){:target=&quot;_blank&quot;}.

1. Nella scheda **Magento**, seleziona **Portale API** nella barra laterale.

1. Dal menu _Ambiente_, seleziona **Produzione** o **Sandbox**.

1. Immetti un nome nella sezione _Chiavi API_ e fai clic su **Aggiungi nuovo**.

   Viene visualizzata una finestra di dialogo per il download della nuova chiave.

   ![Scarica chiave privata](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Questa è l&#39;unica opportunità di copiare o scaricare le chiavi.

1. Fai clic su **Scarica**, quindi su **Annulla**.

1. Ripeti i passaggi precedenti per ogni ambiente (produzione e sandbox).

   Nella sezione **Chiavi API** sono ora visualizzate le chiavi API (pubbliche). Quando si [seleziona o si crea un progetto SaaS](#createsaasenv), sono necessarie sia le chiavi di produzione che quelle di sandbox (pubblico+privato).

## Configurazione SaaS {#saasenv}

Le istanze di [!DNL Commerce] devono essere configurate con un progetto SaaS e uno spazio dati SaaS in modo che [!DNL Commerce Services] possa inviare i dati alla posizione giusta. Un progetto SaaS raggruppa tutti gli spazi di dati SaaS. Gli spazi dati SaaS vengono utilizzati per raccogliere e archiviare dati che consentono il funzionamento di [!DNL Commerce Services]. Alcuni di questi dati possono essere esportati dall&#39;istanza [!DNL Commerce] e altri possono essere raccolti dal comportamento dell&#39;acquirente nella vetrina. Tali dati vengono quindi salvati in modo permanente nell’archiviazione cloud protetta.

Per [!DNL Product Recommendations], lo spazio dati SaaS contiene dati di catalogo e comportamentali. È possibile indirizzare un&#39;istanza [!DNL Commerce] a uno spazio dati SaaS [selezionandola](https://docs.magento.com/user-guide/configuration/services/saas.html) nella configurazione [!DNL Commerce].

>[!WARNING]
>
> Utilizzare lo spazio dati SaaS di produzione solo nell&#39;installazione di [!DNL Commerce] di produzione per evitare conflitti di dati. In caso contrario, si rischia di inquinare i dati del sito di produzione con i dati di test, causando ritardi nell’implementazione. Ad esempio, i dati del prodotto di produzione potrebbero essere erroneamente sovrascritti dai dati di staging, come gli URL di staging.

### Selezionare o creare un progetto SaaS {#createsaasenv}

Per selezionare o creare un progetto SaaS, richiedere la chiave API [!DNL Commerce] al proprietario della licenza [!DNL Commerce] per l&#39;archivio:

>[!NOTE]
>
> Se la sezione **[!UICONTROL Commerce Services Connector]** non è visualizzata nella configurazione di [!DNL Commerce], è necessario installare i moduli [!DNL Commerce] per il [[!DNL Commerce] servizio](#availableservices) desiderato.

1. Nella barra laterale _Admin_, vai a **Sistema** > Servizi > **Connettore servizi Commerce**.

   Se non vedi la sezione **[!UICONTROL Commerce Services Connector]** nella configurazione [!DNL Commerce], installa i moduli [!DNL Commerce] per il [[!DNL Commerce] servizio](#availableservices) desiderato. Verificare inoltre che il pacchetto `magento/module-services-id` sia installato.

1. Nelle sezioni _Chiavi API sandbox_ e _Chiavi API di produzione_, incolla i valori chiave.

   Le chiavi private devono includere `----BEGIN PRIVATE KEY---` all&#39;inizio della chiave e `----END PRIVATE KEY----` alla fine della chiave privata.

1. Fai clic su **Salva**.

Tutti i progetti SaaS associati alle chiavi vengono visualizzati nel campo **Progetto** della sezione **Identificatore SaaS**.

1. Se non esistono progetti SaaS, fare clic su **Crea progetto**. Quindi nel campo **Progetto**, inserisci un nome per il progetto SaaS.

   Quando si crea un progetto SaaS, [!DNL Commerce] genera uno o più spazi di dati SaaS a seconda della licenza di [!DNL Commerce]:
   - Adobe Commerce: uno spazio dati di produzione; due spazi dati di test. Nei progetti Cloud Pro con più ambienti di staging, puoi richiedere spazi di dati di test aggiuntivi per ogni ambiente di staging [inviando una richiesta di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).
   - Magento Open Source: uno spazio dati di produzione; nessuno spazio dati di prova

1. Seleziona lo **Spazio dati** da utilizzare per la configurazione corrente dell&#39;archivio [!DNL Commerce].

>[!NOTE]
>
>Se si dispone di istanze separate da integrare con Commerce Services, [inviare un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) per richiedere un nuovo progetto SaaS per ogni istanza aggiuntiva. Dopo aver creato il progetto SaaS, configura l’integrazione dei servizi Commerce per l’istanza utilizzando la stessa chiave API e selezionando il nuovo progetto SaaS per lo spazio dati.

>[!WARNING]
>
> Se generi nuove chiavi nella sezione Portale API di Il mio account, aggiorna immediatamente le chiavi API nella configurazione Amministratore. Se generi nuove chiavi e non le aggiorni nell’amministratore, le estensioni SaaS non funzioneranno più e perderai dati preziosi.

Per modificare i nomi del progetto SaaS o dello spazio dati, fare clic su **Rinomina** accanto a uno dei due. La modifica del nome non influisce sul servizio, in quanto il nome è solo un’etichetta per identificare e distinguere tra progetti e spazi di dati.

## Organizzazione IMS (opzionale) {#organizationid}

Per collegare la tua istanza di Adobe Commerce a Adobe Experience Platform, accedi al tuo account di Adobe utilizzando il tuo Adobe ID. Dopo l’accesso, l’organizzazione IMS associata al tuo account Adobe viene visualizzata in questa sezione.

## Esportazione dati SaaS

Quando l&#39;istanza [!DNL Commerce] si connette a [!DNL Commerce Services], il processo di esportazione dei dati SaaS esporta i dati Commerce dal server [!DNL Commerce] in [!DNL Commerce SaaS Services] in modo che possano essere sincronizzati con i servizi Commerce connessi. In Admin, puoi controllare lo stato di sincronizzazione utilizzando [Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Per informazioni dettagliate, vedere la [Guida all&#39;esportazione dei dati SaaS](../data-export/overview.md).
