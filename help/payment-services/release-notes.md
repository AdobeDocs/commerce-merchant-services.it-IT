---
title: "[!DNL Payment Services] Note sulla versione"
description: Consulta le note sulla versione per informazioni su tutte le  [!DNL Payment Services]  versioni.
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
source-git-commit: 0800b4a0f9a3297a3490fa11f32e6af0abe67e2a
workflow-type: tm+mt
source-wordcount: '2576'
ht-degree: 0%

---

# Note sulla versione

Queste note sulla versione descrivono la versione iniziale di [!DNL Payment Services] e includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Problema risolto](../assets/fix.svg) correzioni e miglioramenti
![Problema noto](../assets/bug.svg) Problemi noti

Per le modifiche e le correzioni delle funzionalità rilasciate al di fuori della normale versione di rilascio delle funzionalità, controlla le sezioni _Aggiornamenti dei servizi ospitati_.

Per ulteriori informazioni sulle prossime versioni, sul supporto del prodotto e sulle versioni di Adobe Commerce che supportano l&#39;estensione [!DNL Payment Services], consulta gli argomenti Pianificazione della versione [di Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) e [Disponibilità del prodotto](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Aggiornamenti dei servizi in hosting

Queste note sulla versione descrivono le modifiche e le correzioni apportate alle funzioni e sono state rilasciate al di fuori delle normali versioni del servizio ospitato.

+++Aggiornamenti dei servizi in hosting

_15 luglio 2024_

![Nuovo problema](../assets/new.svg)<!-- Issue PAY-5571 --> Ora gli esercenti possono filtrare le transazioni in base all&#39;e-mail del cliente Commerce nel [report delle transazioni](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html). Inserisci l’e-mail del cliente per filtrare le transazioni per quella specifica e-mail.

_9 luglio 2024_

![Nuovo problema](../assets/new.svg)<!-- Issue PAY-5488 --> Ora gli esercenti possono visualizzare l&#39;ID cliente Commerce come colonna nel [report delle transazioni](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html) per identificare le transazioni inserite da un particolare cliente. Inoltre, gli esercenti possono filtrare il rapporto transazioni in base a questo ID cliente Commerce per gli ordini associati.

_5 marzo 2024_

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-5252 --> Ora gli esercenti possono copiare i dati dalle griglie del dashboard selezionando il contenuto di una singola cella.

_10 ottobre 2023_

![Nuovo problema](../assets/fix.svg)<!-- Issue PAY-4888 --> Ora gli esercenti possono filtrare le transazioni con carta di credito e di debito in base alle ultime quattro cifre del numero di carta nel [report Transazioni](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html).

_12 luglio 2023_

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-4587 --> È stato risolto un problema introdotto nella versione [!DNL Payment Services] 2.1.0 che impediva la cancellazione delle autorizzazioni effettuate da versioni precedenti dell&#39;estensione. I commercianti che utilizzano qualsiasi versione di [!DNL Payment Services] possono annullare le autorizzazioni.

_9 giugno 2023_

