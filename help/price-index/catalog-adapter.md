---
title: Estensione scheda catalogo
description: Utilizzo di Catalog Adapter per il rendering dei prezzi da Commerce Services
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
source-git-commit: 6b578e7113c278a05a64f2db5e032bccc4a9580a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Adattatore catalogo

Il `Catalog Adapter` L&#39;estensione disabilita l&#39;indicizzatore predefinito del prezzo del prodotto Adobe Commerce e utilizza i prezzi forniti dall&#39; [Servizio catalogo](../catalog-service/overview.md).
L’indicizzatore del prezzo del prodotto Adobe Commerce è disabilitato e non può essere attivato con questi moduli di estensione installati. Solo rimuovendo o disabilitando questa estensione è possibile riabilitare l’indicizzatore predefinito del prezzo del prodotto.

## Requisiti

* Adobe Commerce 2.4.4+
* È installato uno dei seguenti servizi Commerce:

   * [Servizio catalogo](../catalog-service/overview.md)
   * [Live Search](../live-search/guide-overview.md)

## Installazione

Per utilizzare `catalog-adapter` modulo, [!DNL Live Search] e [!DNL Catalog Service] deve prima essere installato e configurato. Segui le [Installa [!DNL Live Search]](../live-search/install.md) e [Installazione di Catalog Service](../catalog-service/installation.md) prima di continuare.

Dopo aver installato tali servizi, eseguire il comando seguente:

```bash
composer require adobe-commerce/catalog-adapter
```

## Abilitare nuovamente l’indicizzatore del prezzo del prodotto Adobe Commerce

Se disponi di applicazioni di terze parti che si basano sull’indicizzatore predefinito del prezzo del prodotto Adobe Commerce, puoi riabilitarlo con i seguenti comandi:

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# reindex Product Price indexer 
bin/magento index:reindex catalog_product_price
```

## Disattiva l&#39;indicizzatore del prezzo del prodotto per lo scenario Headless Storefront

Se disponi di un’istanza Commerce headless, potresti dover disabilitare l’indicizzatore prezzo prodotto Adobe Commerce per ridurre il carico sull’istanza Adobe Commerce.
A questo scopo, installa il `magento/module-price-indexer-disabler` modulo:

```bash
composer require magento/module-price-indexer-disabler
```

## Scenari di utilizzo

Di seguito sono riportati alcuni esempi comuni `Catalog Adapter` scenari.

### Nessuna dipendenza da Adobe Commerce Product Price indexer

* Sei un commerciante Luma o Adobe Commerce Core GraphQL con installato un servizio richiesto (Live Search, Product Recommendations, Catalog Service)
* Nessuna estensione di terze parti basata sull’indicizzatore del prezzo del prodotto Adobe Commerce

1. Installare la scheda catalogo.

### Con dipendenze dall’indicizzatore dei prezzi dei prodotti Adobe Commerce

* Sei un commerciante Luma o Adobe Commerce Core GraphQL con installato un servizio supportato (Live Search, Product Recommendations, Catalog Service)
* Puoi utilizzare un’estensione di terze parti basata sull’indicizzatore del prezzo del prodotto Adobe Commerce

1. Installare la scheda catalogo.
1. Riattiva l’indicizzatore predefinito del prezzo del prodotto Adobe Commerce.

### Istanze Commerce headless

* Un commerciante con un’istanza Commerce headless con i servizi richiesti installati (Live Search, Product Recommendations, Catalog Service)
* Nessuna dipendenza dall&#39;indicizzatore predefinito del prezzo del prodotto Adobe Commerce

1. Installare &quot;price disabler&quot; dal pacchetto dell&#39;adattatore catalogo
