---
title: "Indicizzazione"
description: "Scopri come [!DNL Live Search] indicizza le proprietà dell’attributo del prodotto."
exl-id: 04441e58-ffac-4335-aa26-893988a89720
source-git-commit: 4978bdb5549f5df911863a23fdfbfc9ab9ad05df
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Indicizzazione

Il [!DNL Live Search] il processo di indicizzazione legge nel catalogo gli attributi del prodotto e crea un indice che consente di cercare, filtrare e visualizzare rapidamente i prodotti.

Le proprietà dell’attributo del prodotto (metadati) determinano:

* Come utilizzare un attributo nel catalogo
* Il suo aspetto e il suo comportamento in negozio
* Dati inclusi nelle operazioni di trasferimento dati

L’ambito dei metadati dell’attributo è `website/store/store view`.

Il [!DNL Live Search] API consente a un client di ordinare per qualsiasi attributo di prodotto che ha [proprietà storefront](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) `Use in Search` imposta su `Yes` in Adobe Commerce Admin. Quando è attivata, `Search Weight` e `Visible in Advanced Search` può essere impostato per l’attributo.

[!DNL Live Search] non indicizza i prodotti eliminati o impostati su `Not Visible Individually`.

>[!NOTE]
>
> Clienti Commerce con [!DNL Live Search] possono sfruttare gli aggiornamenti più rapidi dei cambiamenti di prezzo e i tempi di sincronizzazione sui loro siti web con [Indicizzatore prezzi SaaS](../price-index/price-indexing.md).

## Pipeline di indicizzazione

Il client chiama il servizio di ricerca dalla vetrina per recuperare i metadati dell’indice (filtrabili, ordinabili). Solo gli attributi di prodotto ricercabili con *Uso in navigazione a livelli* proprietà impostata su `Filterable (with results)` e *Usa per l’ordinamento nell’elenco dei prodotti* imposta su `Yes` può essere richiamato dal servizio di ricerca.
Per creare una query dinamica, il servizio di ricerca deve sapere quali attributi sono ricercabili e i relativi [peso](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search). [!DNL Live Search] rispetta i pesi di ricerca di Adobe Commerce (1-10, dove 10 rappresenta la priorità più elevata). L’elenco dei dati sincronizzati e condivisi con il servizio catalogo si trova nello schema, definito in:

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search] diagramma di ricerca client indicizzazione](assets/indexing-pipeline.svg)

1. Controlla esercente per [!DNL Live Search] diritto.
1. Ottieni le visualizzazioni dello store con le modifiche ai metadati dell’attributo.
1. Memorizza attributi di indicizzazione.
1. Reindicizza indice di ricerca.

### Indice completo

Quando [!DNL Live Search] è configurato e sincronizzato durante l’onboarding, la creazione dell’indice iniziale può richiedere fino a 60 minuti. L’indicizzazione di cataloghi di grandi dimensioni può richiedere più tempo. Il processo inizia dopo `cron` invia il feed e termina l’esecuzione.

I seguenti eventi attivano una build di sincronizzazione e indicizzazione completa:

* Onboarding [sincronizzazione dati catalogo](install.md#synchronize-catalog-data)
* Modifiche ai metadati degli attributi

Ad esempio, la modifica di `Use in Search` proprietà del `color` attributo da `No` a `Yes` modifica i metadati dell’attributo in `searchable=true`, e attiva una sincronizzazione e una reindicizzazione complete. I seguenti metadati di attributi attivano la sincronizzazione completa e la reindicizzazione quando vengono modificati:

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### Aggiornamenti dei prodotti in streaming

Dopo che l’indice iniziale è stato generato durante [onboarding](install.md#synchronize-catalog-data), i seguenti aggiornamenti di prodotto incrementali vengono continuamente sincronizzati e reindicizzati:

* Nuovi prodotti aggiunti al catalogo
* Modifiche ai valori degli attributi del prodotto

Ad esempio, l’aggiunta di un nuovo valore di campione al `color` viene gestito come aggiornamento del prodotto in streaming.
Flusso di lavoro di aggiornamento in streaming:

1. I prodotti aggiornati vengono sincronizzati dall’istanza di Adobe Commerce al servizio catalogo.
1. Il servizio di indicizzazione cerca continuamente gli aggiornamenti dei prodotti dal servizio catalogo. I prodotti aggiornati vengono indicizzati al momento dell’arrivo nel servizio catalogo.
1. Possono essere necessari fino a 15 minuti perché un aggiornamento del prodotto sia disponibile in [!DNL Live Search].

## Ricerca client

Il [!DNL Live Search] API consente a un client di ordinare per qualsiasi attributo di prodotto ordinabile impostando [proprietà storefront](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html), *Utilizzato per l’ordinamento negli elenchi di prodotti* a `Yes`. A seconda del tema, questa impostazione determina l’inclusione dell’attributo come opzione nella [Ordina per](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation.html) controllo impaginazione sulle pagine di catalogo. È possibile indicizzare fino a 200 attributi di prodotto per [!DNL Live Search], con [proprietà vetrina](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) ricercabili e filtrabili.
I metadati dell’indice vengono memorizzati nella pipeline di indicizzazione e sono accessibili dal servizio di ricerca.

![[!DNL Live Search] diagramma API metadati indice](assets/index-metadata-api.svg)

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
