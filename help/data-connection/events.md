---
title: Eventi
description: Scopri i dati acquisiti da ogni evento.
exl-id: b0c88af3-29c1-4661-9901-3c6d134c2386
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: f90ef4d2732a0b0676e0899712f94b41a1c2d85a
workflow-type: tm+mt
source-wordcount: '6894'
ht-degree: 0%

---

# [!DNL Data Connection] Eventi

Di seguito è riportato un elenco degli eventi di Commerce disponibili quando si installa [!DNL Data Connection] estensione. I dati raccolti da questi eventi vengono inviati a Adobe Experience Platform Edge. Puoi anche creare [eventi personalizzati](custom-events.md) per la raccolta di dati aggiuntivi non inclusi nella confezione.

Oltre ai dati raccolti dai seguenti eventi, otterrai anche [altri dati](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) fornite da Adobe Experience Platform Web SDK.

## Eventi vetrina

Gli eventi di vetrina raccolgono dati comportamentali anonimi dagli acquirenti che navigano sul tuo sito. Puoi utilizzare i dati raccolti da questi eventi per creare promozioni e campagne indirizzate a un gruppo specifico di acquirenti. I dati dell’evento Storefront includono solo prodotti semplici e configurabili.

>[!NOTE]
>
>Tutti gli eventi della vetrina includono [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) , che include l&#39;indirizzo e-mail dell&#39;acquirente, se disponibile, ed ECID. Includendo questi dati di profilo in ogni evento, non è necessario un’importazione separata dell’account utente da Adobe Commerce.

### addToCart

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un prodotto viene aggiunto al carrello o quando la quantità di un prodotto nel carrello viene incrementata. | `commerce.productListAdds` |

#### Dati raccolti da addToCart

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.productListAdds` | Indica se un prodotto è stato aggiunto a un carrello. Un valore di `1` indica che è stato aggiunto un prodotto. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |

### openCart

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando viene creato un nuovo carrello, ovvero quando un prodotto viene aggiunto a un carrello vuoto. | `commerce.productListOpens` |

#### Dati raccolti da openCart

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.productListOpens` | Indica se è stato creato un carrello. Un valore di `1` indica che è stato creato un carrello. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |

### removeFromCart

| Descrizione | Nome evento XDM |
|---|---|
| Viene attivato ogni volta che un prodotto viene rimosso o ogni volta che la quantità di un prodotto nel carrello diminuisce. | `commerce.productListRemovals` |

#### Dati raccolti da removeFromCart

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.productListRemovals` | Indica se un prodotto è stato rimosso dal carrello. Un valore di `1` indica che un prodotto è stato rimosso dal carrello. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |

### shoppingCartView

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione al caricamento di qualsiasi pagina del carrello. | `commerce.productListViews` |

#### Dati raccolti da shoppingCartView

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.productListViews` | Indica se è stato visualizzato un elenco di prodotti. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |

### pageView

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione al caricamento di qualsiasi pagina. | `web.webpagedetails.pageViews` |

#### Dati raccolti da pageView

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `web.webPageDetails.pageViews` | Indica se una pagina è stata caricata. A `value` di `1` indica che la pagina è stata caricata. |
| `web.webPageDetails.URL` | L’URL normativo o abituale della pagina web. Questo può essere l’URL effettivo utilizzato per raggiungere la pagina, che verrebbe registrato utilizzando `Web Link`. |
| `web.webPageDetails.name` | Il nome normativo della pagina web. Questo nome non è necessariamente il titolo della pagina o è direttamente associato al contenuto della pagina, ma viene utilizzato per organizzare le pagine di un sito a scopo di classificazione. |
| `web.webReferrer.URL` | L’URL della pagina web visitata da un acquirente prima di fare clic su un collegamento al sito. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### productPageView

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione al caricamento di qualsiasi pagina di prodotto. | `commerce.productViews` |

#### Dati raccolti da productPageView

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.productViews` | Indica se il prodotto è stato visualizzato. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |

### startCheckout

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando l&#39;acquirente fa clic su un pulsante di pagamento. | `commerce.checkouts` |

#### Dati raccolti da startCheckout

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.checkouts` | Indica se si è verificata un&#39;azione durante il processo di pagamento. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |

### completeCheckout

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando l’acquirente effettua un ordine. | `commerce.order` |

