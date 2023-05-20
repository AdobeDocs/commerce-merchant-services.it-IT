---
title: Connetti l’istanza
description: Connetti la tua istanza Commerce utilizzando una chiave API e una chiave privata e specifica lo spazio di dati nella configurazione.
exl-id: 5038fd31-bac5-419e-a172-66919a9b5272
source-git-commit: 817a01e98876bddf5f41a253501984539b3351cd
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Connetti l’istanza

[!DNL Payment Services] è alimentato da Commerce Services e distribuito come SaaS (software as a service). Puoi collegare la tua istanza Commerce utilizzando una chiave API e una chiave privata e specificare lo spazio di dati nella configurazione utilizzando [Connettore Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html). **La connessione è stata impostata una sola volta.**

* Se è stato *ha già connesso l’istanza*, ottenendo e utilizzando le credenziali API e configurando Commerce Services, puoi procedere a [configurazione della sandbox di test](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html).
* Se si continua *necessità di collegare l’istanza*, consulta le informazioni in questo argomento su [recupero credenziali API](#obtain-api-credentials) e [configurazione di Commerce Services](#configure-commerce-services).
* Se sei *non sei sicuro se l’istanza è connessa*, passa a **Sistema** > Servizi > **Connettore Commerce Services** e visualizzare i valori delle chiavi API pubblica e privata in [!UICONTROL Sandbox Keys] e [!UICONTROL Production Keys] sezioni e *Progetto* e *Spazio dati* campi in [!UICONTROL SaaS Identifier] sezione. Se tali valori sono presenti, l’istanza è connessa.

## Ottenere le credenziali API

Per utilizzare un servizio Commerce SaaS, devi utilizzare le chiavi API dell’istanza (chiave API pubblica Commerce e chiave privata) sia per la sandbox che per la produzione, che vengono create e gestite nel tuo [Il mio dashboard account](https://account.magento.com/customer/account/login). [La coppia di chiavi](https://docs.magento.com/user-guide/configuration/services/saas.html) può essere creato per un account Commerce, uno per sandbox e uno per produzione, anche se è possibile utilizzare attivamente una sola coppia alla volta.

>[!NOTE]
>
>Hai bisogno di assistenza per accedere al tuo [!UICONTROL My Account] cruscotto? Consulta [Creare un account Commerce](https://docs.magento.com/user-guide/magento/magento-account-create.html).

Una volta creata, una chiave API pubblica è sempre disponibile nella dashboard Il mio account. Può essere copiata o eliminata in base alle esigenze. La chiave API privata diventa visibile quando crei una chiave API pubblica per sandbox o produzione; è disponibile solo per la copia o il salvataggio dalla finestra di dialogo successiva e non è più accessibile in un secondo momento.

Una determinata coppia di chiavi API è valida per tutti i servizi Commerce in un ambiente, quindi se disponi già di servizi Commerce configurati per la tua istanza, la coppia di chiavi API è già presente nel connettore di servizi Commerce.

Se la chiave API viene persa, è necessario specificare una nuova coppia di chiavi API [generato](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#generate-an-api-key-and-private-key) e [applicato](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#configure-saas-project) alla configurazione del Commerce Services Connector in Admin. Se nella configurazione sono configurate le chiavi errate o non ne esistono, in Payment Services viene visualizzata una finestra di dialogo di errore di verifica dell&#39;account che informa che l&#39;account non è stato verificato.

Vedi un [elenco dei servizi Commerce disponibili che utilizzano l’API](https://docs.magento.com/user-guide/system/saas.html#available-services).

Per informazioni su come generare una chiave API per ambienti sandbox o di produzione, consulta [Credenziali](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html#apikey).

>[!IMPORTANT]
>Si consiglia di non rigenerare una coppia di chiavi API *e* modificare l’identificatore SaaS e/o lo spazio dati in un’istanza di produzione attiva. Se vengono modificati, i dati dell’istanza andranno persi.

## Configurare Commerce Services

È possibile utilizzare la stessa chiave API in più istanze, ma ogni istanza deve avere il proprio [Spazio dati SaaS](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html#saasenv).

Dopo aver ottenuto le credenziali, è possibile configurare il progetto SaaS e Saas Data Space.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**.
1. Clic **[!UICONTROL Configure Commerce Services]**.

   Questa opzione è visibile se non hai ancora configurato Commerce Services per il tuo account.

   Ti indirizzano all’area di configurazione nell’Admin, **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**, per configurare Commerce Services Connector.

1. Per configurare Commerce Services, segui i passaggi descritti in [Configurazione SaaS](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html#saasenv).
