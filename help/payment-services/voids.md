---
title: Vuoti
description: I vuoti consentono di liberare i fondi in un conto della carta di credito o di debito che sono bloccati o detenuti da un'autorizzazione per l'importo di un acquisto.
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout
source-git-commit: 90bfa7099924feb308397960cff76bdf177bbe49
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Vuoti

Con [!DNL Payment Services] è possibile utilizzare le funzionalità esistenti di Commerce per annullare le transazioni. I vuoti consentono di liberare i fondi in un conto della carta di credito o di debito che sono bloccati o detenuti da un&#39;autorizzazione per l&#39;importo di un acquisto.

>[!NOTE]
>
>Puoi annullare una transazione solo se il pagamento non è ancora stato acquisito.

Se il tuo negozio è [configurato](https://docs.magento.com/user-guide/configuration/sales/payment-methods.html#payment-actions){target="_blank"} per autorizzare solo i fondi (non acquisirli) presso il punto vendita, un acquisto dal tuo negozio determina un ordine con stato `Processing` nell&#39;amministratore di Commerce.

È inoltre possibile [annullare un ordine](https://docs.magento.com/user-guide/sales/order-update.html#cancel-a-pending-order){target="_blank"} non fatturato. Anche eventuali autorizzazioni non acquisite vengono annullate nell’ambito di tale processo di annullamento.

>[!NOTE]
>
>L’annullamento di un ordine genera anche un annullamento, ma l’annullamento di un ordine non attiva l’annullamento.

Per ulteriori informazioni sui passaggi di base di un ordine, consulta l&#39;argomento [Flusso di lavoro dell&#39;ordine](https://docs.magento.com/user-guide/sales/order-workflow.html){target="_blank"} nella guida utente di base.

Per informazioni sulla funzionalità di annullamento e su come annullare una transazione ordine, vedere [Elaborazione di un ordine](https://docs.magento.com/user-guide/sales/order-processing.html){target="_blank"} nella guida utente di base.