#### Dati raccolti da completeCheckout

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.purchases` | Indica se un ordine è stato accettato. |
| `commerce.order` | Contiene informazioni sull’ordine effettuato per uno o più prodotti. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.paymentTransactionID` | Identificatore univoco per questa transazione di pagamento. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Le opzioni sono: `cash`, `credit_card`, `debit_card`, `gift_card`, `check`, `paypal`, `wire_transfer`, `credit_card_reference`, `other`. |
| `commerce.order.payments.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.taxAmount` | Importo dell&#39;imposta pagato dall&#39;acquirente come parte del pagamento finale. |
| `commerce.order.discountAmount` | Indica l&#39;importo dello sconto applicato all&#39;intero ordine. |
| `commerce.order.createdDate` | L’ora e la data di creazione di un nuovo ordine nel sistema commerce. Ad esempio, `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |  | `shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |

## Eventi profilo

Gli eventi profilo includono informazioni sull’account, ad esempio `signIn`, `signOut`, `createAccount`, e `editAccount`. Questi dati vengono utilizzati per popolare i dettagli chiave dei clienti necessari per definire meglio i segmenti o eseguire campagne di marketing, ad esempio se desideri eseguire il targeting degli acquirenti che vivono a New York.

### signIn

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di accedere. | `userAccount.login` |

>[!NOTE]
>
> Questo evento viene attivato quando si tenta di eseguire l’azione specifica. Non indica che l’azione è stata eseguita correttamente.

#### Dati raccolti da signIn

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `person` | Un singolo attore, contatto o proprietario. |
| `person.accountID` | Acquisisce l’ID dell’account utente. |
| `person.accountType` | Acquisisce il tipo di account utente, ad esempio `Personal` o `Company`, se applicabile. |
| `person.personalEmailID` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `personalEmail` | Acquisisce i dettagli di contatto, ovvero un messaggio di posta elettronica e le informazioni associate. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.login` | Indica se un visitatore ha tentato di accedere. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### disconnetti

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di uscire. | `userAccount.logout` |

>[!NOTE]
>
> Questo evento viene attivato quando si tenta di eseguire l’azione specifica. Non indica che l’azione è stata eseguita correttamente.

#### Dati raccolti da signOut

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.logout` | Indica se un visitatore ha tentato di disconnettersi. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### createAccount

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di creare un account. | `userAccount.createProfile` |

>[!NOTE]
>
> Questo evento viene attivato quando si tenta di eseguire l’azione specifica. Non indica che l’azione è stata eseguita correttamente.

#### Dati raccolti da createAccount

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `person` | Un singolo attore, contatto o proprietario. |
| `person.accountID` | Acquisisce l’ID dell’account utente. |
| `person.accountType` | Acquisisce il tipo di account utente, ad esempio `Personal` o `Company`, se applicabile. |
| `person.personalEmailID` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `personalEmail` | Acquisisce i dettagli di contatto, ovvero un messaggio di posta elettronica e le informazioni associate. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.updateProfile` | Indica se un utente ha aggiornato il proprio profilo account. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### editAccount

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di modificare un account. | `userAccount.updateProfile` |

>[!NOTE]
>
> Questo evento viene attivato quando si tenta di eseguire l’azione specifica. Non indica che l’azione è stata eseguita correttamente.

#### Dati raccolti da editAccount

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `person` | Un singolo attore, contatto o proprietario. |
| `person.accountID` | Acquisisce l’ID dell’account utente. |
| `person.accountType` | Acquisisce il tipo di account utente, ad esempio `Personal` o `Company`, se applicabile. |
| `person.personalEmailID` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `personalEmail` | Acquisisce i dettagli di contatto, ovvero un messaggio di posta elettronica e le informazioni associate. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.updateProfile` | Indica se un utente ha aggiornato il proprio profilo account. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

## Cerca eventi

Gli eventi di ricerca forniscono dati rilevanti per l’intento dell’acquirente. L&#39;intuizione dell&#39;intento di un cliente aiuta i commercianti a capire come gli acquirenti stanno cercando gli articoli, cosa cliccano e, in ultima analisi, acquistano o abbandonano. Un esempio di come puoi utilizzare questi dati è se desideri eseguire il targeting degli acquirenti esistenti che cercano il tuo prodotto principale, ma non acquistano mai il prodotto.

Utilizza il `searchRequest.id` e `searchResponse.id` campi trovati in entrambi i `searchRequestSent` e `searchResponseReceived` eventi per creare un riferimento incrociato tra una richiesta di ricerca e la risposta di ricerca corrispondente.

