---
title: Onboarding e installazione
description: "Scopri come installare [!DNL Catalog Service]"
exl-id: 4e9fbdc9-67a1-4703-b8c0-8b159e0cc2a7
source-git-commit: 6a7efbe0424e35cdec9cb00275d9a953feccaa5b
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Onboarding e installazione

I seguenti video ti guidano attraverso la [!DNL Catalog Service] processo.

**Parte 1**: onboarding e installazione

>[!VIDEO](https://video.tv.adobe.com/v/3415599)

**Parte 2**: utilizzo di [!DNL Catalog Service]

>[!VIDEO](https://video.tv.adobe.com/v/3415600)

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
- Produzione (`https://catalog-service.adobe.io/graphql`): utilizzato per il traffico in tempo reale per i commercianti e i siti web di Commerce

Tutte le istanze di test di Commerce devono utilizzare l’endpoint Sandbox.

Il test di carico deve essere eseguito solo sull’endpoint Sandbox. Si consiglia di: [Ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) essere aperto al momento del test di carico in modo che il team dei servizi possa prevedere il traffico server aggiuntivo.

## Installazione e configurazione

Per iniziare a utilizzare [!DNL Catalog Service] per Adobe Commerce, sono necessari i seguenti passaggi:

- Installare le estensioni di esportazione dei dati
- Configurare il servizio e l’esportazione dei dati
- Accedere al servizio

### Installare le estensioni di esportazione dei dati

Il processo di onboarding per [!DNL Catalog Service] richiede l&#39;accesso alla riga di comando del server.

Il [!DNL Catalog Service] L&#39;estensione può essere installata sia sull&#39;infrastruttura cloud Adobe Commerce che sulle istanze locali.

Il [!DNL Catalog Service] viene installato con le chiavi del Compositore, collegate all’account Commerce [`mageid`](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/) fornite durante il processo di abbonamento. Compositore utilizza queste chiavi durante l’installazione iniziale di Adobe Commerce o in situazioni in cui le chiavi del Compositore non sono state salvate in precedenza in un’istanza esterna `auth.json` file.

Consulta [Ottieni le chiavi di autenticazione](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) per ulteriori informazioni su come ottenere le chiavi del Compositore.

#### Adobe Commerce sull’infrastruttura cloud

Utilizzare questo metodo per installare [!DNL Catalog Service] estensione per un’istanza Commerce Cloud.

1. Sulla workstation locale, passa alla directory del progetto.
1. Aggiungi il modulo Catalog Service.

   ```bash
   composer require "magento/catalog-service" "^3.0.1"
   ```

1. Aggiornare le dipendenze del pacchetto.

   ```bash
   composer update
   ```

1. Modifiche al codice di commit e push per `composer.json` e `composer.lock` file.

#### On-premise

Utilizzare questo metodo per installare [!DNL Catalog Service] estensione per un’istanza on-premise.

1. Utilizza Composer per aggiungere il modulo Catalog Service al progetto:

   ```bash
   composer require "magento/catalog-service" "^3.0.1"
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update
   ```

1. Aggiorna Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Cancella la cache:

   ```bash
   bin/magento cache:clean
   ```

### Configurare il servizio e l’esportazione dei dati

Dopo l’installazione [!DNL Catalog Service], è necessario configurare [Connettore Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html#apikey) specificando le chiavi API e selezionando uno spazio dati SaaS.

Al termine della configurazione SaaS, eseguire una sincronizzazione iniziale dei dati seguendo [Sincronizzazione catalogo](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/data-services/catalog-sync.html) guida.

Per garantire il corretto funzionamento dell’esportazione del catalogo:

- Verificare che i processi cron siano in esecuzione.
- Verificare che gli indicizzatori siano in esecuzione.
- Assicurati che `Catalog Attributes Feed, Product Feed, Product Overrides Feed`, e `Product Variant Feed` Gli indicizzatori sono impostati su &quot;Aggiorna per pianificazione&quot;.

La sincronizzazione iniziale potrebbe richiedere da alcuni minuti ad ore, a seconda della dimensione del catalogo. Dopo la sincronizzazione iniziale, il catalogo esporta i dati dei prodotti dal server Commerce ai servizi Commerce su base continuativa per mantenere aggiornati i servizi. Per monitorare lo stato della sincronizzazione, consultare [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html).

### Accedere al servizio

Il [!DNL Catalog Service] L’API è accessibile tramite comandi POST tramite HTTPS.

Per ottenere la chiave API, vai all’area Commerce Service Connector nell’amministratore e copia la chiave API pubblica.

Leggi le [Documentazione di GraphQL](https://developer.adobe.com/commerce/services/graphql/) per scoprire come eseguire query e inviare le intestazioni necessarie per generare le richieste API.

Per consentire [!DNL Catalog Service] tramite un firewall, aggiungi `commerce.adobe.io` al inserisco nell&#39;elenco Consentiti di.

## Catalog Service e Mesh API

Il [Mesh API per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) consente agli sviluppatori di integrare API private o di terze parti e altre interfacce con i prodotti Adobe utilizzando Adobe IO.

Consulta la  [[!DNL Catalog Service] e Mesh API](mesh.md) argomento per i dettagli di installazione e configurazione.

## Dashboard di gestione dati

Gli utenti possono fare riferimento al [Dashboard di gestione dati](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html) per ulteriori dati su [!DNL Catalog Service] sincronizzazione dei dati.
