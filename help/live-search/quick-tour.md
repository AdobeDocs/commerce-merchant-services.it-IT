---
title: "Presentazione rapida"
description: "Dai un’occhiata [!DNL Live Search] dalla vetrina."
exl-id: bcb19506-6617-4c8a-83df-9d961f81e9e8
source-git-commit: 9f045a049ac775ed4673e807ab5e21b8811cde2d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Presentazione rapida

Con particolare attenzione a velocità, pertinenza e facilità d&#39;uso, [!DNL Live Search] è un cambiavalute sia per gli acquirenti che per i commercianti. Segui per un rapido tour di [!DNL Live Search] dalla vetrina.

## Cerca durante la digitazione

[!DNL Live Search] risponde con i prodotti suggeriti e un&#39;immagine in miniatura dei risultati di ricerca principali in un [popover](storefront-popover.md) quando gli acquirenti digitano query in [Ricerca](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search) casella. Il [dettagli prodotto](https://experienceleague.adobe.com/docs/commerce-admin/start/storefront/storefront.html#product-page) Questa pagina viene visualizzata quando gli acquirenti fanno clic su un prodotto suggerito o in primo piano. A _Visualizza tutto_ nel piè di pagina del popover viene visualizzata la pagina dei risultati della ricerca.

[!DNL Live Search] restituisce i risultati di &quot;ricerca durante la digitazione&quot; per una query di due o più caratteri. Per una corrispondenza parziale, il numero massimo di caratteri per parola è 20. Il numero di caratteri nella query non è configurabile. Nel popover sono inclusi i seguenti campi: `name`, `sku`, e `category_ids`.

![Esempio di vetrina: cerca durante la digitazione](assets/storefront-search-as-you-type.png)

## Visualizza tutti i risultati di ricerca

Per elencare tutti i prodotti restituiti dalla query di ricerca durante la digitazione, fare clic su _Visualizza tutto_ nel piè di pagina della finestra a comparsa.

![Esempio di vetrina - facet di prezzo](assets/storefront-view-all-search-results.png)

## Ricerca filtrata con facet

La ricerca filtrata utilizza più dimensioni di valori di attributo, oppure [facet](facets.md), come criterio di ricerca. La selezione dei filtri è definita dall’esercente e cambia in base ai prodotti restituiti, con i facet più comunemente utilizzati inseriti nella parte superiore dell’elenco.

Utilizza i facet come parametri URL:`http://yourwebsite.com?color=red`, e Live Search filtra i risultati in base a questi valori di attributo.

## Sinonimi

[Sinonimi](synonyms.md) espandi la portata e affina la messa a fuoco delle query includendo le parole che gli acquirenti potrebbero utilizzare diverse da quelle nel catalogo. Puoi regolare il dizionario dei sinonimi per mantenere gli acquirenti coinvolti e sulla strada per l&#39;acquisto.

## Regole di merchandising

Merchandising [regole](rules.md) forma l’esperienza di acquisto con istruzioni if-then che aggiungono logica ed eventi alla ricerca. Puoi facilmente aumentare o seppellire i prodotti per una promozione, una stagione o un altro periodo di tempo.

## Supporto termini di ricerca

[!DNL Live Search] supporta Commerce [reindirizzamenti termini di ricerca](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html). Ad esempio, gli utenti possono cercare un termine come &quot;Tariffe di spedizione&quot; ed essere portati direttamente alla pagina delle tariffe di spedizione.
