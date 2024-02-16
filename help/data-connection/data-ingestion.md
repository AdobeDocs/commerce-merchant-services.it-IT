---
title: Tipi di dati Commerce
description: Scopri i tipi di dati che puoi raccogliere e inviare all’Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: d5824e11b4961b518e35fcf56ff2c7ee00480617
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Tipi di dati Commerce

Il [Estensione connessione dati](overview.md) collega i dati Commerce all’Experience Platform. I dati da utilizzare nell’Experience Platform sono raggruppati in due tipi di comportamento: dati di serie temporali, che appartengono al **Evento esperienza** classe e record, che appartiene alla classe **Profilo individuale** classe.

Ulteriori informazioni su [comportamento dei dati](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#data-behaviors) e [classi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#class) in Experience Platform.

## Dati delle serie temporali

I dati di serie temporali forniscono un&#39;istantanea del sistema nel momento in cui un oggetto record ha intrapreso un&#39;azione, direttamente o indirettamente. Ad esempio, quando un acquirente esplora un prodotto sul tuo sito, aggiunge un prodotto al carrello, effettua un ordine e così via. I dati delle serie temporali vengono acquisiti nell’Experience Platform utilizzando uno schema la cui classe è impostata su **Evento esperienza**.

### Dati acquisiti delle serie temporali

Consulta [eventi comportamentali](events.md) e [eventi di back office](events-backoffice.md) per sapere quali dati vengono acquisiti quando viene generato un evento di serie temporale.

### Schema necessario per acquisire i dati evento della serie temporale

Scopri come [creare uno schema](update-xdm.md) che possono acquisire dati di eventi comportamentali e di serie temporali di back office.

## Registra dati

>[!NOTE]
>
>Questa funzione è in versione beta. Se desideri partecipare al programma beta, invia una richiesta a [dataconnection@adobe.com](mailto:dataconnection@adobe.com).

I dati del record forniscono informazioni sugli attributi di un soggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo. Ad esempio, un acquirente sul tuo sito crea un account e che genera i dati del record. Questi dati vengono acquisiti nell’Experience Platform utilizzando uno schema la cui classe è impostata su **Profilo individuale**. Puoi inviare i dati del record al servizio di gestione dei profili e segmentazione di Adobe: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html).

### Dati record profilo acquisiti

Consulta [dati record profilo cliente](events-profilerecord.md) per scoprire quali dati vengono acquisiti quando viene generato un record di profilo.

### Schema necessario per acquisire i dati del record del profilo

Scopri come [creare uno schema](profile-data.md) che possono acquisire i dati del record del profilo.
