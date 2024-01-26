---
title: Abilita [!DNL Payment Services] per la produzione
description: Completa il processo di onboarding abilitando [!DNL Payment Services] per la produzione.
exl-id: 3b1269e8-127b-47f8-9738-9722a5737c63
feature: Payments, Checkout, Configuration, Install
source-git-commit: 5fe23b5aba9ad0a2a6c995fa6ade78f46fe7e3e1
workflow-type: tm+mt
source-wordcount: '1006'
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
1. Imposta **[!UICONTROL Payment Action]**, per entrambi _[!UICONTROL Credit Card Fields]_e_[!UICONTROL PayPal payment buttons]_, a uno dei seguenti:

   | Impostazione | Descrizione |
   |---|---|
   | `Authorize` | Approva l&#39;acquisto e blocca i fondi. L&#39;importo non viene prelevato fino a quando non viene &quot;catturato&quot; dal mercante. |
   | `Authorize and Capture` | Approva l&#39;acquisto e il commerciante &quot;cattura&quot; i fondi. |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services] supporta le acquisizioni parziali. Un commerciante può acquisire parzialmente (fatturare) parti di un ordine. Ad esempio, puoi acquisire ogni elemento singolarmente oppure un elemento ora e il resto in un secondo momento.

1. Clic **[!UICONTROL Save]**.
1. Clic **[!UICONTROL Go to Payment Services]** per essere reindirizzato al [!DNL Payment Services] A casa.
1. [Cancellare la cache](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html).

   La cancellazione deve essere eseguita dopo ogni modifica della configurazione.

Consulta [Configura servizi di pagamento](settings.md) per ulteriori informazioni sulla configurazione dei campi della carta di credito e dei pulsanti di pagamento PayPal.

## Onboarding completo per gli esercenti

Il passaggio successivo per consentire ai negozi di andare in diretta con Payment Services consiste nel completare l’onboarding in tempo reale.

Servizi di pagamento fornisce [**Avanzate** (completamente supportato) e **Standard** Opzioni di pagamento (Pagamento rapido)](../payment-services/payments-options.md#standard-vs-advanced-payments-experience) e dei flussi di onboarding, in base al paese in cui operi e all’esperienza di pagamento preferita.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clic **[!UICONTROL Live onboarding]**.

   Questa opzione è visibile se non hai ancora completato l’onboarding live per [!DNL Payment Services].

1. In _Seleziona il tuo paese_ , selezionare il paese da cui si sta operando.

   Payment Services offre supporto completo per tutte le opzioni di pagamento disponibili in [cinque paesi](../payment-services/overview.md#availability) attualmente. Payment Services fornisce funzionalità di pagamento rapido (un sottoinsieme di opzioni di pagamento) per tutti gli altri paesi rappresentati nell&#39;elenco dei paesi.

   Il paese selezionato dall&#39;elenco determina le opzioni di pagamento e il flusso di onboarding:[Avanzate](#advanced-onboarding) (completamente supportato) oppure [Standard](#standard-onboarding) (Pagamento rapido), disponibile per l&#39;utente.

>[!TIP]
>
> Una volta scelta e portata avanti l’opzione di onboarding (Standard o Avanzata), è necessario completare di nuovo l’onboarding per effettuare l’aggiornamento o il downgrade dalla selezione iniziale.

### Onboarding avanzato

Questo flusso di onboarding è disponibile per gli esercenti in [paesi pienamente supportati](../payment-services/overview.md#availability).

Dopo aver selezionato il paese:

1. Nel modale visualizzato, seleziona **Avanzate**.

   Per **Standard** , passare alla [Flusso di onboarding standard](#standard-onboarding).

1. Clic **Continua**.
1. Continua con il flusso PayPal per l&#39;onboarding avanzato completamente supportato, utilizzando le credenziali del tuo account PayPal (non le credenziali del tuo account sandbox) _o_ Registrati per un nuovo conto PayPal.

>[!IMPORTANT]
>
>**Onboarding avanzato** richiede ai commercianti di [richiesta di pagamento diritto](#request-payments-entitlement-from-adobe) per abilitare l’onboarding live.

### Onboarding standard

Questo flusso di onboarding standard è disponibile per i commercianti nei paesi disponibili per i quali [Solo supporto per il Checkpoint rapido](../payment-services/overview.md#availability) viene fornito.

Dopo aver selezionato il paese:

1. In _Contratto di servizi di pagamento_ , fare clic sul pulsante **Contratto di servizi di pagamento** per visualizzare il contratto di Adobe Commerce Payment Services.
1. In _Contratto di servizi di pagamento_ modale, fai clic su **Accetto**.
1. Continua con il flusso PayPal per l&#39;onboarding del Checkpoint rapido, utilizzando le credenziali del tuo account PayPal (non le credenziali del tuo account sandbox) o iscriviti a un nuovo account PayPal.

>[!IMPORTANT]
>
>[Campi Apple per pagamenti e carte di credito](../payment-services/payments-options.md) non sono disponibili per **Onboarding standard**.

## Conferma indirizzo e-mail

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

Per consentire ai negozi di andare in diretta, richiedi i pagamenti spettanti a Adobe (per [Solo onboarding avanzato](#advanced-onboarding)):

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clic **[!UICONTROL Get Live Payments]** nel tuo [!DNL Payment Services] A casa.

   ![Richiedi diritti](assets/request-entitlements.png){width="500" zoomable="yes"}

1. Compila il modulo.
1. Un membro del team vendite ti contatterà.

In alternativa, è possibile richiedere il diritto ai pagamenti da Adobe all’indirizzo [business.adobe.com](https://business.adobe.com/resources/payment-services.html).

>[!IMPORTANT]
>
>**Onboarding live** non è accessibile fino all’approvazione del diritto all’aiuto.

## Configura piano tariffario

Ottieni [!DNL Payment Services] _ID esercente_:

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Nella vista Home, fai clic su **[!UICONTROL Settings]**. Consulta [Home](payments-home.md) per ulteriori informazioni.
1. Seleziona la richiesta _ID esercente_ e inviarlo al proprio rappresentante commerciale, che configurerà il piano tariffario corretto.

## Abilita pagamenti live

A _ID commerciante produzione_ viene generato automaticamente e popolato in [configurazione](configure-admin.md). Non modificare o alterare questo ID.

Abilita pagamenti live:

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
