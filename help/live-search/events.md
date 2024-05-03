---
title: '[!DNL Live Search] Eventi'
description: Scopri come gli eventi raccolgono i dati per [!DNL Live Search].
feature: Services, Eventing
exl-id: b0c72212-9be0-432d-bb8d-e4c639225df3
source-git-commit: 0d966c8dbd788563fa453912961fdc62a5a6c23e
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# [!DNL Live Search] Eventi

[!DNL Live Search] utilizza gli eventi per potenziare gli algoritmi di ricerca come &quot;Più visualizzato&quot; e &quot;Più visualizzato, visualizzato questo&quot;. Anche se gli utenti LUMA ottengono eventi pronti all’uso, headless e altre implementazioni personalizzate devono implementare gli eventi in base alle proprie esigenze.

Da [!DNL Live Search] e [!DNL Product Recommendations] utilizza lo stesso algoritmo di back-end; alcuni eventi sono condivisi da entrambi i servizi. Per compilare il dashboard di Recommendations sono necessari alcuni eventi di Product Recommendations.

Questa tabella descrive gli eventi utilizzati da [!DNL Live Search] strategie.

| Strategia | Prodotti | Eventi | Pagina |
| --- | --- | --- | ---|
| Articoli più visualizzati | Live Search<br>Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Più acquistati | Live Search<br>Registrazioni dei prodotti | visualizzazione pagina<br>completa pagamento | Carrello/Pagamento |
| Più aggiunti al carrello | Live Search<br>Registrazioni dei prodotti | visualizzazione pagina<br>aggiungi al carrello | Pagina dettagli prodotto<br>Pagina di elenco prodotti<br>Carrello<br>Lista dei desideri |
| Ha visualizzato questo, ha visualizzato quello | Live Search<br>Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Di tendenza | Live Search<br>Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Ho visto questo, ho comprato quello | Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto<br>Carrello/Pagamento |
| Ho comprato questo e quello | Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Conversione: Visualizza per acquisto | Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Conversione: Visualizza per acquisto | Registrazioni dei prodotti | visualizzazione pagina<br>completa pagamento | Carrello/Pagamento |
| Conversione: Visualizza in carrello | Registrazioni dei prodotti | visualizzazione pagina<br>visualizzazione prodotto | Pagina dettagli prodotto |
| Conversione: Visualizza in carrello | Registrazioni dei prodotti | visualizzazione pagina<br>aggiungi al carrello | Pagina dettagli prodotto<br>Pagina di elenco prodotti<br>Carrello<br>Lista dei desideri |

>[!NOTE]
>
>Raccolta di dati ai fini del [!DNL Live Search] non include informazioni personali (PII, personally identifiable information). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi. [Ulteriori informazioni](https://www.adobe.com/privacy/experience-cloud.html).

## Eventi dashboard richiesti

Alcuni eventi sono necessari per compilare il [Dashboard di Live Search](performance.md)

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

Tutti gli eventi richiedono `Page` e `Storefront` contesti. Questo dovrebbe accadere a livello di pagina/livello di applicazione vetrina piuttosto che durante la generazione di singoli eventi (ad esempio, in una vetrina PHP, il contenitore di applicazioni PHP è responsabile della loro impostazione in fase di esecuzione).

## Utilizzo

Di seguito è riportato un esempio di implementazione di `search-request-sent` evento:

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

I blocchi degli annunci e le impostazioni della privacy possono impedire l’acquisizione degli eventi e causare il coinvolgimento e ricavi [metriche](workspace.md) da non segnalare correttamente.

Eventing non acquisisce ogni transazione che avviene sul sito del commerciante. L&#39;evento ha lo scopo di dare al mercante un&#39;idea generale degli eventi che stanno accadendo sul sito.

Le implementazioni headless devono implementare un evento per alimentare [Dashboard del Recommendations del prodotto](../product-recommendations/events.md).

>[!NOTE]
>
>Se [Modalità di restrizione cookie](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html) è abilitato, Adobe Commerce non raccoglie i dati comportamentali fino a quando l’acquirente non acconsente all’utilizzo dei cookie. Se la modalità di restrizione dei cookie è disabilitata, Adobe Commerce raccoglie i dati comportamentali per impostazione predefinita.
