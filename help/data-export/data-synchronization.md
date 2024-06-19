---
title: Sincronizzare i dati con l’esportazione di dati SaaS
description: "Scopri come [!DNL SaaS Data Export] raccoglie e sincronizza i dati tra le istanze di Adobe Commerce e i servizi SaaS connessi."
role: Admin, Developer
recommendations: noCatalog
source-git-commit: 8230756c203cb2b4bdb4949f116c398fcaab84ff
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# Sincronizzare i dati con l’esportazione di dati SaaS

Quando installi un servizio Commerce che richiede l’esportazione di dati come Catalog Service, Live Search o Product Recommendations, viene installata una raccolta di moduli Saas per l’esportazione dei dati, al fine di gestire il processo di raccolta e sincronizzazione dei dati. Il diagramma seguente mostra il flusso di esportazione dei dati SaaS.

![Flusso di raccolta e sincronizzazione dell’esportazione dei dati SaaS per Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

I componenti principali del flusso di esportazione dei dati SaaS includono:

- Moduli SaaS per l’esportazione dei dati che raccolgono i dati per i feed da Adobe Commerce, assemblano gli elementi dei feed, ascoltano gli aggiornamenti e mantengono lo stato dei feed.
- I moduli SaaS esportano i dati, configurano il routing e pubblicano i feed nei servizi connessi.
- Il servizio Adobe Commerce gestisce il processo di acquisizione dei dati per convalidare i feed in arrivo e mantenere gli aggiornamenti ai servizi connessi.

## Modalità di sincronizzazione

L’esportazione di dati SaaS prevede due modalità per elaborare i feed di entità:

- **Modalità di esportazione immediata**- In questa modalità, i dati vengono raccolti e inviati immediatamente al servizio Commerce in una singola iterazione. Questa modalità accelera la distribuzione degli aggiornamenti delle entità al servizio Commerce e riduce le dimensioni di archiviazione delle tabelle di feed.

- **Modalità di esportazione legacy**- In questa modalità, i dati vengono raccolti in un unico processo. Successivamente, un processo cron invia i dati raccolti ai servizi commerce connessi. Nelle voci del registro di esportazione dei dati, i feed che utilizzano la modalità legacy sono etichettati `(legacy)`.

## Tipi di sincronizzazione

L&#39;esportazione dei dati SaaS supporta tre tipi di sincronizzazione: sincronizzazione completa, sincronizzazione parziale e nuovo tentativo di sincronizzazione degli elementi non riusciti.

### Sincronizzazione completa

Dopo aver collegato un’istanza di Adobe Commerce al servizio Commerce, esegui una sincronizzazione completa per inviare i dati del feed di entità da Adobe Commerce al servizio connesso.

>[!NOTE]
>
>La sincronizzazione completa è principalmente destinata alla fase di onboarding. Evita l’uso regolare per evitare il sovraccarico del database. Dopo la sincronizzazione iniziale, le modifiche in corso vengono sincronizzate automaticamente utilizzando la sincronizzazione parziale.

### Sincronizzazione parziale

Con la sincronizzazione parziale, l’esportazione di dati SaaS invia automaticamente aggiornamenti dall’applicazione Commerce, come modifiche al nome del prodotto o aggiornamenti dei prezzi, ai servizi commerce connessi.

Il processo di esportazione dei dati utilizza i seguenti processi cron per automatizzare l’operazione di sincronizzazione parziale.

- processi del gruppo cron &quot;index&quot;:
   - Il `indexer_reindex_all_invalid` il processo reindicizza tutti i feed non validi. È un processo cron standard di Adobe Commerce.
   - Il `saas_data_exporter` il processo è per i feed di esportazione legacy.
   - Il `sales_data_exporter` processo specifico per il feed di esportazione dei dati di vendita.

Questi processi vengono eseguiti ogni minuto.

Affinché la sincronizzazione parziale funzioni, l&#39;applicazione Commerce richiede la seguente configurazione:

- [La pianificazione delle attività è abilitata tramite processi cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)

- Tutti gli indici di esportazione dei dati SaaS sono configurati in `Update by Schedule` modalità.

  Nella versione 103.1.0 e successive dell’esportazione di dati SaaS, `Update by Schedule` è attivata per impostazione predefinita. È possibile verificare la configurazione dell&#39;indice sul server utilizzando il comando CLI di Commerce, `bin/magento indexer:show-mode | grep -i feed`

### Ritenta sincronizzazione elementi non riusciti

La sincronizzazione di Riprova elementi non riusciti utilizza un processo separato per inviare nuovamente gli elementi non sincronizzati a causa di errori durante il processo di sincronizzazione, ad esempio un errore dell&#39;applicazione, un&#39;interruzione della rete o un errore del servizio SaaS. L’implementazione per questa sincronizzazione si basa anche su processi cron.

- `resync_failed_feeds_data_exporter` processi del gruppo cron:
   - Il `<feed name>_feed_resend_failed_feeds_items` il processo invia nuovamente gli elementi non sincronizzati, ad esempio `products_feed_resend_failed_items`.

### Visualizzare e gestire il processo di sincronizzazione

La maggior parte delle attività di sincronizzazione viene elaborata automaticamente in base alla configurazione dell’applicazione. Tuttavia, l’esportazione di dati SaaS fornisce anche strumenti per gestire il processo.

- Gli utenti amministratori possono visualizzare e tenere traccia dell’avanzamento della sincronizzazione e ottenere informazioni sui dati da [Dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

- Sviluppatori, integratori di sistemi o amministratori con accesso al server applicazioni Commerce possono gestire il processo di sincronizzazione e i feed di dati utilizzando lo strumento da riga di comando (CLI) di Adobe Commerce. Consulta [Riferimento comando esportazione dati](data-export-cli-commands.md).

### Verificare la configurazione dell&#39;applicazione Commerce

La sincronizzazione parziale e il tentativo di riesecuzione degli elementi non riusciti funzionano solo se l&#39;istanza di Commerce è stata configurata correttamente. In genere, la configurazione viene completata al momento della configurazione del servizio Commerce. Se l’esportazione dei dati non funziona correttamente, verifica la seguente configurazione.

- [Verificare che i processi cron siano in esecuzione](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).

- Verificare che gli indicizzatori siano in esecuzione da [Amministratore](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) oppure utilizzando il comando CLI di Commerce `bin/magento indexer:info`.

- Verifica che gli indicizzatori per i seguenti feed siano impostati su `Update by Schedule`: attributi del catalogo, prodotto, sostituzioni prodotto e variante prodotto. Puoi controllare gli indicizzatori da [Gestione indice](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) nell’amministratore o utilizzando CLI (`bin/magento indexer:show-mode | grep -i feed`).
