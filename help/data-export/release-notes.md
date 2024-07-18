---
title: '[!DNL SaaS Data Export Extension] Note sulla versione'
description: Informazioni aggiornate sulla versione di  [!DNL Data Export Extension]  per Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 0c7aeeda-e8a6-4740-b466-0661a6d2df07
source-git-commit: 7757cc382e306a6c074a815d5148a4dcd8fff284
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Note sulla versione dell&#39;estensione [!DNL SaaS Data Export]

Queste note sulla versione descrivono le versioni più recenti dell&#39;estensione [!DNL SaaS data export]. È disponibile il supporto per la versione principale rilasciata corrente. Vengono fornite a titolo di riferimento le note sulla versione per le versioni precedenti.

Gli aggiornamenti includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Correzioni](../assets/fix.svg) correzioni e miglioramenti
![Bug](../assets/bug.svg) problemi noti


>[!NOTE]
>
>L’estensione SaaS per l’esportazione dei dati è una raccolta di moduli che viene installata automaticamente con Live Search, Product Recommendations e Catalog Service. È possibile controllare la versione installata nel sistema utilizzando Compositore. In alcuni casi, potrebbe essere utile aggiornare l’estensione di esportazione dei dati sul sistema per rilevare correzioni o nuove funzionalità senza aggiornare la versione del servizio Commerce.

## Versione principale corrente

## Versione 103.3.8

![Correzione](../assets/fix.svg) Le opzioni di configurazione disabilitate non vengono più esportate come opzioni attive.<!--MDEE-812-->
![Correzione](../assets/fix.svg) Le opzioni e i valori vengono aggiornati in un prodotto configurabile quando si apportano modifiche a un prodotto secondario. <!--MDEE-835-->
![Nuovo](../assets/new.svg) è stata aggiunta la possibilità di includere dati di attributi di sistema aggiuntivi nel feed di attributi di prodotto.

## Versione 103.3.7

![Correzione](../assets/fix.svg) Sono state rimosse le dipendenze non necessarie dal modulo InventoryDataExporter.
![Correzione](../assets/fix.svg) versioni richieste modificate per i moduli inventario inclusi nel modulo CatalogInventoryDataExporter per supportare Adobe Commerce versione 2.4.4.

## Versione 103.3.6

![Correzione](../assets/fix.svg) sono stati corretti i deadlock che si verificavano durante la reindicizzazione del feed in modalità multithread. Le query sono ora separate in operazioni di inserimento e aggiornamento.
![Correzione](../assets/fix.svg) ottimizzata la query dei prezzi per cataloghi di grandi dimensioni con molti siti Web.
![Nuovo](../assets/new.svg) aggiunta della logica di esecuzione di un nuovo tentativo per rieseguire le transazioni non riuscite quando si verifica deadlock.

## Versione 103.3.5

![Correzione](../assets/fix.svg) Imposta la dipendenza per la versione più recente compatibile dell&#39;esportazione dei dati per il modulo comune SaaS.

![Correzione](../assets/fix.svg) L&#39;istanza `ScopeConfig` è stata sostituita con `ServiceConfigInterface` per supportare diverse configurazioni di servizio.

## Versione 103.3.4

![Correzione](../assets/fix.svg) Migliora la registrazione dell&#39;esportazione dei dati SaaS di Commerce aggiungendo ulteriori dettagli sul processo di reindicizzazione.

## Versione 103.3.3

L&#39;esportazione dei dati SaaS ![New](../assets/new.svg) ora memorizza nella cache gli attributi Entity-Attribute-Value (EAV) per la query dei metadati degli attributi.

![Correzione](../assets/fix.svg) è stato risolto un problema che impediva il salvataggio del feed `InventoryStockStatus` durante un nuovo tentativo se il prodotto era stato eliminato.

## Versione 103.3.2

![Correzione](../assets/fix.svg) è stato risolto un problema che causava l&#39;assenza del campo `modifiedAt` dai feed di entità rimossi.

## Versione 103.3.1

![Correzione](../assets/fix.svg) è stato risolto un problema che causava la visualizzazione di un messaggio `Invalid Template File` durante la reindicizzazione del feed dei prodotti quando Page Builder è installato.

## Versione 103.3.0

![Nuovo](../assets/new.svg) è stata eseguita la migrazione delle tabelle dei feed di esportazione immediata nella struttura unificata:
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![Nuovo](../assets/new.svg) ha eseguito la migrazione dei feed di catalogo e inventario alla soluzione di esportazione immediata.

![Nuovo](../assets/new.svg) ha rinominato i processi cron del feed di esportazione immediata in `*_feed_resend_failed_items`.

![Nuovo](../assets/new.svg) ha rinominato il feed di esportazione immediata e le tabelle di registro delle modifiche.

![Correzione](../assets/fix.svg) Imposta il campo `modified_at` nei dati del feed solo per i feed che lo richiedono.

![Correzione](../assets/fix.svg) Modificare la query `productAttributes` per recuperare solo gli attributi del prodotto.

## Versione 103.2.6

![Correzione](../assets/fix.svg) è stato risolto un problema che impediva la reindicizzazione dei feed quando le tabelle hanno un prefisso.

## Versione 103.2.5

![Correzione](../assets/fix.svg) Ottimizzata la query del prezzo.

## Versione 103.2.4

![Correzione](../assets/fix.svg) è stato corretto lo stato Stock errato visualizzato per un prodotto quando Commerce Inventory management è abilitato.

## Versione 103.2.3

![Correzione](../assets/fix.svg) prezzo speciale fisso a livello di sito Web.
![Correzione](../assets/fix.svg) aggiunto mutex per tutti i feed elaborati.


## Versione 103.2.2

![Correzione](../assets/fix.svg) Miglioramento della strategia di invio in batch dei feed per i cataloghi di grandi dimensioni. La tabella dei batch ora è compilata con un numero limitato di ID per ridurre l’utilizzo di memoria.

![Correzione](../assets/fix.svg) eliminata dipendenza rigida di CommerceInventoryDataExporter ai moduli MSI.

![Correzione](../assets/fix.svg) Sono stati migliorati `commerce-data-exporter` registri per raccogliere ulteriori informazioni e organizzarli in base a diverse fasi di esportazione.

## Versione 103.2.1

- È stata rilasciata la versione aggiornata.

## Versione 103.2.0

- È stata aggiunta la sincronizzazione di dati multi-thread per prodotti e prezzi.
