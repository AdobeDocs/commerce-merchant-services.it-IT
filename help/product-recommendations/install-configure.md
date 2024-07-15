---
title: Installazione e configurazione
description: Scopri come installare, aggiornare e disinstallare [!DNL Product Recommendations].
exl-id: fa599f72-1064-41da-ac54-2b3a3c16a1fe
role: Admin, Developer
source-git-commit: 96a5791c5716f612f473540f27bd3f99b1bfe7c8
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Installazione e configurazione

La distribuzione di [!DNL Product Recommendations] nella vetrina e nell&#39;amministratore richiede l&#39;installazione del modulo e la configurazione di [Commerce Services Connector](../landing/saas.md). Man mano che gli aggiornamenti vengono rilasciati, puoi aggiornare facilmente l’installazione con l’ultima versione.

- [Installa](#install)
- [Configura](#configure)
- [Aggiorna](#update)
- [Disinstalla](#uninstall)

## Installa [!DNL Product Recommendations] {#install}

Poiché il modulo [!DNL Product Recommendations] è un metapacchetto autonomo, gli aggiornamenti vengono rilasciati più frequentemente rispetto ad Adobe Commerce. Per essere certi di essere aggiornati sulle ultime correzioni di bug e funzionalità, consulta le [note sulla versione](release-notes.md).

Installa il modulo `magento/product-recommendations` con Composer:

```bash
composer require magento/product-recommendations
```

### Supporto per Aggiungi Page Builder {#pbsupport}

[!DNL Product Recommendations] per Page Builder è un modulo facoltativo e viene installato separatamente. Per utilizzare [!DNL Product Recommendations] con Page Builder, installare il modulo eseguendo il comando seguente:

```bash
composer require magento/module-page-builder-product-recommendations
```

Attivando [!DNL Product Recommendations] in Page Builder, è possibile aggiungere una [unità di consigli](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html) attiva a qualsiasi contenuto creato in Page Builder, ad esempio pagine, blocchi e blocchi dinamici.

Per ulteriori istruzioni, vedi [Utilizzo di [!DNL Product Recommendations] con contenuto Page Builder](page-builder.md).

### Aggiungi tipo di consiglio per somiglianza visiva {#vissimsupport}

Il tipo di consiglio _Somiglianza visiva_ ti consente di distribuire un&#39;unità di consigli nella pagina dei dettagli del prodotto che mostra prodotti [visivamente simili](type.md#visualsim) al prodotto visualizzato. Questo tipo di consigli è più utile quando le immagini e gli aspetti visivi dei prodotti sono parti importanti dell’esperienza di acquisto. Installa il tipo di consiglio _Somiglianza visiva_ eseguendo il comando seguente:

```bash
composer require magento/module-visual-product-recommendations
```

## Configura [!DNL Product Recommendations] {#configure}

Dopo aver installato il modulo `magento/product-recommendations`, è necessario configurare [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html) specificando le chiavi API e selezionando uno spazio dati SaaS.

Per verificare che l&#39;esportazione del catalogo sia eseguita correttamente, verificare che i processi [cron](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html) e gli [indicizzatori](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) siano in esecuzione e che l&#39;indicizzatore `Product Feed` sia impostato su `Update by Schedule`.

Quando si collega correttamente a Commerce Services tramite le chiavi API e si specifica SaaS Data Space, inizia la sincronizzazione del catalogo. Puoi quindi [verificare](verify.md) che i dati comportamentali vengano inviati alla vetrina.

## Aggiorna l&#39;installazione di [!DNL Product Recommendations] {#update}

Come tutti gli altri componenti di Adobe Commerce, [!DNL Product Recommendations] utilizza Composer per l&#39;installazione e gli aggiornamenti. Per aggiornare il modulo `magento/product-recommendations`, eseguire le operazioni seguenti:

```bash
composer update magento/product-recommendations --with-dependencies
```

Per eseguire l&#39;aggiornamento a una versione principale, ad esempio da 3.0 a 4.0, è necessario modificare il file radice `composer.json` del progetto. Per informazioni sull&#39;ultima versione, vedere le [note sulla versione](release-notes.md). Ad esempio, apriamo il file `composer.json` principale e cerchiamo il modulo `magento/product-recommendations`:

```json
"require": {
    ...
    "magento/product-recommendations": "^3.0",
    ...
}
```

Saltiamo la versione principale da `3.0` a `4.0`:

```json
"require": {
    ...
    "magento/product-recommendations": "^4.0",
    ...
}
```

Salva il file `composer.json` ed esegui:

```bash
composer update magento/product-recommendations --with-dependencies
```

Oppure se hai installato i moduli `magento/module-visual-product-recommendations` e `magento/module-page-builder-product-recommendations`:

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> Nelle versioni 3.x.x di Product Recommendations, era necessaria una sola chiave API. Nelle versioni 4.x.x e successive, devi fornire le chiavi API di produzione pubbliche e private nonché le chiavi API sandbox pubbliche e private. Se non fornisci entrambe le coppie di chiavi API, non puoi accedere alla funzione Product Recommendations in Admin. La raccolta dei dati, tuttavia, continuerà nella tua vetrina e i consigli esistenti continueranno a essere visualizzati ai tuoi acquirenti.

## Firewall

Per consentire a Product Recommendations di passare attraverso un firewall, aggiungi `commerce.adobe.io` all&#39;elenco consentiti.

## Disinstalla [!DNL Product Recommendations] {#uninstall}

Se necessario, puoi [disinstallare](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html) il modulo product-recommendations.
