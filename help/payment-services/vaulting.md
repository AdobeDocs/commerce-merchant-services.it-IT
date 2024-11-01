---
title: Vaulting con carta di credito
description: Gli acquirenti possono archiviare (salvare) i dati della carta di credito per acquisti futuri.
exl-id: b4060307-ffcd-41cb-9b9d-a2fef02f23bd
feature: Payments, Checkout
source-git-commit: 37380063242b6d904910be731b8e58471625e9cb
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Vaulting con carta di credito

Converti i clienti occasionali in acquirenti fedeli con il vaulting delle carte di credito. Gli acquirenti possono salvare, o &quot;vaultare&quot;, le credenziali della loro carta di credito durante il pagamento per utilizzarle in un acquisto successivo per lo stesso, o un altro, archiviare all&#39;interno dello stesso account esercente.

![Archivia la carta di credito per un uso successivo](assets/save-card-for-later.png){width="400" zoomable="yes"}

Gli acquirenti utilizzano il token memorizzato per completare un pagamento futuro con le informazioni sulla carta di credito salvate.

![Usa credenziali archiviate per acquisti futuri](assets/use-stored-card.png){width="400" zoomable="yes"}

Possono anche eliminare facilmente le loro carte di credito archiviate da [Metodi di pagamento archiviati](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/stored-payment-methods) nel loro Account personale.

![Metodi di pagamento memorizzati nel mio account](assets/stored-payment-methods.png){width="400" zoomable="yes"}

>[!WARNING]
>
>PayPal può attualmente memorizzare un massimo di cinque carte a pagamento.

## Abilita vaulting

Puoi abilitare il vaulting delle carte di credito, per i clienti _e_ commercianti nell&#39;amministratore, per i tuoi negozi in [!DNL Payment Services] [Impostazioni](settings.md#card-vaulting).

## Utilizzare il vaulting in Amministrazione

Se un cliente dispone di una carta di credito precedentemente archiviata, un esercente può creare un ordine successivo per quel cliente nell&#39;Amministratore utilizzando i propri metodi di pagamento archiviati.

Puoi usare le carte ad archivio nell&#39;Amministratore solo se il cliente ha un account esistente e un token valido memorizzato nel sistema da un pagamento completato in precedenza.

Per creare un ordine nell’amministratore per un cliente utilizzando la sua carta di credito archiviata:

1. [Crea un ordine e aggiungi prodotti](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order.html).
1. In _[!UICONTROL Payment & Shipping Information]_, selezionare **[!UICONTROL Stored Cards]**come metodo di pagamento.
1. Seleziona il metodo di pagamento con carta di credito archiviata desiderato.
1. Dopo aver completato tutti gli altri passaggi necessari per l&#39;ordine, [invialo](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order.html?lang=en#step-3%3A-submit-the-order).

   ![Utilizza carta di credito archiviata in Amministratore per il cliente](assets/admin-vaultedcard.png){width="600" zoomable="yes"}

## Sicurezza

Le informazioni minime sulla carta di credito vengono condivise con l&#39;acquirente, che visualizza solo le ultime quattro cifre, la data di scadenza e il marchio della carta di credito archiviata. Le informazioni sulla carta di credito vengono archiviate con il provider di pagamenti per soddisfare gli standard di conformità [PCI](security.md#PCI-compliance).
