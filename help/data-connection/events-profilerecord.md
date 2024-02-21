---
title: Record profilo
description: Scopri quali dati acquisisce un record di profilo.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: 655b5d18a4fb77232523c9c18a9fb362de93c70a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# [!DNL Data Connection] Record profilo (Beta)

>[!NOTE]
>
>Questa funzione è in versione beta. Se desideri partecipare al programma beta, invia una richiesta a [dataconnection@adobe.com](mailto:dataconnection@adobe.com).

Di seguito sono descritti i dati del record del profilo di Commerce disponibili quando installi [!DNL Data Connection] estensione. I dati nei record del profilo vengono inviati a Adobe Experience Platform.

## Record profilo

Gli aggiornamenti dei record profilo sono disponibili nell’Experience Platform quando viene creato, aggiornato o eliminato un nuovo profilo.

### Dati raccolti dal record del profilo

Di seguito sono descritti i dati acquisiti per un record di profilo.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Entrambi `_id` e `_type` contain [valori namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L’identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l’origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Contiene informazioni sul cliente. |
| `person.name` | Contiene informazioni sul nome del cliente. |
| `person.name.firstName` | Contiene il nome del cliente. |
| `person.name.lastName` | Contiene il cognome del cliente. |
| `person.birthDate` | Data di nascita dell’acquirente. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.startDate` | La data in cui il profilo è stato creato per la prima volta. |

>[!NOTE]
>
>Ogni record di profilo include anche [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) , che include l&#39;indirizzo e-mail dell&#39;acquirente, se disponibile, ed ECID.

Scopri come [creare uno schema specifico per il record del profilo](profile-data.md) che possono acquisire i dati dai record del profilo.
