---
title: Aggiungi attributi ordine personalizzati
description: Scopri come aggiungere attributi di ordine personalizzati ai dati del backoffice e inviare tali attributi all’Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 14d190726324e2f42d66c2270f2e27be5a74132f
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Aggiungi attributi ordine personalizzati

In questo articolo imparerai ad aggiungere attributi personalizzati agli eventi di back office. Con gli attributi personalizzati, puoi acquisire informazioni approfondite su dati avanzati per migliorare l’analisi e creare ulteriori esperienze personalizzate per gli acquirenti.

Gli attributi personalizzati sono supportati a due livelli:

- Livello dell’ordine
- Livello articolo ordine

>[!NOTE]
>
>L&#39;Adobe [!DNL Commerce] supporta attributi personalizzati con tipo di dati stringa, booleano o data.

Per aggiungere attributi personalizzati agli eventi di back office è necessario:

1. Crea un progetto nell&#39;installazione di [!DNL Commerce].
1. Aggiorna lo schema in modo che i nuovi attributi personalizzati possano essere correttamente acquisiti in Experience Platform.
1. In Admin, verifica che gli attributi personalizzati vengano acquisiti e inviati a Experience Platform.

>[!IMPORTANT]
>
>La struttura della directory e gli esempi di codice riportati di seguito illustrano come implementare gli attributi personalizzati. La struttura e il codice effettivi della directory dipendono dalla configurazione e dall’ambiente dell’archivio.

## Passaggio 1: creare la struttura della directory

1. Passare alla directory `app/code` nell&#39;installazione di [!DNL Commerce] e creare una directory di moduli. Esempio: `Magento/AepCustomAttributes`. Questa directory contiene i file necessari per gli attributi personalizzati.
1. Nella directory del modulo, creare una sottodirectory denominata `etc`. La directory `etc` contiene i file `module.xml`, `query.xml`, `di.xml` e `et_schema.xml`.

## Passaggio 2: definire le dipendenze e la versione di impostazione

Creare un file `module.xml` che definisce le dipendenze e la versione di installazione. Ad esempio:

```xml
<?xml version="1.0"?>
<!--
/**
* Copyright (c) [year], [name]. All rights reserved.
*/
-->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Magento_SalesRuleStaging" setup_version="2.0.0">
        <sequence>
            <module name="Magento_Staging"/>
            <module name="Magento_SalesRule"/>
        </sequence>
    </module>
</config>
```

## Passaggio 3: Recuperare i dati dell&#39;ordine cliente

Creare un file `query.xml` che recupera i dati dell&#39;ordine cliente. Ad esempio:

```xml
<query>
    <source name="sales_order" type="sales">
        <attribute name="increment_id" operator="eq" alias="order_increment_id"/>
        <link source="inventory_source_item" condition_type="by_sku"/>
    </source>
</query>
```

## Passaggio 4: impostare l’iniezione di dipendenza

Creare un file `di.xml` che configura l&#39;iniezione di dipendenza. Ad esempio:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.example.instrumentedtest"
          android:versionCode="1"
          android:versionName="1.0">
    <uses-sdk android:minSdkVersion="8" android:targetSdkVersion="15"/>
    
    <instrumentation
        android:name=".MyInstrumentationTestRunner"
        android:targetPackage="com.example.instrumentedtest"/>
    
    <!-- More instrumentation elements might be here -->
</manifest>
```

## Passaggio 5: definire i servizi utilizzati per l’iniezione della dipendenza

Creare un file `et_schema.xml` che definisce i servizi utilizzati per l&#39;iniezione di dipendenza. Ad esempio:

```xml
<services>
    <service id="App\Controller\MainController" class="App\Controller\MainController">
        <argument type="service" id="doctrine.orm.default_entity_manager"/>
        <argument type="service" id="form.factory"/>
        <argument type="service" id="security.authorization_checker"/>
    </service>

    <!-- ... -->

    <service id="App\Controller\SecurityController" class="App\Controller\SecurityController">
        <argument type="service" id="security.authentication_utils"/>
        <tag name="controller.service_arguments"/>
    </service>

    <!-- ... -->
</services>
```

## Passaggio 6: creare una directory per i file PHP

Allo stesso livello della directory `etc`, creare una directory denominata `Module/Provider`. Questa directory contiene i file PHP `OrderCustomAttributes` e `OrderItemCustomAttributes`.

## Passaggio 7: definire OrderCustomAttributes

Creare un file `OrderCustomAttributes.php` che definisce gli attributi personalizzati dell&#39;ordine. Ad esempio:

```php
namespace App\Transformers;

use League\Fractal\TransformerAbstract;
use Illuminate\Support\Collection;

class CustomAttributeTransformer extends TransformerAbstract
{
    protected $availableIncludes = [];
    protected $defaultIncludes = [];

    public function __construct($signsField, $jsonSignsField = null)
    {
        $this->signsField = $signsField;
        $this->jsonSignsField = $jsonSignsField;
    }

