---
title: Installa [!DNL Payment Services]
description: Installare l'estensione Payments Services.
exl-id: babaa91a-9376-4acb-b934-a89f9df52016
role: Admin
feature: Payments, Checkout, Install, Upgrade
source-git-commit: 692a7e55d72b1e2f1a161d508be5e179c4d26bde
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Installa [!DNL Payment Services]

Per iniziare a utilizzare Payment Services per [!DNL Adobe Commerce] e [!DNL Magento Open Source], è necessario completare alcuni passaggi di onboarding.

>[!INFO]
>
> Per ulteriori informazioni, guarda il video [Configure [!DNL Payment Services] for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services).

Il download e l&#39;installazione dell&#39;estensione [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] è un passaggio preliminare per l&#39;utilizzo di [!DNL Payment Services].

Visualizzazione amministratore dell&#39;estensione ![[!DNL Payment Services]](assets/admin-view.png){width="300" zoomable="yes"}

## Scaricare l’estensione

Prima di installare l&#39;estensione da [Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html), è necessario scaricarla.

1. Passare all&#39;estensione [Payment Services nella Commerce Marketplace](https://commercemarketplace.adobe.com/magento-payment-services.html).
1. Per scegliere l&#39;edizione e la versione, selezionare **[!UICONTROL Edition]** e **[!UICONTROL Your store version]** in base alle proprie preferenze.
1. Fare clic su **[!UICONTROL Add to Cart]**.
1. Completare l&#39;estrazione e fare clic su **[!UICONTROL Place Order]**.
1. Per informazioni dettagliate e conferma dell’ordine, controlla l’e-mail associata al download per Marketplace.

## Installare l’estensione

È possibile installare l&#39;estensione [!DNL Payment Services] sia per [!DNL Adobe Commerce] sull&#39;infrastruttura cloud che per le istanze locali, che sono collegate all&#39;account Commerce [mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys) fornito nel processo di abbonamento.
[!DNL Magento Open Source] clienti utilizzano le istruzioni locali.

Composer utilizza queste chiavi durante l&#39;installazione iniziale di [!DNL Adobe Commerce] o in situazioni in cui le chiavi del Composer non sono state salvate in precedenza nel file `auth.json`.

Per ulteriori informazioni su come ottenere le chiavi del Compositore, vedere [Ottieni le chiavi di autenticazione](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html).

Per ulteriori informazioni su cosa considerare prima di scaricare e installare un&#39;estensione, vedere [Installare un&#39;estensione](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/extensions.html).

### [!DNL Adobe Commerce] sull&#39;infrastruttura cloud

Questo metodo viene utilizzato per installare l&#39;estensione [!DNL Payment Services] per un&#39;istanza Commerce Cloud.

1. Aggiorna il file `composer.json`:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilizzare il comando `composer update` per aggiornare tutte le dipendenze radice.

1. Eseguire il commit e inviare le modifiche.

### Configurazioni locali e di altro tipo

Questo metodo viene utilizzato per installare l&#39;estensione [!DNL Payment Services] per un&#39;istanza locale e [!DNL Magento Open Source] clienti.

1. Per ottenere l’estensione, esegui i seguenti comandi:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilizzare il comando `composer update` per aggiornare tutte le dipendenze radice.

1. Aggiorna l’istanza:

   ```bash
   bin/magento setup:upgrade
   ```

1. Cancella la cache:

   ```bash
   bin/magento cache:clean
   ```

1. Conferma modifiche.
1. Per garantire che il codice confermato sia distribuito, aggiorna l’istanza .

## Aggiornare l’estensione

Quando viene rilasciata una nuova versione di [!DNL Payment Services], è possibile aggiornare facilmente l&#39;estensione.

1. Per ottenere la versione più recente del pacchetto:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilizzare il comando `composer update` per aggiornare tutte le dipendenze radice.

1. Eseguire il commit e inviare le modifiche.

## Risoluzione dei problemi

È possibile che vengano visualizzati errori durante il tentativo di installare l&#39;estensione [!DNL Payment Services]. Per risolvere gli errori, utilizzare i seguenti metodi di risoluzione dei problemi.

### Tasti composizione errati

Se viene visualizzato il seguente errore che indica la presenza di chiavi di composizione errate:

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

Verifica che le chiavi del Compositore siano valide e di avere accesso ad altri pacchetti di Magento.

Per vedere quali chiavi del Compositore sono configurate:

1. Trovare il percorso del file `auth.json`:

   ```bash
   composer config --global home
   ```

1. Visualizza il file `auth.json`:

   ```bash
   cat /path/to/auth.json
   ```

1. Consulta [quali chiavi sono associate al tuo account Commerce `MageID`](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html).

### Memoria insufficiente per PHP

Se viene visualizzato il seguente errore che indica che non si dispone di memoria sufficiente per PHP:

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

[Aumentare il limite di memoria](https://devdocs.magento.com/cloud/project/magento-app-php-ini.html#increase-php-memory-limit) per PHP nell&#39;ambiente in `php.ini`.

In alternativa, è possibile specificare il limite di memoria utilizzando questo comando: `php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`.

Ad esempio:

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
