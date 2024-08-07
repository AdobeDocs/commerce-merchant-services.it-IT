---
title: "Introduzione a  [!DNL Live Search]"
description: "Scopri i requisiti di sistema e i passaggi di installazione per  [!DNL Live Search]  da Adobe Commerce."
exl-id: aa251bb0-d52c-4cff-bccb-76a08ae2a3b2
role: Admin, Developer
source-git-commit: 0b0bc88c13d8c90a6209d9156f6fd6a7ce040f72
workflow-type: tm+mt
source-wordcount: '2357'
ht-degree: 0%

---

# Configurazione per il successo con [!DNL Live Search]

Adobe Commerce [!DNL Live Search] e [[!DNL Catalog Service]](../catalog-service/guide-overview.md) collaborano per fornire una soluzione di ricerca efficiente, pertinente e intuitiva che consenta ai clienti di trovare rapidamente ciò di cui hanno bisogno. In particolare, [!DNL Catalog Service] fa emergere i dati del catalogo per i servizi SaaS, ad esempio [!DNL Live Search] da utilizzare.

Questo articolo fornisce istruzioni dettagliate per l&#39;implementazione di [!DNL Live Search] con [!DNL Catalog Service].

>[!IMPORTANT]
>
>Adobe Commerce offre diverse opzioni per la ricerca del sito. Assicurati di leggere [Limiti e limiti](boundaries-limits.md) prima di implementare, per assicurarti che [!DNL Live Search] sia adatto alle tue esigenze aziendali.

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

A un livello avanzato, l&#39;onboarding di [!DNL Live Search] richiede:

![Flusso di lavoro di Live Search](assets/livesearch-workflow.png)

## 1. Installare l&#39;estensione [!DNL Live Search]

