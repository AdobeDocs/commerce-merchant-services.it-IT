---
title: Introduzione a [!DNL Live Search]
description: '"[!DNL Live Search] Adobe Commerce offre un''esperienza di ricerca rapida, super-rilevante e intuitiva".'
exl-id: aca0ef19-ead1-4c79-90c3-db5ec48cb3c1
recommendations: noCatalog
source-git-commit: d5df2a098dbbb2ecfb68c36dd12843c963d46b17
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Introduzione a [!DNL Live Search]

[!DNL Live Search] è un servizio per Adobe Commerce che sostituisce le funzionalità di ricerca standard. Il [!DNL Live Search] viene installato con Composer e connette il [!DNL Commerce] installazione in [!DNL Live Search] [servizio](../landing/saas.md). Una volta configurato, il campo di testo di ricerca predefinito viene sostituito con [!DNL Live Search] campo di testo. [!DNL Live Search] installa anche il widget Pagina di elenco prodotti (PLP) che fornisce solide funzionalità di filtro durante la navigazione nei risultati di ricerca.

[!DNL Live Search] viene visualizzato sul *Marketing* menu in *SEO e ricerca* nel [!DNL Commerce] *Amministratore*.

Il lato Adobe Commerce dell’architettura include l’hosting della ricerca *Amministratore*, la sincronizzazione dei dati del catalogo e l&#39;esecuzione del servizio query. Dopo [!DNL Live Search] è installato e configurato, Adobe Commerce inizia a condividere i dati di ricerca e catalogo con i servizi SaaS. A questo punto, gli utenti amministratori possono impostare, personalizzare e gestire la ricerca [facet](facets.md), [sinonimi](synonyms.md), e [regole di merchandising](category-merch.md).

## Componenti Live Search

* [!DNL Live Search] [widget popover](storefront-popover.md) è la casella che si apre sotto il campo di ricerca contenente i risultati della ricerca.
* [Widget pagina elenco prodotti](plp-styling.md) fornisce una pagina di elenco dei prodotti ricercabili con supporto per facet e sinonimi.
* Componenti dell’CIF dell’AEM: la [Widget popover](https://github.com/adobe/aem-cif-guides-venia/pull/319) e [Widget PLP](https://github.com/adobe/aem-cif-guides-venia/pull/320) consentire ai siti AEM di sfruttare [!DNL Live Search].
* [[!DNL Live Search] Amministratore](workspace.md) è dove vengono configurati regole, facet e sinonimi.

## Panoramica del flusso di lavoro

[!DNL Live Search] funziona spostando i dati del catalogo nell’infrastruttura SaaS di Adobe Commerce e creando indici utilizzati per fornire rapidamente i risultati della ricerca durante la digitazione da parte degli utenti.

### 1. Installazione

[!DNL Live Search] è [installato](install.md) nell’istanza Adobe Commerce tramite [Compositore](https://getcomposer.org/). In questo modo vengono installati i moduli richiesti che si connettono al servizio e viene configurata l’istanza di Commerce per ignorare il campo di ricerca predefinito. Installa inoltre le opzioni Commerce Admin per la configurazione del servizio.

### 2. Sincronizza dati

[!DNL Live Search] sposta i dati del catalogo nell’infrastruttura SaaS di Adobe. I dati vengono indicizzati e i risultati della ricerca vengono consegnati da questo indice direttamente alla vetrina. A seconda delle dimensioni e della complessità, l’indicizzazione può richiedere da 30 minuti a un paio d’ore.

### 3. Configurare i dati

La corretta configurazione dei dati di prodotto garantisce buoni risultati di ricerca per i clienti. Sono necessari due passaggi di configurazione: assegnazione di categorie e configurazione degli attributi.

#### Assegna categorie

Prodotto restituito in [!DNL Live Search] deve essere assegnato un [categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/categories.html). In Luma, ad esempio, i prodotti sono inseriti in categorie come &quot;Uomini&quot;, &quot;Donne&quot; e &quot;Attrezzi&quot;. Sono impostate anche delle sottocategorie per &quot;Tops&quot;, &quot;Bottoms&quot; e &quot;Watches&quot;. Questo consente una maggiore granularità durante il filtraggio.

#### Campi ricercabili e filtrabili

I prodotti sono assegnati [attributi](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) che possono essere utilizzati per la ricerca e il filtraggio. Gli attributi sono ad esempio &quot;Colore&quot;, &quot;Dimensione&quot;, &quot;Tipo di materiale&quot;. Con questi attributi, gli utenti possono cercare &quot;green tops&quot;. In Commerce admin possono essere definiti molti attributi per ogni prodotto.

Ciascuno di questi attributi può essere definito come [&quot;ricercabile&quot;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html) nell’amministratore. Se impostati come &quot;ricercabili&quot;, tali attributi sono disponibili per la ricerca [!DNL Live Search].

[Facet](facets.md) sono attributi di prodotto definiti in [!DNL Live Search] per essere filtrabile. Qualsiasi attributo filtrabile può essere impostato come facet in [!DNL Live Search] ma ci sono limiti al numero di facet che è possibile cercare contemporaneamente.

[Sinonimi](synonyms.md) sono termini che puoi definire per guidare gli utenti verso il prodotto corretto. Gli utenti alla ricerca di pantaloni potrebbero digitare &quot;pantaloni&quot; o &quot;pantaloni&quot;. È possibile impostare sinonimi in modo che questi termini di ricerca portino gli utenti ai risultati &quot;pantaloni&quot;.

## [!DNL Live Search] workspace

Il [!DNL Live Search] [workspace](workspace.md) è l’area dell’Amin in cui configuri [!DNL Live Search] funzioni quali sinonimi, facet e merchandising di categorie.

## Eventi

[!DNL Live Search] utilizza [Eventi](events.md) per calcolare [Merchandising intelligente](category-merch.md) e [prestazioni](performance.md) dashboard. L’evento viene fornito con le implementazioni predefinite. L’evento per le vetrine headless deve essere abilitato manualmente.

## Personalizzazione dei widget

La maggior parte dei proprietari dei negozi desidera assicurarsi che [!DNL Live Search] I widget si adattano all&#39;aspetto del negozio.

I widget popover e PLP possono essere formattati definendo regole CSS personalizzate in base alle esigenze. Consulta [Elementi Popover Di Stile](storefront-popover-styling.md) e [Widget pagina elenco prodotti](plp-styling.md).

Se desideri estendere la funzionalità dei widget, il codice sorgente per ciascuno di essi è disponibile in un repository pubblico.
In questo scenario, puoi personalizzare JavaScript in base alle tue esigenze e quindi ospitare il codice personalizzato sul tuo sito. Questo script personalizzato comunica con [!DNL Live Search] e restituisce i risultati come normale, consentendoti di controllare la funzionalità del widget.

* [Repo widget PLP](https://github.com/adobe/storefront-product-listing-page)
* [Archivio barra di ricerca](https://github.com/adobe/storefront-search-as-you-type)

Ottieni ulteriori dettagli su [!DNL Live Search] nel [Panoramica tecnica](technical-overview.md).

## [!DNL Live Search] demo

Guarda questo video per saperne di più su [!DNL Live Search]:

>[!VIDEO](https://video.tv.adobe.com/v/3418679?quality=12&learn=on)

Per un video più approfondito sull’utilizzo e la configurazione di Live Search, vedi [Dimostrazione completa su [!DNL Live Search]](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/marketing/live-search-full-demonstration.html) argomento.
