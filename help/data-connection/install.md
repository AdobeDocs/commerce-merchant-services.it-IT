---
title: Installa [!DNL Data Connection]
description: Scopri come installare, aggiornare e disinstallare [!DNL Data Connection] estensione da Adobe Commerce.
exl-id: e78e8ab0-8757-4ab6-8ee1-d2e137fe6ced
role: Admin, Developer
feature: Install
source-git-commit: 2392cb4257f6efdcb8fc3e38c007148e03e338fd
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Installa [!DNL Data Connection]

Prima di installare l’estensione, [esaminare i prerequisiti](overview.md#prereqs).

## Installare l’estensione

Il [!DNL Data Connection] l&#39;estensione è disponibile da [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html). Quando installi questa estensione dalla riga di comando del server, questa si connette all’installazione di Adobe Commerce come [servizio](../landing/saas.md). Al termine del processo, **[!DNL Data Connection]** e **Connettore Commerce Services** vengono visualizzati sul **Sistema** menu in **Servizi** in Commerce _Amministratore_.

>[!IMPORTANT]
>
>Mentre il nome dell’estensione è cambiato da connettore Experience Platform a [!DNL Data Connection], il nome del pacchetto rimane `experience-platform-connector` per supportare la compatibilità con le versioni precedenti.

1. Per scaricare `experience-platform-connector` , eseguire quanto segue dalla riga di comando:

   ```bash
   composer require magento/experience-platform-connector
   ```

   Questo metapacchetto contiene i moduli e le estensioni seguenti:

   * `module-experience-connector-admin` : aggiorna l’interfaccia utente di amministrazione in modo da poter selezionare l’ID dello stream di dati per una specifica istanza di Adobe Commerce.
   * `module-experience-connector` - Imposta il `Organization ID` e `datastreamId` nell’SDK degli eventi di Storefront.
   * `data-services` : fornisce il contesto degli attributi per gli eventi storefront. Ad esempio, quando si verifica un evento di pagamento, vengono incluse informazioni sul numero di elementi presenti nel carrello e i dati degli attributi del prodotto relativi a tali elementi.
   * `services-id` : collega l’istanza Adobe Commerce a [SaaS Adobe Commerce](../landing/saas.md) utilizzando le chiavi sandbox e API di produzione e in Adobe Experience Platform per recuperare l’ID organizzazione IMS.
   * `orders-connector` : collega il servizio di stato dell’ordine all’istanza Adobe Commerce.

1. (Facoltativo) Da includere [!DNL Live Search] dati, che comprendono [eventi di ricerca](events.md#search-events), installare [[!DNL Live Search]](../live-search/install.md) estensione.

1. (Facoltativo) Per includere i dati B2B, che comprendono [eventi richiesta di acquisto](events.md#b2b-events), installare [Estensione B2B](#install-the-b2b-extension).

### Configurare il connettore ordini

Dopo aver installato `experience-platform-connector` dell&#39;estensione, è necessario finalizzare l&#39;installazione di `orders-connector` modulo basato sul tipo di distribuzione: on-premise o Adobe Commerce su infrastruttura Cloud.

#### On-premise

Negli ambienti locali, devi abilitare manualmente la generazione del codice e gli eventi Adobe Commerce:

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### Infrastruttura cloud

Nell’infrastruttura Adobe Commerce on Cloud, abilita `ENABLE_EVENTING` variabile globale in `.magento.env.yaml`. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html#enable_eventing).

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

Esegui il commit e invia i file aggiornati all’ambiente Cloud. Al termine della distribuzione, abilita l’invio di eventi con il seguente comando:

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### Installare l’estensione B2B

Per gli esercenti B2B, installa la seguente estensione per includere [elenco richieste di acquisto](events.md#b2b-events) dati evento.

Scarica il file `magento/experience-platform-connector-b2b` eseguendo quanto segue dalla riga di comando:

```bash
composer require magento/experience-platform-connector-b2b
```

## Aggiornare il [!DNL Data Connection] estensione {#update}

Per aggiornare [!DNL Data Connection] , eseguire quanto segue dalla riga di comando:

```bash
composer update magento/experience-platform-connector --with-dependencies
```

Oppure, per gli esercenti B2B:

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

Per eseguire l’aggiornamento a una versione principale, ad esempio da 2.0.0 a 3.0.0, modifica la directory principale del progetto [!DNL Composer] `.json` file come segue:

1. Apri la directory principale `composer.json` file e ricerca `magento/experience-platform-connector`.

1. In `require` , aggiorna il numero di versione come segue:

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **Salva** `composer.json`. Quindi, esegui quanto segue dalla riga di comando:

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   Oppure, per gli esercenti B2B:

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## Disinstalla [!DNL Data Connection] estensione {#uninstall}

Per disinstallare [!DNL Data Connection] , fare riferimento a [disinstalla moduli](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html).
