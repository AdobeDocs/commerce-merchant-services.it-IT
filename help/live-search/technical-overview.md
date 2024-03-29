---
title: "Panoramica tecnica"
description: "[!DNL Live Search] flusso di onboarding, requisiti di sistema, limiti e limitazioni"
exl-id: 45f6c1ae-544b-47ef-9feb-c1a05f93108a
recommendations: noCatalog
source-git-commit: e8d4215b1f16f1cb34783674cabc046dec135729
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Panoramica tecnica

Questo argomento esamina i requisiti tecnici e i suggerimenti per l&#39;installazione e l&#39;ottimizzazione [!DNL Live Search] per Adobe Commerce.

## Requisiti {#requirements}

* [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
* PHP 8.1 / 8.2
* [!DNL Composer]

### Piattaforme supportate

* Adobe Commerce on-prem (EE) : 2.4.4+
* Adobe Commerce on Cloud (ECE) : 2.4.4+

## Endpoint

[!DNL Live Search] comunica attraverso l’endpoint in corrispondenza di `https://catalog-service.adobe.io/graphql`.

As [!DNL Live Search] non ha accesso alla banca dati completa dei prodotti, [!DNL Live Search] GraphQL e Commerce core GraphQL non avranno parità completa.

Si consiglia di chiamare direttamente le API SaaS, in particolare l’endpoint Catalog Service.

* Migliora le prestazioni e riduci il carico del processore bypassando il database Commerce/processo Graphql
* Sfrutta i vantaggi [!DNL Catalog Service] federazione da chiamare [!DNL Live Search], [!DNL Catalog Service], e [!DNL Product Recommendations] da un singolo endpoint.

Per alcuni casi d’uso, potrebbe essere meglio chiamare [!DNL Catalog Service] per informazioni dettagliate sul prodotto e casi simili. Consulta [refineProduct](https://developer.adobe.com/commerce/services/graphql/catalog-service/refine-product/) per ulteriori informazioni.

Se disponi di un’implementazione headless personalizzata, vedi [!DNL Live Search] implementazioni di riferimento:

* [Widget PLP](https://github.com/adobe/storefront-product-listing-page)
* [Campo Live Search](https://github.com/adobe/storefront-search-as-you-type)

Se non utilizzi i componenti predefiniti, come Search Adapter o widget su Luma, o i widget CIF dell’AEM, gli eventi (dati di click-stream che alimentano Adobe Sensei per merchandising intelligente e metriche delle prestazioni) non funzioneranno immediatamente e richiederanno uno sviluppo personalizzato per implementare eventi headless.
Ultima versione di [!DNL Live Search] utilizza già [!DNL Catalog Service].

## Limiti e soglie

Attualmente, il [!DNL Live Search] l’API di ricerca/categoria ha i seguenti limiti supportati e limiti statici:

### Indicizzazione

* [Indici](indexing.md) fino a 300 attributi di prodotto per visualizzazione store.
* Indica solo i prodotti dal database di Adobe Commerce.
* Le pagine CMS non sono indicizzate.

### Query

* [!DNL Live Search] non ha accesso alla tassonomia completa dell’albero delle categorie, il che rende alcuni scenari di ricerca di navigazione a più livelli al di fuori della sua portata.
* [!DNL Live Search] utilizza un endpoint GraphQL univoco per le query per supportare funzioni quali il faceting dinamico e la ricerca in base al tipo di utente. Anche se simile al [API GRAPHQL](https://developer.adobe.com/commerce/webapi/graphql/), esistono alcune differenze e alcuni campi potrebbero non essere completamente compatibili.

Per limitare i gruppi di clienti utilizzando le autorizzazioni del catalogo:

* I prodotti devono essere assegnati alla categoria principale.
* Al gruppo di clienti &quot;Non connesso&quot; devono essere assegnate autorizzazioni di navigazione &quot;Consenti&quot;.
* Per limitare i prodotti al gruppo di clienti Non connesso, passare a ogni categoria e impostare le autorizzazioni per ogni gruppo di clienti.

### Regole

* Numero massimo di ricerche di merchandising [regole](rules.md) la visualizzazione per negozio è 50.
* Il merchandising per categoria può avere una regola per categoria.
* Il numero massimo di condizioni per regola è 10.
* Il numero massimo di eventi per regola è 25.

### Sinonimi

* [!DNL Live Search] può gestire fino a 200 [sinonimi](synonyms.md) per la visualizzazione store.

## Supporto linguistico

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

Se il widget rileva che l’impostazione della lingua di amministrazione di Commerce (_Negozi_ > Impostazioni > _Configurazione_ > _Generale_ > Country Options) corrisponde a una lingua supportata. Per impostazione predefinita è tale lingua. In caso contrario, per impostazione predefinita i widget sono inglesi.

Gli amministratori possono anche impostare la lingua [indice di ricerca](settings.md#language), per garantire risultati di ricerca migliori.

## Merchandising categorie

[Merchandising categorie](category-merch.md) consente di configurare [!DNL Live Search] per lavorare a livello di categoria di prodotto.

Questo video è un’introduzione alla categoria Merchandising.

>[!VIDEO](https://video.tv.adobe.com/v/3424617)

## Archivio del codice widget

I widget Pagina di elenco prodotti e Campo Live Search sono entrambi disponibili per il download dall’archivio GitHub.

Questo consente agli sviluppatori di personalizzare completamente la funzionalità e lo stile. Questi utenti ospitano il codice da soli, pur sfruttando [!DNL Live Search] servizio.

* [Widget PLP](https://github.com/adobe/storefront-product-listing-page)
* [Barra di ricerca](https://github.com/adobe/storefront-search-as-you-type)

## Inventory management

[!DNL Live Search] supporta [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) funzionalità in Commerce (noto in precedenza come Multi-Source Inventory o MSI). Per abilitare il supporto completo, è necessario [aggiorna](install.md#update) modulo di dipendenza `commerce-data-export` alla versione 102.2.0+.

[!DNL Live Search] restituisce un valore booleano che indica se un prodotto è disponibile in Inventory management, ma non contiene informazioni sull’origine del titolo.

## Indicizzatore prezzi

I clienti di Live Search possono utilizzare il nuovo [Indicizzatore prezzi SaaS](../price-index/price-indexing.md), che fornisce aggiornamenti più rapidi per la modifica del prezzo e tempi di sincronizzazione.

## Supporto del prezzo

I widget Live Search supportano la maggior parte dei tipi di prezzo supportati da Adobe Commerce, ma non tutti.

Attualmente sono sostenuti i prezzi di base. I prezzi avanzati non supportati sono:

* Costo
* Prezzo minimo annunciato

Osserva [Mesh API](../catalog-service/mesh.md) per calcoli dei prezzi più complessi.

Il formato del prezzo supporta l’impostazione di configurazione locale nell’istanza Commerce: *Negozi* > Impostazioni > *Configurazione* > Generale > *Generale* > Opzioni locali > Impostazioni internazionali.

## Supporto PWA

[!DNL Live Search] funziona con PWA Studi, ma gli utenti possono vedere lievi differenze rispetto ad altre implementazioni di Commerce. Le funzionalità di base, come la ricerca e la pagina di elenco dei prodotti, funzionano in Venia, ma alcune permutazioni di Graphql potrebbero non funzionare correttamente. Potrebbero esserci anche differenze di prestazioni.

* L’attuale implementazione PWA di [!DNL Live Search] richiede più tempo di elaborazione per restituire i risultati di ricerca di [!DNL Live Search] con la vetrina nativa di Commerce.
* [!DNL Live Search] in PWA non supporta [gestione degli eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). Di conseguenza, funzioneranno sia la generazione di rapporti di ricerca che il merchandising intelligente.
* Filtrare direttamente su `description`, `name`, `short_description` non è supportato da GraphQL se utilizzato con [PWA](https://developer.adobe.com/commerce/pwa-studio/), ma vengono restituiti con un filtro più generale.

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

## Non attualmente supportato

* Il [Ricerca avanzata](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) il modulo è disattivato quando [!DNL Live Search] e il collegamento Ricerca avanzata nel piè di pagina della vetrina viene rimosso.
* [Determinazione prezzi livello](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier) e [Prezzi speciali](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) non sono supportati nella [!DNL Live Search] campo e widget pagina elenco prodotti.

## Cookie

[!DNL Live Search] raccoglie i dati di interazione dell’utente come parte della sua funzionalità di base e i cookie vengono utilizzati per memorizzare tali dati. Quando raccoglie informazioni sull’utente, quest’ultimo deve accettare di memorizzare i cookie. [!DNL Live Search] e [!DNL Product Recommendations] condividere il flusso di dati e quindi lo stesso meccanismo di cookie. Ulteriori informazioni sono disponibili in [Gestire le restrizioni dei cookie](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/developer/setting-cookie).
