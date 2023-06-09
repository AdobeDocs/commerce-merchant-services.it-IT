---
title: "[!DNL Payment Services] Note sulla versione"
description: Consulta le note sulla versione per informazioni su tutte [!DNL Payment Services] versioni.
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
source-git-commit: e9209d7361d0dd6b6f502df9a898a5a35c53ec1a
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---

# Note sulla versione

Queste note sulla versione descrivono la versione iniziale di [!DNL Payment Services] e includono:

![Nuovo](../assets/new.svg) Nuove funzioni
![Problema risolto](../assets/fix.svg) Correzioni e miglioramenti
![Problema noto](../assets/bug.svg) Problemi noti

Per le modifiche e le correzioni di funzionalità rilasciate al di fuori del normale rilascio di funzionalità con versione, consulta le sezioni Aggiornamenti dei servizi in hosting.

Consulta [Prossime versioni](https://devdocs.magento.com/release/) per informazioni sulle pianificazioni delle versioni e sul supporto.

Consulta [Disponibilità](https://devdocs.magento.com/release/availability.html) nella documentazione per gli sviluppatori per informazioni sulla compatibilità dei prodotti.

## Aggiornamenti dei servizi in hosting

Queste note sulla versione descrivono le modifiche e le correzioni apportate alle funzioni e sono state rilasciate al di fuori delle normali versioni del servizio ospitato.

+++Aggiornamenti dei servizi in hosting

_9 giugno 2023_

![Nuovo](../assets/new.svg)<!-- Issue PAY-4288 --> Ora i commercianti possono [configura _solo_ Pulsanti di pagamento PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#use-only-paypal-payment-buttons)—e _non_ utilizzare l&#39;opzione di pagamento con carta di credito PayPal per fornire diverse opzioni di pagamento senza richiedere l&#39;approvazione della carta di credito PayPal.

![Nuovo](../assets/new.svg)<!-- Issue PAY-4050 --> È stato aggiunto un [visualizzazione dati](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#order-payment-status-data-visualization-view), visualizzato nella pagina Home del servizio di pagamento, per il rapporto Stato pagamento ordine.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-4486--> In precedenza, il pulsante PayPal PayLater non veniva visualizzato nel pagamento per gli esercenti del Regno Unito. La questione è risolta.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-4485--> Le visualizzazioni di visualizzazione dei dati dei rapporti vengono ora visualizzate nella Home di Payment Services quando Payment Services è disabilitato.

_25 gennaio 2023_

![Problema noto](../assets/bug.svg)<!-- Issue PAY-4102 --> Le nuove installazioni di Payment Services non sono in grado di configurare Commerce Services, rendendo Payment Services inutilizzabile. Per risolvere il problema, aggiorna l’estensione Payment Services alla versione 1.5.3.

_12 settembre 2022_

![Nuovo](../assets/new.svg)<!-- Issue PAY-3705 --> Il `increment_id` è ora disponibile per l&#39;utilizzo nella riconciliazione dei pagamenti nei sistemi ERP esterni. Viene propagato al [`custom_id` _e_ `invoice_id`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/data.html#reconcile-with-erp-system), visibile sia nel webhook PayPal che nei dettagli dell&#39;attività esercente per una vincita.

_31 agosto 2022_

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3629 --> Quando un nuovo esercente accede alla Home di Payment Services per la prima volta, la pagina viene caricata immediatamente per visualizzare il contenuto, anziché richiedere l’aggiornamento della pagina.

_9 agosto 2021_

![Nuovo](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay è ora disponibile come Smart Button PayPal. Questo [opzione di pagamento](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-options.html#apple-pay-button) consente ai clienti di utilizzare la funzione Touch ID sul dispositivo iOS o macOS per selezionare Apple Pay. Apple Pay elabora il pagamento utilizzando le credenziali di pagamento della carta di credito e di debito memorizzate sul dispositivo.

_28 giugno 2021_

![Nuovo](../assets/new.svg)<!-- Issue PAY-1720 --> Le controversie per gli ordini dei punti vendita sono ora disponibili in [il rapporto Stato pagamento ordine](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#view-disputes). Puoi intervenire sulle controversie navigando direttamente al Centro di risoluzione PayPal da [!DNL Payment Services].

![Nuovo](../assets/new.svg)<!-- Issue PAY-2854 --> Miglioramenti all’esperienza utente da [!DNL Payment Services] Home includono la possibilità di modificare una configurazione al livello di ereditarietà corrente e miglioramenti alla visualizzazione dell’intestazione e della navigazione.

![Nuovo](../assets/new.svg)<!-- Issue PAY-2854 --> Ora è possibile visualizzare avvisi quando si passa dalla modalità sandbox alla modalità di produzione e quando si tenta di uscire da una visualizzazione con aggiornamenti che non sono stati salvati.

![Nuovo](../assets/new.svg)<!-- Issue PAY-2761 --> Ora puoi personalizzare i dati visualizzati nella sezione [Rapporto stato pagamento ordine](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#show-and-hide-columns) e [Rapporto Pagamenti](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/payouts.html#show-and-hide-columns) visualizzando o nascondendo le colonne tramite il controllo Impostazioni colonna.

+++

## v2.1.0

_9 giugno 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg)<!-- Issue xxx --> È stato aggiunto il supporto per Adobe Commerce 2.4.7-beta1.

![Nuovo](../assets/new.svg)<!-- Issue xxx --> Aggiunto [disponibilità nei seguenti paesi e valute associate](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#availability): Australia, Francia, Regno Unito.

![Nuovo](../assets/new.svg)<!-- Issue PAY-4296 --> Aggiunto [risorse espanse per i ruoli amministratore](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-roles) per garantire che gli utenti amministratori possano creare e gestire gli ordini per i clienti e possano visualizzare Payment Services (Servizi di pagamento) nel menu Sales (Vendite).

![Nuovo](../assets/new.svg)<!-- Issue PAY-4236 --> Aggiunto [annullamento automatico per gli ordini che generano errori durante l&#39;estrazione](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/checkout.html#order-auto-voided-if-error).

![Nuovo](../assets/new.svg)<!-- Issue PAY-4183 --> Funzionalità creata per [mostra il pulsante opzione di pagamento con carta di credito](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#debit-or-credit-card-button) nella pagina di pagamento.

## v2.0.0

_10 marzo 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-4152 --> È stato aggiunto il supporto per PHP 8.2 e Adobe Commerce 2.4.6. Non compatibile con PHP 7.x.

## v1.6.1

_10 marzo 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Correzione](../assets/fix.svg)<!-- Issue PAY-4226 --> È stato risolto un problema che impediva ai nuovi commercianti di servizi di pagamento di utilizzare il pagamento in Admin. Payment Services utilizzava in precedenza l’ID cliente Commerce, che non esiste per i nuovi clienti.

![Correzione](../assets/fix.svg)<!-- Issue PAY-4205 --> È stato risolto un problema che causava la sostituzione dello stato dell&#39;indirizzo di spedizione specificato con lo stato nelle impostazioni di imposta predefinite durante il pagamento tramite [Opzione PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#paypal-smart-buttons). Ora i clienti possono far spedire i loro ordini in uno stato diverso da quello configurato come predefinito nelle impostazioni fiscali dell’esercente.

![Correzione](../assets/fix.svg)<!-- Issue PAY-4202 --> È stato risolto un problema che impediva ai clienti di utilizzare il vaulting delle carte di credito per completare un acquisto o eliminare un metodo di pagamento a scaffale per un negozio. [utilizzando `Authorize and Capture` azione di pagamento](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html#set-payment-services-as-payment-method). In precedenza, quando il cliente tentava di utilizzare o modificare le proprie carte di credito archiviate, veniva visualizzato l’errore &quot;Provider Vault ID not found&quot; (ID archivio provider non trovato).

## v1.6.0

_17 febbraio 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-3540 --> Aggiunto [Funzione di conformità PCI 3DS per gli esercenti che effettuano transazioni nell&#39;Unione europea (UE) e in Gran Bretagna](security.md#3ds). Questo ulteriore livello di sicurezza, che impone agli acquirenti di autenticarsi presso l’emittente della carta di credito, contribuisce a prevenire le frodi online ed è richiesto nell’ambito delle normative di conformità dell’Unione europea (UE).

![Nuovo](../assets/new.svg)<!-- Issue PAY-3609 --> Aggiunta la possibilità di [abilitare il vaulting delle schede in Amministrazione](vaulting.md#use-vaulting-in-the-admin). Questo consente agli esercenti di creare un ordine per i clienti nell’Amministratore utilizzando i propri metodi di pagamento a scaffale.

## v1.5.4

_29 gennaio 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-4110 --> È stato risolto un problema che impediva agli acquirenti di effettuare un ordine utilizzando i pulsanti avanzati sulla pagina del prodotto, sul mini carrello e sul carrello. Gli acquirenti ora possono completare gli ordini con successo.

## v1.5.3

_25 gennaio 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-4102 --> È stata rilasciata una correzione a un problema noto non compatibile con le versioni precedenti. Questa versione blocca la versione dell’estensione Service ID alla versione stabile più recente, che riabilita le nuove installazioni di Payment Services per configurare Commerce Services.

## v1.5.2

_22 dicembre 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3992 --> È stata migliorata la fatturazione in Payment Services quando un metodo di pagamento viene rifiutato.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3999 --> Payment Services ora visualizza correttamente i pulsanti avanzati PayPal per gli esercenti che utilizzano [Fire Checkout&#39;s](https://marketplace.magento.com/swissup-firecheckout.html){target=_blank} modello personalizzato per la pagina di pagamento. In precedenza, i pulsanti venivano visualizzati in modo intermittente.

## v1.5.1

_23 novembre 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-3923 --> Payment Services ora include il numero di versione nell’intestazione dell’agente utente per consentire alle richieste di tenere traccia, filtrare o dichiarare obsoleti gli endpoint non utilizzati.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3968 --> Payment Services ora visualizza correttamente i dati dell&#39;ordine quando un ordine viene effettuato dalla pagina del prodotto utilizzando i pulsanti avanzati.

## v1.5.0

_18 novembre 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-3880 --> Ora un acquirente può [archivia (salva) le informazioni sulla carta di credito durante il pagamento](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html) da utilizzare in un acquisto successivo per lo stesso o un altro negozio all’interno dello stesso account esercente.

![Nuovo](../assets/new.svg)<!-- Issue PAY-3950 --> Gli esercenti possono ora abilitare [Funzione di Instant Purchase Commerce](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html) per i loro negozi in modo che gli acquirenti possano (utilizzare [informazioni su carta di credito archiviate](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html)) per accelerare il pagamento.

## v1.4.1

_14 ottobre 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Correzione](../assets/fix.svg)<!-- Issue PAY-3766 --> Quando il metodo di pagamento di un cliente viene rifiutato, il messaggio di errore visibile è più descrittivo. Consiglia al cliente di inserire nuovamente le informazioni di pagamento e riprovare, provare con un altro metodo di pagamento o contattare la banca per informazioni sulla transazione rifiutata.

## v1.4.0

_30 settembre 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-784 --> Payment Services ora include la possibilità di impostare un account esercente per [utilizzare più account aziendali PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#use-multiple-paypal-accounts). Questo consente al commerciante di gestire i negozi in più paesi utilizzando valute diverse o di utilizzare Adobe Commerce per una parte della tua attività.

![Nuovo](../assets/new.svg)<!-- Issue PAY-3231 --> I commercianti possono [aggiungi un [!UICONTROL Soft Descriptor]](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#add-soft-descriptor) a siti web o a singole configurazioni di visualizzazioni store che vengono visualizzate nei rendiconti bancari delle transazioni dei clienti per delineare marchi, negozi o linee di prodotti.

![Nuovo](../assets/new.svg)<!-- Issue PAY-3707 --> [Attiva o disattiva i campi della carta di credito e gli smart button PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-payment-options) per il pagamento nelle impostazioni di Payment Services.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3546 --> Quando un cliente fa clic **[!UICONTROL Edit cart]**, la pagina viene reindirizzata alla pagina del carrello e mostra gli elementi aggiornati anziché mostrare un carrello vuoto.

## v1.3.1

_6 settembre 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3663 --> Ora, quando un negozio di merchant acquisisce un ordine autorizzato con una valuta non globale, il processo di acquisizione viene completato e non viene visualizzato alcun errore.

## v1.3.0

_9 agosto 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-XX --> Versione con disponibilità generale:[!DNL Payment Services] è ora [compatibile con [!DNL Adobe Commerce] e [!DNL Magento Open Source] versioni da 2.4.0 a 2.4.5](https://devdocs.magento.com/release/availability.html#compatibility).

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-x --> Apple Pay è ora compatibile con il browser Safari v15.5 su dispositivi mobili e desktop.

## v1.2.0

_29 giugno 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Problema noto](../assets/bug.svg)<!-- Issue PAY-x --> Apple Pay non è compatibile con il browser Safari v15.5 su dispositivi mobili e desktop. Con Safari versione 15.5 non puoi completare il pagamento con Apple Pay.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3264 --> In precedenza, quando un utente connesso selezionava un indirizzo di fatturazione/spedizione diverso da quello predefinito per il proprio account, l’estrazione non riusciva. Il problema è stato risolto ed è stato inviato l&#39;indirizzo di fatturazione/spedizione selezionato (anziché l&#39;indirizzo salvato predefinito) ed è stato completato il pagamento.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3314 --> Se disattivi i pulsanti avanzati PayPal per il pagamento, non vengono visualizzati errori.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3330 --> I pagamenti non hanno più esito negativo durante l&#39;estrazione quando un utente ospite immette un numero di telefono che include trattini.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 --> Quando le credenziali di Commerce Services non sono valide, il [!DNL Payment Services] La pagina principale verrà ora visualizzata in Amministrazione. Viene visualizzato un errore di credenziali per avvisarti che le tue credenziali non sono valide.

![Problema noto](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services] è attualmente incompatibile con `commerce-data-export` v101.20 e versioni successive, che la rendono incompatibile con [[!DNL Channel manager] estensione](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html).

## v1.1.0

_31 marzo 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-2127 --> Versione con disponibilità generale:[!DNL Payment Services] è ora [compatibile con [!DNL Adobe Commerce] e [!DNL Magento Open Source] versioni da 2.4.0 a 2.4.4](https://devdocs.magento.com/release/availability.html#compatibility).

![Nuovo](../assets/new.svg)<!-- Issue PAY-2682 --> Il [!DNL Payment Services] estensione per [!DNL Adobe Commerce] e [!DNL Magento Open Source] è ora disponibile per i commercianti canadesi. Gli esercenti possono visualizzare la configurazione dei pagamenti in [Francese](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=fr#carte-de-cr%C3%A9dit-et-devises-accept%C3%A9es) o [Inglese](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#accepted-credit-cards-and-currencies).

![Nuovo](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services] supporta [Dollaro canadese (CAD)](overview.md#accepted-credit-cards-and-currencies) per carte di credito e transazioni PayPal.

![Nuovo](../assets/new.svg)<!-- Issue PAY-2680 --> I commercianti possono [integrato [!DNL Payment Services]](onboard.md) estensione in inglese o francese.

![Nuovo](../assets/new.svg)<!-- Issue PAY-2678 --> Gli esercenti possono ora visualizzare i rapporti finanziari, sia [Stato pagamento ordine](order-payment-status.md) e [Rapporti Pagamenti](payouts.md), in dollari canadesi (CAD).

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-2710 --> [!DNL Payment Services] è ora compatibile con [PHP 8.1](https://www.php.net/releases/8.1/en.php).

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3017 --> È stato migliorato l’avviso relativo alla modalità sandbox per visualizzare gli avvisi corretti con più store.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-2742 --> Ora puoi abilitare e disabilitare i metodi di pagamento disponibili, come Venmo, a livello di visualizzazione punto vendita. In precedenza era possibile configurare i metodi di pagamento solo per il sito Web.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-2277 --> Ora puoi selezionare [attivare o disattivare singoli pulsanti avanzati PayPal](settings.md#payment-buttons).

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-2561 --> I prodotti precedentemente rimossi non vengono visualizzati nel carrello nella _Ordine di revisione_ pagina.

![Problema noto](../assets/bug.svg)<!-- Issue PAY-2842 --> Verifica transazioni con carta di credito [potrebbe non riuscire con PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html) durante l’elaborazione dei pagamenti in un ambiente sandbox.

## v1.0.0

_29 novembre 2021_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-2127 --> Versione con disponibilità generale:[[!DNL Payment Services]](https://marketplace.magento.com/magento-payment-services.html) è ora compatibile con [!DNL Adobe Commerce] e [!DNL Magento Open Source] versioni da 2.4.0 a 2.4.3-p1.

![Nuovo](../assets/new.svg)<!-- Issue PAY-124 --> Il [!DNL Payment Services] estensione per [!DNL Adobe Commerce] e [!DNL Magento Open Source] può essere installato per [[!DNL Adobe Commerce] sull’infrastruttura cloud](install.md#adobe-commerce-on-cloud-infrastructure) o [On-premise](install.md#on-premises) istanze. Questi metodi richiedono l&#39;utilizzo di un&#39;interfaccia della riga di comando.

![Nuovo](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services] supporta un [account sandbox](sandbox.md) che consente agli esercenti di valutare l’estensione in modalità di test.

![Nuovo](../assets/new.svg)<!-- Issue PAY-666 --> I commercianti possono [configurare Payment Services](settings.md) estensione con comportamenti di pagamento di base, come l’utilizzo di [`Authorize and Capture`](production.md#set-payment-services-as-payment-method) passaggio tra ambienti sandbox o di produzione.

![Nuovo](../assets/new.svg)<!-- Issue PAY-780 --> Gli acquirenti possono effettuare il check-out con [!DNL Payment Services] o tramite [creazione manuale degli ordini](create-order.md).

![Nuovo](../assets/new.svg)<!-- Issue PAY-1856 --> Reporting completo, tramite [Stato pagamento ordine](order-payment-status.md) e [Rapporti Pagamenti](payouts.md), sono disponibili per [!DNL Payment Services] per avere una visione chiara degli ordini del tuo negozio e dei relativi pagamenti.

![Nuovo](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services] supporta prezzi flessibili su più livelli, basati sul volume totale di elaborazione, adattati a qualsiasi commerciante.

![Nuovo](../assets/new.svg)<!-- Issue PAY-1443 --> Si può facilmente [personalizzazione dell&#39;aspetto](payments-options.md) di campi smart button e carta di credito PayPal per [!DNL Payment Services] estensione.

![Problema noto](../assets/bug.svg)<!-- Issue PAY-2473 --> Utilizzo di [chiavi di composizione non corrette](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html) durante l&#39;installazione dell&#39;estensione impedisce all&#39;utente di [autenticazione](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html) con il corretto `MAGEID`.

![Problema noto](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services] rapporti [potrebbe non essere sincronizzato immediatamente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html).

![Problema noto](../assets/bug.svg)<!-- Issue PAY-2475 --> Il tuo [Conto sandbox PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html) per [!DNL Payment Services] non può essere verificato se crei tale account durante l’onboarding.
