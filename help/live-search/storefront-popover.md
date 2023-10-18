---
title: "[!DNL Storefront Popover]"
description: "Il [!DNL Live Search storefront popover] restituisce dinamicamente prodotti e miniature suggeriti."
exl-id: 88fdc3ed-b606-40de-94b7-435be09c4072
source-git-commit: 5d76d5537c8625296663239195abd26d4ee24db4
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# [!DNL Storefront Popover]

Quando [!DNL Live Search] è [installato](install.md), a [!DNL popover] viene visualizzato nella vetrina quando gli acquirenti digitano nella [Ricerca](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search) casella. Con ogni carattere digitato, il [!DNL popover] viene aggiornato con i prodotti consigliati e le miniature dei risultati di ricerca principali.

[!DNL Live Search] restituisce risultati per una query di due o più caratteri. Per una corrispondenza parziale, il numero massimo di caratteri per parola è 20. Il numero di caratteri in una query di ricerca durante la digitazione non è configurabile.

Per impostazione predefinita, [!DNL Live Search] supporta [reindirizzamenti termini di ricerca](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html).

![[!DNL Live Search popover]](assets/storefront-search-as-you-type.png)

## Attributi ricercabili

Per produrre risultati altamente mirati, rivedi l’insieme di [ricercabile](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) (`searchable=true`) attributi del prodotto. Per garantire la rilevanza, rendi gli attributi ricercabili solo se contengono contenuto con un significato chiaro e conciso. Evita di utilizzare attributi che contengono testo meno preciso e lungo, ad esempio `description`, anche se la ricerca è abilitata per impostazione predefinita, può ridurre la precisione dei risultati di ricerca.
Ad esempio, se una persona cerca i &quot;pantaloncini corti&quot; e ci sono camicie con una descrizione che include il termine &quot;maniche corte&quot;, allora le camicie saranno incluse nei risultati della ricerca.

[!DNL Live Search] rispetta anche le [peso](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search) di un attributo di prodotto, come impostato in Adobe Commerce. Gli attributi con un peso maggiore appariranno più in alto nei risultati di ricerca.

È sempre possibile cercare i seguenti attributi:

* `sku`
* `name`
* `categories`

## [!DNL Popover] dimensioni pagina

Dimensione della pagina del [!DNL popover] determina quante righe di prodotti completati automaticamente possono essere restituite. In precedenza, la dimensione della pagina era hardcoded in sei righe. Tuttavia, il `page_size` è ora un&#39;impostazione che può essere configurata dal *Amministratore*. Durante l’installazione di Live Search, il `page_size` il valore cambia rispetto al valore corrente del [Ricerca nel catalogo](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/catalog.html) - `Autocomplete Limit` impostazione.

Per impostazione predefinita, il valore Ricerca nel catalogo - Limite completamento automatico è impostato su otto righe. Per modificare le dimensioni della pagina [!DNL popover], eseguire le operazioni seguenti:

1. Il giorno *Amministratore* barra laterale, vai a **Negozi** > Impostazioni > **Configurazione**.
1. Nel pannello a sinistra, espandi **Catalogo** e scegli **Catalogo** dall&#39;elenco delle impostazioni.
1. Espandi *Ricerca nel catalogo* sezione.
1. Imposta il **Limite completamento automatico** al numero di righe che si desidera consentire nel [!DNL popover].
1. Al termine, fai clic su **Salva configurazione**.

## Servizio catalogo

Il [Catalog Service per Adobe Commerce](../catalog-service/overview.md) L&#39;estensione fornisce dati di catalogo avanzati per modelli di visualizzazione per eseguire in modo rapido e completo il rendering delle esperienze di vetrina relative ai prodotti. Catalog Service può essere utilizzato insieme a Live Search per fornire funzionalità non attualmente supportate dall’estensione nativa:

* Campioni colore
* Attributi estesi
* È possibile inserire altre informazioni sul prodotto

I commercianti possono personalizzare ed estendere i widget o gli elementi della vetrina utilizzando Catalog Service, ma questo non rientra nell’ambito del team di supporto di Adobe.

## Implementazioni headless

Per chi dispone di implementazioni headless, è possibile installare il popover Live Search con un [pacchetto npm](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).

## Limitazioni

* Il [!DNL Live Search] [!DNL storefront popover] è disponibile solo per i negozi che utilizzano *Luma* tema o un tema personalizzato basato su *Luma*. Le breadcrumb nella pagina dei risultati di ricerca non avranno *Luma* stile.
* Il [!DNL popover] non supporta *Vuoto* tema. Consulta [Stile [!DNL Popover] Elementi](storefront-popover-styling.md) per ulteriori informazioni.
* Il [!DNL popover] non è supportato nel modulo Ordine rapido.
* Non sono supportate le liste dei desideri e i confronti tra prodotti.
