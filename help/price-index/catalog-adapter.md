---
title: Estensione scheda catalogo
description: Utilizzo di Catalog Adapter per il rendering dei prezzi da Commerce Services
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
exl-id: 2c9120eb-aa51-48e9-b6a4-fffe25fc31f2
source-git-commit: 8230756c203cb2b4bdb4949f116c398fcaab84ff
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# Adattatore catalogo

Il `[!DNL Catalog Adapter]` L&#39;estensione disabilita l&#39;indicizzatore predefinito dei prezzi del prodotto incluso nell&#39;applicazione Commerce e utilizza i prezzi forniti dall&#39;estensione [Servizio catalogo](../catalog-service/overview.md) invece.

L&#39;adattatore è progettato per l&#39;utilizzo con [Esportazione dati SaaS](../data-export/overview.md) e il servizio Adobe Commerce. L&#39;esportazione dei dati SaaS è responsabile della presentazione dei prezzi, [!DNL Catalog Adapter] recupera tutti i prezzi dal servizio Adobe Commerce.

Quando si abilita [!DNL Catalog Adapter], l’indicizzazione dei prezzi e le operazioni sono influenzate nei seguenti modi:

- L’indicizzatore prezzi incluso nell’applicazione Adobe Commerce è disabilitato.
- I prezzi vengono gestiti mediante l&#39;esportazione di dati SaaS e [Indicizzatore prezzi SaaS](price-indexing.md).
- Quando un cliente apre un prodotto, una categoria o un’altra pagina che mostra i prezzi dei prodotti, questi vengono recuperati dal servizio Adobe Commerce.
- I prezzi vengono inviati al servizio Adobe Commerce sincronizzando i dati dal [Esportazione dati SaaS](../data-export/overview.md).
- Il Checkout ricalcola i prezzi in modo dinamico.

È possibile riabilitare l&#39;indicizzazione dei prezzi nell&#39;applicazione Commerce rimuovendo o disabilitando l&#39;estensione Catalog Adapter.

## Requisiti

- Adobe Commerce 2.4.4+
- Installare uno dei seguenti servizi Commerce:

   - [Live Search](../live-search/install.md)
   - [Recommendations del prodotto](../product-recommendations/install-configure.md)
   - [Servizio catalogo](../catalog-service/installation.md)

## Installazione

L&#39;estensione Catalog Adapter è un metapacchetto Compositore che installa i seguenti moduli:

- **Disattivazione indicizzatore prezzi**-Questo modulo disattiva l&#39;indice dei prezzi nell&#39;applicazione Commerce in modo che i prezzi vengano distribuiti tramite l&#39;indicizzazione dei prezzi SaaS. Impossibile attivare l&#39;indicizzatore prezzi prodotto nell&#39;applicazione Commerce quando è installata l&#39;estensione per l&#39;indicizzazione prezzi SaaS.
- **Provider prezzi**-Questo modulo fornisce i prezzi per i prodotti del servizio Adobe Commerce. Crea la query di ricerca e ottiene i prezzi per i prodotti sul front-end.
- **Adattatore ricerca servizio catalogo**-Questo modulo trasferisce i prezzi dall’applicazione Adobe Commerce a un servizio Adobe Commerce in risposta a una richiesta di ricerca di prodotti.

## Passaggi per l’installazione

>[!BEGINTABS]

>[!TAB Infrastruttura cloud]

Utilizzare questo metodo per installare [!DNL Catalog Adapter] per un’istanza Commerce Cloud.

1. Sulla workstation locale, passa alla directory del progetto per il progetto Adobe Commerce su infrastruttura cloud.

   >[!NOTE]
   >
   >Per informazioni sulla gestione locale degli ambienti di progetto Commerce, vedi [Gestione dei rami con CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) nel _Guida utente di Adobe Commerce su infrastruttura cloud_.

1. Consulta il ramo dell’ambiente da aggiornare utilizzando Adobe Commerce Cloud CLI.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Aggiungere il modulo adattatore catalogo.

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Aggiornare le dipendenze del pacchetto.

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. Modifiche al codice di commit e push per `composer.json` e `composer.lock` file.

1. Aggiungi, esegui il commit e invia le modifiche al codice per `composer.json` e `composer.lock` nell&#39;ambiente cloud.

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   Inviando gli aggiornamenti all’ambiente cloud si avvia [Processo di distribuzione cloud Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) per applicare le modifiche. Controlla lo stato della distribuzione da [registro di distribuzione](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB On-premise]

Utilizzare questo metodo per installare [!DNL Catalog Adapter] per un’istanza on-premise.

1. Aggiungi l&#39;adattatore catalogo al progetto utilizzando il Compositore:

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update  "magento/catalog-adapter"
   ```

1. Aggiorna Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Cancella la cache:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >In alcuni casi, in particolare durante la distribuzione in produzione, potrebbe essere opportuno evitare di cancellare il codice compilato perché potrebbe richiedere del tempo. Prima di apportare qualsiasi modifica, assicurati di eseguire il backup del sistema.

>[!ENDTABS]


## Riattiva l’indicizzatore dei prezzi del prodotto Adobe Commerce

Se esistono applicazioni di terze parti che si basano sull’indicizzatore prezzi del prodotto Adobe Commerce predefinito, puoi abilitarlo nuovamente con i seguenti comandi:

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## Disattiva l&#39;indicizzatore del prezzo del prodotto per lo scenario Headless Storefront

Se disponi di un’istanza Commerce headless, potresti dover disabilitare l’indicizzatore dei prezzi del prodotto Adobe Commerce per ridurre il carico sull’istanza Adobe Commerce. Per completare questa attività, installa `magento/module-price-indexer-disabler` modulo:

```bash
composer require magento/module-price-indexer-disabler
```

## Scenari di utilizzo

Di seguito sono riportati alcuni esempi comuni `[!DNL Catalog Adapter]` scenari.

### Nessuna dipendenza dall’indicizzatore dei prezzi dei prodotti Adobe Commerce

- Sei un commerciante Luma o Adobe Commerce Core GraphQL con installato un servizio richiesto (Live Search, Product Recommendations, Catalog Service)
- Nessuna integrazione con estensioni di terze parti basate sull’indicizzatore dei prezzi del prodotto di Adobe Commerce

1. Installare [!DNL Catalog Adapter].

### Con dipendenze dall’indicizzatore dei prezzi dei prodotti Adobe Commerce

- Sei un commerciante Luma o Adobe Commerce Core GraphQL con installato un servizio supportato (Live Search, Product Recommendations, Catalog Service)
- Puoi utilizzare un’estensione di terze parti basata sull’indicizzatore dei prezzi del prodotto Adobe Commerce

1. Installare [!DNL Catalog Adapter].
1. Abilita nuovamente l’indicizzatore prezzi prodotto Adobe Commerce predefinito.

### Istanze Commerce headless

- Un commerciante con un’istanza Commerce headless con i servizi richiesti installati (Live Search, Product Recommendations, Catalog Service)
- Nessuna dipendenza dall&#39;indicizzatore prezzi prodotto Adobe Commerce predefinito

1. Installare `magento/module-price-indexer-disabler` modulo da [!DNL Catalog Adapter] pacchetto.

