---
title: Note sulla versione
description: Informazioni aggiornate sulla versione di [!DNL Data Connection] estensione da Adobe Commerce.
exl-id: 7636664b-488a-46f7-8d19-a9faac126aec
feature: Personalization, Integration, Release Notes
source-git-commit: ace61fa579404962a9ca3eb97f61ed50bc43db52
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# Note sulla versione

>[!IMPORTANT]
>
>Il connettore di Experience Platform è stato rinominato in [!DNL Data Connection].

Queste note sulla versione contengono aggiornamenti del [!DNL Data Connection] e include:

![Nuovo](../assets/new.svg) - Nuove funzioni
![Correzione](../assets/fix.svg) - Correzioni e miglioramenti
![Bug](../assets/bug.svg) - Problemi noti

Per modifiche e correzioni di funzionalità relative alle estensioni utilizzate da [!DNL Data Connection] estensione, consulta **Aggiornamenti dei servizi supportati**.

Consulta [Prossime versioni](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html) per informazioni sulle pianificazioni delle versioni e sul supporto.

Consulta la documentazione per gli sviluppatori per [scopri quali versioni di Commerce supportano questo modulo](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html).

## Aggiornamenti dei servizi supportati

Queste note sulla versione descrivono le modifiche e le correzioni relative alle estensioni utilizzate da [!DNL Data Connection] estensione.

+++Aggiornamenti dei servizi supportati

_24 gennaio 2024_

