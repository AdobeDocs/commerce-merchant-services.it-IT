---
title: "[!DNL SaaS Data Export Extension] Note sulla versione"
description: Informazioni aggiornate sulla versione di [!DNL Data Export Extension] per Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
source-git-commit: 8230756c203cb2b4bdb4949f116c398fcaab84ff
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL SaaS Data Export] Note sulla versione dell’estensione

Queste note sulla versione descrivono le versioni più recenti di [!DNL SaaS data export] estensione. È disponibile il supporto per la versione principale rilasciata corrente. Vengono fornite a titolo di riferimento le note sulla versione per le versioni precedenti.

Gli aggiornamenti includono:

![Nuovo](../assets/new.svg) Nuove funzioni
![Correzione](../assets/fix.svg) Correzioni e miglioramenti
![Bug](../assets/bug.svg) Problemi noti


>[!NOTE]
>
>L’estensione SaaS per l’esportazione dei dati è una raccolta di moduli che viene installata automaticamente con Live Search, Product Recommendations e Catalog Service. È possibile controllare la versione installata nel sistema utilizzando Compositore. In alcuni casi, potrebbe essere utile aggiornare l’estensione di esportazione dei dati sul sistema per rilevare correzioni o nuove funzionalità senza aggiornare la versione del servizio Commerce.

## Versione principale corrente

## Versione 103.3.5

![Correzione](../assets/fix.svg) Imposta la dipendenza per la versione più recente compatibile di esportazione dei dati per il modulo comune SaaS.

![Correzione](../assets/fix.svg) Sostituito `ScopeConfig` istanza con `ServiceConfigInterface` per supportare diverse configurazioni di servizio.

## Versione 103.3.4

![Correzione](../assets/fix.svg) Migliora la registrazione dell’esportazione dei dati SaaS di Commerce aggiungendo ulteriori dettagli sul processo di reindicizzazione.

## Versione 103.3.3

![Nuovo](../assets/new.svg) L’esportazione dei dati SaaS ora memorizza nella cache gli attributi Entity-Attribute-Value (EAV) per la query dei metadati degli attributi.

![Correzione](../assets/fix.svg) È stato risolto un problema a causa del quale `InventoryStockStatus` il feed non è stato salvato al nuovo tentativo se il prodotto è stato eliminato.

## Versione 103.3.2

![Correzione](../assets/fix.svg) È stato risolto un problema a causa del quale `modifiedAt` campo mancante nei feed di entità rimossi.

## Versione 103.3.1

![Correzione](../assets/fix.svg) È stato risolto un problema che causava `Invalid Template File` messaggio da visualizzare durante la reindicizzazione del feed dei prodotti quando è installato Page Builder.

## Versione 103.3.0

![Nuovo](../assets/new.svg) Migrazione delle tabelle dei feed di esportazione immediata alla struttura unificata:
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![Nuovo](../assets/new.svg) Migrazione dei feed di catalogo e inventario alla soluzione di esportazione immediata.

![Nuovo](../assets/new.svg) I processi cron del feed di esportazione immediata sono stati rinominati in `*_feed_resend_failed_items`.

![Nuovo](../assets/new.svg) Il feed di esportazione immediata e le tabelle di registro delle modifiche sono stati rinominati.

![Correzione](../assets/fix.svg) Imposta `modified_at` campo nei dati feed solo per i feed che lo richiedono.

![Correzione](../assets/fix.svg) Modifica il `productAttributes` per recuperare solo gli attributi del prodotto.

## Versione 103.2.6

![Correzione](../assets/fix.svg) È stato risolto un problema che impediva la reindicizzazione dei feed quando le tabelle avevano un prefisso.

## Versione 103.2.5

![Correzione](../assets/fix.svg) Query prezzo ottimizzata.

## Versione 103.2.4

![Correzione](../assets/fix.svg) È stato corretto lo stato Stock errato visualizzato per un prodotto quando Commerce Inventory management è abilitato.

## Versione 103.2.3

![Correzione](../assets/fix.svg) Prezzi speciali a livello di sito web fisso.
![Correzione](../assets/fix.svg) È stato aggiunto il mutex per tutti i feed elaborati.


## Versione 103.2.2

![Correzione](../assets/fix.svg) È stata migliorata la strategia di gestione dei feed in batch per i cataloghi di grandi dimensioni. La tabella dei batch ora è compilata con un numero limitato di ID per ridurre l’utilizzo di memoria.

![Correzione](../assets/fix.svg) È stata eliminata la dipendenza rigida di CommerceInventoryDataExporter dai moduli MSI.

![Correzione](../assets/fix.svg) Migliorato `commerce-data-exporter` registri per raccogliere ulteriori informazioni e organizzare in base a diverse fasi di esportazione.

## Versione 103.2.1

- È stata rilasciata la versione aggiornata.

## Versione 103.2.0

- È stata aggiunta la sincronizzazione di dati multi-thread per prodotti e prezzi.