[!DNL Live Search] è installato come estensione da [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html) a [Composer](https://getcomposer.org/). Dopo aver installato e configurato [!DNL Live Search], l&#39;Adobe [!DNL Commerce] inizia a condividere i dati di ricerca e catalogo con i servizi SaaS. A questo punto, *Amministratore* utenti possono impostare, personalizzare e gestire facet di ricerca, sinonimi e regole di merchandising.

>[!NOTE]
>
>A partire dalla versione 3.0.2 di [!DNL Live Search], l&#39;estensione [!DNL Catalog Service] è inclusa nell&#39;installazione di [!DNL Live Search].

1. Verificare che [processi cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) e [indicizzatori](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) siano in esecuzione.

   >[!IMPORTANT]
   >
   >A causa dell’annuncio di fine del supporto di Elasticsearch 7 relativo ad agosto 2023, si consiglia a tutti i clienti di Adobe Commerce di migrare al motore di ricerca OpenSearch 2.x. Per informazioni sulla migrazione del motore di ricerca durante un aggiornamento del prodotto, vedere [Migrazione a OpenSearch](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration) nella _Guida all&#39;aggiornamento_.

1. Scarica il pacchetto `live-search` da [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html).

1. Esegui quanto segue dalla riga di comando:

   ```bash
   composer require magento/live-search
   ```

   Se si aggiunge l&#39;estensione [!DNL Live Search] a un&#39;installazione di Adobe Commerce **new**, eseguire le operazioni seguenti per disabilitare [!DNL OpenSearch] e i moduli correlati e installare [!DNL Live Search]. Procedere quindi al punto 4.

   ```bash
      bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   Se stai aggiungendo l&#39;estensione [!DNL Live Search] a un&#39;installazione di Adobe Commerce **esistente**, esegui la procedura seguente per disabilitare temporaneamente i moduli [!DNL Live Search] che forniscono i risultati della ricerca della vetrina. Quindi procedere al punto 4:

   ```bash
      bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing 
   ```

   [!DNL Elasticsearch] continua a gestire le richieste di ricerca dalla vetrina mentre il servizio [!DNL Live Search] sincronizza i dati del catalogo e indicizza i prodotti in background.

1. Esegui quanto segue:

   ```bash
   bin/magento setup:upgrade
   ```

1. Verificare che i seguenti [indicizzatori](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) siano impostati su &quot;Aggiorna in base alla pianificazione&quot;:

   - Feed prodotto
   - Feed variante prodotto
   - Feed attributi catalogo
   - Feed prezzi prodotto
   - Feed dati del sito Web ambiti
   - Feed di dati dei gruppi di clienti per ambiti
   - Feed categorie
   - Feed di autorizzazioni categoria

1. Se stai installando [!DNL Live Search] in una nuova istanza di Commerce, l&#39;operazione è terminata e puoi passare a [2. Configurare la sezione delle chiavi API](#2-configure-api-keys). Se stai installando Live Search in un’istanza Commerce esistente, procedi al passaggio successivo.

1. Eseguire i seguenti comandi per abilitare l&#39;estensione [!DNL Live Search], disabilitare [!DNL OpenSearch] ed eseguire `setup`.

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

Per connettere [!DNL Live Search] a un&#39;installazione di Adobe Commerce sono necessari la chiave API di Adobe Commerce e la chiave privata associata. La chiave API viene generata e mantenuta nell&#39;account del titolare della licenza [!DNL Commerce], che può condividerla con lo sviluppatore o l&#39;integratore di sistemi. Lo sviluppatore può quindi creare e gestire gli spazi dati SaaS per conto del titolare della licenza. Se disponi già di un set di chiavi API, non è necessario rigenerarle.

Scopri come configurare le chiavi API nell’articolo [Commerce Services Connector](../landing/saas.md).

## 3. Sincronizzare i dati del catalogo {#synchronize-catalog-data}

[!DNL Live Search] sposta i dati del catalogo nell&#39;infrastruttura SaaS di Adobe. I dati vengono indicizzati e i risultati della ricerca vengono consegnati da questo indice direttamente alla vetrina. A seconda delle dimensioni e della complessità, l’indicizzazione può richiedere da 30 minuti a un paio d’ore.

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
> Mentre i dati sono indicizzati e sincronizzati, le operazioni di ricerca e di ricerca per categoria non sono disponibili nella vetrina. A seconda delle dimensioni del catalogo, il processo può richiedere almeno un&#39;ora dal momento in cui `cron` viene eseguito per sincronizzare i dati con i servizi SaaS.

### Monitorare l’avanzamento della sincronizzazione

Puoi visualizzare i dati sincronizzati e condivisi utilizzando [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Questa dashboard fornisce informazioni utili sulla disponibilità di dati di prodotto per la vetrina, garantendo che possano essere visualizzati immediatamente agli acquirenti.

![Dashboard di gestione dati](assets/data-management-dashboard.png)

È inoltre possibile eseguire i comandi di sincronizzazione e risolvere i problemi relativi al processo di sincronizzazione utilizzando [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) e i registri delle estensioni di esportazione dei dati.

#### Aggiornamenti futuri del prodotto

Dopo la sincronizzazione iniziale, possono essere necessari fino a 15 minuti perché gli aggiornamenti incrementali dei prodotti siano disponibili per la ricerca nella vetrina. Per ulteriori informazioni, consulta [Indicizzazione - Aggiornamenti del prodotto in streaming](indexing.md).

## 4. Verificare che i dati siano stati esportati {#verify-export}

Per verificare che i dati del catalogo siano stati esportati dall&#39;istanza Adobe Commerce e sincronizzati per [!DNL Live Search], sono disponibili due opzioni:

- Cercare le voci nelle tabelle seguenti:

   - `catalog_data_exporter_products`
   - `catalog_data_exporter_product_attributes`

- Utilizza il [parco giochi GraphQL](https://developer.adobe.com/commerce/services/graphql/live-search/) con la query predefinita per verificare quanto segue:

   - Il conteggio dei prodotti restituito si avvicina a quello previsto per la visualizzazione Store.
   - Vengono restituiti i facet.

Per ulteriori informazioni, vedere [[!DNL Live Search] catalogo non sincronizzato](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) nella Knowledge Base del supporto tecnico.

## 5. Configurare i dati

La corretta configurazione dei dati di prodotto garantisce buoni risultati di ricerca per i clienti. In questa sezione, abiliti i widget per l’elenco dei prodotti e assegna le categorie.

### Abilita widget elenco prodotti

Quando si installa [!DNL Live Search] 4.0.0+, i widget dell&#39;elenco prodotti sono abilitati per impostazione predefinita. Quando i widget sono attivati, viene utilizzato un componente diverso dell’interfaccia utente per la pagina dei risultati della ricerca e per la pagina dell’elenco dei prodotti per la navigazione delle categorie. Questo componente dell&#39;interfaccia utente effettua chiamate dirette all&#39;[API Catalog Service](https://developer.adobe.com/commerce/services/graphql/catalog-service/product-search/), il che si traduce in tempi di risposta più rapidi.

Se hai una versione di [!DNL Live Search] precedente alla 4.0.0+, devi abilitare manualmente il widget dell&#39;elenco di prodotti.

1. Da *Amministratore*, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. In **[!UICONTROL Live Search]**, selezionare **[!UICONTROL Storefront Features]**.
1. Imposta **[!UICONTROL Enable Product Listing Widgets]** su `Yes`.

   ![Abilita widget elenco prodotti](assets/ls-admin-enable-widget.png)

Quando si modifica questa configurazione, viene visualizzato il messaggio `Page cache is invalidated`. Per salvare le modifiche, è necessario svuotare la cache del Magento.

1. Accedere alla pagina [Gestione cache](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management) effettuando una delle operazioni seguenti:

   - Fare clic sul collegamento **[!UICONTROL Cache Management]** nel messaggio sopra l&#39;area di lavoro.
   - Nella barra laterale _Admin_, passa a **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Cache Management]**.

1. Selezionare la **configurazione** [!UICONTROL Cache Type] e fare clic su **[!UICONTROL Flush Magento Cache]**.

   Le modifiche alla vetrina vengono apportate subito dopo il flushing della cache.

### Assegna categorie

I prodotti restituiti in [!DNL Live Search] devono essere assegnati a una [categoria](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/categories). In Luma, ad esempio, i prodotti sono inseriti in categorie come &quot;Uomini&quot;, &quot;Donne&quot; e &quot;Attrezzi&quot;. Sono impostate anche delle sottocategorie per &quot;Tops&quot;, &quot;Bottoms&quot; e &quot;Watches&quot;. Questo consente una maggiore granularità durante il filtraggio.

## 6. Verificare la connessione {#test-connection}

Con i dati del catalogo ora in SaaS, verifica che i dati del prodotto vengano restituiti nei seguenti scenari:

- La casella [!UICONTROL Search] restituisce correttamente i risultati
- La ricerca delle categorie restituisce correttamente i risultati
- I facet sono disponibili come filtri nelle pagine dei risultati di ricerca

Se tutto funziona correttamente, [!DNL Live Search] è installato, connesso e pronto all&#39;uso.

Se si verificano problemi nella vetrina, controllare il file `var/log/system.log` per individuare eventuali errori o errori di comunicazione API sul lato servizi.

Per consentire a [!DNL Live Search] di attraversare un firewall, aggiungere `commerce.adobe.io` al inserisco nell&#39;elenco Consentiti di.

## 7. Personalizza per la vetrina

Hai installato l&#39;estensione [!DNL Live Search], hai sincronizzato, convalidato e configurato i tuoi dati. A questo punto è necessario assicurarsi che i widget [!DNL Live Search] siano conformi all&#39;aspetto del tuo Negozio.

Puoi assegnare uno stile ai widget popover e PLP definendo regole CSS personalizzate in base alle esigenze. Consulta [Elementi Popover di stile](storefront-popover.md#styling-popover-example) e [Widget pagina elenco prodotti](plp-styling.md#styling-example).

Se desideri estendere la funzionalità dei widget, il codice sorgente per ciascuno di essi è disponibile in un repository pubblico.
In questo scenario, puoi personalizzare il JavaScript in base alle tue esigenze e quindi ospitare il codice personalizzato sulla CDN. Questo script personalizzato comunica con il servizio [!DNL Live Search] e restituisce i risultati come normale, consentendo di controllare la funzionalità del widget.

- [Archivio widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Archivio della barra di ricerca](https://github.com/adobe/storefront-search-as-you-type)

## Aggiornamento di [!DNL Live Search] {#update}

Prima di aggiornare Live Search, esegui quanto segue dalla riga di comando per verificare la versione di Live Search installata:

```bash
composer show magento/module-live-search | grep version
```

Per aggiornare [!DNL Live Search], eseguire quanto segue dalla riga di comando:

```bash
composer update magento/live-search --with-dependencies
```

Per eseguire l&#39;aggiornamento a una versione principale, ad esempio da 3.1.1 a 4.0.0, modificare il file `.json` principale del progetto come segue:[!DNL Composer]

1. Se la versione di `magento/live-search` attualmente installata è `3.1.1` o inferiore e si sta eseguendo l&#39;aggiornamento alla versione `4.0.0` o successiva, eseguire il comando seguente prima dell&#39;aggiornamento:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   Per informazioni sulla versione di `magento/live-search` attualmente installata, eseguire il comando seguente:

   ```bash
   composer show magento/live-search
   ```

1. Aprire il file radice `composer.json` e cercare `magento/live-search`.

1. Nella sezione `require`, aggiornare il numero di versione come segue:

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

## Disinstallazione di [!DNL Live Search] {#uninstall}

Per disinstallare [!DNL Live Search], fare riferimento a [Moduli di disinstallazione](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules).

## [!DNL Live Search] pacchetti {#packages}

L&#39;estensione [!DNL Live Search] è costituita dai pacchetti seguenti:

| Pacchetto | Descrizione |
|--- |--- |
| `module-live-search` | Consente ai commercianti di configurare le impostazioni di ricerca per faceting, sinonimi, regole di query e così via e fornisce l&#39;accesso a un&#39;area di riproduzione GraphQL di sola lettura per testare le query di *Admin*. |
| `module-live-search-adapter` | Indirizza le richieste di ricerca dalla vetrina al servizio [!DNL Live Search] ed esegue il rendering dei risultati nella vetrina. <br />- Sfoglia categorie - Indirizza le richieste dalla [navigazione superiore](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top) della vetrina al servizio di ricerca.<br />- Ricerca globale - Indirizza le richieste dalla casella [Ricerca rapida](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) in alto a destra della vetrina al servizio [!DNL Live Search]. |
| `module-live-search-storefront-popover` | Un popover &quot;search as you type&quot; (cerca durante la digitazione) sostituisce la ricerca rapida standard e restituisce dati e miniature dei risultati di ricerca principali. |

## [!DNL Live Search] dipendenze {#dependencies}

Le [!DNL Live Search] dipendenze seguenti vengono acquisite da [!DNL Composer].

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

Nelle sezioni seguenti vengono forniti argomenti più avanzati quando si utilizzano [!DNL Live Search] e [!DNL Catalog Service].

### Endpoint

[!DNL Live Search] comunica attraverso l&#39;endpoint in `https://catalog-service.adobe.io/graphql`.

Poiché [!DNL Live Search] non ha accesso al database completo dei prodotti, [!DNL Live Search] GraphQL e Commerce Core GraphQL non avranno parità completa.

Si consiglia di chiamare direttamente le API SaaS, in particolare l’endpoint Catalog Service.

- Migliorare le prestazioni e ridurre il carico del processore ignorando il database Commerce/processo Graphql
- Sfruttare la federazione [!DNL Catalog Service] per chiamare [!DNL Live Search], [!DNL Catalog Service] e [!DNL Product Recommendations] da un singolo endpoint.

Per alcuni casi d&#39;uso, potrebbe essere meglio chiamare [!DNL Catalog Service] per i dettagli del prodotto e casi simili. Per ulteriori informazioni, vedere [refineProduct](https://developer.adobe.com/commerce/services/graphql/catalog-service/refine-product/).

Se hai un&#39;implementazione headless personalizzata, vedi le [!DNL Live Search] implementazioni di riferimento:

- [widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Campo Live Search](https://github.com/adobe/storefront-search-as-you-type)

Se non utilizzi i componenti predefiniti, come Search Adapter o widget su Luma, o i widget CIF dell’AEM, gli eventi (dati di click-stream che alimentano Adobe Sensei per merchandising intelligente e metriche delle prestazioni) non funzioneranno immediatamente e richiederanno uno sviluppo personalizzato per implementare eventi headless.

La versione più recente di [!DNL Live Search] utilizza già [!DNL Catalog Service].

### Supporto linguistico

[!DNL Live Search] widget supportano le seguenti lingue:

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

Se il widget rileva che l&#39;impostazione della lingua di amministrazione di Commerce (_Stores_ > Settings > _Configuration_ > _General_ > Country Options) corrisponde a una lingua supportata, per impostazione predefinita viene utilizzata tale lingua. In caso contrario, per impostazione predefinita i widget sono inglesi.

Gli amministratori possono inoltre impostare la lingua dell&#39;[indice di ricerca](settings.md#language) per garantire risultati di ricerca migliori.

### Archivio del codice widget

I widget Pagina di elenco prodotti e Campo Live Search sono entrambi disponibili per il download dall’archivio GitHub.

Questo consente agli sviluppatori di personalizzare completamente la funzionalità e lo stile. Questi utenti ospitano il codice personalmente, sfruttando comunque il servizio [!DNL Live Search].

- [widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Barra di ricerca](https://github.com/adobe/storefront-search-as-you-type)

### Estensione Esportazione dati

Dopo l’abilitazione di Live Search, l’estensione Esportazione dati sincronizza i dati Commerce tra l’applicazione Commerce e Live Search. In questo modo i dati Commerce più aggiornati saranno disponibili nella vetrina. In Admin (Ammin), puoi controllare lo stato di sincronizzazione utilizzando il dashboard Data Management (Gestione dati). È possibile gestire e risolvere i problemi del processo di esportazione dei dati utilizzando CLI e registri di Commerce. Per ulteriori dettagli, vedere la [Guida all&#39;esportazione dei dati](../data-export/overview.md).

### Inventory management

[!DNL Live Search] supporta le funzionalità [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) in Commerce (precedentemente noto come Multi-Source Inventory o MSI). Per abilitare il supporto completo, è necessario [aggiornare](install.md#update) il modulo di dipendenza `commerce-data-export` alla versione 102.2.0+.

[!DNL Live Search] restituisce un valore booleano che indica se un prodotto è disponibile all&#39;interno di Inventory management, ma non contiene informazioni sull&#39;origine che contiene il titolo.

### Indicizzatore prezzi

I clienti di Live Search possono utilizzare l&#39;[Indicizzatore prezzi SaaS](../price-index/price-indexing.md), che fornisce aggiornamenti più rapidi per la modifica del prezzo e tempi di sincronizzazione.

### Supporto del prezzo

I widget Live Search supportano la maggior parte dei tipi di prezzo supportati da Adobe Commerce, ma non tutti.

Attualmente sono sostenuti i prezzi di base. I prezzi avanzati non supportati sono:

- Costo
- Prezzo minimo annunciato

Esaminare [Mesh API](../catalog-service/mesh.md) per calcolare i prezzi più complessi.

Il formato del prezzo supporta l&#39;impostazione di configurazione delle impostazioni locali nell&#39;istanza di Commerce: *Archivi* > Impostazioni > *Configurazione* > Generale > *Generale* > Opzioni locali > Impostazioni internazionali.

### Supporto per vetrina headless

Facoltativamente, potrebbe essere necessario installare il modulo `module-data-services-graphql` che espande la copertura GraphQL esistente dell&#39;applicazione per includere i campi necessari per la raccolta dei dati comportamentali della vetrina.

```bash
composer require magento/module-data-services-graphql
```

Questo modulo aggiunge contesti aggiuntivi alle query GraphQL:

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### Supporto B2B

[!DNL Live Search] supporta la funzionalità [B2B](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview) con ulteriori [limitazioni](boundaries-limits.md#b2b-and-category-permissions).

### Supporto PWA

[!DNL Live Search] funziona con PWA Studio, ma gli utenti potrebbero vedere lievi differenze rispetto ad altre implementazioni di Commerce. Le funzionalità di base, come la ricerca e la pagina di elenco dei prodotti, funzionano in Venia, ma alcune permutazioni di Graphql potrebbero non funzionare correttamente. Potrebbero esserci anche differenze di prestazioni.

- L&#39;attuale implementazione di PWA di [!DNL Live Search] richiede più tempo di elaborazione per restituire i risultati della ricerca rispetto a [!DNL Live Search] con la vetrina nativa di Commerce.
- [!DNL Live Search] in PWA non supporta [gestione eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). Di conseguenza, funzioneranno sia la generazione di rapporti di ricerca che il merchandising intelligente.
- Il filtro diretto su `description`, `name`, `short_description` non è supportato da GraphQL se utilizzato con [PWA](https://developer.adobe.com/commerce/pwa-studio/), ma viene restituito con un filtro più generale.

Per utilizzare [!DNL Live Search] con PWA Studio, gli integratori devono anche:

1. Installa [livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
1. Impostare `environmentId` nell&#39;oggetto `storeDetails`.

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

[!DNL Live Search] raccoglie i dati di interazione dell&#39;utente come parte della funzionalità di base e i cookie vengono utilizzati per memorizzare tali dati. Quando raccoglie informazioni sull’utente, quest’ultimo deve accettare di memorizzare i cookie. [!DNL Live Search] e [!DNL Product Recommendations] condividono il flusso di dati e quindi lo stesso meccanismo di cookie. Ulteriori informazioni sono disponibili in [Gestione delle restrizioni dei cookie](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/developer/setting-cookie).