![Nuovo](../assets/new.svg) - Aggiornato il `data-services-b2b` estensione per includere un nuovo evento di richiesta di acquisto denominato [deleteRichiesteElenco](events.md#deleterequisitionlist) per gli esercenti B2B.

_16 novembre 2023_

![Correzione](../assets/fix.svg) - È stato risolto un problema che causava la visualizzazione errata di un messaggio di errore quando si effettuava un ordine con più indirizzi di spedizione.
![Correzione](../assets/fix.svg) - È stato risolto un problema in [productPageView](events.md#productpageview) evento in cui `productListItems.priceTotal` il campo evento non convertiva il prezzo dopo aver cambiato la valuta nella visualizzazione store.
![Correzione](../assets/fix.svg) - È stato risolto un problema in `productListItems` campo evento in cui il codice valuta non veniva aggiornato quando l’esercente cambiava la visualizzazione del negozio.

_10 ottobre 2023_

![Nuovo](../assets/new.svg) - Aggiunti nuovi eventi di stato dell&#39;ordine: [Ordine fatturato](events-backoffice.md#orderinvoiced), [Restituzione articolo ordine avviata](events-backoffice.md#orderitemsreturninitiated), e [Restituzione articolo ordine completata](events-backoffice.md#orderitemreturncompleted).
![Correzione](../assets/fix.svg) - È stato risolto un problema a causa del quale le modifiche alla configurazione della valuta non venivano applicate negli eventi dopo l’aggiornamento della cache.
![Correzione](../assets/fix.svg) - È stato corretto un errore che si verificava quando non veniva visualizzato il messaggio di conferma dell’ordine se era stato abilitato il posizionamento asincrono dell’ordine.
![Nuovo](../assets/new.svg) - Dati aggiunti a [addToRichiesteList](events.md#addtorequisitionlist) nella pagina di visualizzazione Categoria.
![Correzione](../assets/fix.svg) - È stato risolto un problema in `selectedOptions` dati in [addToRichiesteList](events.md#addtorequisitionlist) quando i prodotti vengono aggiunti dalla pagina di conferma dell’ordine.
![Nuovo](../assets/new.svg) - Dati prodotto aggiunti a [addToRichiesteList](events.md#addtorequisitionlist) evento quando i prodotti vengono aggiunti all&#39;elenco delle richieste dalla pagina di visualizzazione Categoria.
![Nuovo](../assets/new.svg) - Aggiunto [addToRichiesteList](events.md#addtorequisitionlist) evento quando i prodotti configurabili vengono aggiunti all&#39;elenco delle richieste di acquisto dalla pagina di visualizzazione Prodotto.
![Nuovo](../assets/new.svg) - Aggiunto [addToRichiesteList](events.md#addtorequisitionlist) e [removeFromRichiesteList](events.md#removefromrequisitionlist) eventi quando la quantità di prodotto viene aumentata e/o diminuita da un elenco di richieste di acquisto.

_10 giugno 2023_

![Correzione](../assets/fix.svg) - È stato risolto un problema che si verificava quando `orderId` non passato nel contesto a causa di prefissi nell’identificatore dell’ordine Commerce.
![Correzione](../assets/fix.svg) - Configurazioni criteri per la sicurezza dei contenuti aggiornate.

_30 marzo 2023_

![Nuovo](../assets/new.svg) - Aggiunta di un&#39;estensione denominata `data-services-b2b` che include [eventi elenco richieste di acquisto](events.md#b2b-events) per gli esercenti B2B.
![Nuovo](../assets/new.svg) - Aggiunto il `uniqueIdentifier` campo a [ricerca](events.md#search-events) eventi. Questo nuovo campo consente ai commercianti di fare riferimento incrociato tra le richieste di ricerca e le risposte di ricerca.

_12 ottobre 2022_

![Nuovo](../assets/new.svg) - Aggiunti due [eventi vetrina](events.md), `openCart` e `removeFromCart`, all’SDK e al Collector degli eventi Adobe Commerce Storefront.
![Nuovo](../assets/new.svg) - Aggiunta del supporto per [Vetrina AEM](overview.md#aem-support).

+++

## 3.1.1.

_19 marzo 2024_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) È stato aggiunto il supporto per PHP 8.3.

## 3.2.0-beta2

_4 marzo 2024_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) - Se partecipi alla versione beta, assicurati che il tuo `composer.json` il file presenta le seguenti caratteristiche a livello di radice: ` "minimum-stability": "beta"`.
![Nuovo](../assets/new.svg) - Aggiunta la possibilità di [aggiungi attributi personalizzati](update-xdm.md#update-schema-with-time-series-behavioral-and-back-office-event-data).
![Nuovo](../assets/new.svg) - Aggiunta la possibilità di [raccogliere e inviare record di profilo](connect-data.md#send-customer-profile-data) e i dati di Experience Platform.

## 3.1.0.

_16 novembre 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) - Il connettore di Experience Platform è stato rinominato in [!DNL Data Connection].
![Correzione](../assets/new.svg) - Aggiunta la possibilità di registrare la risposta di errore se Adobe IMS non è in grado di generare il token di accesso.
![Correzione](../assets/new.svg) : è stato aggiunto un messaggio di notifica se si tenta di sincronizzare gli ordini cronologici ma non sono state specificate le credenziali dell’account.

## 3,0,0

_10 ottobre 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

Questa è una versione principale. [Modifica](install.md#update-the-data-connection) file compositore.json principale del progetto.

![Nuovo](../assets/new.svg) - Disponibilità generale per [invia ordine storico](connect-data.md#send-historical-order-data) dati e stato dell’Experience Platform.
![Nuovo](../assets/new.svg) - Aggiunta del supporto per OAuth 2.0 quando [configura](connect-data.md#connect-commerce-data-to-adobe-experience-platform) il [!DNL Data Connection] estensione.
![Nuovo](../assets/new.svg) - Supporto terminato per Adobe Commerce 2.4.3.

## 2.3.0.

_27 giugno 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) - Aggiunta la possibilità di [disattivare l&#39;invio di eventi storefront](connect-data.md#data-collection) all&#39;Experience Platform.
![Correzione](../assets/fix.svg) - Configurazioni criteri per la sicurezza dei contenuti aggiornate.
![Correzione](../assets/fix.svg) - È stato corretto il supporto per gli eventi di back office nella versione 2.4.7 di Commerce.
![Nuovo](../assets/new.svg) - È stato aggiunto un messaggio di notifica sull’annullamento della validità della cache quando si salvano le modifiche apportate al [!DNL Data Connection] modulo di estensione.


## 3.0.0-beta1 (solo interno)

_13 giugno 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) - (Beta) Aggiunta la possibilità di [invia ordine storico](connect-data.md#beta-send-historical-order-data) dati e stato dell’Experience Platform.

## 2.2.0.

_30 marzo 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) - Il pacchetto `commerce-data-export` e `saas-export` dipendenze con `experience-platform-connector` estensione. In precedenza, era necessario installare queste dipendenze separatamente. Queste dipendenze, insieme alla configurazione dell’esercente, consentono l’elaborazione lato server di [eventi di back office](events-backoffice.md).
![Nuovo](../assets/new.svg) - È stato aggiunto un nuovo evento back office denominato [`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted).

## 2.1.1.

_28 febbraio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) - Aggiunta del supporto per PHP 8.2 per tutti [!DNL Data Connection] estensioni.

## 2.1.0.

_17 gennaio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) - Aggiornato il [[!DNL Data Connection] Amministrazione estensioni](connect-data.md) in modo da poter specificare il proprio AEP Web SDK (alloy).
![Correzione](../assets/fix.svg) È stato modificato in utilizzando `identityMap` invece di `personID` quando si imposta l’identità primaria per tutti i dati inviati al server Edge di.

## 2.0.1.

_10 novembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) - Ora il contesto Adobe Experience Platform viene impostato solo dopo il caricamento di Storefront Event Collector e Storefront Event SDK.

## 2,0,0

_12 ottobre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) - Aggiunta la possibilità di specificare il proprio Web SDK AEP quando [connessione](connect-data.md) la tua istanza di Adobe Commerce all’Experience Platform.
![Correzione](../assets/fix.svg) : è stato aggiornato il requisito dell’ambito dello stream di dati in modo che gli ID dello stream di dati debbano avere l’ambito del sito web anziché della visualizzazione archivio.

## 1,0,0

_9 agosto 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) - Versione di disponibilità generale.
