---
title: Configurazione processo in background
description: "Configurare le pianificazioni per  [!DNL Store Fulfillment] processi in background utilizzati nella sincronizzazione dei dati con i servizi di evasione."
role: Admin, Developer
level: Intermediate
exl-id: 742ae59e-77a0-4db6-b156-2992d4403be7
source-git-commit: 36b57648e156ead801764f3ee4e5e6a0f3245fe6
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Configurazione processo in background

L&#39;integrazione Store Fulfillment utilizza processi in background e code di messaggi per prestazioni e scalabilità ottimali. Crea ambienti per i tuoi archivi Adobe Commerce utilizzando [variabili di distribuzione](https://devdocs.magento.com/cloud/env/variables-deploy.html#cron_consumers_runner) che avviano automaticamente [i runner della coda messaggi](https://devdocs.magento.com/guides/v2.4/config-guide/mq/rabbitmq-overview.html).

I processi in background vengono gestiti utilizzando la funzionalità standard di Adobe Commerce [Attività pianificate](https://docs.magento.com/user-guide/system/cron.html). Questi processi sono responsabili della sincronizzazione dei dati di configurazione degli ordini e dei negozi con i servizi Web di esecuzione dei negozi.

## Gestisci attività pianificate per il Store Fulfillment

Dall&#39;amministratore, passa a **[!UICONTROL Stores > Configuration > Advanced > System > Cron (Scheduled Tasks) > Cron configuration options for group:store_fulfillment]**.

Rivedi la configurazione predefinita per i servizi di Store Fulfillment. Puoi personalizzare queste impostazioni in base al volume di elaborazione degli ordini e alla disponibilità delle risorse.
