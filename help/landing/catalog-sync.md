---
title: Sincronizzazione catalogo
description: Scopri come esportare i dati di prodotto da [!DNL Commerce] server a [!DNL Commerce Services].
exl-id: 19d29731-097c-4f5f-b8c0-12f9c91848ac
feature: Catalog Management, Data Import/Export, Catalog Service
source-git-commit: 6513fd6dce9648407b0878785f5f59f9f39cd5e1
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---


# Sincronizzazione catalogo

>[!NOTE]
>
> Il Dashboard di sincronizzazione del catalogo è ora il Dashboard di gestione dati. Questo dashboard rinnovato ora supporta [!DNL Product Recommendations], [!DNL Live Search], e [!DNL Catalog Service]. I clienti possono ottenere Data Management Dashboard aggiornando all’ultima versione di uno di questi servizi. Per ulteriori informazioni, consulta [Dashboard di gestione dati](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html) documentazione. Questo argomento corrente rimane valido per gli utenti che devono ancora effettuare l’aggiornamento e che dispongono ancora della dashboard Sincronizzazione catalogo.

Adobe Commerce utilizza gli indicizzatori per compilare i dati del catalogo nelle tabelle. Il processo viene attivato automaticamente da [Eventi](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html#events-that-trigger-full-reindexing) ad esempio una modifica al prezzo di un prodotto o al livello di magazzino.

Il servizio di sincronizzazione catalogo sposta i dati del prodotto da un [!DNL Adobe Commerce] istanza al [!DNL Commerce Services] su base continuativa per mantenere i dati aggiornati. Ad esempio: [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) richiede informazioni sul catalogo correnti per restituire in modo accurato i consigli con nomi, prezzi e disponibilità corretti. Utilizza il _Sincronizzazione catalogo_ dashboard per osservare e gestire il processo di sincronizzazione o [interfaccia della riga di comando](#resynccmdline) per attivare la sincronizzazione di un catalogo e reindicizzare i dati di prodotto per l&#39;utilizzo da parte di [!DNL Commerce Services].

## Accesso al dashboard di sincronizzazione del catalogo

Per accedere al dashboard Sincronizzazione catalogo, seleziona **Sistema** > _Trasferimento dati_ > **Sincronizzazione catalogo**.

Con il **Sincronizzazione catalogo** dashboard è possibile:

- Visualizza stato di sincronizzazione (**In corso**, **Completato**, **Non riuscito**)
- Visualizza il numero totale di prodotti sincronizzati
- Cerca i prodotti sincronizzati per visualizzarne lo stato corrente
- Cerca nel catalogo del negozio per nome, SKU, ecc.
- Visualizza i dettagli del prodotto sincronizzato in JSON per diagnosticare una discrepanza di sincronizzazione
- Riavvia il processo di sincronizzazione

### Ultima sincronizzazione

Segnala uno stato di sincronizzazione di:

- **Completato** - Visualizza la data e l&#39;ora di completamento della sincronizzazione e il numero di prodotti aggiornati
- **Non riuscito** - Visualizza la data e l&#39;ora del tentativo di sincronizzazione
- **In corso** - Visualizza la data e l&#39;ora dell&#39;ultima sincronizzazione riuscita

Il processo di sincronizzazione del catalogo viene eseguito tramite il processo cron. Se non trovi i prodotti previsti nella vetrina o se i prodotti non riflettono le modifiche recenti apportate, puoi risolvere [problemi di sincronizzazione catalogo](#resolvesync).

### Prodotti sincronizzati

Visualizza il numero totale di prodotti sincronizzati dal [!DNL Commerce] catalogo. Dopo la sincronizzazione iniziale, solo i prodotti modificati devono essere sincronizzati.

## Risincronizza {#resync}

Se è necessario avviare una risincronizzazione del catalogo prima che venga eseguita la sincronizzazione oraria pianificata, è possibile forzare una risincronizzazione.

>[!NOTE]
>
> L&#39;imposizione di una risincronizzazione attiva una risincronizzazione dell&#39;intero catalogo prodotti, che può aumentare il carico sulle risorse hardware.

1. Dalla sezione _Sincronizzazione catalogo_ dashboard, seleziona **Impostazioni**.

   Il _Impostazioni sincronizzazione catalogo_ viene visualizzata.

1. In _Risincronizza dati_ , fare clic su [!UICONTROL Resync].

   [!DNL Commerce] sincronizza il catalogo durante la successiva finestra di sincronizzazione pianificata. A seconda delle dimensioni del catalogo, questa operazione può richiedere molto tempo.

## Prodotti catalogo sincronizzati

Il **Prodotti catalogo sincronizzati** nella tabella vengono visualizzate le informazioni seguenti.

| Campo | Descrizione |
|---|---|
| ID | Identificatore univoco del prodotto |
| Nome | Nome vetrina del prodotto |
| Tipo | Identifica il tipo di prodotto, ad esempio semplice, configurabile o scaricabile |
| Ultima esportazione | Data dell’ultima esportazione del prodotto dal catalogo |
| Ultima modifica | Data dell’ultima modifica del prodotto nel catalogo |
| SKU | Visualizza l&#39;unità di gestione delle scorte per il prodotto |
| Prezzo | Prezzo del prodotto |
| Visibilità | L’impostazione di visibilità di un prodotto, definita nella sezione [!DNL Commerce] catalogo |

## Risolvi problemi di sincronizzazione catalogo {#resolvesync}

Quando attivi una risincronizzazione dei dati, l’aggiornamento dei dati potrebbe richiedere fino a un’ora e potrebbe essere incluso nei componenti dell’interfaccia utente, ad esempio le unità per i consigli. Se riscontri ancora delle discrepanze tra il catalogo e i dati nella vetrina, o se la sincronizzazione del catalogo non è riuscita, fai riferimento a quanto segue:

### Discrepanza dei dati

1. Visualizzare la visualizzazione dettagliata del prodotto in questione nei risultati della ricerca.
1. Copia l’output JSON e verifica che il contenuto corrisponda a quello presente in [!DNL Commerce] catalogo.
1. Se il contenuto non corrisponde, apporta una piccola modifica al prodotto nel catalogo, ad esempio aggiungendo uno spazio o un punto.
1. Attendere la risincronizzazione o [attivare una risincronizzazione manuale](#resync).

### Sincronizzazione non in esecuzione

Se la sincronizzazione non è in esecuzione su una pianificazione o non è stato sincronizzato nulla, vedere [KnowledgeBase](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html) articolo.

### Sincronizzazione non riuscita

Se lo stato della sincronizzazione del catalogo è **Non riuscito**, invia una [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

## Interfaccia della riga di comando {#resynccmdline}

Il `saas:resync` il comando fa parte del `magento/saas-export` ed è disponibile con una delle opzioni [!DNL Commerce Services] prodotti, come [[!DNL Product Recommendations]](/help/product-recommendations/install-configure.md) o [[!DNL Live Search]](/help/live-search/install.md).

>[!NOTE]
>
> Quando si esegue una sincronizzazione dati per la prima volta, eseguire `productattributes` primo feed, seguito da `productoverrides`, prima di eseguire `products` feed.

Opzioni comando:

```bash
bin/magento saas:resync --feed <feed name> [no-reindex|cleanup-feed]
```

La tabella seguente descrive `saas:resync` parametri e descrizioni.

| Parametro | Descrizione | Obbligatorio |
|---| ---| ---|
| `feed` | Specifica l&#39;entità da risincronizzare, ad esempio `products` | Sì |
| `no-reindex` | Invia nuovamente i dati del catalogo esistenti a [!DNL Commerce Services] senza reindicizzazione. Se questo parametro non è specificato, il comando esegue una reindicizzazione completa prima di sincronizzare i dati. | No |
| `cleanup-feed` | Pulire la tabella dell&#39;indicizzatore del feed prima di una sincronizzazione. | No |

Il nome del feed può essere uno dei seguenti:

- `products`— Prodotti nel catalogo
- `productattributes`— Attributi del prodotto come `activity`, `gender`, `tops`, `bottoms`, e così via
- `variants`— varianti di prodotto di un prodotto configurabile, ad esempio colore e dimensioni
- `prices` — Prezzi dei prodotti
- `scopesCustomerGroup` — Gruppi di clienti
- `scopesWebsite` — Siti Web con visualizzazioni dello store
- `categories`— Categorie nel catalogo
- `categoryPermissions` - Autorizzazioni per ciascuna categoria
- `productoverrides`regole specifiche per il cliente per la visibilità dei prezzi e dei cataloghi, ad esempio quelle basate sulle autorizzazioni per le categorie

A seconda di quale [Servizi Commerce](../landing/saas.md) , potrebbero essere disponibili diversi tipi di feed per `saas:resync` comando.

Non è consigliabile eseguire il comando `saas:resync` comando su base regolare. Potrebbe essere necessario eseguire manualmente il comando in due scenari:

- Sincronizzazione iniziale
- Il [ID spazio dati SaaS](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html) è stato modificato

### Sincronizzazione iniziale

Quando si attiva una `saas:resync` dalla riga di comando, a seconda delle dimensioni del catalogo, l&#39;aggiornamento dei dati potrebbe richiedere da alcuni minuti a alcune ore.

Per la sincronizzazione iniziale, si consiglia di eseguire i comandi nel seguente ordine:

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions 
```

### Risoluzione dei problemi

Se non trovi i dati previsti in [!DNL Commerce Service], verifica se si è verificato un problema durante la sincronizzazione da [!DNL Adobe Commerce] istanza al [!DNL Commerce Service] piattaforma.

In sono presenti due file di registro `var/log/` directory:

- `commerce-data-export-errors.log` - in caso di errore durante _raccolta_ fase
- `saas-export-errors.log` - in caso di errore durante _trasmissione_ fase

#### Verifica payload del feed

Può essere utile visualizzare il payload del feed inviato al [!DNL Commerce Service]. Questo può essere fatto passando la variabile di ambiente `EXPORTER_EXTENDED_LOG=1`. Il `no-reindex` Il flag indica che vengono inviati solo i dati attualmente raccolti.

```bash
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products --no-reindex
```

Il payload è disponibile in `var/log/saas-export.log`.

#### Mantieni payload nella tabella dell’indice del feed

A partire da `magento/module-data-exporter:103.0.0` alcuni feed: feed di prodotto, feed di prezzo, mantengono solo i dati minimi richiesti nella tabella dell’indice.

In produzione, non è consigliabile mantenere i dati di payload nella tabella di indice, ma questo può essere utile in un’istanza di sviluppo. Questo viene fatto passando il `PERSIST_EXPORTED_FEED=1` variabile di ambiente:

```bash
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

#### Profilatura

Se il processo di reindicizzazione di un feed specifico richiede un tempo eccessivo, esegui il profiler per raccogliere dati aggiuntivi che potrebbero essere utili per il team di supporto. Per farlo, trasmettere il `EXPORTER_PROFILER=1`variabile di ambiente:

```bash
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

I dati del profiler vengono memorizzati in `var/log/commerce-data-export.log` con il formato:

`<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>`

#### Inviare una richiesta di supporto

Se vengono visualizzati errori non correlati alla configurazione o alle estensioni di terze parti, invia una [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) con quante più informazioni possibili.
