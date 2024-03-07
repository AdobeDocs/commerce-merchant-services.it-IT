---
title: Sviluppo per amministratori Recommendations di prodotto
description: Panoramica dell’architettura e delle funzioni di sviluppo di Product Recommendations.
exl-id: caef5e0c-dd69-4846-8f85-b1c5e1c6a28f
source-git-commit: a433d970e83792a9f53b2a09afd84c335d980024
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Sviluppo per amministratori Recommendations di prodotto

Product Recommendations è un potente strumento di marketing che puoi utilizzare per aumentare le conversioni, incrementare i ricavi e stimolare il coinvolgimento degli acquirenti. I Recommendations dei prodotti vengono visualizzati nella vetrina sotto forma di unità quali &quot;I clienti che hanno visualizzato questo prodotto hanno visto anche&quot;, &quot;I clienti che hanno acquistato questo prodotto hanno acquistato anche&quot;, &quot;Consigliato per te&quot; e così via. Adobe Commerce Product Recommendations si basano su [Adobe Sensei](https://www.adobe.com/sensei.html), che utilizza algoritmi di intelligenza artificiale e machine learning per eseguire un’analisi approfondita dei dati aggregati degli acquirenti. Quando vengono combinati con il catalogo Commerce, questi dati offrono esperienze altamente coinvolgenti, pertinenti e personalizzate per l’acquirente.

>[!NOTE]
>
>Se la vetrina è implementata utilizzando PWA Studi, consulta [Documentazione di PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se utilizzi una tecnologia front-end personalizzata come React o Vue JS, consulta la guida utente per scoprire come integrare Product Recommendations in una [headless](headless.md) ambiente. Le istanze headless devono implementare l’evento per alimentare l’area di lavoro Product Recommendation.

## Panoramica dell’architettura

Ad alto livello, Commerce Product Recommendations viene distribuito come SaaS. Il lato Commerce include la vetrina, che contiene l’agente di raccolta eventi e il modello di layout dei consigli, e il back-end, che include i servizi dati, il modulo Esportazione SaaS e l’interfaccia utente amministratore. I servizi di intelligence di Adobe Sensei sono utilizzati lato SaaS.

![Diagramma dell’architettura dei consigli di prodotto](assets/arch-diag-sensei.svg)

Una volta installati e configurati i moduli di consigli, la vetrina inizierà a raccogliere i dati comportamentali. Adobe Sensei elabora questi dati comportamentali insieme ai dati del catalogo e calcola le associazioni di prodotti utilizzate dal servizio Recommendations. A questo punto, il commerciante può creare, gestire e distribuire unità di consigli di prodotto nella vetrina direttamente dall’interfaccia utente di amministrazione.

## Tipi di dati

I Recommendations del prodotto richiedono i seguenti dati:

- **Comportamento** - Dati del coinvolgimento di un cliente sul tuo sito, ad esempio visualizzazioni di prodotti, elementi aggiunti al carrello e acquisti. Commerce e Adobe Sensei non raccolgono informazioni personali identificabili.

- **Catalogo** - Metadati dei prodotti come nome, prezzo, disponibilità e così via.

Quando si installa `magento/product-recommendations` Adobe Sensei aggrega i dati comportamentali e di catalogo e crea Product Recommendations per ciascun tipo di consiglio. Il servizio Product Recommendations distribuisce quindi tali consigli nella vetrina.

>[!NOTE]
>
>Per i prodotti configurabili, Product Recommendations utilizza l’immagine del prodotto principale nell’unità di consigli. Se per il prodotto configurabile non è stata specificata un’immagine, l’unità di consigli sarà vuota per quel prodotto specifico.

## Passaggi successivi

Leggi i seguenti argomenti per iniziare a utilizzare Product Recommendations:

- [Come implementare Product Recommendations](implementation-workflow.md)

- [Installare e configurare Product Recommendations](install-configure.md)

- [Crea Recommendations prodotto](create.md)
