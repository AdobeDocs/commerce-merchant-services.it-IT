---
title: Posizione archivio e configurazione del sistema di mappatura
description: Configurare un provider di servizi a distanza per supportare la mappatura della posizione del negozio nell'interfaccia utente della vetrina. Le soluzioni Store Fulfillment richiedono un fornitore a distanza per abilitare la ricerca nel punto vendita al dettaglio e altre funzionalità di mappatura e pianificazione per il flusso di lavoro di implementazione end-to-end.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
exl-id: d09c4652-e2eb-49dc-8c42-2aa9b6be5d6b
source-git-commit: 36b57648e156ead801764f3ee4e5e6a0f3245fe6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Impostazione della posizione del negozio e della mappatura

Abilitare le funzionalità di mappatura e posizione del negozio per il completamento del negozio configurando un provider di [distanza](https://docs.magento.com/user-guide/catalog/inventory-configure-distance-priority.html) per la ricerca di posizioni del negozio al dettaglio.

**Requisiti**

Durante il processo di configurazione, fornisci una chiave API Google per la piattaforma Google Maps. In caso contrario, [generarne uno dalla piattaforma Google Maps](https://docs.magento.com/user-guide/catalog/inventory-configure-distance-priority.html#configure-google-maps).

Per configurare il provider di distanze:

1. Dalla configurazione **[!UICONTROL Stores > General]** in Admin, aggiungi l&#39;integrazione Google Maps per il tipo di contenuto Map.

   - Vai a **[!UICONTROL Stores > Configuration  > General > Content Management]**.

   - Aggiungi la chiave API Google al campo **[!UICONTROL Google Maps API Key]**.

1. Dalla configurazione **[!UICONTROL Stores > Inventory]** nell&#39;amministratore, selezionare il provider di distanza per il completamento del punto vendita.

   - Vai a **[!UICONTROL Stores > Configuration > Catalog > Inventory]**.

   - Espandere la sezione **[!UICONTROL Distance Provider for Distance Based SSA]**.

   - Impostare **Provider** su **Google Map**.

1. Configurare le impostazioni per **[!UICONTROL Google Distance Provider]**.

   - Aggiungi la tua **chiave API Google**.

   - Imposta **[!UICONTROL Computation Mode]** su `Driving` e **[!UICONTROL Value]** su `Distance`
