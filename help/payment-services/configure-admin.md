---
title: Configurazione servizi di pagamento legacy
description: Dopo l’installazione, puoi configurare [!DNL Payment Services] in Admin at the store configuration (Amministrazione nella configurazione dell’archivio).
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: 8dd4f629fa60959588cee4ea22f9fb577f338716
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# Legacy [!DNL Payment Services] Configurazione

Puoi personalizzare [!DNL Payment Services] alle tue esigenze con utili opzioni di configurazione nell’Admin.

Quando si configura [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] in Admin, tali configurazioni si applicano solo all&#39;ambiente impostato in _[!UICONTROL Method]_campo di_[!UICONTROL General Configuration]_. Tutte le modifiche apportate nei campi di configurazione sono indipendenti dal passaggio _[!UICONTROL Method]_selection - se si cambia metodo, le selezioni non vengono ripristinate.

## Configurazione generale

È possibile abilitare [!DNL Payment Services] per il tuo negozio e abilitare i test sandbox o i pagamenti live nel _[!UICONTROL General Configuration]_sezione.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.

   ![Visualizzazione Metodi](assets/methods-view.png){width="400" zoomable="yes"}

1. Espandi _[!UICONTROL Recommended Solutions]_sezione.
1. In _[!UICONTROL [!DNL Payment Services]]_, espandere la sezione_[!UICONTROL General Configuration]_ sezione.
1. Per **Abilita**, impostarlo su `Yes` per abilitare [!DNL Payment Services] per il tuo negozio.
1. Per **Metodo**, impostarlo su `Sandbox` se stai ancora testando [!DNL Payment Services] per il tuo negozio o `Production` se sei pronto per abilitare i pagamenti live.

   >[!WARNING]
   >
   >Il tuo _[!UICONTROL Sandbox Merchant ID]_e_[!UICONTROL Production Merchant ID]_ sono generati automaticamente e presenti nei rispettivi campi quando hai completato l’onboarding per la sandbox e/o la produzione. Non rimuovere o modificare questi ID.

1. Per **Descrittore morbido** (valori personalizzati visualizzati nei rendiconti bancari delle transazioni dei clienti per distinguere tra negozi, marchi o cataloghi), aggiungi il testo personalizzato (fino a 22 caratteri) nel campo di testo, sostituendo `Custom descriptor` o il valore esistente.
1. Clic **[!UICONTROL Save Config]** per salvare le modifiche.
1. Accedi a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Enable] | sito web | Attiva o disattiva [!DNL Payment Services] per il tuo sito web. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | visualizzazione store | Imposta il metodo o l’ambiente per lo store. Opzioni: [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Sandbox Merchant ID] | visualizzazione store | L’ID venditore della sandbox, generato automaticamente durante l’onboarding della sandbox. Non modificare o alterare questo ID. |
| [!UICONTROL Production Merchant ID] | visualizzazione store | L’ID esercente di produzione, generato automaticamente durante l’onboarding della sandbox. Non modificare o alterare questo ID. |
| [!UICONTROL Soft Descriptor] | visualizzazione sito Web o store | Aggiungi un soft descriptor ai tuoi siti web e alle viste store per aggiungere informazioni alle transazioni dei clienti che delineano marchi, store o linee di prodotti. |

## [!UICONTROL Credit Card Fields]

Il [!UICONTROL Credit Card Fields] le opzioni di pagamento forniscono un pagamento semplice e sicuro per i metodi di pagamento con carta di credito o con carta di debito.

