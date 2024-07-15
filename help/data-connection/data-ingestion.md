---
title: Tipi di dati Commerce
description: Scopri i tipi di dati che puoi raccogliere e inviare all’Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
exl-id: 1cdf3fcb-fb16-47ef-be5c-0ebbf1feaff4
source-git-commit: d5d5741442973d86a2d403edc940d18333defd67
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Tipi di dati Commerce

L&#39;estensione [Connessione dati](overview.md) collega i dati Commerce all&#39;Experience Platform. I dati da utilizzare nell&#39;Experience Platform sono raggruppati in due tipi di comportamento: dati di serie temporali, che appartengono alla classe **Experience Event**, e dati di record, che appartengono alla classe **Individual Profile**.

Ulteriori informazioni su [comportamento dati](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#data-behaviors) e [classi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#class) in Experience Platform.

## Dati delle serie temporali

I dati di serie temporali forniscono un&#39;istantanea del sistema nel momento in cui un oggetto record ha intrapreso un&#39;azione, direttamente o indirettamente. Ad esempio, quando un acquirente esplora un prodotto sul tuo sito, aggiunge un prodotto al carrello, effettua un ordine e così via. I dati della serie temporale vengono acquisiti nell&#39;Experience Platform utilizzando uno schema la cui classe è impostata su **Experience Event**.

### Dati acquisiti delle serie temporali

Consulta [eventi comportamentali](events.md) e [eventi di back office](events-backoffice.md) per scoprire quali dati vengono acquisiti quando viene generato un evento di serie temporale.

### Schema necessario per acquisire i dati evento della serie temporale

Scopri come [creare uno schema](update-xdm.md) in grado di acquisire dati di eventi comportamentali e di serie temporali di back office.

## Registra dati

I dati del record forniscono informazioni sugli attributi di un soggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo. Ad esempio, un acquirente sul tuo sito crea un account e che genera i dati del record. Questi dati vengono acquisiti nell&#39;Experience Platform utilizzando uno schema la cui classe è impostata su **Profilo individuale**. Puoi inviare i dati del record al servizio di segmentazione e gestione dei profili di Adobe: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it).

### Dati record profilo acquisiti

Consulta [dati del record del profilo cliente](events-profilerecord.md) per sapere quali dati vengono acquisiti quando viene generato un record del profilo.

### Schema necessario per acquisire i dati del record del profilo

Scopri come [creare uno schema](profile-data.md) in grado di acquisire i dati del record del profilo.
