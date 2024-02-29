---
title: Aggiornare gli schemi evento serie temporali per l’acquisizione dei dati di Commerce
description: Scopri come creare schemi, set di dati e flussi di dati per raccogliere e inviare dati di eventi di serie temporali per l’acquisizione di dati Commerce.
exl-id: 4401bbe7-1ccc-4349-a998-9e9ee9db590f
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 99d1097b98ea18c8a317613b2366a97db131432f
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# Aggiornare gli schemi evento serie temporali per l’acquisizione dei dati di Commerce

Uno dei [passaggi di onboarding](overview.md#onboarding-steps) per utilizzare [!DNL Data Connection] l’estensione consiste nell’accedere all’area di lavoro dello stream di dati e [creare un flusso di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) specifico per Adobe Commerce. Quando crei tale flusso di dati, devi anche selezionare uno schema che descriva i dati che intendi acquisire. Tale schema deve includere gruppi di campi specifici per l’e-commerce.

Questo articolo fornisce i gruppi di campi che lo schema deve includere per raccogliere correttamente i seguenti dati delle serie temporali forniti dagli eventi di Adobe Commerce:

- [Comportamento](events.md) : include eventi vetrina, di profilo, di ricerca e B2B.
- [Back office](events-backoffice.md) - Include lo stato dell&#39;ordine e gli eventi di profilo.

Ulteriori informazioni su [dati di serie temporali](data-ingestion.md).

Ulteriori informazioni su [nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html).

## Aggiornamento dello schema con i dati comportamentali e di evento di back office delle serie temporali

In questa sezione imparerai ad aggiornare lo schema esistente o a creare uno schema per includere i dati comportamentali e di back office degli eventi.

>[!NOTE]
>
>Consulta [dati evento profilo serie temporali](#time-series-profile-event-data) per scoprire come aggiungere campi specifici per il profilo.

1. Se non disponi già di uno schema, [creare](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#create) uno con la classe impostata su **Evento esperienza**.

1. [Aggiungi](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#add-field-groups) i seguenti gruppi di campi specifici di Commerce (oppure modifica lo schema esistente e aggiungi questi gruppi di campi):

   - Ricerca nel sito
   - Visita pagina web
   - Processo di accesso utente
   - Chiavi di riferimento
   - Dettagli di contatto personali
   - Dettagli canale
   - Dettagli Commerce
   - Adobe Analytics ExperienceEvent Commerce (se desideri inviare dati ad Adobe Analytics)

   >[!NOTE]
   >
   > Non impostare alcun gruppo di campi specifico di Commerce come `Primary identity`. In questo modo il campo viene identificato come obbligatorio e l’Experience Platform prevede che tale campo venga inserito in ogni evento. Se tale campo è assente, l’acquisizione dei dati non riesce.

   Il tuo schema ora contiene gruppi di campi specifici di Commerce, in modo che i dati delle serie temporali raccolti da Commerce [comportamentale](events.md) e [back office](events-backoffice.md) eventi è rappresentato nello schema.

1. [Abilita](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#profile) lo schema per il profilo.

   Quando uno schema è abilitato per il profilo, tutti i set di dati creati da questo schema partecipano a Real-Time CDP, che unisce dati da origini diverse per creare una visualizzazione completa di ciascun cliente.

1. [Creare un set di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) in base allo schema creato o aggiornato.

   Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

1. [Creare un flusso di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) e seleziona lo schema contenente i gruppi di campi specifici di Commerce e il set di dati corrispondente.

   Lo stream di dati inoltra i dati raccolti al set di dati. I dati vengono rappresentati nel set di dati in base allo schema selezionato.

1. **Beta** (Facoltativo) Puoi utilizzare gli attributi personalizzati se desideri trasmettere dati dell’evento back office personalizzato dall’istanza Commerce all’Experience Platform. Questa funzione è in versione beta. Se desideri partecipare al programma beta, invia una richiesta a [dataconnection@adobe.com](mailto:dataconnection@adobe.com). Nella richiesta, includi quanto segue:

   - Il tuo [ID organizzazione Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Ad esempio `organization_id@AdobeOrg`.
   - Elenco degli attributi personalizzati a livello di ordine.
   - Elenco degli attributi a livello di articolo ordine.

   Il team di Adobe Commerce ti contatterà per maggiori informazioni e per i passaggi successivi.

Con gli schemi, i set di dati e i flussi di dati configurati per i dati comportamentali e di back office, puoi [configura](connect-data.md#data-collection) dell’istanza Commerce per raccogliere e inviare tali dati all’Experience Platform.

Per includere le informazioni sul profilo dell&#39;acquirente, vedere la sezione successiva.

## Dati evento profilo serie temporali

I dati dell’evento profilo di serie temporali vengono generati dai seguenti eventi:

- [&#39;accountCreated&#39;](events-backoffice.md#accountcreated)
- [&#39;accountUpdated&#39;](events-backoffice.md#accountupdated)
- [&#39;accountDeleted&#39;](events-backoffice.md#accountdeleted)

Se desideri acquisire i dati dell’evento profilo del cliente nell’Experience Platform, puoi aggiornare lo schema Commerce esistente e utilizzare lo stesso flusso di dati già configurato, oppure puoi creare uno schema e uno stream di dati specifici del profilo. Tale decisione si basa sulla governance dei dati della tua azienda. Le due sezioni successive illustrano entrambi i casi.

### Invia dati evento profilo serie temporale ad Experienci Platform utilizzando lo stream di dati esistente

Per aggiungere serie temporali [dati evento profilo lato server](events-backoffice.md#customer-profile-events-server-side) allo stream di dati di Commerce esistente, aggiungi `Demographic Details` gruppo di campi allo schema. Il tuo schema ora contiene i seguenti gruppi di campi specifici di Commerce:

- Ricerca nel sito
- Visita pagina web
- Processo di accesso utente
- Chiavi di riferimento
- Dettagli di contatto personali
- Dettagli canale
- Dettagli Commerce
- Adobe Analytics ExperienceEvent Commerce (se desideri inviare dati ad Adobe Analytics)
- Nuovo: **Dettagli demografici**

Con l&#39;aggiunta del `Demographic Details` gruppo di campi nello schema di Commerce esistente, il set di dati e lo stream di dati già associati allo schema di Commerce vengono utilizzati per i dati di profilo di questa serie temporale.

### Invia dati evento profilo serie temporale all’Experience Platform in un flusso di dati separato

Se desideri aggiungere [dati evento profilo lato server](events-backoffice.md#customer-profile-events-server-side) in un nuovo stream di dati e schema specifico per il profilo, completa i passaggi seguenti.

1. [Crea](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#create) uno schema e impostare la classe su **Evento esperienza**.

1. [Aggiungi](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#add-field-groups) i seguenti gruppi di campi specifici per il profilo:

   - Dettagli demografici
   - Dettagli di contatto personali
   - Dettagli canale
   - Dettagli Commerce

1. [Abilita](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#profile) lo schema per il profilo.

   Quando uno schema è abilitato per il profilo, tutti i set di dati creati da questo schema partecipano a Real-Time CDP, che unisce dati da origini diverse per creare una visualizzazione completa di ciascun cliente.

1. [Creare un set di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) in base allo schema creato.

   Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

1. [Creare un flusso di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) e seleziona lo schema XDM che contiene i gruppi di campi specifici di Commerce e il set di dati corrispondente.

   Lo stream di dati inoltra i dati raccolti al set di dati. I dati vengono rappresentati nel set di dati in base allo schema selezionato.

Con schemi, set di dati e flussi di dati configurati per i dati del profilo cliente, puoi: [configura](connect-data.md#data-collection) la tua istanza Commerce per raccogliere e inviare tali dati ad Experienci Platform.

Per creare schemi, set di dati e flussi di dati per i dati dei record del profilo, consulta [invia i dati del record del profilo all’Experience Platform](profile-data.md).
