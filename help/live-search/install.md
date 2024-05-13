---
title: "Introduzione a [!DNL Live Search]"
description: "Scopri i requisiti di sistema e i passaggi di installazione per [!DNL Live Search] da Adobe Commerce."
exl-id: aa251bb0-d52c-4cff-bccb-76a08ae2a3b2
role: Admin, Developer
source-git-commit: c66eab4ae0dda9a447a17f357ee0bb7364dc46ba
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 0%

---

# Configurazione per il successo con [!DNL Live Search]

Adobe Commerce [!DNL Live Search] e [[!DNL Catalog Service]](../catalog-service/guide-overview.md) lavorare insieme per fornire una soluzione di ricerca performante, pertinente e intuitiva che consenta ai clienti di trovare rapidamente ciò di cui hanno bisogno. In particolare, [!DNL Catalog Service] fa emergere i dati del catalogo per i servizi SaaS, ad esempio [!DNL Live Search] da utilizzare.

Questo articolo fornisce istruzioni dettagliate per l’implementazione di [!DNL Live Search] con [!DNL Catalog Service].

>[!IMPORTANT]
>
>Adobe Commerce offre diverse opzioni per la ricerca del sito. Assicurati di leggere [Limiti e limiti](boundaries-limits.md) prima dell&#39;implementazione, per garantire [!DNL Live Search] si adatta alle esigenze aziendali.

## Pubblico

Questo articolo è destinato agli sviluppatori o agli integratori di sistemi del team, responsabili dell’installazione e della configurazione dell’istanza di Adobe Commerce.

## Requisiti

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP 8,1 / 8,2 / 8,3
- [!DNL Composer]

## Piattaforme supportate

- Adobe Commerce on Cloud (ECE) : 2.4.4+
- Adobe Commerce on-prem (EE) : 2.4.4+

## Panoramica del flusso di lavoro

Ad alto livello, onboarding [!DNL Live Search] richiede di:

![Flusso di lavoro Live Search](assets/livesearch-workflow.png)

## 1. Installare [!DNL Live Search] estensione

