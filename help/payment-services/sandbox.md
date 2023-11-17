---
title: Configurare la sandbox di prova
description: Utilizza un conto PayPal sandbox per utilizzare [!DNL Payment Services] in modalità di test.
exl-id: 99c14b4e-e6cf-48f9-9546-5c0d5c71464d
feature: Payments, Checkout, Configuration, Install
source-git-commit: bfb49e3602cc80f97817a8fd8d7c4684a3a3bcd2
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---

# Configurare la sandbox di prova

Prima di iniziare l’onboarding in sandbox, devi registrarti per un account PayPal Developer gratuito e creare account sia per esercenti (da utilizzare per l’onboarding) che per acquirenti (da utilizzare per testare l’estrazione). Se necessario, puoi creare più account Developer.

Un account sandbox PayPal ti consente di utilizzare [!DNL Payment Services] in modalità di test. PayPal richiede l’utilizzo di un account di test, di un’e-mail e di una password per l’onboarding in sandbox generato da PayPal Developer Portal (Portale per sviluppatori). *Non creare un altro account durante il processo di onboarding della sandbox.*

## Onboarding nelle sandbox

Per completare l’onboarding della sandbox:

1. Accedi a [Pagina Conto PayPal per sviluppatori](https://developer.paypal.com/developer/accounts/).
1. Clic **[!UICONTROL Log in to Dashboard]** e accedi con il tuo account di test esistente di PayPal Developer Portal generato da Business sandbox o fai clic su **Registrati** per creare un account.
1. Crea un account sandbox PayPal:
   1. Vai a _[!UICONTROL Testing Tools]_>**[!UICONTROL Sandbox Accounts]**.
   1. Clic **[!UICONTROL Create account]**.

      Se hai creato un conto sandbox PayPal durante il processo di onboarding di PayPal nella sandbox, devi [reimpostare la sandbox di onboarding](#reset-your-sandbox-account) perché o non puoi verificare l’e-mail.

   1. Seleziona **[!UICONTROL Business]** come Tipo di account e fai clic su **[!UICONTROL Create]**.
   1. In _[!UICONTROL Sandbox Accounts]_, fare clic sui tre punti nella sezione_[!UICONTROL Manage accounts]_ per l’account sandbox creato.
   1. Clic **[!UICONTROL View/edit account]**.

      ![PayPal - Visualizza/Modifica conto sandbox](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. Copia e salva l&#39;ID e-mail e la password generata dal sistema per utilizzi futuri.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clic **[!UICONTROL Sandbox onboarding]**.

   Questa opzione è visibile se non hai ancora completato l’onboarding della sandbox per [!DNL Payment Services].

   Un ID commerciante sandbox viene generato automaticamente e popolato in [impostazioni](settings.md). Non modificare o alterare questo ID.

   Viene visualizzata una finestra PayPal per collegare un conto PayPal per iniziare ad accettare i pagamenti.

1. Immetti l&#39;e-mail e la password del conto sandbox PayPal generato al passaggio 3 (non le informazioni sul conto aziendale PayPal) e il paese o l&#39;area geografica.
1. Clic **[!UICONTROL Next]**.

   ![PayPal - Connetti conto PayPal per pagamenti](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. Continua a seguire il flusso PayPal, utilizzando le credenziali del tuo account sandbox salvate in precedenza.
1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

   Il **[!UICONTROL Sandbox onboarding]** Non è più visibile ed è visualizzato il testo &quot;Pagamenti sandbox in sospeso&quot;.

Quando l’onboarding in Sandbox PayPal viene approvato, dovresti visualizzare una notifica che informa che il sistema di pagamento è attualmente in modalità sandbox e non elabora pagamenti live.

>[!IMPORTANT]
>
>Se revochi il consenso a [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] per l&#39;elaborazione dei pagamenti (nelle impostazioni del conto PayPal), gli ordini nel tuo Negozio non possono essere elaborati da [!DNL Payment Services]. Nella pagina principale di Payment Services viene visualizzato un avviso relativo alla revoca del consenso. Per ignorare l’avviso, fai clic su **[!UICONTROL Do not show again]**.

### Reimposta l’account sandbox

Se hai creato un account sandbox PayPal durante il processo di onboarding di PayPal sandbox, devi reimpostare la sandbox di onboarding perché o non puoi verificare l’e-mail.

Per ripristinare l’account sandbox:

1. Clic **[!UICONTROL Reset sandbox]**. [Crea un conto PayPal business sandbox](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account).
1. Clic **[!UICONTROL Sandbox onboarding]** e completare la serie di passaggi successiva.

## Abilita numero di telefono del contatto

Il numero di telefono di contatto ti consente di ottenere i numeri di telefono di contatto che PayPal raccoglie dai tuoi clienti. PayPal raccoglie sempre i numeri di telefono di contatto dei titolari dei conti PayPal per aiutarli a confermare le loro identità e a contattarli per risolvere i problemi sui loro conti o per completare i loro processi di evasione. Tuttavia, PayPal scoraggia l&#39;uso dei numeri di telefono di contatto direttamente dal commerciante perché può avere un impatto negativo sulle vendite. Consulta la [PayPal ottieni i numeri di telefono del contatto](https://www.sandbox.paypal.com/businessmanage/preferences/website) per ulteriori informazioni.

Questa funzione è `off` per impostazione predefinita. Quando lo abiliti, gli amministratori dei negozi possono visualizzare i numeri di telefono quando un cliente completa un flusso di pagamento con marchio all’esterno della pagina di pagamento.

>[!IMPORTANT]
>
>Questa impostazione non si applica ad altri flussi di pagamento.

## Test in ambiente sandbox

Consulta [Test e convalida](test-validate.md) per ulteriori informazioni.
