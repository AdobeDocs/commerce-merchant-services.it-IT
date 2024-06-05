---
title: Dati disponibili
description: Utilizza i dati di reporting finanziario per riconciliare il reporting con sistemi non Commerce.
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export
source-git-commit: 9a933d41bffc2af453eed00caeb941eb18b23852
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Dati disponibili

Alcuni dati di ordini e pagamenti sono disponibili per consentire di coordinare Adobe Commerce Financial Reporting tra sistemi esterni.

## Riconciliazione con il sistema ERP

È possibile eseguire la quadratura di Adobe Commerce Financial Reporting con il sistema ERP (Enterprise Resource Planning) non Adobe utilizzando l&#39;ID incremento associato a un ordine specifico.

Quando Payment Services invia l&#39;ordine Commerce a PayPal, l&#39;ID di incremento viene incluso come `custom_id` _e_ nel `invoice_id` (che contiene anche una stringa casuale dopo il `increment_id`).

Gli ID sono facilmente accessibili sia nei dettagli dell&#39;attività esercente per un pagamento che nel webhook PayPal.

Il `invoice_id` e `custom_id` sono visualizzati nella parte inferiore dei dettagli dell&#39;attività esercente per una vincita:

![`custom_id` nei dettagli dell’attività di esercente](assets/merchant-activity-ids.png){width="600" zoomable="yes"}

`custom_id` e `invoice_id` nei dettagli nel webhook di PayPal:

```json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

Per ulteriori informazioni, consulta la documentazione sulle API REST di PayPal:

* [`purchase_unit`, in cui `custom_id` e `invoice_id` risiedere](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [Mostra dettagli ordine](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
