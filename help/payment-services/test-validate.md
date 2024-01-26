---
title: Test e convalida
description: I test e la convalida garantiscono che [!DNL Payment Services] Le funzioni funzionano come previsto e forniscono ai clienti le migliori opzioni di pagamento
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout
source-git-commit: 5fe23b5aba9ad0a2a6c995fa6ade78f46fe7e3e1
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Test e convalida

Prima di esporre [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] per gli acquirenti, è consigliabile eseguire il test nell’ambiente sandbox _e_ in produzione. I test e la convalida garantiscono che [!DNL Payment Services] Le funzioni funzionano come previsto e forniscono le migliori opzioni di pagamento per il tuo negozio e clienti.

## Test in ambiente sandbox

Test [!DNL Payment Services] in un ambiente sandbox è un passaggio importante di convalida, anche se si tratta di un ambiente simulato connesso solo alla sandbox PayPal, non a banche e commercianti reali.

1. Completa il pagamento dal tuo negozio tramite [Campi carta di credito](payments-options.md#credit-card-fields) o uno qualsiasi dei [Pulsanti di pagamento PayPal](payments-options.md#paypal-smart-buttons). Consulta [Verifica delle credenziali](#testing-credentials) per ulteriori informazioni sull&#39;utilizzo di carte di credito false per i test.
1. Acquisizione (quando l&#39;azione di pagamento è [imposta su `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)), [rimborso](refunds.md), o [void](voids.md) l’ordine appena completato. È inoltre possibile [creare una fattura](https://docs.magento.com/user-guide/sales/invoice-create.html){target="_blank"} per un ordine, se l’azione di pagamento è impostata su `Authorize` invece di `Authorize and Capture`.
1. Entro 24-48 ore, visualizza la transazione e altre informazioni in [Rapporto Pagamenti](payouts.md).
1. Vedi i dettagli dell’ordine in [Rapporto stato pagamento ordine](order-payment-status.md).

### Verifica delle credenziali

Durante il test e la convalida della sandbox è necessario utilizzare numeri di carta di credito falsi, in modo da non creare spese effettive per un account di carta di credito esistente.

Utilizza il generatore di carte di credito di PayPal per [genera informazioni casuali sulla carta di credito](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157) per il test.

Per testare Apple Pay in modalità sandbox:

* Creare un [account del tester sandbox di Apple](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account), completo di informazioni false sulla carta di credito e sulla fatturazione.
* [Registrare i domini sandbox](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains).

>[!NOTE]
>
>A volte l&#39;elaborazione dei pagamenti sandbox di PayPal è lenta e il servizio può occasionalmente andare in tilt. Questa situazione non è un&#39;indicazione della velocità e dell&#39;efficienza del processo di pagamento dei prodotti vivi.

## Test in produzione

Si consiglia vivamente di eseguire il test [!DNL Payment Services] in produzione, con carte di credito reali e banche, prima di esporre questa funzionalità agli acquirenti. Anche se il test [!DNL Payment Services] in sandbox è importante, il test in produzione è il metodo più stupido per garantire [!DNL Payment Services] funziona come previsto.

Puoi testare [!DNL Payment Services] in produzione in uno dei due modi seguenti:

* Scegli un momento in cui sai che nessun ordine verrà effettuato dagli acquirenti.
* Utilizza un archivio Web temporaneamente inaccessibile agli acquirenti, ma che è accessibile per i test.

Completa i test di produzione con carte di credito reali e account PayPal, testando l&#39;intero ciclo di vita di un pagamento, inclusa l&#39;acquisizione e il rimborso. Il completamento dell&#39;intero flusso di pagamento e di pagamento durante il test offre un&#39;immagine chiara di come [!DNL Payment Services] Questa funzionalità è disponibile anche quando è utilizzata da clienti live.

È inoltre necessario verificare che le informazioni visualizzate nei rendiconti bancari per i metodi di pagamento utilizzati nei test di produzione siano corrette e previste (inclusa la descrizione della propria attività).

Per testare Apple Pay in modalità di produzione, devi [registrare i domini di produzione](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).