[!DNL Live Search] è installato come estensione da [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html) da a [Compositore](https://getcomposer.org/). Dopo aver installato e configurato [!DNL Live Search], ADOBE [!DNL Commerce] inizia a condividere i dati di ricerca e catalogo con i servizi SaaS. A questo punto *Amministratore* gli utenti possono impostare, personalizzare e gestire facet di ricerca, sinonimi e regole di merchandising.

>[!NOTE]
>
>A partire da [!DNL Live Search] 3.0.2, il [!DNL Catalog Service] l&#39;estensione è inclusa con [!DNL Live Search] installazione.

1. Conferma che [processi cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) e [indici](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) è in esecuzione.

   >[!IMPORTANT]
   >
   >A causa dell’annuncio di fine del supporto di Elasticsearch 7 relativo ad agosto 2023, si consiglia a tutti i clienti di Adobe Commerce di migrare al motore di ricerca OpenSearch 2.x. Per informazioni sulla migrazione del motore di ricerca durante un aggiornamento del prodotto, consulta [Migrazione a OpenSearch](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration) nel _Guida all’aggiornamento_.

1. Scarica il file `live-search` pacchetto da [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html).

1. Esegui quanto segue dalla riga di comando:

   ```bash
   composer require magento/live-search
   ```

   Se stai aggiungendo [!DNL Live Search] estensione a un **nuovo** Installazione di Adobe Commerce, eseguire le operazioni seguenti per disattivare [!DNL OpenSearch] e moduli correlati, e installare [!DNL Live Search]. Procedere quindi al punto 4.

   ```bash
      bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   Se stai aggiungendo [!DNL Live Search] estensione a un **esistente** Installazione di Adobe Commerce, esegui quanto segue per disabilitare temporaneamente [!DNL Live Search] moduli che forniscono i risultati della ricerca della vetrina. Quindi procedere al punto 4:

   ```bash
      bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing 
   ```

   [!DNL Elasticsearch] continua a gestire le richieste di ricerca dalla vetrina mentre [!DNL Live Search] il servizio sincronizza i dati del catalogo e indicizza i prodotti in background.

1. Esegui quanto segue:

   ```bash
   bin/magento setup:upgrade
   ```

1. Verifica che [indici](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) sono impostati su &quot;Update by Schedule&quot; (Aggiorna per pianificazione):

   - Feed prodotto
   - Feed variante prodotto
   - Feed attributi catalogo
   - Feed prezzi prodotto
   - Feed dati del sito Web ambiti
   - Feed di dati dei gruppi di clienti per ambiti
   - Feed categorie
   - Feed di autorizzazioni categoria

1. Se si sta installando [!DNL Live Search] in una nuova istanza di Commerce, hai terminato e puoi passare al [2. Configurare le chiavi API](#2-configure-api-keys) sezione. Se stai installando Live Search in un’istanza Commerce esistente, procedi al passaggio successivo.

1. Esegui i seguenti comandi per abilitare [!DNL Live Search] estensione, disabilita [!DNL OpenSearch], ed eseguire `setup`.

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

## 2. Configurare le chiavi API

Per connettersi sono necessarie la chiave API di Adobe Commerce e la chiave privata associata [!DNL Live Search] a un’installazione di Adobe Commerce. La chiave API viene generata e mantenuta nell’account della [!DNL Commerce] titolare della licenza, che può condividerla con lo sviluppatore o con l’integratore di sistemi. Lo sviluppatore può quindi creare e gestire gli spazi dati SaaS per conto del titolare della licenza. Se disponi già di un set di chiavi API, non è necessario rigenerarle.

Scopri come configurare le chiavi API in [Connettore Commerce Services](../landing/saas.md) articolo.

## 3. Sincronizzare i dati del catalogo {#synchronize-catalog-data}

[!DNL Live Search] sposta i dati del catalogo nell’infrastruttura SaaS di Adobe. I dati vengono indicizzati e i risultati della ricerca vengono consegnati da questo indice direttamente alla vetrina. A seconda delle dimensioni e della complessità, l’indicizzazione può richiedere da 30 minuti a un paio d’ore.

Per avviare la sincronizzazione iniziale dei dati del catalogo con i servizi SaaS, eseguire i comandi seguenti nell&#39;ordine indicato:

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

Quando si eseguono questi comandi, inizia la sincronizzazione iniziale dei dati del catalogo con i servizi SaaS.

>[!WARNING]
>
> Mentre i dati sono indicizzati e sincronizzati, le operazioni di ricerca e di ricerca per categoria non sono disponibili nella vetrina. A seconda delle dimensioni del catalogo, il processo può richiedere almeno un&#39;ora `cron` viene eseguito per sincronizzare i dati con i servizi SaaS.

### Monitorare l’avanzamento della sincronizzazione

Puoi visualizzare i dati sincronizzati e condivisi utilizzando [Dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Questa dashboard fornisce informazioni utili sulla disponibilità di dati di prodotto per la vetrina, garantendo che possano essere visualizzati immediatamente agli acquirenti.

![Dashboard di gestione dati](assets/data-management-dashboard.png)

#### Aggiornamenti futuri del prodotto

Dopo la sincronizzazione iniziale, possono essere necessari fino a 15 minuti perché gli aggiornamenti incrementali dei prodotti siano disponibili per la ricerca nella vetrina. Per ulteriori informazioni, consulta [Indicizzazione - Aggiornamenti dei prodotti in streaming](indexing.md).

## 4. Verificare che i dati siano stati esportati {#verify-export}

Per verificare che i dati del catalogo siano stati esportati dalla tua istanza di Adobe Commerce e sincronizzati per [!DNL Live Search], sono disponibili due opzioni:

- Cercare le voci nelle tabelle seguenti:

   - `catalog_data_exporter_products`
   - `catalog_data_exporter_product_attributes`

- Utilizza il [Playground di GraphQL](https://developer.adobe.com/commerce/services/graphql/live-search/) con la query predefinita per verificare quanto segue:

   - Il conteggio dei prodotti restituito si avvicina a quello previsto per la visualizzazione Store.
   - Vengono restituiti i facet.

Per ulteriori informazioni, consulta [[!DNL Live Search] catalogo non sincronizzato](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) nella Knowledge Base di supporto.

## 5. Configurare i dati

La corretta configurazione dei dati di prodotto garantisce buoni risultati di ricerca per i clienti. In questa sezione, abiliti i widget per l’elenco dei prodotti e assegna categorie e attributi.

### Abilita widget elenco prodotti

Quando si installa [!DNL Live Search] 4.0.0+, i widget per l’elenco dei prodotti sono abilitati per impostazione predefinita. Quando i widget sono attivati, viene utilizzato un componente diverso dell’interfaccia utente per la pagina dei risultati della ricerca e per la pagina dell’elenco dei prodotti per la navigazione delle categorie. Questo componente dell’interfaccia utente effettua chiamate dirette al [API Catalog Service](https://developer.adobe.com/commerce/services/graphql/catalog-service/product-search/), che consente di velocizzare i tempi di risposta.

Se si dispone di [!DNL Live Search] versione precedente alla 4.0.0+, è necessario abilitare manualmente il widget dell’elenco dei prodotti.

1. Dalla sezione *Amministratore*, vai a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Sotto **[!UICONTROL Live Search]**, seleziona **[!UICONTROL Storefront Features]**.
1. Imposta **[!UICONTROL Enable Product Listing Widgets]** a `Yes`.

   ![Abilita widget elenco prodotti](assets/ls-admin-enable-widget.png)

Quando modifichi questa configurazione, il messaggio `Page cache is invalidated` viene visualizzato. Per salvare le modifiche, è necessario svuotare la cache del Magento.

1. Accedere a [Gestione cache](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management) eseguendo una delle operazioni seguenti:

   - Fai clic su **[!UICONTROL Cache Management]** nel messaggio sopra l’area di lavoro.
   - Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Cache Management]**.

1. Seleziona la **Configurazione** [!UICONTROL Cache Type] e fai clic su **[!UICONTROL Flush Magento Cache]**.

   Le modifiche alla vetrina vengono apportate subito dopo il flushing della cache.

### Assegna categorie

Prodotti restituiti in [!DNL Live Search] deve essere assegnato a un [categoria](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/categories). In Luma, ad esempio, i prodotti sono inseriti in categorie come &quot;Uomini&quot;, &quot;Donne&quot; e &quot;Attrezzi&quot;. Sono impostate anche delle sottocategorie per &quot;Tops&quot;, &quot;Bottoms&quot; e &quot;Watches&quot;. Questo consente una maggiore granularità durante il filtraggio.

### Campi ricercabili e filtrabili

I prodotti sono assegnati [attributi](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) che possono essere utilizzati per la ricerca e il filtraggio. Gli attributi sono ad esempio &quot;Colore&quot;, &quot;Dimensione&quot;, &quot;Tipo di materiale&quot;. Con questi attributi, gli utenti possono cercare &quot;green tops&quot;. Ogni prodotto può avere molti attributi definiti nel [!DNL Commerce] Amministratore

Ciascuno di questi attributi può essere definito come [&quot;ricercabile&quot;](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) in Admin. Se impostati come &quot;ricercabili&quot;, tali attributi sono disponibili per la ricerca [!DNL Live Search].

[Facet](facets.md) sono attributi di prodotto definiti in [!DNL Live Search] per essere filtrabile. Qualsiasi attributo filtrabile può essere impostato come facet in [!DNL Live Search] ma ci sono limiti al numero di facet che è possibile cercare contemporaneamente.

[Sinonimi](synonyms.md) sono termini che puoi definire per guidare gli utenti verso il prodotto corretto. Gli utenti alla ricerca di pantaloni potrebbero digitare &quot;pantaloni&quot; o &quot;pantaloni&quot;. È possibile impostare sinonimi in modo che questi termini di ricerca portino gli utenti ai risultati &quot;pantaloni&quot;.

## 6. Verificare la connessione {#test-connection}

Con i dati del catalogo ora in SaaS, verifica che i dati del prodotto vengano restituiti nei seguenti scenari:

- Il [!UICONTROL Search] La casella restituisce correttamente i risultati
- La ricerca delle categorie restituisce correttamente i risultati
- I facet sono disponibili come filtri nelle pagine dei risultati di ricerca

Se tutto funziona correttamente, [!DNL Live Search] è installato, connesso e pronto all&#39;uso.

Se riscontri problemi nella vetrina, controlla `var/log/system.log` file per errori o errori di comunicazione API sul lato servizi.

Per consentire [!DNL Live Search] tramite un firewall, aggiungi `commerce.adobe.io` al inserisco nell&#39;elenco Consentiti di.

## 7. Personalizza per la vetrina

È stato installato [!DNL Live Search] ha sincronizzato, convalidato e configurato i tuoi dati. A questo punto, è necessario assicurarsi che [!DNL Live Search] i widget si adattano all&#39;aspetto del tuo negozio.

Puoi assegnare uno stile ai widget popover e PLP definendo regole CSS personalizzate in base alle esigenze. Consulta [Elementi Popover Di Stile](storefront-popover-styling.md) e [Widget pagina elenco prodotti](plp-styling.md).

Se desideri estendere la funzionalità dei widget, il codice sorgente per ciascuno di essi è disponibile in un repository pubblico.
In questo scenario, puoi personalizzare il JavaScript in base alle tue esigenze e quindi ospitare il codice personalizzato sulla CDN. Questo script personalizzato comunica con [!DNL Live Search] e restituisce i risultati come normale, consentendoti di controllare la funzionalità del widget.

- [Repo widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Archivio barra di ricerca](https://github.com/adobe/storefront-search-as-you-type)

## Aggiornamento [!DNL Live Search] {#update}

Prima di aggiornare Live Search, esegui quanto segue dalla riga di comando per verificare la versione di Live Search installata:

```bash
composer show magento/module-live-search | grep version
```

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

1. Salva `composer.json`. Quindi, esegui quanto segue dalla riga di comando:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## Disinstallazione [!DNL Live Search] {#uninstall}

Per disinstallare [!DNL Live Search], fare riferimento a [Disinstalla moduli](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules).

## [!DNL Live Search] pacchetti {#packages}

Il [!DNL Live Search] l’estensione è costituita dai seguenti pacchetti:

| Pacchetto | Descrizione |
|--- |--- |
| `module-live-search` | Consente ai commercianti di configurare le impostazioni di ricerca per faceting, sinonimi, regole di query e così via e fornisce l’accesso a un’area di riproduzione GraphQL di sola lettura per testare le query dal *Amministratore*. |
| `module-live-search-adapter` | Indirizza le richieste di ricerca dalla vetrina al [!DNL Live Search] ed esegue il rendering dei risultati nella vetrina. <br />- Navigazione tra categorie - Indirizza le richieste dalla vetrina [navigazione superiore](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top) al servizio di ricerca.<br />- Ricerca globale - Indirizza le richieste provenienti da [ricerca rapida](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) in alto a destra nella vetrina [!DNL Live Search] servizio. |
| `module-live-search-storefront-popover` | Un popover &quot;search as you type&quot; (cerca durante la digitazione) sostituisce la ricerca rapida standard e restituisce dati e miniature dei risultati di ricerca principali. |

## [!DNL Live Search] dipendenze {#dependencies}

I seguenti elementi [!DNL Live Search] le dipendenze vengono acquisite da [!DNL Composer].

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## Concetti avanzati

Le sezioni seguenti forniscono argomenti più avanzati quando si utilizza [!DNL Live Search] e [!DNL Catalog Service].

### Endpoint

[!DNL Live Search] comunica attraverso l’endpoint in corrispondenza di `https://catalog-service.adobe.io/graphql`.

As [!DNL Live Search] non ha accesso alla banca dati completa dei prodotti, [!DNL Live Search] GraphQL e Commerce Core GraphQL non avranno parità completa.

Si consiglia di chiamare direttamente le API SaaS, in particolare l’endpoint Catalog Service.

- Migliorare le prestazioni e ridurre il carico del processore ignorando il database Commerce/processo Graphql
- Sfrutta i vantaggi [!DNL Catalog Service] federazione da chiamare [!DNL Live Search], [!DNL Catalog Service], e [!DNL Product Recommendations] da un singolo endpoint.

Per alcuni casi d’uso, potrebbe essere meglio chiamare [!DNL Catalog Service] per informazioni dettagliate sul prodotto e casi simili. Consulta [refineProduct](https://developer.adobe.com/commerce/services/graphql/catalog-service/refine-product/) per ulteriori informazioni.

Se disponi di un’implementazione headless personalizzata, vedi [!DNL Live Search] implementazioni di riferimento:

- [Widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Campo Live Search](https://github.com/adobe/storefront-search-as-you-type)

Se non utilizzi i componenti predefiniti, come Search Adapter o widget su Luma, o i widget CIF dell’AEM, gli eventi (dati di click-stream che alimentano Adobe Sensei per merchandising intelligente e metriche delle prestazioni) non funzioneranno immediatamente e richiederanno uno sviluppo personalizzato per implementare eventi headless.

Ultima versione di [!DNL Live Search] utilizza già [!DNL Catalog Service].

### Supporto linguistico

[!DNL Live Search] i widget supportano le seguenti lingue:

|  |  |  |  |
|--- |--- |--- |--- |
| Lingua | Regione | Codice lingua | Impostazioni locali Magento |
| Bulgaro | Bulgaria | bg_BG | bg_BG |
| Catalano | Spagna | ca_ES | ca_ES |
| Ceco | Repubblica Ceca | cs_CZ | cs_CZ |
| Danese | Danimarca | da_DK | da_DK |
| Tedesco | Germania | de_DE | de_DE |
| Greco | Grecia | el_GR | el_GR |
| Inglese | Regno Unito | en_GB | en_GB |
| Inglese | Stati Uniti | en_US | en_US |
| Spagnolo | Spagna | es_ES | es_ES |
| Estone | Estonia | et_EE | et_EE |
| Basco | Spagna | eu_ES | eu_ES |
| Persiano | Iran | fa_IR | fa_IR |
| Finlandese | Finlandia | fi_FI | fi_FI |
| Francese | Francia | fr_FR | fr_FR |
| Galiziano | Spagna | gl_ES | gl_ES |
| Hindi | India | hi_IN | hi_IN |
| Ungherese | Ungheria | hu_HU | hu_HU |
| Indonesiano | Indonesia | id_ID | id_ID |
| Italiano | Italia | it_IT | it_IT |
| Coreano | Corea del Sud | ko_KR | ko_KR |
| Lituano | Lituania | lt_LT | lt_LT |
| Lettone | Lettonia | lv_LV | lv_LV |
| Norvegese | Norvegia Bokmal | nb_NO | nb_NO |
| Olandese | Paesi Bassi | nl_NL | nl_NL |
| Polacco | Polonia | pl_PL | pl_PL |
| Portoghese | Brasile | pt_BR | pt_BR |
| Portoghese | Portogallo | pt_PT | pt_PT |
| Rumeno | Romania | ro_RO | ro_RO |
| Russo | Russia | ru_RU | ru_RU |
| Svedese | Svezia | sv_SE | sv_SE |
| Thailandese | Thailandia | th_TH | th_TH |
| Turco | Turchia | tr_TR | tr_TR |
| Cinese | Cina | zh_CN | zh_Hans_CN |
| Cinese | Taiwan | zh_TW | zh_Hant_TW |

Se il widget rileva che l&#39;impostazione della lingua di amministrazione di Commerce (_Negozi_ > Impostazioni > _Configurazione_ > _Generale_ > Country Options) corrisponde a una lingua supportata. Per impostazione predefinita è tale lingua. In caso contrario, per impostazione predefinita i widget sono inglesi.

Gli amministratori possono anche impostare la lingua [indice di ricerca](settings.md#language), per garantire risultati di ricerca migliori.

### Archivio del codice widget

I widget Pagina di elenco prodotti e Campo Live Search sono entrambi disponibili per il download dall’archivio GitHub.

Questo consente agli sviluppatori di personalizzare completamente la funzionalità e lo stile. Questi utenti ospitano il codice da soli, pur sfruttando [!DNL Live Search] servizio.

- [Widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Barra di ricerca](https://github.com/adobe/storefront-search-as-you-type)

### Inventory management

[!DNL Live Search] supporta [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) funzionalità in Commerce (noto in precedenza come MSI, Multi-Source Inventory). Per abilitare il supporto completo, è necessario [aggiorna](install.md#update) modulo di dipendenza `commerce-data-export` alla versione 102.2.0+.

[!DNL Live Search] restituisce un valore booleano che indica se un prodotto è disponibile in Inventory management, ma non contiene informazioni sull’origine del titolo.

### Indicizzatore prezzi

I clienti di Live Search possono utilizzare il nuovo [Indicizzatore prezzi SaaS](../price-index/price-indexing.md), che fornisce aggiornamenti più rapidi per la modifica del prezzo e tempi di sincronizzazione.

### Supporto del prezzo

I widget Live Search supportano la maggior parte dei tipi di prezzo supportati da Adobe Commerce, ma non tutti.

Attualmente sono sostenuti i prezzi di base. I prezzi avanzati non supportati sono:

- Costo
- Prezzo minimo annunciato

Osserva [Mesh API](../catalog-service/mesh.md) per calcoli dei prezzi più complessi.

Il formato del prezzo supporta l&#39;impostazione di configurazione delle impostazioni internazionali nell&#39;istanza di Commerce: *Negozi* > Impostazioni > *Configurazione* > Generale > *Generale* > Opzioni locali > Impostazioni internazionali.

### Supporto per vetrina headless

In alternativa, potrebbe essere necessario installare `module-data-services-graphql` modulo che espande la copertura GraphQL esistente dell’applicazione per includere i campi necessari per la raccolta di dati comportamentali storefront.

```bash
composer require magento/module-data-services-graphql
```

Questo modulo aggiunge contesti aggiuntivi alle query GraphQL:

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### Supporto PWA

[!DNL Live Search] funziona con PWA Studi, ma gli utenti potrebbero vedere lievi differenze rispetto ad altre implementazioni di Commerce. Le funzionalità di base, come la ricerca e la pagina di elenco dei prodotti, funzionano in Venia, ma alcune permutazioni di Graphql potrebbero non funzionare correttamente. Potrebbero esserci anche differenze di prestazioni.

- L’attuale implementazione PWA di [!DNL Live Search] richiede più tempo di elaborazione per restituire i risultati di ricerca di [!DNL Live Search] con la vetrina nativa di Commerce.
- [!DNL Live Search] in PWA non supporta [gestione degli eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). Di conseguenza, funzioneranno sia la generazione di rapporti di ricerca che il merchandising intelligente.
- Filtrare direttamente su `description`, `name`, `short_description` non è supportato da GraphQL se utilizzato con [PWA](https://developer.adobe.com/commerce/pwa-studio/), ma vengono restituiti con un filtro più generale.

Da utilizzare [!DNL Live Search] con PWA Studi, gli integratori devono anche:

1. Installa [livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
1. Imposta il `environmentId` nel `storeDetails` oggetto.

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### Cookie

[!DNL Live Search] raccoglie i dati di interazione dell’utente come parte della sua funzionalità di base e i cookie vengono utilizzati per memorizzare tali dati. Quando raccoglie informazioni sull’utente, quest’ultimo deve accettare di memorizzare i cookie. [!DNL Live Search] e [!DNL Product Recommendations] condividere il flusso di dati e quindi lo stesso meccanismo di cookie. Ulteriori informazioni sono disponibili in [Gestire le restrizioni dei cookie](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/developer/setting-cookie).
