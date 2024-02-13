---
title: Servizio di acquisizione feed
description: Scopri il servizio di acquisizione di feed per Adobe Commerce
exl-id: bb5aec74-faca-42ec-9fdb-3261677d451e
source-git-commit: d3798efa038c35f71bb0bb6874d954a8e66c7467
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Servizio di acquisizione feed

Il servizio di acquisizione dei feed consente ai clienti con cataloghi grandi e/o complessi di inviare direttamente i dati ai servizi Adobe Commerce.

Il servizio di acquisizione dei feed riduce il tempo necessario per elaborare le modifiche ai prodotti (aggiornamenti dei prezzi, aggiunta di nuovi attributi) ignorando l’istanza di Adobe Commerce e spostando i dati del catalogo da un ERP (Enterprise Resource Planning) di terze parti direttamente nei servizi di Adobe Commerce.

Questo servizio è destinato ai clienti che memorizzano e gestiscono il catalogo dei prodotti in un sistema esterno all’applicazione principale di Adobe Commerce. Viene fornito come API, in modo che i clienti possano integrarlo nei propri sistemi esistenti, fornendo maggiore flessibilità nelle modalità di implementazione.

I clienti con cataloghi grandi e complessi o che ricevono aggiornamenti frequenti temono che i nuovi dati possano richiedere più tempo del previsto per essere visualizzati nello store live. Poiché Catalog Service sa di quali dati ha bisogno per elaborare questi aggiornamenti, non è necessario inviare i dati tramite il prodotto Commerce di base, ma solo per l’inoltro a Catalog Service. Se si rimuove questo passaggio intermedio, si ottengono miglioramenti in termini di efficienza.

## Flussi di acquisizione dei feed

A seconda della configurazione di Adobe Commerce, l’archiviazione e i flussi di dati possono seguire percorsi diversi.

* In un’istanza standard di Adobe Commerce, il catalogo dei prodotti viene memorizzato all’interno del database di base.
* Quando si utilizzano i servizi Adobe Commerce, i dati del catalogo vengono copiati dal database di base al servizio, quindi elaborati e consegnati da lì.
* Quando i dati del catalogo vengono memorizzati in un sistema di terze parti (ERP, MDM, PIM), passano attraverso l’applicazione Commerce di base e quindi ai servizi Commerce.
* Con il servizio di acquisizione dei feed, i dati dei prodotti passano direttamente dal sistema di terze parti all’infrastruttura dei servizi Commerce.

![Servizio di acquisizione dei feed](assets/feed-ingestion.png)

Ignorando l’applicazione Commerce di base e spostando i dati direttamente nei servizi Commerce, gli aggiornamenti dei prodotti si riflettono nello store più rapidamente. I dati del catalogo di base, come gli SKU, vengono inviati all’applicazione Commerce di base per l’elaborazione separata.

## API

Il [Documentazione API del servizio di acquisizione feed](https://developer.adobe.com/commerce/services/feed-ingestion) fornisce dettagli su come implementare il servizio.
