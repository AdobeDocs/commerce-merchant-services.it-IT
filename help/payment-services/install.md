---
title: Installa [!DNL Payment Services]
description: Installare l'estensione Payments Services.
exl-id: babaa91a-9376-4acb-b934-a89f9df52016
role: Admin
feature: Payments, Checkout, Install, Upgrade
source-git-commit: 5c4fe370507e4154d4495d4c09e2ff8705e53191
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Installa [!DNL Payment Services]

Per iniziare a utilizzare Payment Services per [!DNL Adobe Commerce] e [!DNL Magento Open Source], devi completare alcuni passaggi di onboarding.

>[!INFO]
>
> Visualizza la [Configura [!DNL Payment Services] per Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services) video per ulteriori informazioni.

Download e installazione di [!DNL Payment Services] estensione per [!DNL Adobe Commerce] e [!DNL Magento Open Source] è un passaggio preliminare per l’utilizzo di [!DNL Payment Services].

![[!DNL Payment Services] visualizzazione amministrazione dell’estensione](assets/admin-view.png){width="300" zoomable="yes"}

## Scaricare l’estensione

Scarica l&#39;estensione da [Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html) prima di installarlo.

1. Accedi a [Estensione Payment Services nella Commerce Marketplace](https://commercemarketplace.adobe.com/magento-payment-services.html).
1. Per scegliere l’edizione e la versione, attiva/disattiva **[!UICONTROL Edition]** e **[!UICONTROL Your store version]** alle tue selezioni preferite.
1. Clic **[!UICONTROL Add to Cart]**.
1. Completa il pagamento e fai clic su **[!UICONTROL Place Order]**.
1. Per informazioni dettagliate e conferma dell’ordine, controlla l’e-mail associata al download per Marketplace.

## Installare l’estensione

È possibile installare [!DNL Payment Services] estensione per entrambi [!DNL Adobe Commerce] sull’infrastruttura cloud e sulle istanze locali, collegate al tuo account Commerce [mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys) fornite nel processo di abbonamento.
[!DNL Magento Open Source] i clienti utilizzano le istruzioni on-premise.

Il Compositore utilizza queste chiavi durante l’installazione iniziale di [!DNL Adobe Commerce], o in situazioni in cui le chiavi del Compositore non sono state salvate in precedenza nel `auth.json` file.

Consulta [Ottieni le chiavi di autenticazione](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html) per ulteriori informazioni su come ottenere le chiavi del Compositore.

Consulta [Installare un’estensione](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/extensions.html) per ulteriori informazioni su cosa considerare prima di scaricare e installare un’estensione.

### [!DNL Adobe Commerce] sull’infrastruttura cloud

Questo metodo viene utilizzato per installare [!DNL Payment Services] estensione per un’istanza Commerce Cloud.

1. Aggiorna il tuo `composer.json` file:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilizza il `composer update` per aggiornare tutte le dipendenze radice.

1. Eseguire il commit e inviare le modifiche.

### Configurazioni locali e di altro tipo

Questo metodo viene utilizzato per installare [!DNL Payment Services] estensione per un’istanza on-premise e [!DNL Magento Open Source] clienti.

1. Per ottenere l’estensione, esegui i seguenti comandi:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilizza il `composer update` per aggiornare tutte le dipendenze radice.

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

Quando una nuova versione di [!DNL Payment Services] è stato rilasciato, puoi aggiornare facilmente l’estensione.

1. Per ottenere la versione più recente del pacchetto:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilizza il `composer update` per aggiornare tutte le dipendenze radice.

1. Eseguire il commit e inviare le modifiche.

## Risoluzione dei problemi

È possibile che vengano visualizzati errori durante il tentativo di installazione di [!DNL Payment Services] estensione. Per risolvere gli errori, utilizzare i seguenti metodi di risoluzione dei problemi.

### Tasti composizione errati

Se viene visualizzato il seguente errore che indica la presenza di chiavi di composizione errate:

```terminal
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

Verifica che le chiavi del Compositore siano valide e di avere accesso ad altri pacchetti di Magento.

Per vedere quali chiavi del Compositore sono configurate:

1. Trova la posizione del `auth.json` file:

   ```bash
   composer config --global home
   ```

1. Visualizza `auth.json` file:

   ```bash
   cat /path/to/auth.json
   ```

1. Consulta [quali chiavi sono associate al tuo account Commerce `MageID`](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html).

### Memoria insufficiente per PHP

Se viene visualizzato il seguente errore che indica che non si dispone di memoria sufficiente per PHP:

```terminal
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

[Aumentare il limite di memoria](https://devdocs.magento.com/cloud/project/magento-app-php-ini.html#increase-php-memory-limit) per PHP sul tuo ambiente in `php.ini`.

In alternativa, è possibile specificare il limite di memoria utilizzando questo comando: `php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`.

Ad esempio:

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
