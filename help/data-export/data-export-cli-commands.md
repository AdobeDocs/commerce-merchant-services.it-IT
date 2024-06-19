---
title: Interfaccia della riga di comando per l'esportazione dei dati SaaS
description: "Scopri come utilizzare i comandi dell’interfaccia della riga di comando per gestire feed e processi per [!DNL data export extension] per i servizi SaaS di Adobe Commerce."
recommendations: noCatalog
source-git-commit: 8230756c203cb2b4bdb4949f116c398fcaab84ff
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Riferimento all&#39;interfaccia della riga di comando per l&#39;esportazione di dati SaaS

Sviluppatori e amministratori di sistema possono gestire le operazioni di sincronizzazione per l’esportazione di dati SaaS utilizzando [strumento da riga di comando di Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) Il `saas:resync` è incluso nel `magento/saas-export` pacchetto.

L’Adobe non consiglia di utilizzare il `saas:resync` comandare regolarmente. Gli scenari tipici per l’utilizzo del comando sono:

- Sincronizzazione iniziale
- Il [ID spazio dati SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) è stato modificato ed è necessario sincronizzare i dati con il nuovo spazio dati.
- Risoluzione dei problemi

## Sincronizzazione iniziale

Quando si attiva una `saas:resync` dalla riga di comando, a seconda delle dimensioni del catalogo, l&#39;aggiornamento dei dati può richiedere da alcuni minuti a poche ore.

>[!NOTE]
>Se utilizzi Live Search o Product Recommendations, non è necessario avviare la sincronizzazione. Il processo viene avviato automaticamente dopo la connessione del servizio all’istanza di Commerce.

## Esempi di comandi

Prima di utilizzare `saas:resync` comandi, controlla [descrizioni delle opzioni](#command-options).

- Eseguire una risincronizzazione completa per un feed di entità.

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  I feed già esportati non vengono risincronizzati.

- Risincronizzazione completa del feed specificato e dei dati di pulizia

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  Da utilizzare solo dopo aver eseguito una [!DNL Data Space ID Cleanup] operazione.

- Per i feed di esportazione immediati, invia nuovamente tutti i dati ai servizi Commerce connessi senza troncare i dati di indice nella tabella dei feed

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- Elenca i comandi e le opzioni disponibili con le relative descrizioni.

  ```
  bin/magento saas:resync --help
  ```

## Opzioni di comando

Per la gestione di sono disponibili le seguenti opzioni `saas:resync` operazioni.

>[!NOTE]
>
>Il `saas:resync` Il comando supporta anche opzioni avanzate per migliorare i comandi di esportazione dei dati aumentando le dimensioni del batch e aggiungendo l&#39;elaborazione multi-thread. Consulta [Personalizza elaborazione esportazione](customize-export-processing.md).

### `feed`

Questa opzione obbligatoria specifica l’entità feed da risincronizzare, ad esempio `products`.

Il `feed` il valore dell’opzione può includere uno qualsiasi dei feed di entità disponibili:

- `products`: feed dati prodotto
- `productAttributes`: feed dati per attributi di prodotto
- `categories`: feed dati per categorie
- `variants`: feed dati delle varianti di prodotto configurabili
- `prices`: feed di dati sui prezzi dei prodotti
- `categoryPermissions`: feed dati per autorizzazioni categoria
- `productOverrides`: feed dati per autorizzazioni prodotto
- `inventoryStockStatus`: feed dati stato scorte di magazzino
- `scopesWebsite`: siti web con store e feed dati per visualizzazioni store
- `scopesCustomerGroup`: feed dati di gruppi di clienti
- `orders`: feed dati ordini cliente

A seconda di quale [Servizi Commerce](../landing/saas.md) , è possibile che sia disponibile un diverso set di feed per `saas:resync` comando.

### `no-reindex`

Questa opzione invia nuovamente i dati del catalogo esistenti a [!DNL Commerce Services] senza reindicizzazione. Se questa opzione non è specificata, il comando esegue una reindicizzazione completa prima di sincronizzare i dati.

Il comportamento di questa opzione dipende dal fatto che il feed venga esportato o meno in [modalità di esportazione legacy o immediata](data-synchronization.md#synchronization-modes)

- Per i feed di esportazione legacy, il processo di sincronizzazione non tronca i dati indicizzati nella tabella dei feed. Al contrario, invia nuovamente tutti i dati al servizio Adobe Commerce.
- Per i feed di esportazione immediati, questa opzione viene ignorata se specificata. Per questi feed, il processo di risincronizzazione non troncerà l&#39;indice e risincronizza solo gli aggiornamenti o gli elementi con errori precedenti.

### `cleanup`

Questa opzione consente di pulire la tabella dell’indicizzatore del feed prima di una sincronizzazione. Se specificato, l&#39;esportazione dei dati SaaS esegue una risincronizzazione completa per il feed specificato e pulisce tutti i dati esistenti nella tabella dei feed.

L’Adobe consiglia di utilizzare questo comando solo dopo aver eseguito [!DNL Data Space ID Cleanup] operazione.

>[!WARNING]
>
>**Non utilizzare questa opzione regolarmente**. Può causare problemi di sincronizzazione dei dati nei servizi Adobe Commerce. Ad esempio, il `delete product event` potrebbe non propagarsi al servizio Adobe Commerce se `cleanup` viene utilizzata l&#39;opzione.

## Risoluzione dei problemi

Se non trovi i dati previsti nei servizi Commerce connessi, puoi risolvere i problemi consultando i registri degli errori di esportazione dei dati e utilizzando `saas:resync` con variabili di ambiente per rivedere payload e dati del profiler. Consulta [Revisione dei registri e risoluzione dei problemi](troubleshooting-logging.md).
