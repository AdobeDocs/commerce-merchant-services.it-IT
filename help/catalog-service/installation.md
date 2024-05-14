---
title: Onboarding e installazione
description: "Scopri come installare [!DNL Catalog Service]"
exl-id: 4e9fbdc9-67a1-4703-b8c0-8b159e0cc2a7
source-git-commit: c33ec5a10f9f2570e971e968efd1524e0d384ecd
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---

# Onboarding e installazione

Installa Catalog Service per richiedere e ricevere i dati di prodotto da un’istanza di Commerce utilizzando [API GraphQL di Catalog Service](https://developer.adobe.com/commerce/services/graphql/catalog-service/).

>[!NOTE]
>
>Se la tua istanza di Commerce utilizza Live Search o Product Recommendations, il Servizio catalogo viene installato o aggiornato automaticamente quando effettui l’onboarding o l’aggiornamento di tali servizi. Per ulteriori informazioni, vedere le istruzioni di installazione per [Live Search](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/live-search/install) e [Recommendations del prodotto](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/getting-started/install-configure).

>[!BEGINSHADEBOX]

## Prerequisiti

Il processo di onboarding per [!DNL Catalog Service] richiede l&#39;accesso alla riga di comando del server. Se non hai familiarità con l’utilizzo della riga di comando, chiedi aiuto a uno sviluppatore o a un integratore di sistemi.

**Requisiti software**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
- Compositore: 2.x

**Piattaforme supportate**

- Adobe Commerce sull’infrastruttura cloud: 2.4.4+
- Adobe Commerce on-premise: 2.4.4+

>[!ENDSHADEBOX]

## Endpoint

[!DNL Catalog Service] dispone di due endpoint disponibili per l’onboarding:

- Sandbox (`https://catalog-service-sandbox.adobe.io/graphql`): utilizzato per il test e la convalida prima della pubblicazione
- Produzione (`https://catalog-service.adobe.io/graphql`): utilizzato per il traffico in tempo reale per i rivenditori e i siti Web Commerce

Tutte le istanze di test di Commerce utilizzano l’endpoint Sandbox.

Esegui tutti i test di carico sull’endpoint Sandbox. Prima di iniziare il test di caricamento, invia una [Ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) in modo che il team dei servizi possa prevedere il traffico server aggiuntivo.

## Installazione e configurazione

Per iniziare a utilizzare [!DNL Catalog Service] per Adobe Commerce, sono necessari i seguenti passaggi:

- Installare le estensioni di esportazione dei dati
- Configurare il servizio e l’esportazione dei dati
- Accedere al servizio

### Installare le estensioni di esportazione dei dati

Per completare l&#39;operazione, è necessario avere accesso alla riga di comando del server [!DNL Catalog Service] processo di onboarding.

Il [!DNL Catalog Service] viene installato con le chiavi del Compositore, collegate all’account Commerce [`mageid`](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/) fornite durante il processo di abbonamento. Compositore utilizza queste chiavi durante l’installazione iniziale di Adobe Commerce o in situazioni in cui le chiavi del Compositore non sono state salvate in precedenza in un’istanza esterna `auth.json` file.

Consulta [Ottieni le chiavi di autenticazione](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) per ulteriori informazioni su come ottenere le chiavi del Compositore.

Il [!DNL Catalog Service] L&#39;estensione può essere installata sia sull&#39;infrastruttura cloud Adobe Commerce che sulle istanze locali.

>[!BEGINTABS]

>[!TAB Infrastruttura cloud]

Utilizzare questo metodo per installare [!DNL Catalog Service] estensione per un’istanza Commerce Cloud.

1. Sulla workstation locale, passa alla directory del progetto per il progetto Adobe Commerce su infrastruttura cloud.

   >[!NOTE]
   >
   >Per informazioni sulla gestione locale degli ambienti di progetto Commerce, vedi [Gestione dei rami con CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) nel _Guida utente di Adobe Commerce su infrastruttura cloud_.

1. Consulta il ramo dell’ambiente da aggiornare utilizzando Adobe Commerce Cloud CLI.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Aggiungi il modulo Catalog Service.

   ```bash
   composer require "magento/catalog-service" "^3.0.1" --no-update
   ```

1. Aggiornare le dipendenze del pacchetto.

   ```bash
   composer update "magento/catalog-service"
   ```

1. Modifiche al codice di commit e push per `composer.json` e `composer.lock` file.

1. Aggiungi, esegui il commit e invia le modifiche al codice per `composer.json` e `composer.lock` nell&#39;ambiente cloud.

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   Inviando gli aggiornamenti si avvia [Processo di distribuzione cloud Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) per applicare le modifiche. Controlla lo stato della distribuzione da [registro di distribuzione](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB On-premise]

Utilizzare questo metodo per installare [!DNL Catalog Service] estensione per un’istanza on-premise.

1. Utilizza Composer per aggiungere il modulo Catalog Service al progetto:

   ```bash
   composer require "magento/catalog-service" "^3.0.1"  --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update  "magento/catalog-service"
   ```

1. Aggiorna Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Cancella la cache:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >In alcuni casi, in particolare durante la distribuzione in produzione, potrebbe essere opportuno evitare di cancellare il codice compilato perché potrebbe richiedere del tempo. Prima di apportare qualsiasi modifica, assicurati di eseguire il backup del sistema.

>[!ENDTABS]

### Configurare il servizio e l’esportazione dei dati

Dopo aver installato [!DNL Catalog Service], completa le seguenti attività per integrare Catalog Service con la tua istanza di Adobe Commerce. Questa integrazione consente la sincronizzazione dei dati e la comunicazione tra l’istanza di Commerce, Catalog Service e altri servizi di supporto.

1. Configurare [Connettore Commerce Services](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas) specificando le chiavi API e selezionando uno spazio dati SaaS.

   La configurazione del Connettore servizi Commerce è un processo una tantum necessario per utilizzare i servizi Adobe Commerce come Catalog Service, Live Search e Product Recommendations. Se hai già configurato il connettore per un altro servizio, salta questo passaggio.

1. Eseguire una sincronizzazione iniziale dei dati da [Dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

   La sincronizzazione iniziale potrebbe richiedere da alcuni minuti ad ore, a seconda della dimensione del catalogo. Puoi monitorare lo stato della sincronizzazione dal dashboard Gestione dati. Dopo la sincronizzazione iniziale, il catalogo esporta i dati dei prodotti su base continuativa per mantenere aggiornati i servizi.

Per garantire il corretto funzionamento dell’esportazione del catalogo:

- [Verificare che i processi cron siano in esecuzione](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Verificare che gli indicizzatori siano in esecuzione da [Amministratore](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) oppure utilizzando il comando CLI di Commerce `bin/magento indexer:info`.
- Verificare che `Catalog Attributes Feed, Product Feed, Product Overrides Feed`, e `Product Variant Feed` gli indici sono impostati su `Update by Schedule`.

### Accedere al servizio

Il [!DNL Catalog Service] L’API di GraphQL è accessibile dalla sezione ` https://catalog-service.adobe.io/graphql` endpoint che utilizza i comandi POST su HTTPS.

Nelle query GraphQL, devi specificare più intestazioni HTTP, inclusa la chiave API pubblica aggiunta alla configurazione del connettore di servizi Adobe Commerce nell’amministratore. Per ulteriori informazioni, vedere [GraphQL servizi Storefront](https://developer.adobe.com/commerce/services/graphql/) documentazione.

### Configurazione del firewall

Per consentire [!DNL Catalog Service] tramite un firewall, aggiungi `commerce.adobe.io` al inserisco nell&#39;elenco Consentiti di.

## Catalog Service e Mesh API

Il [Mesh API per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) consente agli sviluppatori di integrare API private o di terze parti e altre interfacce con i prodotti Adobe utilizzando Adobe IO.

Consulta la [[!DNL Catalog Service] e Mesh API](mesh.md) argomento per i dettagli di installazione e configurazione.

## Dashboard di gestione dati

Per ulteriori informazioni su [!DNL Catalog Service] sincronizzazione dei dati, consulta [Dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).
