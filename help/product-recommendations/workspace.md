---
title: '[!DNL Product Recommendations] Workspace'
description: Scopri come configurare, gestire e monitorare le prestazioni dei consigli di prodotto.
exl-id: 85a06cc3-91b9-484a-96a9-fc85718e6d70
source-git-commit: 25d5321b6f29bab5d8cf329170f3644f35100438
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# [!DNL Product Recommendations] Workspace

Nell&#39;area di lavoro [!DNL Product Recommendations] viene visualizzato un elenco di consigli configurati in precedenza con metriche che consentono di tenere traccia del successo di ogni consiglio. L’elenco può essere configurato per calcolare le metriche per l’ultimo giorno, settimana o mese. Puoi utilizzare le metriche per creare informazioni fruibili in base alla frequenza con cui viene visualizzata o cliccata un’unità di consigli, oppure per analizzare le prestazioni dei consigli.

![Area di lavoro Recommendations](assets/workspace.png)
_Recommendations Workspace_

## Impostare l&#39;ambito

Inizialmente l&#39;[ambito](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) di tutte le impostazioni dei consigli è impostato su `Default Store View`. Se l&#39;installazione di Commerce include più visualizzazioni dello store, impostare **Ambito** nella [visualizzazione dello store](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) in cui vengono applicate le raccomandazioni.

## Impostare l’intervallo di date delle metriche

1. Fare clic sul controllo **Calendario** ![Selettore calendario](assets/icon-calendar.png).

1. Scegliere una delle opzioni seguenti:

   - Ultime 24 ore
   - Ultimi 7 giorni
   - Ultimi 30 giorni

   I valori calcolati nelle colonne delle metriche cambiano per riflettere l’intervallo di date corrente.

## Mostra/nascondi colonne

1. Nell&#39;angolo superiore sinistro fare clic su **Mostra/nascondi** ![Selettore colonna](assets/icon-show-hide-columns.png) colonne.

   Le colonne visibili sono contrassegnate da un segno di spunta blu.

1. Nel menu, effettuate una delle seguenti operazioni:

   - Per visualizzare una colonna nascosta, fare clic sul nome di una colonna senza segno di spunta.
   - Per nascondere una colonna visibile, fare clic su un nome di colonna con un segno di spunta.

   La tabella viene aggiornata per includere solo le colonne selezionate.

   ![Area di lavoro Recommendations](assets/workspace-select-columns.png)
   _Mostra/nascondi colonne_

## Impostazioni

Le impostazioni determinano lo spazio di dati SaaS che fornisce i dati comportamentali dei consigli.

- Per modificare la posizione di origine dei dati comportamentali consigliati, scegli un diverso spazio di dati SaaS.

- Per configurare un nuovo spazio dati SaaS, fare clic su **Modifica configurazione**. Per ulteriori informazioni, vedere [Impostazioni](settings.md).

![Impostazioni Recommendations](assets/settings.png)
_Impostazioni Recommendations_

## Visualizza dettagli

1. Nella tabella, fai clic sul consiglio che desideri esaminare.

   ![Area di lavoro Recommendations](assets/recommendation-detail.png)
   _Dettagli tasso di conversione home page_

1. Per cambiare lo stato del consiglio, fare clic su **Attiva** o **Disattiva**.

## Modifica consiglio

Dalla pagina dei dettagli dei consigli, fai clic su **Modifica**. Per ulteriori informazioni, vai a [Modifica Recommendations](edit.md).

## Crea consiglio

Dalla pagina dei dettagli dei consigli, fai clic su **Crea**. Per ulteriori informazioni, vai a [Crea Recommendations](create.md).

## Controlli Workspace

| Controllo | Descrizione |
|---|---|
| ![Selettore calendario](assets/icon-calendar.png) | Determina l’intervallo di tempo utilizzato per i calcoli delle metriche. Opzioni: 24 ore / 7 giorni / 30 giorni |
| ![Selettore colonna](assets/icon-show-hide-columns.png) | Determina le colonne visualizzate nella tabella [!DNL Product Recommendations]. |
| Impostazioni | Determina lo spazio di dati SaaS in cui vengono recuperati i dati sul comportamento dei consigli e abilita anche il tipo di consiglio per similarità visiva. |
| Crea consiglio | Apre la pagina [Crea nuovo consiglio](create.md). |

## Descrizioni colonne

| Colonna | Descrizione |
|---|---|
| Nome | Nome del consiglio. |
| Pagina | Pagina in cui viene visualizzato il consiglio. |
| Tipo | Il tipo di consiglio. |
| Stato | Lo stato del consiglio. Opzioni: Inattivo/Attivo/Bozza |
| Creato | Data di creazione del consiglio. |
| Ultima modifica | Data dell’ultima modifica apportata al consiglio. |
| Impression | Il numero di volte in cui un’unità di consigli viene caricata e sottoposta a rendering su una pagina. Nella pagina viene eseguito il rendering di un’unità di consigli che si trova sotto la piega del riquadro di visualizzazione del browser, ma non viene visualizzata dall’acquirente. In questo caso, l’unità di cui è stato eseguito il rendering viene conteggiata come impression, ma una visualizzazione viene conteggiata solo se l’utente fa scorrere l’unità fino alla visualizzazione. |
| vImpression | (Impression visualizzabili) Il numero di unità di consigli che registrano almeno una visualizzazione. |
| Visualizzazioni | Il numero di unità di consigli visualizzate nella finestra della vista del browser del cliente. Questo evento può essere attivato più volte su una pagina. |
| Clic | Somma del numero di volte in cui un acquirente fa clic su un elemento nell&#39;unità di consigli e del numero di volte in cui fa clic sul pulsante **Aggiungi al carrello** nell&#39;unità di consigli |
| Ricavi | I ricavi determinati dai consigli per l’intervallo di tempo corrente. |
| Ricavi Lt | (Ricavi ciclo di vita) I ricavi del ciclo di vita generati da un consiglio. |
| Visibilità | Percentuale di unità di consigli registrate per la visualizzazione. |
| Ctr | (Percentuale di click-through) Percentuale di unit impression per il consiglio che registra un clic. |
| vCtr | (Percentuale di click-through visualizzabile) Percentuale di impression visualizzabili per l’unità di consigli che registra un clic. |
