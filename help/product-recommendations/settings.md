---
title: Impostazioni
description: Scopri come modificare l'origine dei tuoi dati di [!DNL Product Recommendations]  e come abilitare i consigli visivi.
exl-id: 8c074e11-e0cb-4d55-b646-30279c79bbc2
source-git-commit: 75ff893bf5867ededa49807835676ddf9b19adc9
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Impostazioni

Quando si [configura uno spazio dati SaaS](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html) per Recommendations, lo spazio dati SaaS raccoglie i dati del catalogo e i dati comportamentali della vetrina. [Adobe Sensei](https://www.adobe.com/sensei.html) analizza tali dati e calcola le associazioni di prodotti utilizzate per fornire Recommendations di prodotto.

Gli ambienti non di produzione per il test o la gestione temporanea di solito non dispongono della quantità o della qualità dei dati comportamentali della vetrina per fornire consigli di prodotto realistici. Il comportamento effettivo degli acquirenti su larga scala può essere acquisito solo in un ambiente di produzione. Per risolvere questo problema, Adobe Commerce consente di utilizzare i consigli di prodotto dell’ambiente di produzione con altri spazi di dati SaaS non di produzione. L’utilizzo di dati vetrina reali in un ambiente non di produzione consente di visualizzare in anteprima i consigli visualizzati dagli acquirenti e di sperimentarli con diversi tipi di consigli e posizioni di posizionamento. Gli acquirenti possono visualizzare in anteprima i Recommendations provenienti da uno spazio dati SaaS diverso, ma non fare clic su di essi.

Gli ordini di gestione temporanea vengono registrati utilizzando la gestione temporanea `environmentId`. Non influisce sui dati di produzione. I dati di produzione vengono recuperati utilizzando `alternateEnvironmentId`.

>[!NOTE]
>
>Quando si utilizza Product Recommendations tramite REST, è possibile utilizzare il parametro `alternateEnvironmentId` per specificare altri spazi di dati. Quando si utilizza Product Recommendations tramite GraphQL, questo parametro non è disponibile.

## Scegli l’origine dei consigli

Per modificare l’origine dei dati dei consigli di prodotto, scegli lo spazio dati SaaS con i dati comportamentali che desideri utilizzare. Prima di iniziare, assicurati che:

- La raccolta dati di Storefront deve essere [configurata e abilitata](install-configure.md) per l&#39;ambiente di produzione e [verificata](verify.md) che i dati comportamentali vengano inviati ad Adobe Commerce.
- Il catalogo dell’ambiente non di produzione deve essere essenzialmente lo stesso del catalogo di produzione. L’utilizzo di cataloghi simili garantisce che le unità di consigli sui prodotti restituite rispecchino fedelmente quelle in produzione.

1. Accedi all’amministratore dell’ambiente Adobe Commerce non di produzione.

1. Nella barra laterale _Amministratore_, passa a **Marketing** > _Promozioni_ > **Product Recommendations**.

1. Fare clic su **Impostazioni**.

   ![impostazioni consigli prodotto](assets/settings.png)
   _Impostazioni_

1. Nella sezione _Origine Recommendations_, abilita l&#39;opzione **Recupera consigli da un altro spazio dati SaaS**. La sezione _Origine Recommendations_ viene visualizzata solo in un ambiente non di produzione.

   Viene visualizzato un elenco di _Spazi dati SaaS disponibili_.

   ![impostazioni consigli prodotto](assets/settings-select-saas.png)
   _Impostazioni_

1. Selezionare lo spazio dati SaaS contenente i dati dell&#39;acquirente che si desidera utilizzare.

1. Fai clic su **Salva modifiche**.

   Adobe Commerce ora recupera i consigli dallo spazio dati selezionato.

   >[!NOTE]
   >
   > Anche se è possibile visualizzare i consigli recuperati da un altro spazio dati SaaS nella vetrina non di produzione, non è possibile fare clic sui consigli.

### Configurare un nuovo spazio dati SaaS

1. Nella sezione di origine di Recommendations, fare clic su **Modifica configurazione**.

1. Segui le istruzioni per configurare un nuovo [[!DNL Commerce] servizio](/help/landing/saas.md).

## Abilita consigli visivi

Se è installato il modulo [Visual Product Recommendations](install-configure.md), è necessario abilitare Visual Recommendations per l&#39;utilizzo del tipo di consiglio [Visual Similarity](type.md#visualsim).

Nella sezione _Visual Recommendations_, impostare **Enable Visual Recommendations** nella posizione attiva.
