---
title: Record profilo
description: Scopri quali dati acquisisce un record di profilo.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bd04730d-e37a-48a9-822b-0f4aa68a4651
source-git-commit: 89607d22ba8e69e0c98fce97e041022e33d01c07
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# [!DNL Data Connection] Record profilo (Beta)

Di seguito sono descritti i dati del record del profilo di Commerce disponibili quando si installa [!DNL Data Connection] estensione. I dati nei record del profilo vengono inviati a Adobe Experience Platform.

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
| `billingAddress` | Indirizzo postale di fatturazione. |
| `billingAddress.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada. |
| `billingAddress.street2` | Seconda riga facoltativa sulle informazioni stradali. |
| `billingAddress.city` | Il nome della città. |
| `billingAddress.state` | Nome dello stato. Questo è un campo in formato libero. |
| `billingAddress.country` | Il nome del territorio amministrato dal governo. Diverso da `xdm:countryCode`, questo è un campo in formato libero che può contenere il nome del paese in qualsiasi lingua. |
| `billingAddressPhone` | Numero di telefono associato all’indirizzo di fatturazione. |
| `billingAddressPhone.number` | Il numero di telefono. Nota che il numero di telefono è una stringa e può includere caratteri significativi come parentesi `()`, trattini `-`, o caratteri per indicare identificatori di sotto-composizione come le estensioni `x` ad esempio:  `1-353(0)18391111` o `+613 9403600x1234`. |
| `shippingAddress` | L’indirizzo postale di spedizione. |
| `shippingAddress.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada. |
| `shippingAddress.street2` | Seconda riga facoltativa sulle informazioni stradali. |
| `shippingAddress.city` | Il nome della città. |
| `shippingAddress.state` | Nome dello stato. Questo è un campo in formato libero. |
| `shippingAddress.country` | Il nome del territorio amministrato dal governo. Diverso da `xdm:countryCode`, questo è un campo in formato libero che può contenere il nome del paese in qualsiasi lingua. |
| `shippingAddressPhone` | Numero di telefono associato all’indirizzo di spedizione. |
| `shippingAddressPhone.number` | Il numero di telefono. Nota che il numero di telefono è una stringa e può includere caratteri significativi come parentesi `()`, trattini `-`, o caratteri per indicare identificatori di sotto-composizione come le estensioni `x` ad esempio:  `1-353(0)18391111` o `+613 9403600x1234`. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.startDate` | La data in cui il profilo è stato creato per la prima volta. |

>[!NOTE]
>
>Ogni record di profilo include anche [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) , che include l&#39;ID cliente Commerce generato dal sistema come identificatore principale del profilo e un ID e-mail utilizzato come identificatore secondario.

Scopri come [creare uno schema specifico per il record del profilo](profile-data.md) che possono acquisire i dati dai record del profilo.
