---
title: '''[!DNL Catalog Service] Note sulla versione'
description: Informazioni aggiornate sulla versione di [!DNL Catalog Service] per Adobe Commerce.
exl-id: 9bf8e3f7-5b74-4755-867e-ac1c5000ff33
feature: Services, Catalog Service, Release Notes
source-git-commit: 7eece9b341a27637d7ac00216f18b7fad7c50740
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# [!DNL Catalog Service] Note sulla versione

Queste note sulla versione descrivono le versioni più recenti di [!DNL Catalog Service].
È disponibile il supporto per la versione principale rilasciata corrente. Vengono fornite a titolo di riferimento le note sulla versione per le versioni precedenti.
Gli aggiornamenti includono:

![Nuovo](../assets/new.svg) Nuove funzioni
![Correzione](../assets/fix.svg) Correzioni e miglioramenti
![Bug](../assets/bug.svg) Problemi noti

## Versione principale corrente

### Versione V1.11

_18 luglio 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) Catalog Service ora supporta [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) Query GraphQL per Product Recommendations.

#### Limitazioni note

Queste funzioni non sono ancora supportate:

* Pacchetto prodotti a prezzo fisso
* La dimensione massima per il payload degli attributi dinamici è di 9 MB.
* Prezzo del prodotto di gruppo. Può essere calcolato con prezzi di prodotto semplici.
* In un array di immagini, solo la prima immagine contiene ruoli.

Le seguenti limitazioni possono essere risolte utilizzando l’API Mesh e l’API core di GraphQL:

* Prezzo minimo annunciato
* [Prezzi a livelli](mesh.md)
* Prodotti scaricabili e carte regalo

### Versione V1.10

_27 giugno 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) Catalog Service ora può visualizzare i prodotti correlati nel widget Pagina dettagli prodotto.

### Versione V1.7

_12 aprile 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) Catalog Service ora pulisce le varianti di prodotto eliminate.
![Correzione](../assets/fix.svg) Scalabilità dell&#39;infrastruttura e miglioramenti delle prestazioni.

### Versione V1.6

_28 marzo 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) Campioni aggiunti al [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) query.
![Nuovo](../assets/new.svg) Aggiunta la possibilità di ottenere `entityId` utilizzo [Mesh API](mesh.md).

### Versione V1.5

_6 marzo 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) Aggiunto [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) funzionalità GraphQL.
![Correzione](../assets/fix.svg) Prestazioni e scalabilità API migliorate.

### Versione V1.4

_7 febbraio 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) È stato pubblicato il metapacchetto catalogo-servizio per semplificare i passaggi di installazione.
![Correzione](../assets/fix.svg) Miglioramenti a livello di scalabilità e prestazioni delle API.

### Versione V1.3

_17 gennaio 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) L’esperienza di onboarding è stata semplificata e migliorata.
![Nuovo](../assets/new.svg) Sono disponibili nuovi endpoint sandbox per i clienti per i test di pre-produzione.
![Nuovo](../assets/new.svg) È stato aggiunto il supporto per i prodotti virtuali.
![Correzione](../assets/fix.svg) Miglioramenti a livello di scalabilità e prestazioni delle API.

### Versione V1.1

_18 novembre 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) Catalog Service ora supporta Adobe [Mesh API](https://developer.adobe.com/graphql-mesh-gateway/).
![Correzione](../assets/fix.svg) Sono state migliorate la scalabilità API e le prestazioni complessive.

### Versione V1.0

_4 ottobre 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) Ora supporta prodotti in bundle e raggruppati.
![Nuovo](../assets/new.svg) Sono state aggiunte sostituzioni di visibilità B2B. È ora possibile cercare i prodotti e aggiungerli al carrello per gruppi di clienti specifici.
![Correzione](../assets/fix.svg) Il servizio è ora più stabile e offre prestazioni migliori.

## Versioni precedenti

Versioni +++beta

### Versione 0.3 - Beta+

_12 settembre 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) Supporto immagini per varianti: le immagini del prodotto vengono restituite in base alle opzioni selezionate
![Nuovo](../assets/new.svg) Ruoli per supporto prezzi: consente solo ai membri di gruppi di clienti specifici di visualizzare il prezzo dei prodotti
![Correzione](../assets/fix.svg) Miglioramento della stabilità e delle prestazioni del servizio
![Nuovo](../assets/new.svg) Ricevi aggiornamenti quando i prodotti vengono eliminati dal catalogo

### Versione beta

_9 agosto 2022_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"}

![Nuovo](../assets/new.svg) Il `products` e `refineProduct` le query restituiscono i dati seguenti:

* Attributi di prodotto predefiniti (di sistema).
* Attributi di prodotto dinamici e filtrali per ruolo (pagina di visualizzazione prodotto/pagina di elenco prodotti).
* Opzioni prodotto.
* Immagini dei prodotti e filtrale per ruolo (PDP/PLP).
* Un prezzo specifico per prodotti semplici e fasce di prezzo per prodotti configurabili.
* Prezzi e fasce di prezzo del gruppo di clienti. Restituiscono un prezzo predefinito di fallback sugli acquirenti senza un gruppo di clienti.
* Tipi di prodotto che utilizzano prezzi specifici per il cliente B2B.

+++
