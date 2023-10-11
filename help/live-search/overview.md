---
title: Introduzione a [!DNL Live Search]
description: '"[!DNL Live Search] Adobe Commerce offre un''esperienza di ricerca rapida, super-rilevante e intuitiva".'
exl-id: aca0ef19-ead1-4c79-90c3-db5ec48cb3c1
recommendations: noCatalog
source-git-commit: 4eddad715405f35ea063bab3cf4651fec3beeae5
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Introduzione a [!DNL Live Search]

[!DNL Live Search] è un servizio per Adobe Commerce che sostituisce le funzionalità di ricerca standard. Il [!DNL Live Search] viene installato con Composer e connette il [!DNL Commerce] installazione in [!DNL Live Search] [servizio](../landing/saas.md). Una volta configurato, il campo di testo di ricerca predefinito viene sostituito con [!DNL Live Search] campo di testo.

[!DNL Live Search] viene visualizzato sul *Marketing* menu in *SEO e ricerca* nel [!DNL Commerce] *Amministratore*.

Il lato Adobe Commerce dell’architettura include l’hosting della ricerca *Amministratore*, la sincronizzazione dei dati del catalogo e l&#39;esecuzione del servizio query. Dopo [!DNL Live Search] è installato e configurato, Adobe Commerce inizia a condividere i dati di ricerca e catalogo con i servizi SaaS. A questo punto, gli utenti amministratori possono impostare, personalizzare e gestire la ricerca [facet](facets.md), [sinonimi](synonyms.md), e [regole di merchandising](category-merch.md).

![Diagramma dell’architettura di Live Search](assets/architecture-diagram.svg)

## Componenti Live Search

* [!DNL Live Search] [popover](storefront-popover.md) è la casella che si apre sotto il campo di ricerca contenente i risultati della ricerca.
* [Widget pagina elenco prodotti](plp-styling.md) fornisce una pagina di elenco dei prodotti ricercabili con supporto per facet e sinonimi.
* L&#39;AEM [Componente CIF](https://github.com/adobe/aem-cif-guides-venia/pull/319) consente ai siti AEM di sfruttare [!DNL Live Search].
* [[!DNL Live Search] Amministratore](workspace.md) è dove vengono configurati regole, facet e sinonimi.
* L&#39;adattatore di ricerca è l&#39;implementazione predefinita di [!DNL Live Search].

## [!DNL Live Search] demo

Guarda questo video per saperne di più su [!DNL Live Search]:

>[!VIDEO](https://video.tv.adobe.com/v/3418679?quality=12&learn=on)

Per un video più approfondito sull’utilizzo e la configurazione di Live Search, vedi [Dimostrazione completa su [!DNL Live Search]](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/marketing/live-search-full-demonstration.html) argomento.
