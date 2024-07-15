---
title: "Indicizzazione"
description: "Scopri come [!DNL Live Search] indicizza le proprietà degli attributi del prodotto."
exl-id: 04441e58-ffac-4335-aa26-893988a89720
source-git-commit: 4978bdb5549f5df911863a23fdfbfc9ab9ad05df
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Indicizzazione

Il processo di indicizzazione [!DNL Live Search] legge nel catalogo gli attributi dei prodotti e crea un indice che consente di cercare, filtrare e presentare rapidamente i prodotti.

Le proprietà dell’attributo del prodotto (metadati) determinano:

* Come utilizzare un attributo nel catalogo
* Il suo aspetto e il suo comportamento in negozio
* Dati inclusi nelle operazioni di trasferimento dati

L&#39;ambito dei metadati dell&#39;attributo è `website/store/store view`.

L&#39;API [!DNL Live Search] consente a un client di ordinare in base a qualsiasi attributo di prodotto la cui proprietà [storefront](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) `Use in Search` è impostata su `Yes` nell&#39;amministrazione di Adobe Commerce. Se questa opzione è abilitata, è possibile impostare `Search Weight` e `Visible in Advanced Search` per l&#39;attributo.

[!DNL Live Search] non indicizza i prodotti eliminati o quelli impostati su `Not Visible Individually`.

>[!NOTE]
>
> I clienti Commerce con [!DNL Live Search] possono sfruttare gli aggiornamenti più rapidi delle modifiche dei prezzi e i tempi di sincronizzazione sui loro siti Web con l&#39;[indicizzatore dei prezzi SaaS](../price-index/price-indexing.md).

## Pipeline di indicizzazione

Il client chiama il servizio di ricerca dalla vetrina per recuperare i metadati dell’indice (filtrabili, ordinabili). Il servizio di ricerca può chiamare solo gli attributi di prodotto ricercabili con la proprietà *Use in Layered Navigation* impostata su `Filterable (with results)` e *Use for Sorting in Product Listing* impostata su `Yes`.
Per creare una query dinamica, il servizio di ricerca deve sapere quali attributi sono ricercabili e il relativo [peso](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search). [!DNL Live Search] rispetta i pesi di ricerca di Adobe Commerce (1-10, dove 10 è la priorità più alta). L’elenco dei dati sincronizzati e condivisi con il servizio catalogo si trova nello schema, definito in:

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search] diagramma di indicizzazione ricerca client](assets/indexing-pipeline.svg)

1. Controlla l&#39;esercente per l&#39;adesione [!DNL Live Search].
1. Ottieni le visualizzazioni dello store con le modifiche ai metadati dell’attributo.
1. Memorizza attributi di indicizzazione.
1. Reindicizza indice di ricerca.

### Indice completo

Quando [!DNL Live Search] viene configurato e sincronizzato durante l&#39;onboarding, la generazione dell&#39;indice iniziale può richiedere fino a 60 minuti. L’indicizzazione di cataloghi di grandi dimensioni può richiedere più tempo. Il processo inizia dopo l&#39;invio del feed da parte di `cron` e termina l&#39;esecuzione.

I seguenti eventi attivano una build di sincronizzazione e indicizzazione completa:

* Onboarding di [sincronizzazione dati catalogo](install.md#synchronize-catalog-data)
* Modifiche ai metadati degli attributi

Se ad esempio si modifica la proprietà `Use in Search` dell&#39;attributo `color` da `No` a `Yes`, i metadati dell&#39;attributo verranno modificati in `searchable=true` e verrà attivata la sincronizzazione completa e la reindicizzazione. I seguenti metadati di attributi attivano la sincronizzazione completa e la reindicizzazione quando vengono modificati:

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### Aggiornamenti dei prodotti in streaming

Dopo che l&#39;indice iniziale è stato generato durante [l&#39;onboarding](install.md#synchronize-catalog-data), i seguenti aggiornamenti incrementali del prodotto vengono sincronizzati e reindicizzati in modo continuo:

* Nuovi prodotti aggiunti al catalogo
* Modifiche ai valori degli attributi del prodotto

Ad esempio, l&#39;aggiunta di un nuovo valore di campione all&#39;attributo `color` viene gestita come aggiornamento del prodotto di streaming.
Flusso di lavoro di aggiornamento in streaming:

1. I prodotti aggiornati vengono sincronizzati dall’istanza di Adobe Commerce al servizio catalogo.
1. Il servizio di indicizzazione cerca continuamente gli aggiornamenti dei prodotti dal servizio catalogo. I prodotti aggiornati vengono indicizzati al momento dell’arrivo nel servizio catalogo.
1. Possono essere necessari fino a 15 minuti perché un aggiornamento del prodotto diventi disponibile in [!DNL Live Search].

## Ricerca client

L&#39;API [!DNL Live Search] consente a un client di ordinare in base a qualsiasi attributo di prodotto ordinabile impostando la [proprietà storefront](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html), *utilizzata per l&#39;ordinamento negli elenchi di prodotti* su `Yes`. A seconda del tema, questa impostazione determina l&#39;inclusione dell&#39;attributo come opzione nel controllo di paginazione [Ordina per](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation.html) nelle pagine del catalogo. È possibile indicizzare fino a 200 attributi di prodotto da [!DNL Live Search], con [proprietà storefront](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) ricercabili e filtrabili.
I metadati dell’indice vengono memorizzati nella pipeline di indicizzazione e sono accessibili dal servizio di ricerca.

Diagramma API dei metadati dell&#39;indice ![[!DNL Live Search]](assets/index-metadata-api.svg)

### Flusso di lavoro degli attributi ordinabili

1. Il client chiama il servizio di ricerca.
1. Il servizio di ricerca chiama il servizio di amministrazione della ricerca.
1. Il servizio di ricerca chiama la pipeline di indicizzazione.

## Indicizzato per tutti i prodotti

L’ordine dei campi in questo elenco riflette l’ordine tipico delle colonne nei dati del prodotto esportato.

* `environment_id`
* `website_code`
* `store_code`
* `store_view_code`
* `product_id`
* `sku`
* `name`
* `type`
* `displayable`
* `deleted`
* `url`
* `currency`
* `meta_description`
* `meta_keyword`
* `meta_title`
* `description`
* `short_description`
* `weight`
* `image`
* `small_image`
* `thumbnail_image`
* `prices`
* `in_stock`
* `low_stock`

Il seguente campo è indicizzato per tutti i prodotti configurabili:

* `childrenSkus`
