---
title: Installazione manuale dell'indicizzazione dei prezzi SaaS
description: Installazione dell'indicizzazione dei prezzi SaaS per la versione precedente
seo-title: SaaS Price Indexing installation
seo-description: Installing SaaS Price indexing
exl-id: 4577111a-64a4-4e20-b970-3abfa6758247
role: Admin, Developer
source-git-commit: 3809d27fc3689519e4a162aa52f481d254aec656
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Installazione manuale dell&#39;indicizzazione dei prezzi SaaS

L’indicizzazione dei prezzi SaaS è disponibile come opzione predefinita per i prodotti supportati [ultima versione](index.md#Requirements) di Commerce Services.
Se non disponi della versione più recente e desideri abilitare l’indicizzazione dei prezzi SaaS per la tua istanza di Adobe Commerce, utilizza questa mini-guida.

## Prerequisiti

* Adobe Commerce 2.4.4+
* È installato almeno uno dei seguenti servizi SaaS:

   * [Servizio catalogo](../catalog-service/overview.md)
   * [Live Search](../live-search/guide-overview.md)
   * [Recommendations del prodotto](../product-recommendations/guide-overview.md)

## Installare i moduli richiesti

A seconda della configurazione, il processo di installazione potrebbe essere leggermente diverso.
Esistono estensioni che aggiungono i nuovi feed e il codice di supporto.

1. Aggiungi i seguenti moduli al tuo `composer.json` file:

   ```json
   "magento/module-saas-price": "^102.2.0",
   "magento/module-saas-scopes": ^"102.2.0",
   "magento/module-product-override-price-remover": "^102.2.0",
   "magento/module-bundle-product-override-data-exporter": "^102.2.0",
   ```

1. Esegui il comando di aggiornamento:

   ```bash
   bin/magento setup:upgrade
   ```

Dopo l&#39;upgrade, sono disponibili tre nuovi feed:

* `prices` - responsabile della fornitura dei dati sui prezzi al servizio
* `scopesCustomerGroup` - responsabile della fornitura dei gruppi di clienti al servizio
* `scopesWebsite` - responsabile della fornitura di siti Web, gruppi di store e visualizzazioni di store al servizio


1. Configura i nuovi feed da impostare sulla modalità &quot;Aggiorna in base a pianificazione&quot;:

   ```bash
   bin/magento indexer:set-mode schedule catalog_data_exporter_product_prices scopes_customergroup_data_exporter scopes_website_data_exporter
   ```

1. Reindicizzare i nuovi feed:

   ```bash
   bin/magento saas:resync --feed=scopesCustomerGroup
   bin/magento saas:resync --feed=scopesWebsite
   bin/magento saas:resync --feed=prices
   ```

Esegui manualmente gli indicizzatori di cui sopra, in base alle esigenze. In caso contrario, i dati vengono aggiornati nel processo di sincronizzazione standard. Ulteriori informazioni su [Sincronizzazione catalogo](../landing/catalog-sync.md) servizio.


Per configurare Live Search e l&#39;adattatore del catalogo, attenersi alla procedura [Connettore Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html) istruzioni.

## Avvertenze

Prima di `103.0.0` Supporto dell’indicizzazione dei prezzi SaaS per i tipi di prodotto semplici, raggruppati, virtuali, configurabili e dinamici bundle.
Il supporto per i tipi di prodotti scaricabili, gift card e bundle fissi è disponibile a partire da `magento/module-saas-price:103.0.0` e disponibile come opzione predefinita per i servizi Commerce supportati.

I nuovi feed devono essere sincronizzati manualmente con `resync` [Comando CLI](../landing/catalog-sync.md#resynccmdline). In caso contrario, i dati vengono aggiornati nel processo di sincronizzazione standard. Ulteriori informazioni su [Sincronizzazione catalogo](../landing/catalog-sync.md) processo.
