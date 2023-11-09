---
title: Indicizzazione dei prezzi SaaS
description: Utilizzo dell'indicizzazione dei prezzi SaaS per migliorare le prestazioni
seo-title: Adobe SaaS Price Indexing
seo-description: Price indexing give performance improvements using SaaS infrastructure
exl-id: 747c0f3e-dfde-4365-812a-5ab7768342ab
source-git-commit: 92129633adadd3ed699ae6427c01622dcb6ae3b4
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Indicizzazione dei prezzi SaaS

L&#39;indicizzazione dei prezzi SaaS accelera il tempo necessario per riflettere le variazioni di prezzo [Servizi Commerce](../landing/saas.md) dopo che sono stati inviati. Questo consente ai commercianti con cataloghi complessi di grandi dimensioni o con più siti web o gruppi di clienti di elaborare continuamente le variazioni di prezzo.
Se hai una vetrina headless o utilizza [catalog-adapter](./catalog-adapter.md) I clienti possono disabilitare l’indicizzatore dei prezzi core di Adobe Commerce.

I processi computazionali pesanti come l’indicizzazione e il calcolo dei prezzi sono stati spostati dal core Commerce all’infrastruttura cloud di Adobe. Questo consente agli esercenti di aumentare rapidamente le risorse per accelerare i tempi di indicizzazione dei prezzi e riflettere tali cambiamenti più rapidamente.

Il flusso di dati di indicizzazione Core ai servizi SaaS è simile al seguente:

![Flusso di dati predefinito](assets/old_way.png)

Con l’indicizzazione dei prezzi SaaS, il flusso è:

![Flusso di dati di indicizzazione prezzi SaaS](assets/new_way.png)

Tutti i commercianti possono trarre vantaggio da questi miglioramenti, ma coloro che ne trarranno i maggiori vantaggi sono i clienti con:

* Variazioni di prezzo costanti: commercianti che richiedono modifiche ripetute ai prezzi per soddisfare obiettivi strategici quali promozioni frequenti, sconti stagionali o riduzioni di scorte.
* Più siti web e/o gruppi di clienti: commercianti con cataloghi di prodotti condivisi su più siti web (domini/marchi) e/o gruppi di clienti.
* Un numero elevato di prezzi univoci su siti web o gruppi di clienti: commercianti con cataloghi di prodotti condivisi e completi che contengono prezzi univoci su siti web o gruppi di clienti, ad esempio commercianti B2B con prezzi pre-negoziati, marchi con diverse strategie di prezzo.

L’indicizzazione dei prezzi SaaS è disponibile gratuitamente per i clienti che utilizzano i servizi Adobe Commerce e supporta il calcolo dei prezzi per tutti i tipi di prodotto Adobe Commerce incorporati.

Questa guida descrive come funziona l’indicizzazione dei prezzi SaaS e come abilitarla.

## Requisiti

* Adobe Commerce 2.4.4+
* Almeno uno dei seguenti servizi Commerce con la versione più recente dell’estensione Adobe Commerce:

   * [Servizio catalogo](../catalog-service/overview.md)
   * [Live Search](../live-search/guide-overview.md)

Gli utenti di Luma e Adobe Commerce Core GraphQL possono installare [`catalog-adapter`](catalog-adapter.md) estensione che fornisce compatibilità con Luma e Core GraphQl e disabilita l’indicizzatore del prezzo del prodotto di Adobe Commerce.

## Utilizzo

Dopo aver aggiornato l’istanza di Adobe Commerce con il supporto per l’indicizzazione dei prezzi SaaS, sincronizza i nuovi feed:

```bash
bin/magento saas:resync --feed=scopesCustomerGroup
bin/magento saas:resync --feed=scopesWebsite
bin/magento saas:resync --feed=prices
```

## Prezzi per tipi di prodotto personalizzati

I calcoli dei prezzi sono supportati per i tipi di prodotto personalizzati come prezzo di base, prezzo speciale, prezzo di gruppo, prezzo della regola di catalogo e così via.

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
