---
title: '"Installazione [!DNL Live Search]"'
description: '"Scopri come installare, aggiornare e disinstallare [!DNL Live Search] da Adobe Commerce."'
exl-id: aa251bb0-d52c-4cff-bccb-76a08ae2a3b2
source-git-commit: bffbede99865e9085f60392e474065a454446370
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# Installa [!DNL Live Search]

Live Search è installato come estensione da Adobe Marketplace. Dopo la [!DNL Live Search] è installato e configurato il modulo (con moduli di catalogo come dipendenze), [!DNL Commerce] inizia a condividere i dati di ricerca e catalogo con i servizi SaaS. A questo punto, *Amministratore* gli utenti possono impostare, personalizzare e gestire facet di ricerca, sinonimi e regole di merchandising.

Questo argomento fornisce istruzioni su come effettuare le seguenti operazioni:

* Installa [!DNL Live Search] (Metodi 1 e 2)
* [Aggiorna [!DNL Live Search]](#update)
* [Disinstalla [!DNL Live Search]](#uninstall)

## Prima di iniziare {#before-you-begin}

Effettua le seguenti operazioni:

1. Conferma che [lavori cron](https://devdocs.magento.com/guides/v2.4/config-guide/cli/config-cli-subcommands-cron.html) e [indicizzatori](https://docs.magento.com/user-guide/system/index-management.html) stanno correndo.

1. Scegli il metodo di onboarding che soddisfa le tue esigenze e segui le istruzioni.

   * [Metodo 1](#method-1): Installazione senza [!DNL Elasticsearch]
   * [Metodo 2](#method-2): Installa con [!DNL Elasticsearch] (Nessun tempo di inattività)

## Metodo 1: Installazione senza Elasticsearch {#method-1}

Questo metodo di onboarding è consigliato durante l&#39;installazione [!DNL Live Search] a:

* Nuovo [!DNL Commerce] installazione
* Ambiente di staging

In questo scenario, le operazioni di vetrina vengono interrotte mentre il [!DNL Live Search] il servizio indicizza tutti i prodotti del catalogo. Durante l&#39;installazione, [!DNL Live Search] i moduli sono abilitati e [!DNL Elasticsearch] i moduli sono disabilitati.

>[!TIP]
>
>Per evitare errori di digitazione, passa il cursore del mouse sull&#39;estrema destra della casella di codice e fai clic sul pulsante [!UICONTROL **Copia**] e incollarlo nella riga di comando.

1. Installa Adobe Commerce 2.4.x senza [!DNL Live Search].

1. Per scaricare i `live-search` esegui quanto segue dalla riga di comando:

   ```bash
   composer require magento/live-search
   ```

   Per ulteriori informazioni, consulta l’elenco di [!DNL Live Search] [dipendenze](#dependencies) catturati da [!DNL Composer].

1. Esegui i seguenti comandi per disabilitare [!DNL Elasticsearch] e i relativi moduli, e installare [!DNL Live Search]:

   ```bash
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch 
   Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   ```bash
   bin/magento setup:upgrade
   ```

   >[!WARNING]
   >
   > Mentre i dati sono indicizzati e sincronizzati, le operazioni di ricerca e ricerca per categorie non sono disponibili nella vetrina. A seconda delle dimensioni del catalogo, il processo può richiedere almeno un&#39;ora dal `cron` esegue per sincronizzare i dati con [!DNL Live Search] servizi.

1. Verifica quanto segue [indicizzatori](https://docs.magento.com/user-guide/system/index-management.html) sono impostati su `Update by Schedule`:

   * Feed di prodotto
   * Feed variante di prodotto
   * Feed attributi del catalogo

1. Configura le [Chiavi API](#configure-api-keys) e verifica che i dati del catalogo siano [sincronizzato](#synchronize-catalog-data) con [!DNL Live Search] servizi.

1. Per rendere i facet disponibili come filtri nella vetrina, aggiungi [facet](facets-add.md) è necessario, secondo il [requisiti](facets.md).

   Dovresti essere in grado di aggiungere facet dopo `cron` esegue i feed degli attributi ed esporta i metadati degli attributi.

1. Attendi almeno un&#39;ora dopo `cron` esegue per sincronizzare i dati. Allora, [verify](#verify-export) che i dati sono stati esportati.

1. [Test](#test-the-connection) la connessione dalla vetrina.

## Metodo 2: Installa con Elasticsearch {#method-2}

Questo metodo di onboarding è consigliato durante l&#39;installazione [!DNL Live Search] a:

* Una produzione esistente [!DNL Commerce] installazione

In questo scenario, [!DNL Elasticsearch] gestisce temporaneamente le richieste di ricerca dalla vetrina mentre il [!DNL Live Search] il servizio indicizza tutti i prodotti in background, senza interruzioni alle normali operazioni di vetrina. [!DNL Elasticsearch] è disabilitato e [!DNL Live Search] abilitati dopo che tutti i dati del catalogo sono indicizzati e sincronizzati.

>[!TIP]
>
>Per evitare errori di digitazione, passa il cursore del mouse sull&#39;estrema destra della casella di codice e fai clic sul pulsante [!UICONTROL **Copia**] e incollarlo nella riga di comando.

1. Per scaricare i `live-search` esegui quanto segue dalla riga di comando:

   ```bash
   composer require magento/live-search
   ```

   Per ulteriori informazioni, consulta l’elenco di [!DNL Live Search] [dipendenze](#live-search-dependencies) catturati da [!DNL Composer].

1. Esegui il comando seguente per disattivare temporaneamente il [!DNL Live Search] moduli che distribuiscono i risultati della ricerca in vetrina.

   ```bash
   bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover
   ```

   ```bash
   bin/magento setup:upgrade
   ```

   [!DNL Elasticsearch] continua a gestire le richieste di ricerca dalla vetrina mentre il [!DNL Live Search] sincronizza i dati del catalogo e indicizza i prodotti in background.

1. Verifica quanto segue [indicizzatori](https://docs.magento.com/user-guide/system/index-management.html) sono impostati su `Update by Schedule`:

   * Feed di prodotto
   * Feed variante di prodotto
   * Feed attributi del catalogo

1. Configura le [Chiavi API](#configure-api-keys) e verifica che i dati del catalogo siano [sincronizzato](#synchronize-catalog-data) con [!DNL Live Search] servizi.

1. Per rendere i facet disponibili come filtri nella vetrina, aggiungi [facet](facets-add.md) è necessario, secondo il [requisiti](facets.md).

   Dovresti essere in grado di aggiungere facet dopo `cron` esegue i feed di prodotto e attributo ed esporta i metadati degli attributi in [!DNL Live Search] servizi.

1. Attendi almeno un’ora per l’indicizzazione e la sincronizzazione dei dati. Quindi, utilizza il [Campo giochi GraphQL](https://devdocs.magento.com/live-search/graphql-support.html) con la query predefinita per verificare quanto segue:

   * Il conteggio dei prodotti restituito è simile a quello previsto per la visualizzazione store.
   * I facet vengono restituiti.

1. Esegui i seguenti comandi per abilitare [!DNL Live Search] moduli, disattiva [!DNL Elasticsearch]ed esegui `setup`.

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover
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

Per connettersi è necessaria la chiave API di Adobe Commerce e la relativa chiave privata associata [!DNL Live Search] a un’installazione di Adobe Commerce. La chiave API viene generata e mantenuta nell’account della [!DNL Commerce] titolare della licenza, che può condividerlo con lo sviluppatore o con SI. Lo sviluppatore può quindi creare e gestire gli spazi dati SaaS per conto del titolare della licenza.  Se disponi già di un set di chiavi API, non è necessario rigenerarle.

### Titolare della licenza Adobe Commerce

Per generare una chiave API e una chiave privata, fai riferimento a [Connettore Commerce Services](../landing/saas.md).

### Sviluppatore Adobe Commerce o SI

Lo sviluppatore o l’SI configura lo spazio dati SaaS come descritto nel *Commerce Services* della configurazione. In *Amministratore*, Commerce Services diventa disponibile in *Configurazione* barra laterale quando è installato un modulo SaaS.

## Sincronizzazione dei dati del catalogo {#synchronize-catalog-data}

[!DNL Live Search] richiede dati di prodotto sincronizzati per le operazioni di ricerca e dati di attributi sincronizzati per configurare i facet. La sincronizzazione iniziale tra il catalogo dei prodotti e il servizio catalogo inizia quando [!DNL Live Search] è collegato per la prima volta. A seconda del metodo di installazione e delle dimensioni del catalogo, possono essere necessarie fino a otto ore per l’esportazione e l’indicizzazione dei dati da parte di [!DNL Live Search]. L’elenco dei dati sincronizzati e condivisi con il servizio catalogo si trova nello schema, definito in:

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

### Verifica esportazione {#verify-export}

Per verificare che i dati del catalogo siano stati esportati dall’istanza di Adobe Commerce e siano sincronizzati per [!DNL Live Search], cerca le voci nelle tabelle seguenti:

* `catalog_data_exporter_products`
* `catalog_data_exporter_product_attributes`

Per ulteriore assistenza, consulta [[!DNL Live Search] catalogo non sincronizzato](https://support.magento.com/hc/en-us/articles/4405637804301-Live-search-catalog-not-synchronized) nella Knowledge Base del supporto.

### Aggiornamenti futuri dei prodotti

Dopo la sincronizzazione iniziale, possono essere necessari fino a quindici minuti perché gli aggiornamenti incrementali dei prodotti siano disponibili per la ricerca in vetrina. Per ulteriori informazioni, vai a [Indicizzazione - Aggiornamenti dei prodotti in streaming](indexing.md).

## Verificare la connessione {#test-connection}

Nella vetrina, verifica quanto segue:

* La [!UICONTROL Search] box restituisce correttamente i risultati
* Il browser delle categorie restituisce correttamente i risultati
* I facet sono disponibili come filtri nelle pagine dei risultati di ricerca

Se tutto funziona correttamente, congratulazioni! [!DNL Live Search] è installato, collegato e pronto per l&#39;uso.

Se riscontri problemi nella vetrina, controlla la `var/log/system.log` per errori o errori di comunicazione API sul lato servizi.

## Controllo della versione installata

Prima di aggiornare Live Search, esegui quanto segue dalla riga di comando per controllare la versione di Live Search attualmente installata:

```bash
composer show magento/module-live-search | grep version
```

## Aggiornamento [!DNL Live Search] {#update}

Per aggiornare [!DNL Live Search], esegui quanto segue dalla riga di comando:

```bash
composer update magento/live-search --with-dependencies
```

Per eseguire l’aggiornamento a una versione principale, ad esempio da 1.0.0 a 2.0.0, modifica la directory principale del progetto [!DNL Composer] `.json` file come segue:

1. Se è installato `magento/live-search` versione `1.3.1` o versioni successive e stai effettuando l&#39;aggiornamento alla versione `2.0.0` o superiore, esegui il seguente comando prima dell&#39;aggiornamento:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   Per informazioni sull&#39;installazione corrente `magento/live-search` version, esegui il seguente comando:

   ```bash
   composer show magento/live-search
   ```

1. Apri la radice `composer.json` file e cerca `magento/live-search`.

1. In `require` aggiorna il numero di versione come segue:

   ```json
   "require": {
      ...
      "magento/live-search": "^2.0",
      ...
    }
   ```

1. **Salva** `composer.json`. Esegui quindi quanto segue dalla riga di comando:

   ```bash
   composer update magento/live-search –-with-dependencies
   ```

## Disinstallazione [!DNL Live Search] {#uninstall}

Per disinstallare [!DNL Live Search], fare riferimento a [Disinstallare i moduli](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-uninstall-mods.html).

## [!DNL Live Search] pacchetti {#packages}

| Pacchetto | Descrizione |
|--- |--- |
| `module-live-search` | Consente agli esercenti di configurare le impostazioni di ricerca per faceting, sinonimi, regole di query, ecc. e fornisce l’accesso a un parco giochi GraphQL di sola lettura per testare le query da *Amministratore*. |
| `module-live-search-adapter` | Invia richieste di ricerca dalla vetrina al [!DNL Live Search] ed esegue il rendering dei risultati nella vetrina. <br />- Navigazione tra categorie - Routes richieste dalla vetrina [navigazione superiore](https://docs.magento.com/user-guide/catalog/navigation-top.html) al servizio di ricerca.<br />- Ricerca globale - Richieste di percorsi da [ricerca rapida](https://docs.magento.com/user-guide/catalog/search-quick.html) in alto a destra della vetrina [!DNL Live Search] servizio. |
| `module-live-search-storefront-popover` | Il puntatore &quot;Ricerca durante la digitazione&quot; sostituisce la ricerca rapida standard e restituisce suggerimenti di prodotto dinamici e miniature dei risultati di ricerca principali. |

## [!DNL Live Search] dipendenze {#dependencies}

I seguenti [!DNL Live Search] le dipendenze vengono acquisite da [!DNL Composer]:

| Dipendenza | Descrizione |
|--- |--- |
| Moduli di esportazione | I seguenti moduli raccolgono e sincronizzano i dati del catalogo:<br />`saas-export`<br />`module-bundle-product-exporter`<br />`module-catalog-data-exporter`<br />`module-catalog-inventory-data-exporter`<br />`module-catalog-url-rewrite-data-exporter`<br />`module-configurable-product-data-exporter`<br />`module-data-exporter`<br />`module-parent-product-data-exporter` |
| `services-connector` | Obbligatorio per configurare la connessione a Commerce Services. |
| `module-services-id` | Obbligatorio per configurare la connessione a Commerce Services. |
