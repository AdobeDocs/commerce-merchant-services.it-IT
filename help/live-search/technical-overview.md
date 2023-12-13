---
title: "Panoramica tecnica"
description: "[!DNL Live Search] flusso di onboarding, requisiti di sistema, limiti e limitazioni"
exl-id: 45f6c1ae-544b-47ef-9feb-c1a05f93108a
recommendations: noCatalog
source-git-commit: 10b9f087da1346734735379846d50b53d36c1562
workflow-type: tm+mt
source-wordcount: '689'
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

>[!NOTE]
>
>As [!DNL Live Search] non ha accesso alla banca dati completa dei prodotti, [!DNL Live Search] GraphQL e Commerce core GraphQL non avranno parità completa.

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

* en_US (impostazione predefinita)
* de_DE
* es_MX
* fr_FR
* it_IT
* ja_JA
* nl_NL
* no_NO
* pt_PT

Se il widget rileva che l’impostazione della lingua di amministrazione di Commerce (_Negozi_ > Impostazioni > _Configurazione_ > _Generale_ > Country Options) corrisponde a una lingua supportata. Per impostazione predefinita è tale lingua. In caso contrario, per impostazione predefinita i widget sono inglesi.

Gli amministratori possono anche impostare la lingua [indice di ricerca](settings.md#language), per garantire risultati di ricerca migliori.

## Merchandising categorie

[Merchandising categorie](category-merch.md) consente di configurare [!DNL Live Search] per lavorare a livello di categoria di prodotto.

Questo video è un’introduzione alla categoria Merchandising.

>[!VIDEO](https://video.tv.adobe.com/v/3424617)

## Archivio del codice widget

Il widget Pagina di elenco prodotti e il widget Popover di ricerca sono entrambi disponibili per il download dall’archivio GitHub.

Questo consente agli sviluppatori di personalizzare completamente la funzionalità e lo stile. Questi utenti ospitano il codice da soli, pur sfruttando [!DNL Live Search] servizio.

* [Widget PLP](https://github.com/adobe/storefront-product-listing-page)
* [Barra di ricerca](https://github.com/adobe/storefront-search-as-you-type)

## Inventory management

[!DNL Live Search] supporta [Inventory management](https://experienceleague.adobe.com/docs/commerce-admin/inventory/introduction.html) funzionalità in Commerce (noto in precedenza come Multi-Source Inventory o MSI). Per abilitare il supporto completo, è necessario [aggiorna](install.md#update) modulo di dipendenza `commerce-data-export` alla versione 102.2.0+.

[!DNL Live Search] restituisce un valore booleano che indica se un prodotto è disponibile in Inventory management, ma non contiene informazioni sull’origine del titolo.

## Indicizzatore prezzi

I clienti di Live Search possono utilizzare il nuovo [Indicizzatore prezzi SaaS](../price-index/index.md), che fornisce aggiornamenti più rapidi per la modifica del prezzo e tempi di sincronizzazione.

## Supporto PWA

[!DNL Live Search] funziona con PWA Studi, ma gli utenti possono vedere lievi differenze rispetto ad altre implementazioni di Commerce. Le funzionalità di base, come la ricerca e la pagina di elenco dei prodotti, funzionano in Venia, ma alcune permutazioni di Graphql potrebbero non funzionare correttamente. Potrebbero esserci anche differenze di prestazioni.

* L’attuale implementazione PWA di [!DNL Live Search] richiede più tempo di elaborazione per restituire i risultati di ricerca di [!DNL Live Search] con la vetrina nativa di Commerce.
* [!DNL Live Search] in PWA non supporta [gestione degli eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). Di conseguenza, il merchandising intelligente non funzionerà.
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

* Il [Ricerca avanzata](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#advanced-search) il modulo è disattivato quando [!DNL Live Search] e il collegamento Ricerca avanzata nel piè di pagina della vetrina viene rimosso.
* [Determinazione prezzi livello](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/product-price-tier.html) e [Prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/product-price-special.html) non sono supportati nella [!DNL Live Search] Widget pagina elenco prodotti e popover.

## Cookie

[!DNL Live Search] raccoglie i dati di interazione dell’utente come parte della sua funzionalità di base e i cookie vengono utilizzati per memorizzare tali dati. Quando raccoglie informazioni sull’utente, quest’ultimo deve accettare di memorizzare i cookie. [!DNL Live Search] e [!DNL Product Recommendations] condividere il flusso di dati e quindi lo stesso meccanismo di cookie. Ulteriori informazioni sono disponibili in [Gestire le restrizioni dei cookie](https://experienceleague.adobe.com/docs/commerce-merchant-services/product-recommendations/developer/setting-cookie.html).
