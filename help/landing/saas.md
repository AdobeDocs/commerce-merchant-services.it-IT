---
title: Connettore Commerce Services
description: Scopri come integrare la tua istanza di Adobe Commerce o di Magento Open Source nei servizi utilizzando le chiavi API di produzione e sandbox.
exl-id: 28027a83-449b-4b96-b926-a7bfbfd883d8
feature: Services, Saas
role: Admin, User
source-git-commit: e5d9576f0c326dd3a97eeaf9831db0d89b85caff
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Alcune funzioni di Adobe Commerce e di Magento Open Source sono basate su [!DNL Commerce Services]  e distribuito come SaaS (software as a service). Per utilizzare questi servizi, è necessario connettere [!DNL Commerce] utilizzando le chiavi API di produzione e sandbox e specifica lo spazio di dati in [configurazione](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html). È necessario configurarlo una sola volta.

## Servizi disponibili {#availableservices}

Di seguito sono elencati i [!DNL Commerce] funzionalità accessibili tramite [!DNL Commerce Services Connector]:

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

Ad alto livello, la [!DNL Commerce Services Connector] è costituito dai seguenti elementi essenziali:

![Architettura di Commerce Services Connector](assets/saas-config-sync-workflow.png)

Le sezioni seguenti descrivono ciascuno di questi elementi in modo più dettagliato.

## Credenziali {#apikey}

Le chiavi API di produzione e sandbox sono generate dal [!DNL Commerce] conto del titolare della licenza, identificato da un unico [!DNL Commerce] ID (MageID). Per superare la convalida dell&#39;adesione per servizi quali [!DNL Product Recommendations] o [!DNL Live Search], il titolare della licenza dell’organizzazione dell’esercente può generare l’insieme di chiavi API purché l’account sia in buono stato. Le chiavi possono essere condivise in base alle necessità con l&#39;integratore di sistemi o il team di sviluppo che gestisce progetti e ambienti per conto del titolare della licenza. Inoltre, gli integratori di soluzioni sono anche autorizzati a utilizzare [!DNL Commerce Services]. Se sei un integratore di soluzioni, il firmatario del [!DNL Commerce] Il contratto del partner deve generare le chiavi API.

### Generare le chiavi API di produzione e sandbox {#genapikey}

