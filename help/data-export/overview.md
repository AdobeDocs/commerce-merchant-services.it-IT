---
title: "[!DNL SaaS Data Export Guide]"
description: "Scopri come utilizzare la [!DNL data export] estensione per i servizi SaaS di Adobe Commerce che sincronizza i dati tra Adobe Commerce e i servizi Commerce connessi."
role: Admin, Developer
recommendations: noCatalog
source-git-commit: 8230756c203cb2b4bdb4949f116c398fcaab84ff
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Guida [!DNL SaaS Data Export]

[!DNL SaaS data export] migliora le prestazioni front-end ottimizzando la sincronizzazione dei dati tra un’istanza di Adobe Commerce e i servizi Commerce connessi. Quando aggiungi Live Search, Product Recommendations o Catalog Service a un’installazione di Adobe Commerce, il [!DNL Data export] L&#39;estensione viene installata automaticamente.

L’esportazione di dati SaaS raccoglie ed esporta vari tipi di dati, denominati _feed_, che aggregano tipi specifici di informazioni. A seconda dei servizi Commerce installati, i feed di esportazione dei dati SaaS includono:

- **Feed entità catalogo** dati aggregati sui prodotti. I dati includono prodotti, attributi del prodotto, prezzi dei prodotti, varianti dei prodotti, categorie, autorizzazioni per le categorie e autorizzazioni per i prodotti.
- Il **Feed ambiti** aggrega i dati per i gruppi di clienti, i siti web, gli store e le visualizzazioni dello store.
- Il **Feed ordine cliente** aggrega i dati relativi agli ordini, incluse le entità correlate quali fatture, spedizioni, note di accredito e così via.
- Il **Feed inventario multi-sorgente** aggrega i dati relativi agli elementi dello stato delle scorte.

L’estensione per l’esportazione dei dati supporta diversi metodi per avviare e gestire il processo di sincronizzazione dei dati.

- **Sincronizzazione manuale dall’amministratore o dalla riga di comando**

   - Il [Dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) in Commerce Admin fornisce una visualizzazione grafica dello stato di sincronizzazione. È possibile utilizzare il dashboard per eseguire una risincronizzazione completa (_sincronizzazione completa_) di tutti i feed. Tuttavia, in Adobe si consiglia di eseguire una sincronizzazione completa solo la prima volta che si connette Adobe Commerce a un servizio Commerce. Consulta [Processo di sincronizzazione](data-synchronization.md).

   - Il [strumento da riga di comando di Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) fornisce comandi per sincronizzare feed specifici e include opzioni aggiuntive per personalizzare l’elaborazione dei feed.

- **Sincronizzazione automatizzata con processi cron**

   - [Sincronizzazione parziale dei dati](data-synchronization.md#partial-synchronization-with-cron-jobs)- I processi Cron attivano una sincronizzazione parziale dei dati quando un utente amministratore di Commerce aggiorna un&#39;entità. Il processo di esportazione dei dati invia solo questi aggiornamenti ai servizi Commerce connessi. Il processo di sincronizzazione parziale si basa sul meccanismo MView e non richiede alcuna azione da parte dell&#39;utente amministratore o dell&#39;integratore di sistema.

   - [Nuovo tentativo automatico per errori di sincronizzazione](data-synchronization.md#failed-items-sync-for-error-recovery)- I processi Cron attivano un nuovo tentativo automatico di sincronizzazione quando si verificano errori durante il processo di sincronizzazione dei dati.

- **Esporta pianificazione e prestazioni**

   - Sviluppatori e integratori di sistemi possono stimare il tempo necessario all’esportazione di dati SaaS per sincronizzare i dati tra Adobe Commerce e i servizi connessi. Questa stima può aiutare a pianificare l’elaborazione dell’esportazione dei dati per evitare interruzioni del sito. Consulta [Stima del volume dei dati e del tempo di trasmissione](estimate-data-volume-sync-time.md).

   - Nei casi in cui la sincronizzazione deve essere eseguita più rapidamente, l’esportazione dei dati SaaS offre opzioni di personalizzazione per migliorare le prestazioni di elaborazione delle esportazioni. Consulta [Migliorare le prestazioni di esportazione dei dati](customize-export-processing.md).

- **Tracciare e risolvere i problemi relativi alle attività di esportazione dei dati**: utilizza i registri di esportazione dei dati e saas per esaminare lo stato di sincronizzazione e i payload di feed durante il processo di sincronizzazione e indicizzazione. Consulta [Registrazione e risoluzione dei problemi](troubleshooting-logging.md).



