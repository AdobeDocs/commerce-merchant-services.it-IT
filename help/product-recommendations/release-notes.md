---
title: '[!DNL Product Recommendations] Note sulla versione'
description: Informazioni aggiornate sulla versione di [!DNL Product Recommendations] da Adobe Commerce.
exl-id: 1758e688-d26f-45e7-818c-d4726338a6c3
feature: Services, Recommendations, Release Notes
source-git-commit: 7bc63a6b647dd010ef58c5d4d4df7a0a2c3cabe0
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 0%

---

# [!DNL Product Recommendations] Note sulla versione

Le note sulla versione contengono aggiornamenti ai seguenti elementi [!DNL Product Recommendations] moduli:

* [!DNL Product Recommendations] metapackage: `magento/product-recommendations`
* Supporto di Page Builder in [!DNL Product Recommendations] (facoltativo) modulo: `magento/module-page-builder-product-recommendations`
* Supporto del tipo di consiglio per somiglianza visiva per [!DNL Product Recommendations] (facoltativo) modulo: `magento/module-visual-product-recommendations`

È disponibile il supporto per la versione principale rilasciata corrente. Vengono fornite a titolo di riferimento le note sulla versione per le versioni precedenti.
Le note sulla versione includono:

![Nuovo](../assets/new.svg) Nuove funzioni
![Correzione](../assets/fix.svg) Correzioni e miglioramenti
![Bug](../assets/bug.svg) Problemi noti

Consulta la documentazione per gli sviluppatori per [informazioni sul supporto del prodotto](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html).

## Aggiornamenti dei servizi in hosting

Queste note descrivono gli aggiornamenti pubblicati al di fuori di una versione con versione o i miglioramenti al servizio ospitato.

+++Aggiornamenti dei servizi in hosting

_18 luglio 2023_

![Nuovo](../assets/new.svg) Il Recommendations del prodotto ora dispone di un GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) query.

_25 aprile 2023_

![Nuovo](../assets/new.svg) I clienti di Recommendations di prodotto ora possono sfruttare [Indicizzazione dei prezzi SaaS](../price-index/index.md).

+++

## Versione principale corrente

### 5.0.1 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Sono stati aggiunti nuovi moduli per supportare [Indicizzatore prezzi Saas](../price-index/index.md).
![Nuovo](../assets/new.svg) Sono stati aggiunti nuovi moduli di esportazione dati per supportare l’esportazione di più tipi di prodotto, inclusi prodotti in bundle e gift card.

#### Limitazioni note

* Il `websiteCode` viene restituito erroneamente se contiene un carattere di sottolineatura (_).

### Versioni precedenti

+++5.0.0 e versioni precedenti

