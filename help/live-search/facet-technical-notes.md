---
title: '"Note tecniche"'
description: '"Note tecniche sull''utilizzo [!DNL Live Search] facet."'
exl-id: 37982610-0ff7-48b7-b088-be7d2eff8a57
source-git-commit: bffbede99865e9085f60392e474065a454446370
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Note tecniche su facet

Faceting è un metodo di filtraggio ad alte prestazioni che utilizza più dimensioni di valori di attributi statici e dinamici ricercabili come criteri di ricerca.

[!DNL Live Search] utilizza `productSearch` query che restituisce facet e altri dati specifici per [!DNL Live Search]. Fai riferimento a [`productSearch` query](https://devdocs.magento.com/live-search/product-search.html) per esempi di codice.

## Aggregazione di facet

L&#39;aggregazione dei facet viene eseguita come segue se la vetrina ha tre facet (categorie, colore e prezzo) e i filtri dell&#39;acquirente su tutti e tre (colore = blu, prezzo = $ 10,00-50,00, categorie = `promotions`).

* `categories` aggregazione - Aggregati `categories`, si applica `color` e `price` filtri, ma non `categories` filtro.
* `color` aggregazione - Aggregati `color`, si applica `price` e `categories` filtri, ma non `color` filtro.
* `price` aggregazione - Aggregati `price`, si applica `color` e `categories` filtri, ma non `price` filtro.
