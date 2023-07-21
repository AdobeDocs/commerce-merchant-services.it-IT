---
title: Configurazione utente
description: Imposta le origini Inventory management avanzate come negozi per esercenti per supportare la soluzione Store Fulfillment per Adobe Commerce.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, User Account, Tools and External Services
exl-id: eb735bef-c339-4d0b-b3e7-10328915725b
source-git-commit: 36b57648e156ead801764f3ee4e5e6a0f3245fe6
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Configurazione utente

Gli utenti dell’app Store Assist vengono gestiti in Adobe Commerce. Tuttavia, questi utenti non interagiscono direttamente con Adobe Commerce. La gestione utenti è configurata in Adobe Commerce per abilitare connessioni sicure tra Adobe Commerce e l’app.

Il modello utente dell’app Store Fulfillment è separato dagli altri modelli utente di Adobe Commerce. L’app mantiene il proprio modello di autorizzazione tramite ruoli utente e utenti che possono essere assegnati a tutte le posizioni o a posizioni specifiche. Sono supportate le seguenti autorizzazioni: Ordine di prelievo, Ordine di fornitura e Riduzione quantità articolo (e annullamento).

>[!TIP]
>
>Per ottenere risultati ottimali, [configurare la connessione](connect-set-up-service.md) prima di aggiungere utenti e autorizzazioni per gli associati allo store che utilizzano l’app Store Assist.

## App assistenza store - Ruoli utente

Durante la configurazione iniziale dell’utente per l’app Store Assist, crea i ruoli utente per personalizzare le autorizzazioni utente per l’app Store Assist. Ad esempio, puoi creare ruoli diversi per i responsabili dei negozi e gli associati ai negozi e assegnare risorse di ruolo diverse per gestire le autorizzazioni per ogni tipo di utente.

Configura ruoli utente da **[!UICONTROL System > Store Fulfillment App Permissions > All Store Fulfillment App Users]**.

### Informazioni ruolo

| **Campo** | **Descrizione** | **Ambito** | **Obbligatorio** |
|----------------------------|-------------------------|-----------|--------------|
| **[!UICONTROL Role Name]** | Attiva o disattiva l&#39;utente. | Globale | Sì |

### Risorse per il ruolo

| **Campo** | **Descrizione** | **Ambito** | **Obbligatorio** |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Resource Access]** | Elencare i gruppi di autorizzazioni disponibili che possono essere assegnati a un ruolo utente. Al momento, la soluzione di evasione archivio non dispone di diversi livelli di autorizzazione definiti per i ruoli delle risorse. Tutti i ruoli utente dispongono dello stesso accesso alle risorse. | Globale | Sì |

## Store Assist - Informazioni utente

Gestisci i profili utente dell&#39;app Store Assist dalle impostazioni di Admin System:  **[!UICONTROL System > Store Fulfillment App Permissions > All Store Fulfillment App Users]**.

| **Campo** | **Descrizione** | **Ambito** | **Obbligatorio** |
|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL is Active]** | Attiva o disattiva l&#39;utente. | Globale | Sì |
| **[!UICONTROL User Name]** | Nome utente associato all&#39;utente | Globale | Sì |
| **[!UICONTROL First Name]** | Nome associato all&#39;utente | Globale | No |
| **[!UICONTROL Last Name]** | Cognome associato all’utente | Globale | No |
| **[!UICONTROL Role]** | Ruolo associato all’utente | Globale | No |
| **[!UICONTROL Access to all locations]** | Assegnare agli utenti l&#39;accesso a tutti i negozi o selezionare i singoli negozi. | Globale | No |
| **Impostazioni internazionali interfaccia** | Se lo store dispone di più lingue, impostare Impostazioni internazionali interfaccia sulla lingua da utilizzare per l&#39;interfaccia di amministrazione. | Globale | No |
| **Attivo da** | Per impostare una data di inizio, seleziona l’icona del calendario. | Globale | No |
| **Attivo a** | Impostare la Data di scadenza selezionando l&#39;icona del calendario. L&#39;impostazione di una data di scadenza è utile per impostare assegnazioni temporanee di utenti o ruoli. Dopo la data di scadenza, lo stato dell’account utente cambia in `Inactive`, ma l’account può comunque essere aggiornato, se necessario. | Globale | No |