![Nuovo](../assets/new.svg)<!-- Issue PAY-4288 --> Ora gli esercenti possono [configurare _solo_ pulsanti di pagamento PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#use-only-paypal-payment-buttons) e _non_ utilizzare l&#39;opzione di pagamento PayPal con carta di credito. Questo consente agli esercenti di fornire varie opzioni di pagamento, tra cui i pulsanti di pagamento Venmo e PayPal, e di utilizzare un provider di carte di credito esistente invece dell&#39;opzione di pagamento PayPal con carta di credito.

![Nuovo](../assets/new.svg)<!-- Issue PAY-4050 --> aggiunta [visualizzazione visualizzazione dati](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#order-payment-status-data-visualization-view), visualizzata nella Home page del servizio di pagamento, per il report sullo stato del pagamento dell&#39;ordine.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue PAY-4486-->. In precedenza, il pulsante PayPal PayLater non veniva visualizzato nel checkout per gli esercenti britannici. La questione è risolta.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-4485--> Le visualizzazioni di visualizzazione dei dati dei report sono ora visualizzate nella Home di [!DNL Payment Services] quando[!DNL Payment Services] è disabilitato.

_25 gennaio 2023_

![Problema noto](../assets/bug.svg)<!-- Issue PAY-4102 --> Le nuove installazioni di [!DNL Payment Services] non sono in grado di configurare i servizi Commerce. Rendendo [!DNL Payment Services] inutilizzabile. Per risolvere il problema, aggiorna l&#39;estensione [!DNL Payment Services] alla versione 1.5.3.

_12 settembre 2022_

![Nuovo](../assets/new.svg)<!-- Issue PAY-3705 --> `increment_id` è ora disponibile per l&#39;utilizzo nella riconciliazione dei pagamenti nei sistemi ERP esterni. Viene propagato a [`custom_id` _e_ `invoice_id`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/data.html#reconcile-with-erp-system), visibile sia nel webhook PayPal che nei dettagli dell&#39;attività esercente per un pagamento.

_31 agosto 2022_

![È stato risolto il problema](../assets/fix.svg)<!-- Issue PAY-3629 --> Quando un nuovo commerciante accede alla Home di [!DNL Payment Services] per la prima volta, la pagina ora si carica immediatamente per visualizzare il contenuto anziché richiedere l&#39;aggiornamento della pagina.

_9 agosto 2021_

![Nuovo](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay è ora disponibile come Smart Button PayPal. Questa [opzione di pagamento](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-options.html#apple-pay-button) consente ai clienti di utilizzare la funzionalità Touch ID sul dispositivo iOS o macOS per selezionare Apple Pay. Apple Pay elabora il pagamento utilizzando le credenziali di pagamento della carta di credito e di debito memorizzate sul dispositivo.

_28 giugno 2021_

![Nuove](../assets/new.svg)<!-- Issue PAY-1720 --> controversie per gli ordini del punto vendita sono ora disponibili in [Report stato pagamento ordine](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#view-disputes). Puoi risolvere le controversie navigando direttamente al Centro di risoluzione PayPal da [!DNL Payment Services].

![Nuovo](../assets/new.svg)<!-- Issue PAY-2854 --> I miglioramenti dell&#39;esperienza utente dalla [!DNL Payment Services] Home includono la possibilità di modificare una configurazione al livello di ereditarietà corrente e miglioramenti alla visualizzazione dell&#39;intestazione e della navigazione.

![Nuovo](../assets/new.svg)<!-- Issue PAY-2854 --> Ora puoi visualizzare avvisi quando passi dalla modalità sandbox alla modalità di produzione e quando tenti di uscire da una visualizzazione con aggiornamenti che non sono stati salvati.

![Nuovo](../assets/new.svg)<!-- Issue PAY-2761 --> È ora possibile personalizzare i dati visualizzati nel [report sullo stato dei pagamenti dell&#39;ordine](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#show-and-hide-columns) e nel [report sui pagamenti](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/payouts.html#show-and-hide-columns) visualizzando o nascondendo le colonne tramite il controllo Impostazioni colonna.

+++

## v2.6.0

_4 giugno 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- PAY-4877 --> Ora [!DNL Payment Services] supporta le [funzionalità di determinazione prezzi L2/L3](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/levels-card-payment-transactions.html). Questa funzionalità è disponibile solo per i clienti [!DNL Payment Services] per i quali è abilitata la determinazione prezzi IC++. Se si desidera utilizzare i dati di elaborazione L2/L3 per [!DNL Payment Services], contattare l&#39;account manager [!DNL Payment Services].

![Correzione](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services] consente di abilitare Apple Pay direttamente dall&#39;estensione senza scaricare e ospitare il [file di associazione dominio](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).

## v2.5.0

_23 aprile 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services] ora supporta [le linee guida di Adobe Commerce per il parametro `--db-prefix`](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line) per Adobe Commerce versioni 2.4.7 e successive.

## v2.4.3

_16 aprile 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg)<!-- Issue PAY-5106 --> è stato risolto un problema che popolava in modo errato i totali degli importi degli ordini durante il pagamento tra PayPal e Adobe Commerce. Ora, i commercianti possono garantire che i totali dell&#39;importo dell&#39;ordine siano corretti quando si effettua un ordine.

## v2.4.2

_11 aprile 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- Issue xxx --> Aggiunto supporto per Adobe Commerce 2.4.7.

## v2.4.1

_4 aprile 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg)<!-- PAY-5322 --> di un problema di compatibilità PCI con le versioni più recenti di Adobe Commerce. Adesso [!DNL Payment Services] è adattato ai requisiti di pagamento in Adobe Commerce come opzione di pagamento.

![Correzione](../assets/fix.svg)<!-- PAY-5323 --> PayLater e Venmo sono visualizzati correttamente in Adobe Commerce. È stato corretto un errore che impediva all’amministratore di visualizzare le opzioni di attivazione/disattivazione di PayLater e Venmo.

## v2.4.0

_20 marzo 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![I nuovi](../assets/new.svg)<!-- PAY-4868 --> commercianti possono [configurare Google Pay durante l&#39;intera esperienza di acquisto](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html), in modo analogo ad altri pulsanti di pagamento in[!DNL Payment Services] tramite l&#39;amministratore.

![Nuovo](../assets/new.svg)<!-- PAY-4381 --> [I servizi di pagamento supportano Google Pay tramite GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/), consentendo agli esercenti di avere un&#39;esperienza Commerce headless con il metodo di pagamento Google Pay.

![Nuovo](../assets/new.svg)<!-- PAY-4878 --> Ora la funzione di estrazione di base [!DNL Payment Services] è inclusa nel bundle per Adobe Commerce e gli esercenti di Magento Open Source.[!DNL Payment Services] può ora supportare i commercianti con aziende in qualsiasi area geografica di 200 paesi.Il pagamento di base di [!DNL Payment Services] fornisce le opzioni dare/avere, PayPal, Venmo (se disponibile) e PayLater (se disponibile) in un onboarding self-service.

![Correzione](../assets/fix.svg)<!-- PAY-5291 --> La ricezione della conferma del pagamento per alcune transazioni potrebbe essere ritardata. In questo caso, ora i commercianti possono ottenere uno stato di pagamento aggiornato per un ordine. [I servizi di pagamento rilevano lo stato in sospeso di una transazione di pagamento](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html) in un ordine rilevando le transazioni in sospeso e monitorandole in modo proattivo e aggiornando quando lo stato in sospeso viene acquisito.

## v2.3.4

_1 marzo 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- PAY-5244 --> È stata corretta la compatibilità di estrazione asincrona.

![Correzione](../assets/fix.svg)<!-- PAY-5253 --> è stato corretto un errore che impediva l&#39;eliminazione di un token di Vault non appartenente a [!DNL Payment Services].

## v2.3.3

_14 febbraio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- PAY-5048 --> aggiunto supporto per PHP 8.3

![Correzione](../assets/fix.svg)<!-- PAY-5048 --> è stato corretto un errore con il flag `is_deleted`. Ora gli ordini non hanno esito negativo a causa dello stato `Rejected` inviato dall&#39;estensione.

## v2.3.2

_26 gennaio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg)<!-- PAY-5183 --> di problemi di prestazioni REST/GraphQL risolti. Adesso, il pulsante della carta di credito viene riprodotto quando viene recuperato tramite l’API.

## v2.3.1

_7 dicembre 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- PAY-5047 --> Il marchio della carta di credito o il tipo di metodo di pagamento è ora disponibile nelle seguenti posizioni:

- la pagina ordine cliente nella vetrina
- l’e-mail di conferma dell’ordine inviata all’acquirente
- dalla [visualizzazione dettagli ordine](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html#view-an-order) in Commerce Admin.

## v2.3.0

_1 dicembre 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- PAY-4381 --> [Payment Services ora supporta l&#39;integrazione con GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/). Con il supporto GraphQL per i pulsanti di pagamento PayPal, i campi ospitati e Apple Pay,[!DNL Payment Services] ora supporta una configurazione di Commerce headless.

## v2.2.1

_27 settembre 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![È stato risolto un problema](../assets/fix.svg)<!-- Issue PAY-4870 --> che popolava in modo errato il nuovo attributo di intestazione in Storefront durante l&#39;invio della versione dell&#39;estensione con la versione più recente. In precedenza, con la versione `1.3.0` del connettore Commerce Services, non era possibile estendere `User-Agent header` dall&#39;estensione [!DNL Payment Services].

## v2.2.0

_30 agosto 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- PAY-4638 --> Aggiunta integrazione [con Signifyd](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security-compliance/fraud-protection.html), che fornisce servizi automatizzati di protezione dalle frodi.

![Nuovo](../assets/new.svg)<!-- PAY-3981 --> [Apple Pay è stato promosso a un&#39;opzione di pagamento separata](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=en#apple-pay-button), al di fuori dei pulsanti di pagamento PayPal, per aumentare la visibilità dell&#39;opzione di pagamento da parte dell&#39;acquirente e consentire agli esercenti di controllare il posizionamento e lo stile di Apple Pay.

![Nuovo](../assets/new.svg)<!-- PAY-4002 --> è stata migliorata l&#39;esperienza utente relativa al pagamento dei campi della carta di credito, inclusi miglioramenti di stile come l&#39;aggiunta di icone di pagamento, per ridurre il carico cognitivo dell&#39;acquirente e aumentare le conversioni.

![Nuovo](../assets/new.svg)<!-- PAY-4002 --> è stata aggiunta la funzionalità per consentire agli esercenti di [ordinare l&#39;ordine delle opzioni di pagamento](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#payment-buttons) per assegnare la priorità ad alcune opzioni di pagamento. Questa funzionalità incoraggia un tasso di conversazione più elevato per il pagamento.

![New](../assets/new.svg)<!-- PAY-4035 --> I commercianti possono ora monitorare in modo efficiente lo stato dei loro negozi e identificare eventuali problemi di transazione utilizzando il nuovo [report sulle transazioni](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html) disponibile nella home page dell&#39;amministratore [!DNL Payment Services]. Il rapporto presenta anche dati sui tassi di autorizzazione delle transazioni e sulle tendenze negative delle transazioni.

## v2.1.0

_9 giugno 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- Issue xxx --> Aggiunto supporto per Adobe Commerce 2.4.7-beta1.

![Nuovo](../assets/new.svg)<!-- Issue xxx --> Aggiunta [disponibilità nei seguenti paesi e nelle valute associate](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#availability): Australia, Francia, Regno Unito.

![Nuovo](../assets/new.svg)<!-- Issue PAY-4296 --> aggiunte [risorse espanse per i ruoli di amministratore](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-roles) per garantire che gli utenti amministratori possano creare e gestire gli ordini per i clienti e possano visualizzare[!DNL Payment Services] nel menu Vendite.

![Nuovo](../assets/new.svg)<!-- Issue PAY-4236 --> aggiunto [annullamento automatico per gli ordini che generano errori durante l&#39;estrazione](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/checkout.html#order-auto-voided-if-error).

![Nuovo](../assets/new.svg)<!-- Issue PAY-4183 --> funzionalità creata per [visualizzare il pulsante di opzione per il pagamento con carta di credito](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#debit-or-credit-card-button) nella pagina di pagamento.

## v2.0.0

_10 marzo 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-4152 --> Aggiunto supporto per PHP 8.2 e Adobe Commerce 2.4.6. Non compatibile con PHP 7.x.

## v1.6.1

_10 marzo 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg)<!-- Issue PAY-4226 --> è stato risolto un problema che impediva ai nuovi commercianti [!DNL Payment Services] di utilizzare l&#39;estrazione in Amministrazione.[!DNL Payment Services] utilizzava in precedenza l&#39;ID cliente Commerce, che non esiste per i nuovi clienti.

![Correzione](../assets/fix.svg)<!-- Issue PAY-4205 --> è stato risolto un problema che causava la sostituzione dello stato dell&#39;indirizzo di spedizione specificato con lo stato nelle impostazioni fiscali predefinite durante l&#39;estrazione tramite l&#39;opzione [PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#paypal-smart-buttons). Ora i clienti possono far spedire i loro ordini in uno stato diverso da quello configurato come predefinito nelle impostazioni fiscali dell’esercente.

![Correzione](../assets/fix.svg)<!-- Issue PAY-4202 --> è stato risolto un problema che impediva ai clienti di utilizzare il vaulting delle carte per completare un acquisto o eliminare un metodo di pagamento con vaulting per un negozio [utilizzando l&#39;azione di pagamento `Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html#set-payment-services-as-payment-method). In precedenza, quando il cliente tentava di utilizzare o modificare le proprie carte di credito archiviate, veniva visualizzato l’errore &quot;Provider Vault ID not found&quot; (ID archivio provider non trovato).

## v1.6.0

_17 febbraio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-3540 --> Aggiunta della [funzionalità di conformità PCI 3DS per gli esercenti che effettuano transazioni nell&#39;Unione europea (UE) e in Gran Bretagna](security.md#3ds). Questo ulteriore livello di sicurezza, che impone agli acquirenti di autenticarsi presso l’emittente della carta di credito, contribuisce a prevenire le frodi online ed è richiesto nell’ambito delle normative di conformità dell’Unione europea (UE).

![Nuovo](../assets/new.svg)<!-- Issue PAY-3609 --> Aggiunta la possibilità di [abilitare il vaulting delle schede nell&#39;amministratore](vaulting.md#use-vaulting-in-the-admin). Questo consente agli esercenti di creare un ordine per i clienti nell’Amministratore utilizzando i propri metodi di pagamento a scaffale.

## v1.5.4

_29 gennaio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-4110 --> è stato risolto un problema che impediva agli acquirenti di effettuare un ordine utilizzando i pulsanti di pagamento nella pagina del prodotto, nel mini-carrello e nel carrello. Gli acquirenti ora possono completare gli ordini con successo.

## v1.5.3

_25 gennaio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-4102 --> È stata rilasciata una correzione a un problema noto non compatibile con le versioni precedenti. Questa versione blocca la versione dell&#39;estensione dell&#39;ID servizio alla versione stabile più recente, che riabilita le nuove installazioni di [!DNL Payment Services] per configurare i servizi Commerce.

## v1.5.2

_22 dicembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3992 --> Fatturazione migliorata in [!DNL Payment Services] quando un metodo di pagamento viene rifiutato.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services] ora visualizza correttamente i pulsanti di pagamento PayPal per gli esercenti che utilizzano il modello personalizzato [Fire Checkout&#39;s](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank} per la pagina di pagamento. In precedenza, i pulsanti venivano visualizzati in modo intermittente.

## v1.5.1

_23 novembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![New](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services] ora include il numero di versione nell&#39;intestazione dell&#39;agente utente in modo che le richieste possano tenere traccia, filtrare o deprecare gli endpoint non utilizzati.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services] ora visualizza correttamente i dati dell&#39;ordine quando un ordine viene effettuato dalla pagina del prodotto utilizzando i pulsanti di pagamento.

## v1.5.0

_18 novembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-3880 --> Un acquirente ora può [archiviare (salvare) le informazioni sulla sua carta di credito durante l&#39;acquisto](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html) per utilizzarle in un acquisto successivo per lo stesso o un altro negozio all&#39;interno dello stesso account esercente.

![New](../assets/new.svg)<!-- Issue PAY-3950 --> I commercianti possono ora abilitare la funzionalità [Commerce per l&#39;acquisto immediato](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html) per i loro negozi in modo che gli acquirenti possano (utilizzare [informazioni sulla carta di credito in deposito](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html)) accelerare il pagamento.

## v1.4.1

_14 ottobre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg)<!-- Issue PAY-3766 --> Quando il metodo di pagamento di un cliente viene rifiutato, il messaggio di errore visibile è più descrittivo. Consiglia al cliente di inserire nuovamente le informazioni di pagamento e riprovare, provare con un altro metodo di pagamento o contattare la banca per informazioni sulla transazione rifiutata.

## v1.4.0

_30 settembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services] ora include la possibilità di impostare un account esercente per [utilizzare più account business PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#use-multiple-paypal-accounts). Questo consente al commerciante di gestire i negozi in più paesi utilizzando valute diverse o di utilizzare Adobe Commerce per una parte della tua attività.

![Nuovi](../assets/new.svg)<!-- Issue PAY-3231 --> I commercianti possono [aggiungere un [!UICONTROL Soft Descriptor]](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#add-soft-descriptor) ai siti Web o alla configurazione delle singole visualizzazioni dello store che vengono visualizzate nei rendiconti bancari delle transazioni dei clienti per delineare marchi, store o linee di prodotti.

![Nuovo](../assets/new.svg)<!-- Issue PAY-3707 --> [Attiva o disattiva i campi della carta di credito e i pulsanti di pagamento PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-payment-options) per l&#39;estrazione nelle impostazioni [!DNL Payment Services].

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3546 --> Quando un cliente fa clic su **[!UICONTROL Edit cart]**, la pagina viene reindirizzata alla pagina del carrello e vengono visualizzati gli elementi aggiornati anziché un carrello vuoto.

## v1.3.1

_6 settembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![È stato risolto il problema](../assets/fix.svg)<!-- Issue PAY-3663 --> Ora, quando un commerciante acquisisce un ordine autorizzato con una valuta non globale, il processo di acquisizione viene completato e non viene visualizzato alcun errore.

## v1.3.0

_9 agosto 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuova](../assets/new.svg)<!-- Issue PAY-XX --> versione di disponibilità generale—[!DNL Payment Services] è ora [supportata da [!DNL Adobe Commerce] e [!DNL Magento Open Source] versioni da 2.4.0 a 2.4.5](https://devdocs.magento.com/release/availability.html#compatibility).

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-x --> Apple Pay è ora compatibile con il browser Safari v15.5 su dispositivi mobili e desktop.

## v1.2.0

_29 giugno 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Problema noto](../assets/bug.svg)<!-- Issue PAY-x --> Apple Pay non è compatibile con il browser Safari v15.5 su dispositivi mobili e desktop. Con Safari versione 15.5 non puoi completare il pagamento con Apple Pay.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue PAY-3264 -->. In precedenza, l&#39;estrazione non riusciva quando un utente connesso selezionava un indirizzo di fatturazione/spedizione diverso da quello predefinito per il proprio account. Ora l&#39;indirizzo di fatturazione/spedizione selezionato viene inviato (invece dell&#39;indirizzo salvato predefinito) e il pagamento viene completato correttamente.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3314 --> Se disattivi i pulsanti di pagamento PayPal per l&#39;estrazione, non vengono visualizzati errori.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-3330 --> I pagamenti non hanno più esito negativo durante l&#39;estrazione quando un utente ospite immette un numero di telefono che include trattini.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 --> Quando le credenziali dei servizi Commerce non sono valide,[!DNL Payment Services] ti avvisa ora visualizzando un errore di credenziali dalla home page di [!DNL Payment Services] nell&#39;amministratore.

![Problema noto](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services] non è compatibile con `commerce-data-export` v101.20 e versioni successive, pertanto è incompatibile con l&#39;estensione [[!DNL Channel manager] extension](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html).

## v1.1.0

_31 marzo 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuova](../assets/new.svg)<!-- Issue PAY-2127 --> versione di disponibilità generale—[!DNL Payment Services] è ora [supportata da [!DNL Adobe Commerce] e [!DNL Magento Open Source] versioni da 2.4.0 a 2.4.4](https://devdocs.magento.com/release/availability.html#compatibility).

![Nuovo](../assets/new.svg)<!-- Issue PAY-2682 --> L&#39;estensione [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] è ora disponibile per i commercianti canadesi. Gli esercenti possono visualizzare la configurazione dei pagamenti in [francese](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=fr#carte-de-cr%C3%A9dit-et-devises-accept%C3%A9es) o [inglese](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#accepted-credit-cards-and-currencies).

![Nuovo](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services] supporta [Dollari canadesi (CAD)](overview.md#accepted-credit-cards-and-currencies) per le carte di credito e le transazioni PayPal.

![New](../assets/new.svg)<!-- Issue PAY-2680 --> I commercianti possono [integrare [!DNL Payment Services]](onboard.md) l&#39;estensione in inglese o francese.

![Nuovo](../assets/new.svg)<!-- Issue PAY-2678 --> I commercianti possono ora visualizzare i report finanziari, sia il [stato pagamento ordine](order-payment-status.md) che il [report Pagamenti](payouts.md), in dollari canadesi (CAD).

![Il problema risolto](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services] è ora compatibile con [PHP 8.1](https://www.php.net/releases/8.1/en.php).

![È stato risolto il problema](../assets/fix.svg)<!-- Issue PAY-3017 -->. È stato migliorato l&#39;avviso relativo alla modalità sandbox per visualizzare gli avvisi corretti con più archivi.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-2742 --> È ora possibile abilitare e disabilitare i metodi di pagamento disponibili, ad esempio Venmo, a livello di visualizzazione punto vendita. In precedenza era possibile configurare i metodi di pagamento solo per il sito Web.

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-2277 --> Ora puoi [abilitare o disabilitare in modo selettivo i singoli pulsanti di pagamento PayPal](settings.md#payment-buttons).

![Problema risolto](../assets/fix.svg)<!-- Issue PAY-2561 --> I prodotti precedentemente rimossi non vengono visualizzati nel carrello nella pagina _Rivedi ordine_.

![Problema noto](../assets/bug.svg)<!-- Issue PAY-2842 --> Le transazioni con carta di credito [di prova potrebbero non riuscire con PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html) durante l&#39;elaborazione dei pagamenti in un ambiente sandbox.

## v1.0.0

_29 novembre 2021_

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuova](../assets/new.svg)<!-- Issue PAY-2127 --> versione di disponibilità generale—[[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html) è ora supportata da [!DNL Adobe Commerce] e [!DNL Magento Open Source] versioni da 2.4.0 a 2.4.3-p1.

![Nuovo](../assets/new.svg)<!-- Issue PAY-124 --> L&#39;estensione [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] può essere installata per [[!DNL Adobe Commerce] nell&#39;infrastruttura cloud](install.md#adobe-commerce-on-cloud-infrastructure) o per [istanze locali](install.md#on-premises). Questi metodi richiedono l&#39;utilizzo di un&#39;interfaccia della riga di comando.

![Nuovo](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services] supporta un account [sandbox](sandbox.md) che consente ai commercianti di valutare l&#39;estensione in modalità di test.

![New](../assets/new.svg)<!-- Issue PAY-666 --> I commercianti possono [configurare l&#39;estensione Payment Services](settings.md) con comportamenti di pagamento di base, ad esempio utilizzando [`Authorize and Capture`](production.md#set-payment-services-as-payment-method) per passare da un ambiente sandbox a un ambiente di produzione.

![Nuovo](../assets/new.svg)<!-- Issue PAY-780 --> Gli acquirenti possono effettuare il check-out con [!DNL Payment Services] o tramite [creazione manuale dell&#39;ordine](create-order.md).

![Nuovi](../assets/new.svg)<!-- Issue PAY-1856 --> Rapporti completi, tramite [Stato pagamento ordine](order-payment-status.md) e [Rapporti pagamenti](payouts.md), sono disponibili per [!DNL Payment Services] per consentirti di avere una visione chiara degli ordini del tuo Negozio e dei relativi pagamenti.

![Nuovo](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services] supporta prezzi flessibili su più livelli, basati sul volume di elaborazione totale, adattati a qualsiasi commerciante.

![Nuovo](../assets/new.svg)<!-- Issue PAY-1443 --> Puoi facilmente [personalizzare l&#39;aspetto](payments-options.md) dei pulsanti di pagamento PayPal e dei campi della carta di credito per l&#39;estensione [!DNL Payment Services].

![Problema noto](../assets/bug.svg)<!-- Issue PAY-2473 --> L&#39;utilizzo di [chiavi di composizione non corrette](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html) durante l&#39;installazione dell&#39;estensione impedisce all&#39;utente di [autenticarsi](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html) con `MAGEID` corretto.

![Problema noto](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services] report [ potrebbero non essere sincronizzati immediatamente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html).

![Problema noto](../assets/bug.svg)<!-- Issue PAY-2475 --> Il tuo [account sandbox PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html) per [!DNL Payment Services] non può essere verificato se crei tale account durante l&#39;onboarding.