### 5.0.0 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Recommendations di prodotto aggiornato per supportare Adobe Commerce 2.4.6.
![Nuovo](../assets/new.svg) Questa è una versione principale. [Modifica](install-configure.md#update) la radice `composer.json` per il progetto.
![Nuovo](../assets/new.svg) [!DNL Product Recommendations] ora supporta full [Inventory management](https://experienceleague.adobe.com/docs/commerce-admin/inventory/introduction.html) funzionalità in Commerce (noto in precedenza come Multi-Source Inventory o MSI). Per abilitare il supporto completo, è necessario [aggiorna](install-configure.md#update) modulo di dipendenza `commerce-data-export` alla versione 102.2.0+.

### 4.0.1 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) In precedenza, in Product Recommendations veniva visualizzato un errore quando la valuta di visualizzazione veniva cambiata in una valuta non predefinita. Il cambio delle valute ora funziona correttamente.

### 4.0.0 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Aggiunto [indicatori di predisposizione](create.md) per aiutarti a visualizzare l’avanzamento della formazione di ciascun tipo di consiglio.
![Nuovo](../assets/new.svg) Questa è una versione principale. [Modifica](install-configure.md#update) la radice `composer.json` per il progetto. Questa versione richiede anche di fornire due chiavi API durante l’installazione e la configurazione di Product Recommendations: [una chiave di produzione e una chiave sandbox](../landing/saas.md).

#### Limitazioni note

* Il `websiteCode` viene restituito erroneamente se contiene un carattere di sottolineatura (_).

### 3.3.7 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Supporto PHP 8.1 aggiunto
![Nuovo](../assets/new.svg) È stato migliorato il ridimensionamento delle immagini in modo da gestirlo più correttamente nel modello di visualizzazione di riferimento

### 3.3.6 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Ottimizzato [!DNL Product Recommendations] metapackage elencando esplicitamente le dipendenze

### 3.3.5 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Aggiunto [Supporto B2B](onboarding.md#b2bsupport) nel Recommendations del prodotto
![Nuovo](../assets/new.svg) Sono stati aggiunti nuovi feed a [sincronizza dati catalogo](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/data-services/catalog-sync.html) a Commerce Services tramite la riga di comando

### 3.3.3 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Aggiunto nuovo [tipi di consigli](type.md): Conversione (dalla vista al carrello), Conversione (dalla vista all’acquisto) e Visualizzato di recente. Questi nuovi tipi di consigli sono disponibili nel `magento/product-recommendations` modulo 3.2.2 e versioni successive.
![Correzione](../assets/fix.svg) È stato risolto un problema che causava il blocco errato di un cookie da parte di Web Application Firewall (WAF) di Fastly
![Correzione](../assets/fix.svg) È stato risolto un problema che impediva la visualizzazione dei prodotti assegnati alla visualizzazione Store non predefinita in _Anteprima prodotto Recommendations_ durante la creazione di un consiglio per quella specifica visualizzazione store
![Correzione](../assets/fix.svg) È stato risolto un problema a causa del quale alcuni nomi di unità di consigli in Page Builder impedivano la visualizzazione dell&#39;unità di consigli nella vetrina

### 3.3.2 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) È stata corretta una dipendenza mancante per il supporto B2B

### 3.3.1 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) È stato aggiunto il supporto per i prezzi di gruppo dei clienti B2B. Quando si imposta un [filtro prezzi](filters.md) in un’unità di consigli, i clienti B2B che hanno effettuato l’accesso vedono i prezzi del gruppo di clienti impostati per i prodotti visualizzati.

### 3.3.0 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) È stato aggiunto il supporto di Adobe Client Data Layer per standardizzare la raccolta di dati comportamentali tra le funzioni e i servizi di Adobe Commerce. Consulta la [leggimi](https://github.com/adobe/magento-storefront-event-collector/blob/main/README.md) per ulteriori informazioni.

### 3.2.6 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) È stato corretto un errore modale JavaScript
![Correzione](../assets/fix.svg) È stato risolto un problema che causava il blocco errato di un cookie da parte di Web Application Firewall (WAF) di Fastly

### 3.2.5 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Servizi di Magento rinominati [Servizi Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html) e una migliore usabilità in Admin

### 3.2.4 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) È stato corretto l’errore &quot;Impossibile recuperare i dati delle opzioni di prodotto configurabili&quot; durante l’indicizzazione degli attributi del prodotto

### 3.2.3 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) È stato corretto l’errore &quot;Impossibile recuperare i dati delle opzioni di prodotto configurabili&quot; durante la sincronizzazione del catalogo
![Correzione](../assets/fix.svg) È stato risolto un problema che impediva la corretta impostazione del codice store quando si abilitava la configurazione &quot;Aggiungi codice store a URL&quot;
![Correzione](../assets/fix.svg) È stato migliorato il rilevamento delle modifiche alla configurazione del pannello di amministrazione per garantire che tali modifiche vengano riportate nei dati di sincronizzazione del catalogo

### 3.2.2 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Aggiunta la possibilità di [visualizzare in anteprima i risultati dei consigli](create.md) al momento della creazione. Potrebbe essere necessario aggiornare il modulo alla versione più recente.
![Nuovo](../assets/new.svg) Aggiunta la possibilità di [monitorare e gestire](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/data-services/catalog-sync.html) il processo di sincronizzazione del catalogo dall’amministratore.
![Nuovo](../assets/new.svg) Aggiunto [filtri](filters.md) per controllare quali prodotti vengono visualizzati nei consigli.
![Nuovo](../assets/new.svg) È stata aggiunta la [Somiglianza visiva](type.md#visualsim) tipo di consiglio.

### 1.2.1 di magento/module-page-builder-consigli-di-prodotto per Page Builder

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) È stato aggiunto il supporto per la versione 3.2.0+ di `magento/product-recommendations` modulo

### 3.1.0 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Aggiunta la possibilità di [risincronizza](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/data-services/catalog-sync.html) il catalogo ai servizi SaaS tramite riga di comando.
![Nuovo](../assets/new.svg) È stato aggiunto il supporto per i prefissi delle tabelle del database
![Correzione](../assets/fix.svg) Supporto di PHP 7.1 rimosso

### 3.0.8 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) È stato risolto un problema a causa del quale gli eventi venivano inviati per la raccolta dati prima della configurazione del modulo, causando traffico non valido.

### 3.0.6 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) **(Beta)** Include il supporto per i nuovi [Somiglianza visiva](type.md#visualsim) tipo di consiglio.

### 1.0.0 di magento/module-visual-product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) **(Beta)** [Somiglianza visiva](type.md#visualsim). Con il _Somiglianza visiva_ tipo di consiglio, puoi implementare un’unità di consigli nella pagina dei dettagli del prodotto che mostra prodotti visivamente simili al prodotto visualizzato.

### 3.0.5 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) È stato corretto l’errore &quot;Impossibile recuperare i dati delle opzioni del prodotto&quot; che poteva verificarsi durante l’esportazione del catalogo.
![Correzione](../assets/fix.svg) Il simbolo di valuta nel _Ricavi_ colonna sulla _Recommendations del prodotto_ la dashboard ora riflette correttamente la valuta di base configurata.

### 3.0.4 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) È stato aggiunto il supporto per Adobe Commerce 2.4.0

### 3.0.3 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Correzione](../assets/fix.svg) Miglioramento dell’implementazione dei simboli nel modello storefront

### 1.0.4 di magento/module-page-builder-consigli-di-prodotto per Page Builder

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) È stato aggiunto il nome del consiglio di prodotto durante la modifica del tipo di contenuto Page Builder

### 3.0.2 magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) È stata aggiunta una colonna di stato sulla griglia durante la selezione delle unità per i consigli in Page Builder
![Correzione](../assets/fix.svg) È stato risolto un problema relativo a protocolli http/https errati negli URL di prodotti e immagini.

### 3.0.1 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

Questa è una versione principale. [Modifica](install-configure.md#update) file compositore.json principale del progetto.

![Nuovo](../assets/new.svg) Recupera [!DNL Product Recommendations] da spazi dati SaaS alternativi. Questo consente di utilizzare i consigli di prodotto calcolati nell’ambiente del prodotto in altri ambienti non di produzione. [Passaggio da uno spazio dati SaaS a un altro](settings.md) descrive ulteriormente questa funzione.

![Correzione](../assets/fix.svg) È stato risolto un problema che impediva il pagamento da parte degli acquirenti che utilizzavano Origine uBlock.
![Correzione](../assets/fix.svg) È stato risolto un problema che inviava eventi aggiuntivi al carrello estranei

### 1.0.3 di magento/module-page-builder-consigli-di-prodotto per Page Builder

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Supporto di Page Builder. Con l’integrazione di Page Builder, puoi posizionare in modo accurato e dettagliato le unità di consigli in qualsiasi posizione arbitraria su contenuti creati da Page Builder. Puoi anche assegnare uno stile ai titoli e alle unità di consigli. Vai a [Page Builder](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html) per ulteriori informazioni.

### 2.0.0 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/new.svg) Rilascio di disponibilità generale.

+++

## Documentazione

Per ulteriori informazioni su [!DNL Product Recommendations] e [!DNL Product Recommendations] Sviluppo:

* [Guida utente](overview.md)
* [Documentazione per gli sviluppatori](https://experienceleague.adobe.com/docs/commerce-merchant-services/product-recommendations/developer/development-overview.html)
