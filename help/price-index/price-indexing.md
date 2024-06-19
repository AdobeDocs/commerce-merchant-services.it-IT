---
title: Indicizzazione dei prezzi SaaS
description: Utilizzo dell'indicizzazione dei prezzi SaaS per migliorare le prestazioni
seo-title: Adobe SaaS Price Indexing
seo-description: Price indexing give performance improvements using SaaS infrastructure
exl-id: 5b92d6ea-cfd6-4976-a430-1a3aeaed51fd
source-git-commit: 8230756c203cb2b4bdb4949f116c398fcaab84ff
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Indicizzazione dei prezzi SaaS

L’indicizzazione dei prezzi SaaS migliora le prestazioni del sito spostando pesanti processi di calcolo, come l’indicizzazione e il calcolo dei prezzi, dall’applicazione Commerce all’infrastruttura cloud di Adobe. Questo approccio consente ai commercianti di aumentare rapidamente le risorse per aumentare i tempi di indicizzazione dei prezzi in modo da riflettere più rapidamente le variazioni di prezzo durante l’invio dei dati allo storefront e ai servizi Commerce connessi.

Il diagramma seguente mostra il flusso di dati di indicizzazione verso i servizi SaaS quando Commerce utilizza [indicizzazione dei prezzi](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) processo incluso nell&#39;applicazione Commerce:

![Flusso di dati predefinito](assets/old_way.png)

Con l’indicizzazione dei prezzi SaaS abilitata, il flusso di dati cambia. L’indicizzazione dei prezzi viene eseguita utilizzando [Esportazione di dati SaaS Commerce](../data-export/data-synchronization.md).

![Flusso di dati di indicizzazione prezzi SaaS](assets/new_way.png)

Tutti i commercianti possono beneficiare dell’indicizzazione dei prezzi SaaS, ma i commercianti che hanno progetti con le seguenti caratteristiche possono realizzare i maggiori vantaggi:

* **Variazioni di prezzo costanti**-Mercanti che richiedono ripetute modifiche ai prezzi per soddisfare obiettivi strategici quali promozioni frequenti, sconti stagionali o riduzioni di scorte.
* **Più siti web e/o gruppi di clienti**-Mercanti con cataloghi di prodotti condivisi su più siti web (domini/marchi) e/o gruppi di clienti.
* **Molti prezzi univoci tra siti web o gruppi di clienti**-Mercanti con estesi cataloghi di prodotti condivisi che contengono prezzi univoci tra siti web o gruppi di clienti. Alcuni esempi includono i commercianti B2B che hanno prezzi pre-negoziati o marchi con diverse strategie di prezzo.

## Usa indicizzazione prezzi SaaS

L’indicizzazione dei prezzi SaaS viene abilitata automaticamente quando si installa Adobe Commerce Services. Supporta il calcolo dei prezzi per tutti i tipi di prodotto Adobe Commerce incorporati.

### Requisiti

* Adobe Commerce 2.4.4+

### Prerequisiti

* Con la versione più recente dell&#39;estensione Commerce deve essere installato uno dei servizi Commerce seguenti:

   * [Servizio catalogo](../catalog-service/overview.md)
   * [Live Search](../live-search/overview.md)
   * [Recommendations del prodotto](../product-recommendations/guide-overview.md)


>[!NOTE]
>
>Se necessario, l&#39;indicizzatore prezzi predefinito nell&#39;applicazione Commerce può essere disabilitato utilizzando [Adattatore catalogo](catalog-adapter.md).

## Sincronizzare i prezzi con l&#39;indicizzazione SaaS

Dopo aver abilitato l’indicizzazione dei prezzi SaaS per Adobe Commerce, aggiorna i prezzi su Storefront e in Commerce Services sincronizzando i nuovi feed:

```bash
bin/magento saas:resync --feed=scopesCustomerGroup
bin/magento saas:resync --feed=scopesWebsite
bin/magento saas:resync --feed=prices
```

### Prezzi per tipi di prodotto personalizzati

I calcoli dei prezzi sono supportati per i tipi di prodotto personalizzati, ad esempio il prezzo di base, il prezzo speciale, il prezzo di gruppo, il prezzo delle regole di catalogo e così via.

Se si dispone di un tipo di prodotto personalizzato che utilizza una formula specifica per calcolare il prezzo finale, è possibile estendere il comportamento del feed del prezzo del prodotto.

1. Creare un plug-in in `Magento\ProductPriceDataExporter\Model\Provider\ProductPrice` classe.

   ```xml
   <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
       <type name="Magento\ProductPriceDataExporter\Model\Provider\ProductPrice">
           <plugin name="custom_type_price_feed" type="YourModule\CustomProductType\Plugin\UpdatePriceFromFeed" />
       </type>
   </config>
   ```

1. Crea un metodo con la formula personalizzata:

   ```php
   class UpdatePriceFromFeed
   {
       /**
       * @param ProductPrice $subject
       * @param array $result
       * @param array $values
       *
       * @return array
       */
       public function afterGet(ProductPrice $subject, array $result, array $values) : array
       {
           // Override the output $result with your data for the corresponding products (see original method for details) 
           return $result;
       }
   }
   ```

