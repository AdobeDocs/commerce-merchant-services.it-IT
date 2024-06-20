---
title: Sincronizzazione catalogo
description: Scopri come esportare i dati di prodotto da [!DNL Commerce] server a [!DNL Commerce Services].
exl-id: 19d29731-097c-4f5f-b8c0-12f9c91848ac
feature: Catalog Management, Data Import/Export, Catalog Service
source-git-commit: af9de40a717d2cb55a5f42483bd0e4cbcd913f64
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Sincronizzazione catalogo

>[!NOTE]
>
> Il Dashboard di sincronizzazione del catalogo è ora il Dashboard di gestione dati. Questo dashboard rinnovato ora supporta [[!DNL Product Recommendations]](../product-recommendations/guide-overview.md), [[!DNL Live Search]](../live-search/overview.md), e [[!DNL Catalog Service]](../catalog-service/overview.md). I clienti possono ottenere Data Management Dashboard aggiornando all’ultima versione di uno di questi servizi. Per ulteriori informazioni, consulta [Dashboard di gestione dati](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html) documentazione. Questo argomento corrente rimane valido per gli utenti che devono ancora effettuare l’aggiornamento e che dispongono ancora della dashboard Sincronizzazione catalogo.

Adobe Commerce utilizza gli indicizzatori per compilare i dati del catalogo nelle tabelle. Il processo viene attivato automaticamente da [Eventi](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html#events-that-trigger-full-reindexing) ad esempio una modifica al prezzo di un prodotto o al livello di magazzino.

Il servizio di sincronizzazione catalogo sposta i dati del prodotto da un [!DNL Adobe Commerce] istanza al [!DNL Commerce Services] su base continuativa per mantenere i dati aggiornati. Ad esempio: [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) richiede informazioni sul catalogo correnti per restituire in modo accurato i consigli con nomi, prezzi e disponibilità corretti. Utilizza il _Sincronizzazione catalogo_ dashboard per osservare e gestire il processo di sincronizzazione o l’interfaccia della riga di comando per attivare la sincronizzazione di un catalogo e reindicizzare i dati del prodotto per l’utilizzo da parte di [!DNL Commerce Services]. Consulta [Riferimento interfaccia della riga di comando](../data-export/data-export-cli-commands.md) nel _Esportazione dati SaaS_ Guida.

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

Il processo di sincronizzazione del catalogo viene eseguito automaticamente ogni ora. Se non trovi i prodotti previsti nella vetrina o se i prodotti non riflettono le modifiche recenti apportate, puoi risolvere [problemi di sincronizzazione catalogo](#resolvesync).

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

Consulta [Registri e risoluzione dei problemi](../data-export/troubleshooting-logging.md#troubleshooting) nel _Guida all’esportazione dei dati SaaS_.
