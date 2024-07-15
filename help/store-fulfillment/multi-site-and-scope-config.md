---
title: Configurazione di più siti web e ambiti
description: Configura le scorte e i metodi di consegna per più siti Web e ambiti di archiviazione.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
exl-id: 8939046e-1c26-4380-83be-ff8e074e591d
source-git-commit: 36b57648e156ead801764f3ee4e5e6a0f3245fe6
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Configurazione di più siti web e ambiti

È possibile impostare l&#39;[Ambito](https://docs.magento.com/user-guide/configuration/scope.html) per alcuni elementi in modo da includere più siti Web, store e visualizzazioni dello store:

- [Gestisci Stock](https://docs.magento.com/user-guide/catalog/inventory-stock.html) per ambito

- Gestisci [!DNL Delivery Methods] per ambito

È possibile assegnare le scorte a un sito Web o a un ambito del negozio. Quindi, aggiorna le origini del negozio per impostare i metodi di consegna disponibili (consegna a domicilio, prelievo dal negozio).

Dopo aver aggiornato correttamente la configurazione, è possibile selezionare le opzioni di prelievo dello store nella pagina dei dettagli del prodotto (PDP) della vetrina Adobe Commerce solo per i prodotti disponibili da un’origine che consente il prelievo dello store.

## Gestione impostazioni di ritiro in-store

Abilita o disabilita le opzioni [!UICONTROL In-Store Pickup] per ogni sito Web o ambito archivio dalle [Configurazioni del metodo di consegna](enable-general.md#delivery-methods) nell&#39;amministratore.

1. Passa a **[!UICONTROL Stores > Configuration]**.

1. Selezionare l&#39;ambito (sito Web da archiviare) da configurare.

1. Con ambito selezionato, passare a **[!UICONTROL Sales > Delivery Methods]**.

1. Disabilitare o abilitare il metodo di consegna **[!UICONTROL In-Store Pickup]**.

In questa sezione puoi anche gestire la disponibilità globale del ritiro lato bordo o in-store.

Gestisci le impostazioni [!UICONTROL In-Store Pickup] e [!UICONTROL Delivery Method] per origine azionaria. Esistono numerose altre configurazioni per garantire la massima flessibilità nell’implementazione.