Consulta [Opzioni di pagamento](payments-options.md#paypal-smart-buttons) per ulteriori informazioni.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandi _[!UICONTROL Recommended Solutions]_sezione.
1. In _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL Credit Card Fields]_ sezione.
1. Per **[!UICONTROL Title]**, immettere il testo (se necessario) per modificare il nome del metodo di pagamento come mostrato durante l&#39;estrazione.
1. A [imposta l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), seleziona **[!UICONTROL Authorize]** o **Autorizza e acquisisci**.
1. Per assegnare la priorità a un metodo di pagamento nella pagina di pagamento, fornisci `Numeric Only` valore in **[!UICONTROL Sort order]** campo.
1. Per **[!UICONTROL Show on checkout page]**, scegli `Yes` per abilitare i campi della carta di credito nella pagina di pagamento.
1. Per **[!UICONTROL Vault Enabled]**, scegli `Yes` per abilitare il vaulting della carta di credito per il pagamento.
1. Per **[!UICONTROL Vault Enabled in Admin]**, scegli `Yes` per consentire al commerciante di creare ordini per i clienti utilizzando la carta di credito a scaffale.
1. Per abilitare **[!UICONTROL 3DS Secure authentication]** (`Off` per impostazione predefinita) scegli `Always` o `When required`.
1. Per **[!UICONTROL Debug Mode]**, scegli `Yes` per abilitare la modalità di debug, oppure `No` per disattivarlo.
1. Clic **[!UICONTROL Save Config]** per salvare le modifiche.
1. Accedi a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella vista Metodo di pagamento durante l&#39;estrazione. Opzioni: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sito web | Il [azione di pagamento](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | visualizzazione store | L&#39;ordinamento per il metodo di pagamento specificato nella pagina di pagamento. `Numeric Only` valore |
| [!UICONTROL Show on checkout page] | sito web | Attiva o disattiva i campi della carta di credito nella pagina di pagamento. Opzioni: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | visualizzazione store | Attiva o disattiva [vaulting con carta di credito](vaulting.md). Opzioni: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | visualizzazione store | Attiva o disattiva la possibilità per [esercente per completare gli ordini per i clienti nell’Admin](vaulting.md) utilizzando un metodo di pagamento a scaffale. Opzioni: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3DS Secure authentication] | sito web | Attiva o disattiva [Autenticazione protetta 3DS](security.md#3ds). Opzioni: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Apple Pay]

Il [!UICONTROL Apple Pay] L&#39;opzione di pagamento consente al commerciante di offrire Apple Pay ai propri acquirenti, che possono utilizzare il Touch ID sui loro dispositivi per effettuare acquisti dal browser Safari. Gli esercenti possono aggiungere fino a 99 domini per account esercente.

Consulta [Opzioni di pagamento](payments-options.md#apple-pay-button) per ulteriori informazioni.

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandi _[!UICONTROL Recommended Solutions]_sezione.
1. In _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL Apple Pay]_ sezione.
1. Per **[!UICONTROL Title]**, immettere il testo (se necessario) per modificare il nome del metodo di pagamento come mostrato durante l&#39;estrazione.
1. A [imposta l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), seleziona **[!UICONTROL Authorize]** o **[!UICONTROL Authorize and Capture]**.
1. Da mostrare [!DNL Apple Pay] nella pagina di pagamento, seleziona `Yes` per **[!UICONTROL Show buttons on checkout page]**.
1. Da mostrare [!DNL Apple Pay] nella pagina dei dettagli del prodotto seleziona `Yes` per **[!UICONTROL Show buttons on product detail page]**.
1. Da mostrare [!DNL Apple Pay] nell’anteprima del mini carrello, seleziona `Yes` per **[!UICONTROL Show buttons in mini cart preview]**.
1. Da mostrare [!DNL Apple Pay] nella pagina del carrello, seleziona `Yes` per **[!UICONTROL Show buttons on cart page]**.
1. Per abilitare la modalità di debug, seleziona `Yes` per **[!UICONTROL Debug Mode]** (`No` disattiva).
1. Per salvare le modifiche, fai clic su **[!UICONTROL Save Config]** .
1. Accedi a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella vista Metodo di pagamento durante l&#39;estrazione. Opzioni: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sito web | Il [azione di pagamento](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | sito web | Attiva o disattiva [!DNL Apple Pay] nella pagina di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on product detail page] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] nella pagina dei dettagli del prodotto. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] nell’anteprima del mini-carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] nella pagina del carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!DNL PayPal Payment Buttons]

Il [!DNL PayPal payment buttons] le opzioni di pagamento offrono al cliente un processo di pagamento semplice, veloce e sicuro.

Consulta [Opzioni di pagamento](payments-options.md#paypal-smart-buttons) per ulteriori informazioni.

Configura [!DNL PayPal payment buttons]

Puoi abilitare e configurare le opzioni di pagamento dei pulsanti di pagamento PayPal in Admin:

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandi _[!UICONTROL Recommended Solutions]_sezione.
1. In _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL PayPal payment buttons]_ sezione.
1. Per modificare il nome del metodo di pagamento come mostrato durante l&#39;estrazione, modificare il _[!UICONTROL Title]_campo.
1. A [imposta l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), seleziona **[!UICONTROL Authorize]** o **[!UICONTROL Authorize and Capture]**.
1. Per assegnare la priorità a un metodo di pagamento nella pagina di pagamento, fornisci `Numeric Only` valore in **[!UICONTROL Sort order]** campo.
1. Per attivare/disattivare la [Messaggistica pagamento posticipato](payments-options.md#pay-later-button), seleziona `Yes`/`No` per **[!UICONTROL Display Pay Later Message]**.
1. Per visualizzare i pulsanti di pagamento PayPal nella pagina di pagamento, seleziona `Yes` per **[!UICONTROL Show buttons on checkout page]**.
1. Per visualizzare i pulsanti di pagamento PayPal nella pagina dei dettagli del prodotto, seleziona `Yes` per **[!UICONTROL Show buttons on product detail page]**.
1. Per visualizzare i pulsanti di pagamento PayPal nell&#39;anteprima del mini carrello, seleziona `Yes` per **[!UICONTROL Show buttons in mini cart preview]**.
1. Per visualizzare i pulsanti di pagamento PayPal nella pagina del carrello, seleziona `Yes` per **[!UICONTROL Show buttons on cart page]**.
1. Per abilitare Venmo come opzione di pagamento, seleziona `Yes` per **[!UICONTROL Venmo Enabled]**.
1. Per abilitare le carte di credito e di debito come opzione di pagamento (pulsante PayPal Smart), seleziona `Yes` per **[!UICONTROL Credit and Debit Card Enabled]**.
1. Per attivare/disattivare la [PayPal Paga più tardi](payments-options.md#pay-later-button) opzione di pagamento, seleziona `Yes`/`No` per **[!UICONTROL PayPal Pay Later Enabled]**.
1. Per abilitare la modalità di debug, seleziona `Yes` per **[!UICONTROL Debug Mode]** (`No` disattiva).
1. Per salvare le modifiche, fai clic su **[!UICONTROL Save Config]** .
1. Accedi a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella visualizzazione Metodo di pagamento durante l&#39;estrazione. Opzioni: campo di testo |
| [!UICONTROL Payment Action] | sito web | Il [azione di pagamento](https://docs.magento.com/user-guide/configuration/sales/payment-methods.html#payment-actions){target="_blank"} per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | sito web | Abilita o disabilita la funzione di messaggistica Paga più tardi nel carrello, nella pagina del prodotto, nel mini-carrello e durante il flusso di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on checkout page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on product detail page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina dei dettagli del prodotto. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nell’anteprima del mini-carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina del carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | visualizzazione store | Abilita o disabilita l&#39;opzione di pagamento Venmo in cui sono visualizzati i pulsanti di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | visualizzazione store | Abilita o disabilita le opzioni per le carte di credito e di debito in cui vengono visualizzati i pulsanti di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | visualizzazione store | Abilita o disabilita l&#39;opzione di pagamento PayPal Pay Later quando vengono visualizzati i pulsanti di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Stile pulsante

Puoi anche configurare il _[!UICONTROL Button style]_opzioni dei pulsanti di pagamento:

1. Il giorno _Amministratore_ barra laterale, vai a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandi _[!UICONTROL Recommended Solutions]_sezione.
1. In _[!UICONTROL [!DNL Payment Services]]_, espandere la sezione_[!UICONTROL PayPal Smart Button Styling]_ sezione.
1. Per impostare il layout, seleziona `Vertical` o `Horizontal` per **[!UICONTROL Layout]**
1. Per impostare il colore, selezionare uno dei colori disponibili in **[!UICONTROL Color]**.
1. Per impostare la forma, selezionare `Rectangular` o `Pill` per **[!UICONTROL Shape]**.
1. Per utilizzare l&#39;altezza di default, selezionate `Yes` o `No` per **[!UICONTROL Use Default Height]**.
1. Per impostare l&#39;altezza personalizzata, aggiungi l&#39;altezza in pixel desiderata per **[!UICONTROL Height]**.
1. Per impostare la tagline, seleziona `Yes` o `No` per **[!UICONTROL Tagline]**.
1. Per salvare le modifiche, fai clic su **[!UICONTROL Save Config]** .
1. Accedi a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

Puoi anche configurare lo stile dei pulsanti di pagamento [in Impostazioni](settings.md#button-style) dalla pagina Home di Payment Services.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|--- |--- |--- |
| [!UICONTROL Layout] | Visualizzazione store | Definire lo stile del layout per i pulsanti di pagamento Paypal. Opzioni: `[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | Visualizzazione store | Definisci il colore dei pulsanti di pagamento Paypal. Opzioni: [!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | Visualizzazione store | Definire la forma dei pulsanti di pagamento Paypal. Opzioni: `[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | Visualizzazione store | Definisce se i pulsanti di pagamento PayPal utilizzano un&#39;altezza predefinita. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | Visualizzazione store | Definisci l&#39;altezza dei pulsanti di pagamento PayPal. Valore predefinito: nessuno |
| [!UICONTROL Label] | Visualizzazione store | Definisci l&#39;etichetta visualizzata nei pulsanti di pagamento PayPal. Opzioni: `[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | Visualizzazione store | Attiva tagline. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Svuota la cache

Se si modifica la configurazione, [svuotare manualmente la cache](/help/payment-services/settings.md#flush-the-cache) in modo che nell’archivio siano visualizzate le impostazioni di configurazione più recenti.