    public function transform(Collection $collection)
    {
        // Initialize array for additional information.
        $additionalInformation = [];

        // Source - this comes from values sent to this transformer.
        foreach ($collection->{$this->signsField} ?: [] as $value) {
            if (is_array($value)) {
                // If value is an array, serialize it.
                foreach ($value as &$item) {
                    if (isset($item['custom_attr'])) {
                        // Serialize custom attribute data.
                        ...
                    }
                }
            } else {
                // Add non-array values directly.
                ...
            }
        }

        ...

        return [
            'current' => ...,
            'additional_information' => ...,
            'source' => ...,
        ];
    }

    private function flatten(array $values)
    {
      return Arr::flatten($values);
  }
}
```

## Passaggio 8: definire OrderItemCustomAttributes

Creare un file `OrderItemCustomAttributes.php` che definisce gli attributi personalizzati dell&#39;elemento dell&#39;ordine. Ad esempio:

```php
namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class OrderItemCustomAttribute
{
    private Json $jsonSerializer;
    private string $usingField;

    public function __construct(Json $jsonSerializer, string $usingField)
    {
        $this->jsonSerializer = $jsonSerializer;
        $this->usingField = $usingField;
    }

    public function get(array $values): array
    {
        $output = [];
        $values = $this->flatten($values);

        foreach ($values as $row) {
            $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
            $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];

            $attrLabel = implode(',', ['label1', 'label2']);
            $unserializedData['custom_attr1'] = $attrLabel;

            $additionalInformation = [];
            foreach ($unserializedData as $name => $value) {
                $additionalInformation[] = [
                    'name' => $name,
                    'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value),
                ];
            }

            foreach ($additionalInformation as $information) {
                $output[] = [
                    'additionalInformation' => $information,
                    $this->usingField => $row[$this->usingField],
                ];
            }
        }

        return $output;
    }

    private function flatten(array $values): array
    {
        return array_merge([], ...array_values($values));
    }
}
```

## Passaggio 9: creare una directory per il file productContext

Allo stesso livello della directory `etc`, creare una directory denominata `Plugin/Module`. Questa directory contiene il file `ProductContext.php`.

## Passaggio 10: definire la classe ProductContext

Creare un file denominato `ProductContext.php` che definisce la classe `ProductContext`. Ad esempio:

```php
namespace Magento\Catalog\Model\Product;

use Magento\Framework\App\ResourceConnection;
use Magento\Quote\Api\Data\CartInterface;

class ProductContext
{
    private $brandCache = [];
    private $resourceConnection;

    public function __construct(
        ResourceConnection $resourceConnection
    ) {
        $this->resourceConnection = $resourceConnection;
    }

    public function afterGetProductData($subject, array $result)
    {
        if (isset($result['brand_id'])) {
            if (!isset($this->brandCache[$result['brand_id']])) {
                // @todo load brand label by brand id.
                $this->brandCache[$result['brand_id']] = 'Brand Label ' . $result['brand_id'];
            }
            $result['brands'] = ['label' => $this->brandCache[$result['brand_id']]];
        }

        return $result;
    }
}
```

## Passaggio 11: registrare il modulo

Allo stesso livello della directory `etc`, creare un file `registration.php` che registri il modulo. Ad esempio:

```php
use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Dfe_Stripe',
    __DIR__
);
```

## Passaggio 12: estendere lo schema XDM esistente

Per garantire che i nuovi attributi dell&#39;ordine personalizzato possano essere acquisiti dallo schema [!DNL Commerce] in Experience Platform, è necessario estendere lo schema per includere questi campi personalizzati.

Per informazioni su come estendere uno schema XDM esistente per includere questi campi personalizzati, consulta l&#39;articolo [Creazione e modifica di schemi nell&#39;interfaccia utente](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas#custom-fields-for-standard-groups) nella documentazione di Experience Platform. Il campo ID tenant viene generato in modo dinamico; tuttavia, la struttura del campo deve essere simile all’esempio fornito nella documentazione dell’Experience Platform.

>[!IMPORTANT]
>
>Gli attributi personalizzati XDM devono corrispondere agli attributi inviati da [!DNL Commerce].

A `commerce.order`, aggiungere un campo per il livello Ordine:

![Livello ordine](assets/order-level.png)

A `productListItems`, aggiungere i campi per il livello di elemento dell&#39;ordine:

![Livello elemento ordine](assets/order-item-level.png)

## Passaggio 12: verifica che i dati vengano acquisiti

Visualizza la scheda [Personalizzazione dati](connect-data.md#data-customization) nell&#39;amministratore per verificare che i dati degli attributi personalizzati vengano acquisiti e inviati all&#39;Experience Platform.

### Risoluzione dei problemi

Se viene visualizzato il messaggio `No custom order attributes found.` nella scheda **[!UICONTROL Data Customization]**, confermare quanto segue:

1. Sono stati completati i prerequisiti per abilitare l&#39;estensione [Data Connector](overview.md#prerequisites).
1. Hai configurato [attributi ordine personalizzati](#add-custom-order-attributes).
1. È stato generato almeno un evento ordine.