1. Accedi al tuo [!DNL Commerce] account in [https://account.magento.com](https://account.magento.com/){:target=&quot;_blank&quot;}.

1. Sotto **Magento** , seleziona **Portale API** sulla barra laterale.

1. Dalla sezione _Ambiente_ menu, seleziona **Produzione** o **Sandbox**.

1. Immetti un nome in _Chiavi API_ e fai clic su **Aggiungi nuovo**.

   Viene visualizzata una finestra di dialogo per il download della nuova chiave.

   ![Scarica chiave privata](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Questa è l&#39;unica opportunità di copiare o scaricare le chiavi.

1. Clic **Scarica** quindi fai clic su **Annulla**.

1. Ripeti i passaggi precedenti per ogni ambiente (produzione e sandbox).

   Il **Chiavi API** Nella sezione sono ora visualizzate le chiavi API (pubbliche). Sono necessari sia i tasti di produzione che i tasti sandbox (pubblico+privato) quando [selezionare o creare un progetto SaaS](#createsaasenv).

## Configurazione SaaS {#saasenv}

[!DNL Commerce] le istanze devono essere configurate con un progetto SaaS e uno spazio dati SaaS in modo che [!DNL Commerce Services] può inviare i dati alla posizione giusta. Un progetto SaaS raggruppa tutti gli spazi di dati SaaS. Gli spazi dati SaaS vengono utilizzati per raccogliere e memorizzare dati che consentono [!DNL Commerce Services] al lavoro. Alcuni di questi dati possono essere esportati da [!DNL Commerce] e alcuni possono essere raccolti dal comportamento dell’acquirente nella vetrina. Tali dati vengono quindi salvati in modo permanente nell’archiviazione cloud protetta.

Per [!DNL Product Recommendations], lo spazio dati SaaS contiene dati di catalogo e comportamentali. Puoi puntare una [!DNL Commerce] a uno spazio di dati SaaS da [selezione](https://docs.magento.com/user-guide/configuration/services/saas.html) nel [!DNL Commerce] configurazione.

>[!WARNING]
>
> Utilizza lo spazio dati SaaS di produzione solo per la produzione [!DNL Commerce] per evitare conflitti di dati. In caso contrario, si rischia di inquinare i dati del sito di produzione con i dati di test, causando ritardi nell’implementazione. Ad esempio, i dati del prodotto di produzione potrebbero essere erroneamente sovrascritti dai dati di staging, come gli URL di staging.

### Selezionare o creare un progetto SaaS {#createsaasenv}

Per selezionare o creare un progetto SaaS, richiedi [!DNL Commerce] Chiave API da [!DNL Commerce] titolare della licenza per il tuo negozio.

1. Il giorno _Amministratore_ barra laterale, vai a **Sistema** > Servizi > **Connettore Commerce Services**.

   Se non vede il **[!UICONTROL Commerce Services Connector]** sezione nella sezione [!DNL Commerce] , installare [!DNL Commerce] moduli per il [[!DNL Commerce] servizio](#availableservices). Inoltre, assicurati che le `magento/module-services-id` è installato.

1. In _Chiavi API sandbox_ e _Chiavi API di produzione_ sezioni, incolla i valori chiave.

   Le chiavi private devono includere `----BEGIN PRIVATE KEY---` all’inizio della chiave e `----END PRIVATE KEY----` alla fine della chiave privata.

1. Clic **Salva**.

Tutti i progetti SaaS associati alle chiavi vengono visualizzati nel **Progetto** campo in **Identificatore SaaS** sezione.

1. Se non esistono progetti SaaS, fai clic su **Crea progetto**. Quindi nel **Progetto** immettere un nome per il progetto SaaS.

   Quando crei un progetto SaaS, [!DNL Commerce] genera uno o più spazi di dati SaaS a seconda [!DNL Commerce] licenza:
   - Adobe Commerce: uno spazio dati di produzione; due spazi dati di test
   - Magento Open Source: uno spazio dati di produzione; nessuno spazio dati di prova

1. Seleziona la **Spazio dati** da utilizzare per la configurazione corrente del [!DNL Commerce] archiviare.

>[!WARNING]
>
> Se generi nuove chiavi nella sezione Portale API di Il mio account, aggiorna immediatamente le chiavi API nella configurazione Amministratore. Se generi nuove chiavi e non le aggiorni nell’amministratore, le estensioni SaaS non funzioneranno più e perderai dati preziosi.

Per modificare i nomi del progetto SaaS o dello spazio dati, fare clic su **Rinomina** accanto a uno dei due. La modifica del nome non influisce sul servizio, in quanto il nome è solo un’etichetta per identificare e distinguere tra progetti e spazi di dati.

## Organizzazione IMS (opzionale) {#organizationid}

Per collegare la tua istanza di Adobe Commerce a Adobe Experience Platform, accedi al tuo account di Adobe utilizzando il tuo Adobe ID. Dopo l’accesso, l’organizzazione IMS associata al tuo account Adobe viene visualizzata in questa sezione.

## Sincronizzazione catalogo

Quando [!DNL Commerce] l’istanza si connette correttamente a [!DNL Commerce Services], il processo di sincronizzazione del catalogo esporta i dati di prodotto dal tuo [!DNL Commerce] server a [!DNL Commerce Services]. Attualmente, solo Product Recommendations utilizza il servizio di sincronizzazione catalogo. [Ulteriori informazioni](catalog-sync.md) informazioni sul processo di sincronizzazione del catalogo.
