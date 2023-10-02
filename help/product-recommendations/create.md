---
title: Crea nuovo consiglio
description: Scopri come creare un’unità di consigli di prodotto.
exl-id: d393ab78-0523-463f-9b03-ad3f523dce0f
source-git-commit: 2b5ee71618055c48bf4d6a86dbbd4708647b5d7c
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Crea nuovo consiglio

Quando crei un consiglio, puoi creare una _unità consigli_ che contiene il prodotto consigliato _elementi_.

![Unità consigli](assets/unit.png)
_Unità consigli_

Quando attivi l’unità di consigli, Adobe Commerce inizia a [raccogliere dati](workspace.md) per misurare impression, visualizzazioni, clic e così via. Il [!DNL Product Recommendations] Questa tabella mostra le metriche di ogni unità di consigli per aiutarti a prendere decisioni aziendali informate.

1. Il giorno _Amministratore_ barra laterale, vai a **Marketing** > _Promozioni_ > **Recommendations del prodotto** per visualizzare _Recommendations del prodotto_ Workspace.

1. Specifica la [Visualizzazione store](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) dove desideri che vengano visualizzati i consigli.

   >[!NOTE]
   >
   > Le unità di consigli di Page Builder devono essere create nella vista store predefinita, ma possono essere utilizzate ovunque. Per ulteriori informazioni sulla creazione di consigli di prodotto con Page Builder, consulta [Aggiungi contenuto - Product Recommendations](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html).

1. Clic **Crea consiglio**.

1. In _Denomina il consiglio_ , immettere un nome descrittivo per il riferimento interno, ad esempio `Home page most popular`.

1. In _Seleziona tipo di pagina_ , seleziona la pagina in cui vuoi visualizzare il consiglio tra le seguenti opzioni:

   - Home page
   - Categoria
   - Dettagli prodotto
   - Carrello
   - Conferma
   - [Page Builder](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html)

   Puoi creare fino a cinque unità di consigli attive per ogni tipo di pagina e fino a 25 per Page Builder. Il tipo di pagina è disattivato Al raggiungimento del limite.

   ![Nome e pagina del consiglio](assets/create-recommendation.png)
   _Nome consiglio e posizionamento della pagina_

1. In _Seleziona tipo di consiglio_ , specificare [tipo di consiglio](type.md) che si desidera visualizzare nella pagina selezionata. Per alcune pagine, il [posizionamento](placement.md) di raccomandazioni è limitato a determinati tipi.

   Alcuni tipi di consigli utilizzano dati comportamentali provenienti dai tuoi acquirenti per [modelli di apprendimento automatico del treno](behavioral-data.md) per creare consigli personalizzati. Per aiutarti a visualizzare l’avanzamento della formazione di ciascun tipo di consiglio, in questa sezione viene visualizzata una misura di preparazione per ciascun tipo. Questi indicatori di prontezza sono calcolati sulla base di due fattori:

   - Dimensione sufficiente del set di risultati: nella maggior parte degli scenari sono presenti risultati sufficienti per evitare di utilizzare [consigli di backup](behavioral-data.md#backuprecs)?

   - Sufficiente varietà di set di risultati: i prodotti restituiti rappresentano una varietà di prodotti del catalogo? L’obiettivo con questo fattore è evitare di avere una minoranza di prodotti come unici articoli consigliati in tutto il sito.

   In base ai fattori di cui sopra, viene calcolato e visualizzato un valore di fattibilità. Un tipo di consiglio è considerato pronto per la distribuzione quando il suo valore di fattibilità è pari o superiore al 75%. Un tipo di consiglio è considerato parzialmente pronto quando la sua prontezza è almeno del 50%. Un tipo di consiglio è considerato non pronto per la distribuzione quando il suo valore di fattibilità è inferiore al 50%.

   >[!NOTE]
   >
   >L’indicatore non può mai raggiungere il 100%.

   ![Tipo di consiglio](assets/create-recommendation-select-type.png)
   _Tipo di consiglio_

1. In _Etichetta di visualizzazione vetrina_ , immetti il [etichetta](placement.md#recommendation-labels) visibile agli acquirenti, ad esempio &quot;Più venduti&quot;.

1. In _Scegli il numero di prodotti_ , utilizza il cursore per specificare il numero di prodotti da visualizzare nell’unità consigli.

   Il valore predefinito è `5`, con un massimo di `20`.

1. In _Seleziona posizionamento_ , specifica il percorso in cui l&#39;unità di consigli deve essere visualizzata nella pagina.

   - Nella parte inferiore del contenuto principale
   - Nella parte superiore del contenuto principale

1. (Facoltativo) Per modificare l’ordine dei consigli, seleziona e sposta le righe nella sezione _Scegli posizione_ tabella.

   Il _Scegli posizione_ In questa sezione vengono visualizzati tutti i consigli (se presenti) creati per il tipo di pagina selezionato.

   ![Ordine consigli](assets/create-recommendation-select-placement.png)
   _Ordine consigli sulla pagina_

1. (Facoltativo) In _Filtri_ sezione, [applicare filtri](filters.md) per controllare quali prodotti vengono visualizzati nell’unità consigli.

   ![Filtri per consigli](assets/create-recommendation-filter-products.png)
   _Filtri di prodotto per consigli_

1. Al termine, fare clic su una delle seguenti opzioni:

   - **Salva come bozza** per modificare l&#39;unità di consigli in un secondo momento. Non è possibile modificare il tipo di pagina o il tipo di consiglio per un&#39;unità di consigli in stato bozza.

   - **Attiva** per abilitare l&#39;unità di consigli nella vetrina.

## Anteprima Recommendations {#preview}

Il _Anteprima prodotti consigliati_ il pannello è sempre disponibile con una selezione di esempi di prodotti che potrebbero apparire nell&#39;unità consigli quando viene distribuita nella vetrina.

Per testare un consiglio quando si lavora in un ambiente non di produzione, è possibile recuperare i dati dei consigli da un [origine diversa](settings.md). Questo consente ai commercianti di sperimentare le regole e visualizzare in anteprima i consigli prima di distribuirli in produzione.

| Campo | Descrizione |
|---|---|
| Nome | Il nome del prodotto. |
| SKU | Unità di stoccaggio assegnata al prodotto |
| Prezzo | Il prezzo del prodotto. |
| Tipo di risultato | Principale: indica che sono stati raccolti dati di formazione sufficienti per visualizzare un consiglio.<br />Backup: indica che non sono stati raccolti dati di formazione sufficienti, pertanto per riempire lo slot viene utilizzato un consiglio di backup. Vai a [Dati comportamentali](behavioral-data.md) per ulteriori informazioni sui modelli di apprendimento automatico e sui consigli di backup, |

Quando crei la tua unità di consigli, prova con il tipo di pagina, il tipo di consiglio e i filtri per ottenere un feedback in tempo reale e immediato sui prodotti che verranno inclusi. Quando inizi a capire quali prodotti vengono visualizzati, puoi configurare l’unità di consigli in base alle tue esigenze aziendali.

Adobe Commerce [filtri](filters.md) consigli per evitare di visualizzare prodotti duplicati quando più unità di consigli vengono distribuite in una singola pagina. Di conseguenza, i prodotti visualizzati nel pannello di anteprima potrebbero essere diversi da quelli visualizzati nella vetrina.

>[!NOTE]
>
> Non è possibile visualizzare in anteprima `Recently viewed` tipo di consiglio perché i dati non sono disponibili nell’amministratore.
