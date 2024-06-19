---
title: "[!DNL Manage the Data Export extension]"
description: "Scopri come aggiornare [!DNL Data Export] e per rimuovere o disabilitare i servizi di esportazione dei dati non necessari."
role: Admin, Developer
recommendations: noCatalog
source-git-commit: 8230756c203cb2b4bdb4949f116c398fcaab84ff
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Gestire l’estensione di esportazione dei dati SaaS

Il [!DNL data export] l&#39;estensione per i servizi SaaS è una raccolta di moduli che consentono la raccolta e la sincronizzazione di dati tra Adobe Commerce e i servizi Commerce connessi.

Moduli specifici sono inclusi nei metapacchetti per le estensioni di Adobe Commerce Services, ad esempio [Live Search](/help/live-search/overview.md), [Recommendations del prodotto](/help/product-recommendations/overview.md), e [Servizio catalogo](/help/catalog-service/overview.md). Se utilizzi questi servizi, non è necessaria alcuna installazione separata per abilitare l’estensione Esportazione dati.

## Rimuovere o disabilitare le funzioni di esportazione dei dati di Commerce

Se non hai bisogno di uno dei moduli di esportazione dei dati di commerce installati, utilizza `magento:module:disable` Comando CLI per disattivarlo.

Ad esempio, è presente un [API per categorie](https://developer.adobe.com/commerce/services/graphql/catalog-service/categories/) che utilizza internamente i dati del feed di autorizzazioni categorie. Se non utilizzi questa API, puoi disabilitare l’esportazione dei dati per il feed di autorizzazioni per le categorie.

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### Aggiornare un modulo a una versione specifica

Puoi aggiornare uno qualsiasi dei moduli di esportazione dei dati di e-commerce installati utilizzando Composer. Ad esempio, puoi aggiornare un modulo a una versione specificata e anche aggiornare eventuali dipendenze richieste.

1. Accedere al server applicazioni Commerce.

1. Dalla riga di comando, aggiorna il modulo utilizzando Compositore:

   ```bash
   composer require magento/module-saas-price:103.3.1 --with-all-dependencies
   ```

Se l’istanza Commerce è distribuita nell’infrastruttura cloud, aggiorna l’estensione dalla directory del progetto cloud. Consulta [Aggiornare un’estensione](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension) nel _Guida di Adobe Commerce sull’infrastruttura cloud_.




