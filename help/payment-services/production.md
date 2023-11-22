---
title: Abilita [!DNL Payment Services] per la produzione
description: Completa il processo di onboarding abilitando [!DNL Payment Services] per la produzione.
exl-id: 3b1269e8-127b-47f8-9738-9722a5737c63
feature: Payments, Checkout, Configuration, Install
source-git-commit: 6769e29a4ae07b8cf15aa2da3cac2fe8583497e0
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---

# Abilita [!DNL Payment Services] per la produzione

È possibile mettere il servizio in produzione e completare [processo di onboarding](onboard.md), in base ai passaggi descritti in questo argomento, dopo:

* [Installa](install.md) l&#39;estensione Payment Services
* [Configurare e connettersi](connect.md) istanza
* [Configurazione](sandbox.md) e [test](test-validate.md) sandbox

## Imposta [!DNL Payment Services] come metodo di pagamento

Dopo di te [configurare Commerce Services](connect.md#configure-commerce-services) e abilita [test sandbox](sandbox.md#enable-sandbox-testing) o [pagamenti live](#enable-live-payments), è necessario impostare [!DNL Payment Services] come metodo di pagamento.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clic **[!UICONTROL Enable Payment Services]**.

   Questa opzione è visibile se non hai ancora configurato [!DNL Payment Services] come metodo di pagamento per uno o più siti Web.

   L&#39;utente viene indirizzato all&#39;area delle impostazioni nella vista Home con le opzioni pertinenti espanse (**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Settings]_), dove è possibile abilitare [!DNL Payment Services] opzioni come [metodo di pagamento](https://docs.magento.com/user-guide/configuration/sales/payment-methods.html){target="_blank"}.

1. In entrata _[!UICONTROL General Configuration]_, impostato **[!UICONTROL Enable]**a `Yes`.
1. Imposta **[!UICONTROL Payment Action]**, per entrambi _[!UICONTROL Credit Card Fields]_e_[!UICONTROL PayPal Smart Buttons]_, a uno dei seguenti:

   | Impostazione | Descrizione |
   |---|---|
   | `Authorize` | Approva l&#39;acquisto e blocca i fondi. L&#39;importo non viene prelevato fino a quando non viene &quot;catturato&quot; dal mercante. |
   | `Authorize and Capture` | Approva l&#39;acquisto e il commerciante &quot;cattura&quot; i fondi. |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services] supporta le acquisizioni parziali. Un commerciante può acquisire parzialmente (fatturare) parti di un ordine. Ad esempio, puoi acquisire ogni elemento singolarmente oppure un elemento ora e il resto in un secondo momento.

1. Clic **[!UICONTROL Save]**.
1. Clic **[!UICONTROL Go to Payment Services]** per essere reindirizzato al [!DNL Payment Services] A casa.
1. [Cancellare la cache](https://docs.magento.com/user-guide/system/cache-management.html){target="_blank"}.

   La cancellazione deve essere eseguita dopo ogni modifica della configurazione.

Consulta [Configura servizi di pagamento](settings.md) per ulteriori informazioni sulla configurazione dei campi della carta di credito e dei pulsanti avanzati PayPal.

## Onboarding completo per gli esercenti

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clic **[!UICONTROL Live onboarding]**.

   Questa opzione è visibile se non hai ancora completato l’onboarding live per [!DNL Payment Services].

   Viene visualizzata una finestra PayPal.

1. Continua con il flusso PayPal, utilizzando le credenziali del tuo account PayPal (non le credenziali del tuo account sandbox) o iscriviti a un nuovo account PayPal.
1. Nella barra laterale Amministratore, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**

   Il _[!UICONTROL Live onboarding]_non è più visibile e viene visualizzato un &quot;[!UICONTROL Live payments pending]&quot;.

   In questa casella di testo, ti potrebbe anche essere chiesto di confermare il tuo indirizzo e-mail con PayPal per completare l&#39;onboarding.

1. Se ti viene richiesto di confermare il tuo indirizzo e-mail, controlla la tua e-mail per il messaggio di conferma inviato da PayPal e fai clic per confermare il tuo indirizzo e-mail.
1. Nella barra laterale Amministratore, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Aggiorna la finestra del browser.

   Quando l&#39;onboarding del commerciante PayPal viene approvato, dovrebbe essere visualizzata una notifica che informa che il sistema di pagamento è in modalità sandbox e non elabora pagamenti live.

   >[!IMPORTANT]
   >
   >Se revochi il consenso a [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] per l&#39;elaborazione dei pagamenti (nelle impostazioni del conto PayPal), gli ordini nel tuo Negozio non possono essere elaborati da [!DNL Payment Services]. Nella pagina Home di Payment Services viene visualizzato un avviso relativo alla revoca del consenso.

## Richiedi diritti pagamenti da Adobe

Per abilitare l’onboarding in tempo reale, devi richiedere i pagamenti spettanti a Adobe:

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clic **[!UICONTROL Get Live Payments]** nel tuo [!DNL Payment Services] A casa.

   ![Richiedi diritti](assets/request-entitlements.png){width="500" zoomable="yes"}

1. Compila il modulo.
1. Un membro del team vendite ti contatterà.

In alternativa, è possibile richiedere diritti all’aiuto da Adobe all’indirizzo [business.adobe.com](https://business.adobe.com/resources/payment-services.html).

>[!IMPORTANT]
>
>**Onboarding live** non è accessibile fino all’approvazione del diritto all’aiuto.

## Configura piano tariffario

Per ottenere [!DNL Payment Services] _ID esercente_:


1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Nella vista Home, fai clic su **[!UICONTROL Settings]**. Consulta [Home](payments-home.md) per ulteriori informazioni.
1. Seleziona la richiesta _ID esercente_ e inviarlo al proprio rappresentante commerciale, che configurerà il piano tariffario corretto.

## Abilita pagamenti live

A _ID commerciante produzione_ viene generato automaticamente e popolato in [configurazione](configure-admin.md). Non modificare o alterare questo ID.

Per abilitare i pagamenti live:

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Nella Home, fai clic su **[!UICONTROL Settings]** in alto a destra. Consulta [Home](payments-home.md) per ulteriori informazioni.
1. In _[!UICONTROL General Configuration]_set di sezioni **[!UICONTROL Payment mode]**a `Production`.
1. Clic **[!UICONTROL Save]**.
1. [Cancellare la cache](https://docs.magento.com/user-guide/system/cache-management.html){target="_blank"}.

   >[!IMPORTANT]
   >
   >Se non cancelli la cache, i clienti non possono vedere le opzioni di pagamento PayPal durante il pagamento.

Se si torna a [!DNL Payment Services] Home, il messaggio della modalità di pagamento Sandbox non viene più visualizzato perché stai elaborando pagamenti live.

Consulta [Configurare in Admin](configure-admin.md) per le opzioni di configurazione legacy.

>[!IMPORTANT]
>
>Se revochi il consenso a [!DNL Payment Services] per l&#39;elaborazione dei pagamenti (nelle impostazioni del conto PayPal), gli ordini nel tuo Negozio non possono essere elaborati da [!DNL Payment Services]. Se desideri riabilitare l’elaborazione dei pagamenti, devi completare di nuovo l’onboarding. Nella pagina Home di Payment Services viene visualizzato un avviso relativo alla revoca del consenso.

## Test in produzione

Si consiglia vivamente di testare i pagamenti in produzione, con carte di credito reali e banche, prima di esporre questa funzionalità agli acquirenti.

Consulta [Test e convalida](test-validate.md) per ulteriori informazioni.
