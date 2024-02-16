---
title: Aggiornamento dello schema dei record di profilo per l’acquisizione di dati Commerce
description: Scopri come creare schemi, set di dati e flussi di dati per raccogliere e inviare all’Experience Platform i dati dei record del profilo Commerce.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 8456f9b81812cf8ace55b7406d8b4fe50332c17a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Aggiornamento dello schema dei record di profilo per l’acquisizione di dati Commerce

>[!NOTE]
>
>Questa funzione è in versione beta. Se desideri partecipare al programma beta, invia una richiesta a [dataconnection@adobe.com](mailto:dataconnection@adobe.com).

Quando gli acquirenti creano un profilo nel sito Commerce, viene creato un record di profilo e i dati vengono acquisiti. È necessario creare uno schema e un set di dati specifici per quel record di profilo prima di poter inviare in streaming i dati di profilo all’Experience Platform.

1. [Crea](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#create) uno schema e impostare la classe su **Profilo individuale**.

1. [Aggiungi](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#add-field-groups) i seguenti gruppi di campi specifici per il profilo:

   - identityMap
   - Dettagli demografici
   - Dettagli di contatto personali
   - Dettagli dell’account utente

1. [Abilita](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#profile) lo schema per il profilo.

   Quando uno schema è abilitato per il profilo, tutti i set di dati creati da questo schema partecipano a Real-Time CDP, che unisce dati da origini diverse per creare una visualizzazione completa di ciascun cliente.

1. [Creare un set di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) in base allo schema creato o aggiornato.

   Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

Con lo schema e il set di dati configurati per i dati del record del profilo cliente, puoi [configura](connect-data.md#data-collection) la tua istanza Commerce per raccogliere e inviare tali dati ad Experienci Platform.

Per creare uno schema, un set di dati e uno stream di dati per i dati di eventi comportamentali e di back office, consulta [aggiornare gli schemi evento delle serie temporali per l’acquisizione dei dati di Commerce](update-xdm.md).
