---
title: Sviluppo per amministratori Recommendations di prodotto
description: Panoramica dell’architettura e delle funzioni di sviluppo di Product Recommendations.
exl-id: caef5e0c-dd69-4846-8f85-b1c5e1c6a28f
source-git-commit: 4a5c3550b03651279c24de6b6361ffa6dc28776e
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Sviluppo per amministratori Recommendations di prodotto

Product Recommendations è un potente strumento di marketing che puoi utilizzare per aumentare le conversioni, incrementare i ricavi e stimolare il coinvolgimento degli acquirenti. I Recommendations dei prodotti vengono visualizzati nella vetrina sotto forma di unità quali &quot;I clienti che hanno visualizzato questo prodotto hanno visto anche&quot;, &quot;I clienti che hanno acquistato questo prodotto hanno acquistato anche&quot;, &quot;Consigliato per te&quot; e così via. Adobe Commerce Product Recommendations è basato su [Adobe Sensei](https://www.adobe.com/sensei.html), che utilizza algoritmi di intelligenza artificiale e machine learning per eseguire un&#39;analisi approfondita dei dati aggregati degli acquirenti. Quando vengono combinati con il catalogo Commerce, questi dati offrono esperienze altamente coinvolgenti, pertinenti e personalizzate per l’acquirente.

>[!NOTE]
>
>Se la vetrina è stata implementata utilizzando PWA Studio, consulta la [documentazione di PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se utilizzi una tecnologia front-end personalizzata come React o Vue JS, consulta la guida utente per scoprire come integrare Product Recommendations in un ambiente [headless](headless.md). Le istanze headless devono implementare l’evento per alimentare l’area di lavoro Product Recommendation.

## Panoramica dell’architettura

Ad alto livello, i Recommendations di prodotto Commerce vengono distribuiti come SaaS. Il lato Commerce include la vetrina, che contiene l’agente di raccolta eventi e il modello di layout dei consigli, e il back-end, che include i servizi dati, il modulo Esportazione SaaS e l’interfaccia utente amministratore. I servizi di intelligence di Adobe Sensei sono utilizzati lato SaaS.

![Diagramma dell&#39;architettura dei consigli di prodotto](assets/arch-diag-sensei.svg)

Una volta installati e configurati i moduli di consigli, la vetrina inizierà a raccogliere i dati comportamentali. Adobe Sensei elabora questi dati comportamentali insieme ai dati del catalogo e calcola le associazioni di prodotti utilizzate dal servizio Recommendations. A questo punto, il commerciante può creare, gestire e distribuire unità di consigli di prodotto nella vetrina direttamente dall’interfaccia utente di amministrazione.

## Passaggi successivi

Leggi i seguenti argomenti per iniziare a utilizzare Product Recommendations:

- [Come implementare Product Recommendations](implementation-workflow.md)

- [Installare e configurare Product Recommendations](install-configure.md)

- [Crea Recommendations prodotto](create.md)