### searchRequestSent

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione dai seguenti eventi nel popover &quot;cerca durante la digitazione&quot;:<br><br>Premi Invio, Fai Clic Su _Visualizza tutto_<br><br> Attivato dai seguenti eventi sulle pagine dei risultati di ricerca:<br><br>Selezionare un filtro, Modificare l&#39;ordinamento (_Ordina per_), Cambia la direzione di ordinamento (crescente o decrescente), Cambia il numero di risultati per pagina (_Mostra numero per pagina_), Passa alla pagina successiva, Passa alla pagina precedente, Passa a una pagina diversa | `searchRequest` |

>[!NOTE]
>
>Gli eventi di ricerca non sono supportati in Adobe Commerce Enterprise Edition con l’estensione B2B installata.

#### Dati raccolti da searchRequestSent

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `searchRequest` | Indica se è stata inviata una richiesta di ricerca. |
| `searchRequest.id` | ID univoco per questa particolare richiesta di ricerca. |
| `searchRequest.value` | Valore quantificabile della richiesta. |
| `siteSearch` | Contiene informazioni sulla ricerca. |
| `siteSearch.filter` | Indica se sono stati applicati filtri per limitare i risultati della ricerca. |
| `siteSearch.filter.attribute` (filtro) | Facet di un elemento utilizzato per determinare se includerlo nei risultati di ricerca. |
| `siteSearch.filter.isRange` | Se è true, i valori indicano gli endpoint di un intervallo di valori accettabile. |
| `siteSearch.filter.value` | Valore attributo utilizzato per determinare quali elementi sono inclusi nei risultati di ricerca. |
| `siteSearch.sort` | Indica come ordinare i risultati della ricerca. |
| `siteSearch.sort.attribute` (sort) | Attributo utilizzato per ordinare gli elementi nei risultati di ricerca. |
| `siteSearch.sort.order` | Ordine in cui restituire i risultati della ricerca. |
| `siteSearch.query` | Termini cercati. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### searchResponseReceived

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando Live Search restituisce i risultati per la pagina dei risultati di ricerca o popover &quot;cerca durante la digitazione&quot;. | `searchResponse` |

>[!NOTE]
>
>Gli eventi di ricerca non sono supportati in Adobe Commerce Enterprise Edition con l’estensione B2B installata.

#### Dati raccolti da searchResponseReceived

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `searchResponse` | Indica se è stata ricevuta una risposta di ricerca. |
| `searchResponse.id` | L’ID univoco per questa particolare risposta di ricerca. |
| `searchResponse.value` | Il valore quantificabile della risposta. |
| `siteSearch.numberOfResults` | Il numero di prodotti restituiti. |
| `siteSearch.suggestions` | Matrice di stringhe che includono i nomi di prodotti e categorie presenti nel catalogo simili alla query di ricerca. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

## Eventi B2B

