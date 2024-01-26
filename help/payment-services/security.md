---
title: Sicurezza e conformità
description: Verifica i requisiti di sicurezza e conformità per il sito.
exl-id: 083c5a12-1d78-48b5-b9e3-612b104ce7e0
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security.html
source-git-commit: 5fe23b5aba9ad0a2a6c995fa6ade78f46fe7e3e1
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Sicurezza e conformità

La sicurezza è la preoccupazione principale in [!DNL Payment Services] e nessuna informazione riservata o regolamentata da Payment Card Industry (PCI) viene trasmessa al cliente [!DNL Payment Services].

## Sicurezza Commerce

[!DNL Adobe Commerce] e [!DNL Magento Open Source] include il supporto di diverse funzioni di sicurezza.

Consulta [Sicurezza](https://docs.magento.com/user-guide/stores/security.html){target="_blank"} nella guida utente di base per rivedere le best practice sulla sicurezza e imparare a gestire le sessioni e le credenziali amministratore, implementare CAPTCHA e gestire le restrizioni per i siti web.

## Conformità PCI

Il settore delle carte di pagamento (Payment Card Industry, PCI) ha stabilito una serie di requisiti per le imprese che accettano il pagamento tramite carta di credito su Internet. Oltre a mantenere un ambiente sicuro, i commercianti che gestiscono le informazioni della carta di credito del cliente sono responsabili del rispetto di alcune linee guida standard.

Consulta [Linee guida per la conformità PCI](https://docs.magento.com/user-guide/stores/compliance-pci.html){target="_blank"} per ulteriori informazioni.

I commercianti possono completare una [questionario di autovalutazione (SAQ)](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"}, che è uno strumento di autovalutazione per valutare la sicurezza dei dati dei titolari della carta.

### Campi carta di credito

Con i campi della carta di credito, non vengono trasmessi dati regolamentati PCI ai servizi. Non è necessario archiviare o mantenere tali dati, il che riduce notevolmente i problemi di conformità PCI.

### 3DS

PCI 3-D Secure (3DS) consente l&#39;autenticazione dell&#39;acquirente con l&#39;emittente della carta di credito quando si effettuano acquisti online con carta di credito. Questo ulteriore livello di sicurezza contribuisce a prevenire le frodi online ed è richiesto come parte delle normative di conformità dell&#39;Unione europea (UE).

[!UICONTROL Payment Services] fornisce funzionalità 3DS per consentire ai commercianti di rispettare le normative dell&#39;UE e per proteggere i clienti e i commercianti da attività fraudolente nei loro negozi.

Se sei un commerciante all&#39;interno dell&#39;UE o della Gran Bretagna in cui è richiesta la conformità 3DS, devi attivare manualmente 3DS (è `Off` per impostazione predefinita) in [Impostazioni](settings.md#credit-card-fields).

>[!NOTE]
>
>Il requisito 3DS si applica alle operazioni in cui la banca dell&#39;impresa e del titolare della carta sono situate nel [Spazio economico europeo](https://www.efta.int/eea) (SEE) e la Gran Bretagna. I commercianti degli Stati Uniti non richiedono 3DS, ma possono abilitarlo per le loro transazioni se lo desiderano.

Gli ordini effettuati per l&#39;acquirente dal personale del commerciante/negozio non sono configurati con le misure di conformità 3DS.

Consulta [3DS in Impostazioni](settings.md#3ds) per ulteriori informazioni.

### Vaulting delle carte

Quando un acquirente [vaults—o &quot;salva&quot;—le informazioni sulla carta di credito](vaulting.md) per acquisti futuri nei negozi, le informazioni minime sulla carta di credito vengono condivise con l&#39;acquirente (ultime quattro cifre, data di scadenza della carta e marchio della carta). Le informazioni relative alla carta di credito vengono memorizzate presso il fornitore dei servizi di pagamento. Quando una carta scade, o non hanno più bisogno delle informazioni salvate, possono eliminare quel token in modo che le informazioni non vengano più memorizzate dal provider di pagamenti.

Consulta [Vaulting con carta di credito](vaulting.md) per ulteriori informazioni.

### Pulsanti di pagamento PayPal

Con i pulsanti di pagamento PayPal non vengono trasmessi dati regolamentati PCI ai servizi. Non è necessario archiviare o mantenere tali dati, il che riduce notevolmente i problemi di conformità PCI.

Per motivi di sicurezza, PayPal non passa l&#39;indirizzo di fatturazione durante il pagamento: paese, e-mail e nome sono le uniche informazioni di fatturazione utilizzate. Facoltativamente, puoi abilitare l&#39;estrazione PayPal del tuo sito per restituire l&#39;indirizzo di fatturazione completo contattando PayPal e completando un processo di verifica.

PayPal ha anche la protezione integrata contro le frodi che utilizza l&#39;apprendimento automatico per aiutarti a combattere le frodi. Vedi PayPal [Documentazione sulla protezione del venditore](https://www.paypal.com/us/webapps/mpp/security/seller-protection) per ulteriori informazioni.

## Protezione dalle frodi

È possibile abilitare la protezione antifrode automatizzata per i servizi di pagamento con [Estensione Signifyd](https://commercemarketplace.adobe.com/signifyd-module-connect.html).

Consulta [Protezione contro le frodi significative](fraud-protection.md) per ulteriori informazioni.

