---
title: "Installa [!DNL Live Search]"
description: "Scopri come installare, aggiornare e disinstallare [!DNL Live Search] da Adobe Commerce."
exl-id: aa251bb0-d52c-4cff-bccb-76a08ae2a3b2
role: Admin, Developer
source-git-commit: 8a98e069cd9ec3d2c4fec33485e5c8186d94518f
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Installa [!DNL Live Search]

[!DNL Live Search] viene installato come estensione da Adobe Marketplace. Dopo il [!DNL Live Search] il modulo (con i moduli catalogo come dipendenze) sia installato e configurato, [!DNL Commerce] inizia a condividere i dati di ricerca e catalogo con i servizi SaaS. A questo punto *Amministratore* gli utenti possono impostare, personalizzare e gestire facet di ricerca, sinonimi e regole di merchandising.

In questo argomento vengono fornite istruzioni per eseguire le operazioni seguenti:

* Installa [!DNL Live Search] (Metodi 1 e 2)
* [Aggiorna [!DNL Live Search]](#update)
* [Disinstalla [!DNL Live Search]](#uninstall)

## Prima di iniziare {#before-you-begin}

Effettua le seguenti operazioni:

1. Conferma che [processi cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) e [indici](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) è in esecuzione.

1. Scegli il metodo di onboarding che soddisfa le tue esigenze e segui le istruzioni.

   * [Metodo 1](#method-1): installazione senza [!DNL OpenSearch]
   * [Metodo 2](#method-2): installazione con [!DNL OpenSearch] (nessun downtime)

>[!IMPORTANT]
>
>A causa dell’annuncio di fine del supporto di Elasticsearch 7 relativo ad agosto 2023, si consiglia a tutti i clienti di Adobe Commerce di migrare al motore di ricerca OpenSearch 2.x. Per informazioni sulla migrazione del motore di ricerca durante l’aggiornamento del prodotto, consulta [Migrazione a OpenSearch](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration) nel _Guida all’aggiornamento_.

## Metodo 1: installare senza OpenSearch {#method-1}

Questo metodo di onboarding è consigliato durante l’installazione [!DNL Live Search] a:

* Nuovo [!DNL Commerce] installazione
* Ambiente di staging

In questo scenario, le operazioni di storefront vengono interrotte mentre il [!DNL Live Search] service indicizza tutti i prodotti nel catalogo. Durante l&#39;installazione, [!DNL Live Search] i moduli sono abilitati e [!DNL OpenSearch] i moduli sono disattivati.

1. Installare Adobe Commerce 2.4.4+ senza [!DNL Live Search].

1. Per scaricare `live-search` , eseguire quanto segue dalla riga di comando:

   ```bash
   composer require magento/live-search
   ```

1. Esegui i seguenti comandi per disabilitare [!DNL OpenSearch] e moduli correlati, e installare [!DNL Live Search]:

   ```bash
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   ```bash
   bin/magento setup:upgrade
   ```

   >[!WARNING]
   >
   > Mentre i dati sono indicizzati e sincronizzati, le operazioni di ricerca e di ricerca per categoria non sono disponibili nella vetrina. A seconda delle dimensioni del catalogo, il processo può richiedere almeno un&#39;ora `cron` viene eseguito per sincronizzare i dati con [!DNL Live Search] servizi.

1. Verifica che [indici](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) sono impostati su &quot;Update by Schedule&quot; (Aggiorna per pianificazione):

   * Feed prodotto
   * Feed variante prodotto
   * Feed attributi catalogo
   * Feed prezzi prodotto
   * Feed dati del sito Web Ambiti
   * Scopi Feed dati di gruppi di clienti
   * Feed categorie
   * Feed di autorizzazioni categoria

1. Configurare [Chiavi API](#configure-api-keys) e verifica che i dati del catalogo siano [sincronizzato](#synchronize-catalog-data) con [!DNL Live Search] servizi.

1. Per rendere i facet disponibili come filtri nella vetrina, aggiungi [facet](facets-add.md) è necessario, in base al [requisiti di sfaccettatura](facets.md).

   Dovresti poter aggiungere i facet dopo `cron` esegue i feed di attributi ed esporta i metadati degli attributi.

1. Esegui il comando seguente in questo ordine:

   ```bash
   bin/magento saas:resync --feed productattributes
   bin/magento saas:resync --feed products
   bin/magento saas:resync --feed scopesCustomerGroup
   bin/magento saas:resync --feed scopesWebsite
   bin/magento saas:resync --feed prices
   bin/magento saas:resync --feed productoverrides
   bin/magento saas:resync --feed variants
   bin/magento saas:resync --feed categories
   bin/magento saas:resync --feed categoryPermissions
   ```

1. [Verifica](#verify-export) che i dati sono stati esportati.

1. [Test](#test-the-connection) la connessione dalla vetrina.

## Metodo 2: installare con OpenSearch {#method-2}

Questo metodo di onboarding è consigliato durante l’installazione [!DNL Live Search] a:

* Una produzione esistente [!DNL Commerce] installazione

In questo scenario, [!DNL OpenSearch] gestisce temporaneamente le richieste di ricerca dalla vetrina, mentre [!DNL Live Search] service indicizza tutti i prodotti in background, senza alcuna interruzione delle normali operazioni di storefront. [!DNL OpenSearch] è disabilitato e [!DNL Live Search] attivato dopo l&#39;indicizzazione e la sincronizzazione di tutti i dati del catalogo.

1. Per scaricare `live-search` , eseguire quanto segue dalla riga di comando:

   ```bash
   composer require magento/live-search
   ```

1. Esegui il comando seguente per disabilitare temporaneamente [!DNL Live Search] moduli che forniscono i risultati della ricerca della vetrina.

   ```bash
   bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing 
   ```

   ```bash
   bin/magento setup:upgrade
   ```

   [!DNL Elasticsearch] continua a gestire le richieste di ricerca dalla vetrina mentre [!DNL Live Search] il servizio sincronizza i dati del catalogo e indicizza i prodotti in background.

1. Verifica che [indici](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) sono impostati su &quot;Update by Schedule&quot; (Aggiorna per pianificazione):

   * Feed prodotto
   * Feed variante prodotto
   * Feed attributi catalogo
   * Feed prezzi prodotto
   * Feed dati del sito Web degli ambiti
   * Ambiti feed dati di gruppi di clienti

1. Configurare [Chiavi API](#configure-api-keys) e verifica che i dati del catalogo siano [sincronizzato](#synchronize-catalog-data) con [!DNL Live Search] servizi.

1. Per rendere i facet disponibili come filtri nella vetrina, aggiungi [facet](facets-add.md) è necessario, in base al [requisiti di sfaccettatura](facets.md).

   Dovresti poter aggiungere i facet dopo `cron` esegue il prodotto e i feed di attributi ed esporta i metadati di attributi in [!DNL Live Search] servizi.

1. Esegui il comando seguente in questo ordine:

   ```bash
   bin/magento saas:resync --feed productattributes
   bin/magento saas:resync --feed products
   bin/magento saas:resync --feed scopesCustomerGroup
   bin/magento saas:resync --feed scopesWebsite
   bin/magento saas:resync --feed prices
   bin/magento saas:resync --feed productoverrides
   bin/magento saas:resync --feed variants
   bin/magento saas:resync --feed categories
   bin/magento saas:resync --feed categoryPermissions
   ```

1. Al termine della sincronizzazione, utilizzare [Playground di GraphQL](https://developer.adobe.com/commerce/services/graphql/live-search/) con la query predefinita per verificare quanto segue:

   * Il conteggio dei prodotti restituito si avvicina a quello previsto per la visualizzazione Store.
   * Facet restituiti.

1. Esegui i seguenti comandi per abilitare [!DNL Live Search] moduli, disattiva [!DNL OpenSearch], ed eseguire `setup`.

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing 
   ```

   ```bash
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch 
   Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   ```bash
   bin/magento setup:upgrade
   ```

1. [Test](#test-the-connection) la connessione dalla vetrina.

## Configurare le chiavi API {#configure-api-keys}

Per connettersi sono necessarie la chiave API di Adobe Commerce e la chiave privata associata [!DNL Live Search] a un’installazione di Adobe Commerce. La chiave API viene generata e mantenuta nell’account della [!DNL Commerce] titolare della licenza, che può condividerla con lo sviluppatore o con il SI. Lo sviluppatore può quindi creare e gestire gli spazi dati SaaS per conto del titolare della licenza.  Se disponi già di un set di chiavi API, non è necessario rigenerarle.

### Titolare licenza Adobe Commerce

Per generare una chiave API e una chiave privata, consulta [Connettore Commerce Services](../landing/saas.md).

### Sviluppatore Adobe Commerce o SI

Lo sviluppatore o il SI configura lo spazio dati SaaS come descritto nella *Servizi Commerce* sezione della configurazione. In *Amministratore*, i servizi Commerce diventano disponibili nel *Configurazione* barra laterale quando è installato un modulo SaaS.

## Sincronizza dati catalogo {#synchronize-catalog-data}

[!DNL Live Search] richiede dati prodotto sincronizzati per le operazioni di ricerca e dati attributo sincronizzati per configurare i facet. La sincronizzazione iniziale tra il catalogo prodotti e il servizio catalogo inizia quando [!DNL Live Search] è il primo collegamento. A seconda del metodo di installazione e delle dimensioni del catalogo, l&#39;esportazione e l&#39;indicizzazione dei dati possono richiedere fino a 30 minuti [!DNL Live Search]. L’elenco dei dati sincronizzati e condivisi con il servizio catalogo si trova nello schema, definito in:

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

Utilizza il [Dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) per monitorare lo stato di sincronizzazione dei dati di prodotto trasferiti dal database Commerce ai servizi SaaS Commerce.

### Verifica esportazione {#verify-export}

Per verificare che i dati del catalogo siano stati esportati dalla tua istanza di Adobe Commerce e sincronizzati per [!DNL Live Search], cercare le voci nelle tabelle seguenti:

* `catalog_data_exporter_products`
* `catalog_data_exporter_product_attributes`

Per ulteriori informazioni, consulta [[!DNL Live Search] catalogo non sincronizzato](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) nella Knowledge Base di supporto.

### Aggiornamenti futuri del prodotto

Dopo la sincronizzazione iniziale, possono essere necessari fino a 15 minuti perché gli aggiornamenti incrementali dei prodotti siano disponibili per la ricerca nella vetrina. Per ulteriori informazioni, consulta [Indicizzazione - Aggiornamenti dei prodotti in streaming](indexing.md).

## Verifica la connessione {#test-connection}

Nella vetrina, verifica quanto segue:

* Il [!UICONTROL Search] La casella restituisce correttamente i risultati
* La ricerca delle categorie restituisce correttamente i risultati
* I facet sono disponibili come filtri nelle pagine dei risultati di ricerca

Se tutto funziona correttamente, congratulazioni! [!DNL Live Search] è installato, connesso e pronto all&#39;uso.

Se riscontri problemi nella vetrina, controlla `var/log/system.log` file per errori o errori di comunicazione API sul lato servizi.

Per consentire Live Search tramite un firewall, aggiungi `commerce.adobe.io` all&#39;elenco consentiti.

## Controllo della versione installata

Prima di aggiornare Live Search, esegui quanto segue dalla riga di comando per verificare la versione di Live Search installata:

```bash
composer show magento/module-live-search | grep version
```

## Aggiornamento [!DNL Live Search] {#update}

Da aggiornare [!DNL Live Search], esegui quanto segue dalla riga di comando:

```bash
composer update magento/live-search --with-dependencies
```

Per aggiornare a una versione principale, ad esempio da 3.1.1 a 4.0.0, modifica la directory principale del progetto [!DNL Composer] `.json` file come segue:

1. Se il programma di installazione `magento/live-search` versione è `3.1.1` o inferiore e si sta effettuando l&#39;aggiornamento alla versione `4.0.0` o versione successiva, eseguire il comando seguente prima dell&#39;aggiornamento:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   Per informazioni sul `magento/live-search` versione, esegui il seguente comando:

   ```bash
   composer show magento/live-search
   ```

1. Apri la directory principale `composer.json` file e ricerca `magento/live-search`.

1. In `require` , aggiorna il numero di versione come segue:

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. **Salva** `composer.json`. Quindi, esegui quanto segue dalla riga di comando:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## Disinstallazione [!DNL Live Search] {#uninstall}

Per disinstallare [!DNL Live Search], fare riferimento a [Disinstalla moduli](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules).

## [!DNL Live Search] pacchetti {#packages}

| Pacchetto | Descrizione |
|--- |--- |
| `module-live-search` | Consente ai commercianti di configurare le impostazioni di ricerca per faceting, sinonimi, regole di query e così via e fornisce l’accesso a un’area di riproduzione GraphQL di sola lettura per testare le query dal *Amministratore*. |
| `module-live-search-adapter` | Indirizza le richieste di ricerca dalla vetrina al [!DNL Live Search] ed esegue il rendering dei risultati nella vetrina. <br />- Navigazione tra categorie - Indirizza le richieste dalla vetrina [navigazione superiore](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top) al servizio di ricerca.<br />- Ricerca globale - Indirizza le richieste provenienti da [ricerca rapida](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) in alto a destra nella vetrina [!DNL Live Search] servizio. |
| `module-live-search-storefront-popover` | Un popover &quot;search as you type&quot; (cerca durante la digitazione) sostituisce la ricerca rapida standard e restituisce dati e miniature dei risultati di ricerca principali. |

## [!DNL Live Search] dipendenze {#dependencies}

I seguenti elementi [!DNL Live Search] le dipendenze vengono acquisite da [!DNL Composer].

* `magento/module-saas-catalog`
* `magento/module-saas-category`
* `magento/module-saas-category-permissions`
* `magento/module-saas-product-override`
* `magento/module-saas-product-variant`
* `magento/module-saas-price`
* `magento/module-saas-scopes`
* `magento/module-bundle-product-data-exporter`
* `magento/module-catalog-inventory-data-exporter`
* `magento/module-catalog-url-rewrite-data-exporter`
* `magento/module-configurable-product-data-exporter`
* `magento/module-parent-product-data-exporter`
* `magento/module-gift-card-product-data-exporter`
* `magento/module-bundle-product-override-data-exporter`
* `data-services`
* `services-id`