![B2B per Adobe Commerce](../assets/b2b.svg) Per gli esercenti B2B, devi [installare](install.md#install-the-b2b-extension) il `experience-platform-connector-b2b` per abilitare questi eventi.

Gli eventi B2B contengono [elenco richieste di acquisto](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html) informazioni, ad esempio se è stato creato, aggiunto o eliminato un elenco di richieste di acquisto. Tenendo traccia degli eventi specifici degli elenchi di richieste di acquisto, è possibile vedere quali prodotti i clienti acquistano frequentemente e creare campagne basate su tali dati.

### createRichiesteList

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente crea un elenco di richieste di acquisto. | `commerce.requisitionListOpens` |

#### Dati raccolti da createRichiesteList

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.requisitionListOpens` | Indica l&#39;inizializzazione di un nuovo elenco di richieste. |
| `commerce.requisitionList` | Proprietà dell&#39;elenco di richieste di acquisto creato dal cliente. |
| `commerce.requisitionList.ID` | Identificatore univoco dell&#39;elenco di richieste di acquisto. |
| `commerce.requisitionList.name` | Nome dell&#39;elenco di richieste specificato dal cliente. |
| `commerce.requisitionList.description` | Descrizione dell&#39;elenco di richieste di acquisto specificato dal cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### addToRichiesteList

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente aggiunge un prodotto a un elenco di richieste di acquisto esistente o durante la creazione di un elenco. | `commerce.requisitionListAdds` |

#### Dati raccolti da addToRichiitionList

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.requisitionListAdds` | Indica l&#39;aggiunta di uno o più prodotti a un elenco di richieste. |
| `commerce.requisitionList` | Proprietà dell&#39;elenco di richieste di acquisto creato dal cliente. |
| `commerce.requisitionList.ID` | Identificatore univoco dell&#39;elenco di richieste di acquisto. |
| `commerce.requisitionList.name` | Nome dell&#39;elenco di richieste specificato dal cliente. |
| `commerce.requisitionList.description` | Descrizione dell&#39;elenco di richieste di acquisto specificato dal cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Array di prodotti aggiunti all&#39;elenco delle richieste di acquisto. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |

### removeFromRichiesteList

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente rimuove un prodotto da un elenco di richieste di acquisto. | `commerce.requisitionListRemovals` |

#### Dati raccolti da removeFromRichiitionList

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.requsitionListRemovals` | Indica la rimozione di uno o più prodotti da un elenco di richieste di acquisto. |
| `commerce.requisitionList` | Proprietà dell&#39;elenco di richieste di acquisto creato dal cliente. |
| `commerce.requisitionList.ID` | Identificatore univoco dell&#39;elenco di richieste di acquisto. |
| `commerce.requisitionList.name` | Nome dell&#39;elenco di richieste specificato dal cliente. |
| `commerce.requisitionList.description` | Descrizione dell&#39;elenco di richieste di acquisto specificato dal cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Array di prodotti aggiunti all&#39;elenco delle richieste di acquisto. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |

## Eventi back office

Gli eventi di back office contengono informazioni sullo stato di un ordine, ad esempio se un ordine è stato effettuato, annullato, rimborsato, spedito o completato. I dati raccolti da questi eventi lato server mostrano una visualizzazione 360 dell’ordine cliente. Questa visualizzazione consente ai commercianti di eseguire meglio il targeting o analizzare l’intero stato dell’ordine durante lo sviluppo di campagne di marketing. Ad esempio, puoi individuare le tendenze in determinate categorie di prodotti che ottengono risultati ottimali in momenti diversi dell’anno. Ad esempio, vestiti invernali che vendono meglio durante i mesi più freddi o alcuni colori di prodotto che gli acquirenti sono interessati negli anni. Inoltre, i dati sullo stato dell&#39;ordine possono essere utili per calcolare il valore del cliente per tutta la sua durata comprendendo la propensione di un acquirente a eseguire la conversione in base agli ordini precedenti.

>[!NOTE]
>
>Tutti gli eventi di back office includono [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) , che fornisce l&#39;indirizzo e-mail dell&#39;acquirente. Includendo questi dati di profilo in ogni evento, non è necessario un’importazione separata dell’account utente da Adobe Commerce.

### orderPlaced

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente effettua un ordine. | `commerce.backofficeOrderPlaced` |

#### Dati raccolti da orderPlaced

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.paymentTransactionID` | Identificatore univoco per questa transazione di pagamento. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.order.payments.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.taxAmount` | Importo dell&#39;imposta pagato dall&#39;acquirente come parte del pagamento finale. |
| `commerce.order.discountAmount` | Indica l&#39;importo dello sconto applicato all&#39;intero ordine. |
| `commerce.order.createdDate` | L’ora e la data di creazione di un nuovo ordine nel sistema commerce. Ad esempio, `2022-10-15T20:20:39+00:00`. |
| `commerce.order.currencyCode` | Il codice valuta ISO 4217 utilizzato per i totali dell’ordine. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |
| `commerce.shipping.currencyCode` | Il codice valuta ISO 4217 utilizzato per il totale delle spedizioni. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `commerce.billing.address` | Indirizzo postale di fatturazione. |
| `commerce.billing.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada |
| `commerce.billing.address.street2` | Campo aggiuntivo per informazioni a livello stradale. |
| `commerce.billing.address.city` | Il nome della città. |
| `commerce.billing.address.state` | Nome dello stato. Questo è un campo in formato libero. |
| `commerce.billing.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.billing.address.country` | Il nome del territorio amministrato dal governo. Diverso da `xdm:countryCode`, questo è un campo in formato libero che può contenere il nome del paese in qualsiasi lingua. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.id` | L’identificatore di riga per questa voce di prodotto. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |

### orderInvoiced

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un commerciante presenta una fattura per richiedere il pagamento. | `commerce.backofficeOrderInvoiced` |

#### Dati raccolti da orderInvoiced

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.priceTotal` | Il prezzo totale dell&#39;ordine dopo l&#39;applicazione di tutti gli sconti e le imposte. |
| `commerce.order.currencyCode` | Il codice valuta ISO 4217 utilizzato per i totali dell’ordine. |
| `commerce.order.purchaseOrderNumber` | Identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.id` | L’identificatore di riga per questa voce di prodotto. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |

### orderItemsShipped

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando viene spedito un ordine. | `commerce.backofficeOrderItemsShipped` |

#### Dati raccolti da orderItemsShipped

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.paymentTransactionID` | Identificatore univoco per questa transazione di pagamento. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.order.payments.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.priceTotal` | Il prezzo totale dell&#39;ordine dopo l&#39;applicazione di tutti gli sconti e le imposte. |
| `commerce.order.purchaseOrderNumber` | Identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |
| `commerce.order.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.lastUpdatedDate` | L’ora dell’ultimo aggiornamento di un determinato record dell’ordine nel sistema commerciale. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |
| `commerce.shipping.address` | L&#39;indirizzo fisico di spedizione. |
| `commerce.shipping.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada. |
| `commerce.shipping.address.street2` | Seconda riga facoltativa sulle informazioni stradali. |
| `commerce.shipping.address.city` | Il nome della città. |
| `commerce.shipping.address.state` | Il nome dello Stato. Questo è un campo in formato libero. |
| `commerce.shipping.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.shipping.address.country` | Il nome del territorio amministrato dal governo. Diverso da `xdm:countryCode`, questo è un campo in formato libero che può contenere il nome del paese in qualsiasi lingua. |
| `commerce.shipping.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.shipping.trackingNumber` | Il numero di registrazione fornito dal vettore di spedizione per una spedizione dell&#39;articolo dell&#39;ordine. |
| `commerce.shipping.trackingURL` | URL per tenere traccia dello stato di spedizione di un articolo dell&#39;ordine. |
| `commerce.shipping.shipDate` | Data di spedizione di uno o più articoli di un ordine. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `commerce.billing.address` | Indirizzo postale di fatturazione. |
| `commerce.billing.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada |
| `commerce.billing.address.street2` | Campo aggiuntivo per informazioni a livello stradale. |
| `commerce.billing.address.city` | Il nome della città. |
| `commerce.billing.address.state` | Nome dello stato. Questo è un campo in formato libero. |
| `commerce.billing.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.billing.address.country` | Il nome del territorio amministrato dal governo. Diverso da `xdm:countryCode`, questo è un campo in formato libero che può contenere il nome del paese in qualsiasi lingua. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |

### orderCanceled

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente annulla un ordine. | `commerce.backofficeOrderCancelled` |

#### Dati raccolti da orderCanceled

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.purchaseOrderNumber` | Identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |
| `commerce.order.cancelDate` | La data e l’ora in cui un acquirente annulla un ordine. |
| `commerce.order.lastUpdatedDate` | L’ora dell’ultimo aggiornamento di un determinato record dell’ordine nel sistema commerciale. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |

### orderLineItemRereturned

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente viene rimborsato per un articolo restituito. | `commerce.backofficeCreditMemoIssued` |

#### Dati raccolti da orderLineItemRereturned

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.lastUpdatedDate` | L’ora dell’ultimo aggiornamento di un determinato record dell’ordine nel sistema commerciale. |
| `commerce.order.purchaseOrderNumber` | Identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |
| `commerce.refunds` | Elenco dei rimborsi per questo ordine. |
| `commerce.refunds.transactionID` | Identificatore univoco per questo rimborso. |
| `commerce.refunds.refundAmount` | Il valore del rimborso. |
| `commerce.refunds.refundPaymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.refunds.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |

### orderItemsReturnInitiated

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente richiede di restituire un elemento. | `commerce.backofficeOrderItemsReturnInitiated` |

#### Dati raccolti da orderItemsReturnInitiated

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.returns` | Le informazioni RMA (Return Merchandise Authorization) per questo ordine. |
| `commerce.order.returns.returnID` | L&#39;identificatore univoco di questa RMA (Return Merchandise Authorization). |
| `commerce.order.returns.returnStatus` | Lo stato della RMA (Return Merchandise Authorization), ad esempio In sospeso, Chiuso e così via. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |
| `productListItems.returnItem` | Le informazioni RMA (Return Merchandise Authorization) per questo oggetto. |
| `productListItems.returnItem.returnStatus` | Lo stato dell&#39;elemento restituito, ad esempio In sospeso, Approvato e così via. |
| `productListItems.returnItem.returnReason` | Motivo per cui è richiesta una restituzione per questo oggetto. |
| `productListItems.returnItem.returnItemCondition` | La condizione dell&#39;elemento per cui viene richiesta la restituzione. |
| `productListItems.returnItem.returnResolution` | La risoluzione richiesta dell&#39;articolo restituito, ad esempio Rimborso, Scambio e così via. |
| `productListItems.returnItem.returnQuantityRequested` | Il numero di questo oggetto che l&#39;acquirente ha richiesto di restituire. |
| `productListItems.returnItem.returnQuantityAuthorized` | Il numero di questo elemento che può essere restituito. |
| `productListItems.returnItem.eturnQuantityReceived` | Numero di elementi restituiti ricevuti. |
| `productListItems.returnItem.returnQuantityApproved` | Il numero di questo oggetto con restituzione completa e approvata. |

### orderItemReturnCompleted

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando viene completato un elemento che un acquirente ha richiesto di restituire. | `commerce.backofficeOrderItemsReturnCompleted` |

#### Dati raccolti da orderItemReturnCompleted

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.returns` | Le informazioni RMA (Return Merchandise Authorization) per questo ordine. |
| `commerce.order.returns.returnID` | L&#39;identificatore univoco di questa RMA (Return Merchandise Authorization). |
| `commerce.order.returns.returnStatus` | Lo stato della RMA (Return Merchandise Authorization), ad esempio In sospeso, Chiuso e così via. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |
| `productListItems.returnItem` | Le informazioni RMA (Return Merchandise Authorization) per questo oggetto. |
| `productListItems.returnItem.returnStatus` | Lo stato dell&#39;elemento restituito, ad esempio In sospeso, Approvato e così via. |
| `productListItems.returnItem.returnReason` | Motivo per cui è richiesta una restituzione per questo oggetto. |
| `productListItems.returnItem.returnItemCondition` | La condizione dell&#39;elemento per cui viene richiesta la restituzione. |
| `productListItems.returnItem.returnResolution` | La risoluzione richiesta dell&#39;articolo restituito, ad esempio Rimborso, Scambio e così via. |
| `productListItems.returnItem.returnQuantityRequested` | Il numero di questo oggetto che l&#39;acquirente ha richiesto di restituire. |
| `productListItems.returnItem.returnQuantityAuthorized` | Il numero di questo elemento che può essere restituito. |
| `productListItems.returnItem.eturnQuantityReceived` | Numero di elementi restituiti ricevuti. |
| `productListItems.returnItem.returnQuantityApproved` | Il numero di questo oggetto con restituzione completa e approvata. |

### orderShipmentCompleted

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione al completamento di una spedizione. | `commerce.backofficeOrderShipmentCompleted` |

#### Dati raccolti da orderShipmentCompleted

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.paymentTransactionID` | Identificatore univoco per questa transazione di pagamento. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.order.payments.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.taxAmount` | Importo dell&#39;imposta pagato dall&#39;acquirente come parte del pagamento finale. |
| `commerce.order.createdDate` | L’ora e la data di creazione di un nuovo ordine nel sistema commerce. Ad esempio, `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |
| `commerce.shipping.shipDate` | Data di spedizione di uno o più articoli di un ordine. |
| `commerce.shipping.address` | L&#39;indirizzo fisico di spedizione. |
| `commerce.shipping.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada. |
| `commerce.shipping.address.street2` | Seconda riga facoltativa sulle informazioni stradali. |
| `commerce.shipping.address.city` | Il nome della città. |
| `commerce.shipping.address.state` | Il nome dello Stato. Questo è un campo in formato libero. |
| `commerce.shipping.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.shipping.address.country` | Il nome del territorio amministrato dal governo. Diverso da `xdm:countryCode`, questo è un campo in formato libero che può contenere il nome del paese in qualsiasi lingua. |
| `commerce.billing.address` | Indirizzo postale di fatturazione. |
| `commerce.billing.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada |
| `commerce.billing.address.street2` | Campo aggiuntivo per informazioni a livello stradale. |
| `commerce.billing.address.city` | Il nome della città. |
| `commerce.billing.address.state` | Nome dello stato. Questo è un campo in formato libero. |
| `commerce.billing.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.billing.address.country` | Il nome del territorio amministrato dal governo. Diverso da `xdm:countryCode`, questo è un campo in formato libero che può contenere il nome del paese in qualsiasi lingua. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L’indirizzo tecnico, ad esempio: `name@domain.com` come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Il [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) codice valuta utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell’attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |
