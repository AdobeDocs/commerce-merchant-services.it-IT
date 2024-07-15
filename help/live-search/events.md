---
title: '[!DNL Live Search] eventi'
description: Scopri come gli eventi raccolgono i dati per  [!DNL Live Search].
feature: Services, Eventing
exl-id: b0c72212-9be0-432d-bb8d-e4c639225df3
source-git-commit: 0d966c8dbd788563fa453912961fdc62a5a6c23e
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# [!DNL Live Search] eventi

[!DNL Live Search] utilizza gli eventi per attivare gli algoritmi di ricerca, ad esempio &quot;Più visualizzati&quot; e &quot;Più visualizzati, visualizzati&quot;. Anche se gli utenti LUMA ottengono eventi pronti all’uso, headless e altre implementazioni personalizzate devono implementare gli eventi in base alle proprie esigenze.

Poiché [!DNL Live Search] e [!DNL Product Recommendations] utilizzano lo stesso algoritmo di back-end, alcuni eventi sono condivisi da entrambi i servizi. Per compilare il dashboard di Recommendations sono necessari alcuni eventi di Product Recommendations.

Questa tabella descrive gli eventi utilizzati dalle strategie [!DNL Live Search].

| Strategia | Prodotti | Eventi | Pagina |
| --- | --- | --- | ---|
| Articoli più visualizzati | Live Search<br>Registri prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Più acquistati | Live Search<br>Registri prodotti | visualizzazione pagina<br>estrazione completata | Carrello/Pagamento |
| Più aggiunti al carrello | Live Search<br>Registri prodotti | visualizzazione pagina<br>aggiungi al carrello | Pagina dettagli prodotto<br>Pagina elenco prodotti<br>Carrello<br>Elenco desideri |
| Ha visualizzato questo, ha visualizzato quello | Live Search<br>Registri prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Di tendenza | Live Search<br>Registri prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Ho visto questo, ho comprato quello | Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto<br>Carrello/Pagamento |
| Ho comprato questo e quello | Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Conversione: Visualizza per acquisto | Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Conversione: Visualizza per acquisto | Registrazioni dei prodotti | visualizzazione pagina<br>estrazione completata | Carrello/Pagamento |
| Conversione: Visualizza in carrello | Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Conversione: Visualizza in carrello | Registrazioni dei prodotti | visualizzazione pagina<br>aggiungi al carrello | Pagina dettagli prodotto<br>Pagina elenco prodotti<br>Carrello<br>Elenco desideri |

>[!NOTE]
>
>La raccolta dei dati ai fini di [!DNL Live Search] non include informazioni personali (PII). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi. [Ulteriori informazioni](https://www.adobe.com/privacy/experience-cloud.html).

## Eventi dashboard richiesti

Alcuni eventi sono necessari per popolare il [dashboard di Live Search](performance.md)

| Area del dashboard | Eventi | Unisci campo |
| ------------------- | ------------- | ---------- |
| Ricerche univoche | `page-view`, `search-request-sent`, | searchRequestId |
| Nessuna ricerca di risultati | `page-view`, `search-request-sent`, | searchRequestId |
| Percentuale risultati zero | `page-view`, `search-request-sent`, | searchRequestId |
| Ricerche comuni | `page-view`, `search-request-sent`, | searchRequestId |
| Media posizione clic | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | searchRequestId |
| Percentuale di click-through | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | searchRequestId, sku |
| Tasso di conversione | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click`, `product-view`, `add-to-cart`, `place-order` | searchRequestId, sku |

### Contesti richiesti

Tutti gli eventi richiedono i contesti `Page` e `Storefront`. Questo dovrebbe accadere a livello di pagina/livello di applicazione vetrina piuttosto che durante la generazione di singoli eventi (ad esempio, in una vetrina PHP, il contenitore di applicazioni PHP è responsabile della loro impostazione in fase di esecuzione).

## Utilizzo

Di seguito è riportato un esempio di implementazione dell&#39;evento `search-request-sent`:

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## Avvertenze

Gli ad blocker e le impostazioni di privacy possono impedire l&#39;acquisizione degli eventi e causare la mancata generazione di rapporti per [metriche](workspace.md) relative a coinvolgimento e ricavi.

Eventing non acquisisce ogni transazione che avviene sul sito del commerciante. L&#39;evento ha lo scopo di dare al mercante un&#39;idea generale degli eventi che stanno accadendo sul sito.

Le implementazioni headless devono implementare l&#39;evento per alimentare il [dashboard di Product Recommendations](../product-recommendations/events.md).

>[!NOTE]
>
>Se è abilitata la modalità di restrizione dei cookie [](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html), Adobe Commerce non raccoglie i dati comportamentali fino a quando l&#39;acquirente non acconsente all&#39;utilizzo dei cookie. Se la modalità di restrizione dei cookie è disabilitata, Adobe Commerce raccoglie i dati comportamentali per impostazione predefinita.
