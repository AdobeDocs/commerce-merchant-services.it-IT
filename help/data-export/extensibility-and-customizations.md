---
title: Estendere e personalizzare i dati del feed di esportazione dei dati SaaS
description: Scopri come estendere e personalizzare i dati del feed  [!DNL SaaS Data Export] .
role: Admin, Developer
recommendations: noCatalog
source-git-commit: 51238f86f36a756b86d07bdf6bb0a5cf0c61cbeb
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Estendere e personalizzare i dati del feed di esportazione dei dati SaaS

L&#39;estensione [!DNL Commerce Data Export] consente di esportare i dati dall&#39;applicazione [!DNL Commerce] a Commerce Services quali Live Search, Catalog Service e Product Recommendations. Se necessario, è possibile estendere e personalizzare i dati del feed per includere dati aggiuntivi o modificare i dati raccolti aggiornando il modulo `Magento\CatalogDataExporter`.

>[!NOTE]
>
>L’aggiunta di nuovi dati al feed o la modifica di dati esistenti può influire sulle prestazioni della raccolta di feed e causare problemi nella logica di elaborazione sul lato Adobe Commerce. Assicurati di testare il codice personalizzato prima di unire a un ambiente di produzione.

## Estendere i dati degli attributi nel feed dei prodotti

Il feed dei prodotti include attributi predefiniti necessari per l’elaborazione del prodotto o comunemente utilizzati dai consumatori. Puoi includere attributi di sistema aggiuntivi nel feed dei prodotti aggiungendoli al feed.

Per completare l&#39;attività, aggiornare il modulo `magento/catalog-data-exporter` per aggiungere gli attributi di sistema aggiuntivi al file di configurazione [dependency injection](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`). Aggiungere gli attributi alla query dell&#39;attributo di prodotto (`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`).

**Esempio**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```
