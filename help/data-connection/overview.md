---
title: Panoramica della guida
description: Scopri come integrare i dati di Adobe Commerce con Adobe Experience Platform utilizzando [!DNL Data Connection] estensione.
exl-id: a8362e71-e21c-4b1d-8e3f-336e748e1018
recommendations: noCatalog
source-git-commit: 4a5877d6e1a5c7d840e36f4913306b0c440bbac5
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 1%

---

# [!DNL Data Connection] panoramica

>[!IMPORTANT]
>
>Il connettore di Experience Platform è stato rinominato in [!DNL Data Connection].

Il [!DNL Data Connection] L&#39;estensione consente ai commercianti di Adobe Commerce di inviare [vetrina](events.md#storefront-events) e [back office](events.md#back-office-events) Adobe Experience Platform in modo che altri prodotti Adobe Experience Cloud, come Adobe Analytics e Adobe Journey Optimizer, possano utilizzare tali dati Commerce. Collegando i dati di Commerce ad altri prodotti in Adobe Experience Cloud, puoi eseguire attività quali analizzare il comportamento degli utenti sul sito, eseguire test AB e creare campagne personalizzate.

[Eventi vetrina](events.md#storefront-events) acquisire interazioni con gli acquirenti, ad esempio `View Page`, `View Product`, `Add to Cart`, e [elenco richieste di acquisto](events.md#b2b-events) informazioni (per gli esercenti B2B). [Back office](events.md#back-office-events) gli eventi acquisiscono informazioni sullo stato di un ordine, ad esempio se un ordine è stato effettuato, annullato, rimborsato, spedito o completato. I dati acquisiti non includono informazioni personali (PII, personally identifiable information). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi. [Ulteriori informazioni](https://www.adobe.com/privacy/experience-cloud.html).

Il [!DNL Data Connection] L’estensione viene visualizzata in Amministrazione di Commerce in **Sistema** > Servizi > **[!DNL Data Connection]**.

![[!DNL Data Connection] visualizzazione amministrazione dell’estensione](assets/epc-adminui.png)

## Prerequisiti {#prereqs}

Per utilizzare [!DNL Data Connection] deve disporre dei seguenti elementi:

- Adobe Commerce 2.4.3 o versione successiva
- Adobe ID e ID organizzazione
- [Adobe Client Data Layer (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html). L’ACDL è necessario per raccogliere i dati dell’evento vetrina.
- Diritti ad altri prodotti Adobe DX

## Passaggi di onboarding

1. [Installa](install.md) il [!DNL Data Connection] estensione.
1. [Accedi](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) al tuo account Adobe e [visualizza per confermare](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255) il tuo ID organizzazione. L’ID organizzazione è l’ID associato alla società di Experience Cloud con provisioning. Questo ID è una stringa alfanumerica composta da 24 caratteri, seguita da (deve includere) `@AdobeOrg`.
1. [Crea o aggiorna](update-xdm.md) lo schema XDM con gruppi di campi specifici di Commerce.
1. [Creare un set di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) in base allo schema creato o aggiornato. Questo set di dati contiene i dati Commerce inviati.
1. [Creare un flusso di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) e seleziona lo schema XDM che contiene i gruppi di campi specifici di Commerce.
1. [Connetti a Commerce Services](../landing/saas.md).
1. [Connetti a Adobe Experience Platform](connect-data.md).

## Pubblico

Questa guida è stata progettata per gli esercenti di Adobe Commerce che desiderano collegare i propri dati Adobe Commerce ad altri prodotti DX Adobe.

### Supporto PWA Studi

Consulta la [PWA Studi](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/) per informazioni su come utilizzare il [!DNL Data Connection] estensione in una vetrina PWA Studi.

### Supporto AEM {#aem-support}

Consulta la [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html) documentazione per scoprire come inviare all’Experience Platform i dati di un evento vetrina da una pagina di prodotto sottoposta a rendering AEM utilizzando l’CIF - [!DNL Data Connection] estensione.

Se hai bisogno di informazioni o hai domande che non sono trattate in questa guida, utilizza le risorse seguenti:

- [Centro assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html){target="_blank"}
- [Ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket){target="_blank"}- Inviate un ticket per ricevere ulteriore aiuto.
