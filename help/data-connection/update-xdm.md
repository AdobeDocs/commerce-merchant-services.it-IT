---
title: Aggiungere gruppi di campi allo schema XDM
description: Scopri come aggiungere gruppi di campi specifici di Adobe Commerce a uno schema XDM.
exl-id: 4401bbe7-1ccc-4349-a998-9e9ee9db590f
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 4a5877d6e1a5c7d840e36f4913306b0c440bbac5
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Aggiungere gruppi di campi allo schema XDM

Uno dei [passaggi di onboarding](overview.md#onboarding-steps) per utilizzare [!DNL Data Connection] l’estensione consiste nell’accedere all’area di lavoro dello stream di dati e [creare un flusso di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) specifico per Adobe Commerce. Quando crei tale flusso di dati, devi anche selezionare uno schema XDM che rappresenti i dati che intendi acquisire. Questo argomento descrive i gruppi di campi che lo schema XDM deve includere per raccogliere correttamente i dati forniti da Adobe Commerce [Eventi](events.md).

1. Se non disponi già di uno schema XDM, [creare](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#create) uno. Altrimenti, [modifica](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#edit) lo schema XDM esistente nell’interfaccia utente di Adobe Experience Platform.

1. [Aggiungi](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#add-field-groups) i seguenti gruppi di campi specifici di Commerce:

   - Ricerca nel sito
   - Visita pagina web
   - Processo di accesso utente
   - Chiavi di riferimento
   - Dettagli di contatto personali
   - Dettagli Commerce
   - Adobe Analytics ExperienceEvent Commerce (se desideri inviare dati ad Adobe Analytics)
   - Mappa identità

   >[!NOTE]
   >
   > Non impostare alcun gruppo di campi specifico di Commerce come `Primary identity`. In questo modo il campo viene identificato come obbligatorio e l’Experience Platform prevede che tale campo venga inserito in ogni evento. Se tale campo è assente, l’acquisizione dei dati non riesce.

   Lo schema XDM ora contiene gruppi di campi specifici di Commerce, in modo che i dati raccolti da Commerce [Eventi](events.md) è rappresentato in XDM.

1. [Creare un set di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) in base allo schema creato o aggiornato.

   Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

1. [Creare un flusso di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) e seleziona lo schema XDM che contiene i gruppi di campi specifici di Commerce e il set di dati corrispondente.

   Lo stream di dati inoltra i dati raccolti al set di dati. I dati vengono rappresentati nel set di dati in base allo schema selezionato.
