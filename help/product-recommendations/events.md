---
title: Raccogli dati
description: Scopri come gli eventi raccolgono i dati per i consigli di prodotto.
exl-id: b827d88c-327f-4986-8239-8f1921d8383c
feature: Services, Recommendations, Eventing
source-git-commit: 67296ea42bfddb10b0c86cb1ca47324f5fec7825
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Raccogli dati

Quando installi e configuri funzionalità di Adobe Commerce basate su SaaS come [Product Recommendations](install-configure.md) o [Live Search](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html), i moduli distribuiscono la raccolta di dati comportamentali nella vetrina. Questo meccanismo raccoglie dati comportamentali anonimi dai tuoi acquirenti e potenzia le raccomandazioni sui prodotti. Ad esempio, l&#39;evento `view` viene utilizzato per calcolare il tipo di consiglio `Viewed this, viewed that` e l&#39;evento `place-order` per calcolare il tipo di consiglio `Bought this, bought that`.

>[!NOTE]
>
>La raccolta dei dati ai fini delle raccomandazioni sui prodotti non include informazioni personali identificabili (PII, personally identifiable information). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi. Ulteriori informazioni [su](https://www.adobe.com/privacy/experience-cloud.html).

I seguenti eventi non sono specifici per Product Recommendations, ma sono necessari per restituire risultati:

- `view`
- `add-to-cart`
- `place-order`

L&#39;[Agente di raccolta eventi Adobe Commerce Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start) elenca tutti gli eventi distribuiti nella vetrina. Da tale elenco, tuttavia, è disponibile un sottoinsieme di eventi specifici per Product Recommendations. Questi eventi raccolgono dati quando gli acquirenti interagiscono con le unità di consigli sulla vetrina e alimentano le metriche utilizzate per aiutarti ad analizzare le prestazioni dei consigli.

| Evento | Descrizione | Utilizzato per le metriche? |
| --- | --- | --- |
| `impression-render` | L’unità di consigli viene sottoposta a rendering sulla pagina. | Sì |
| `rec-add-to-cart-click` | Il cliente fa clic sul pulsante **Aggiungi al carrello** per un elemento nell&#39;unità di consigli. | Sì, quando nel modello di consigli è presente il pulsante **Aggiungi al carrello**. |
| `rec-click` | Il cliente fa clic su un prodotto nell’unità di consigli. | Sì |
| `view` | L’unità di consigli diventa visualizzabile sulla pagina, ad esempio scorrendo all’interno della visualizzazione. | Sì |

Per popolare correttamente il dashboard sono necessari i seguenti eventi.

| Colonna del dashboard | Eventi | Unisci campo |
| ---------------- | --------- | ----------- |
| Impression | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | unitId |
| Visualizzazioni | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | unitId |
| Clic | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | unitId |
| Ricavi | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | unitId, SKU |
| Retribuzioni LT | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | unitId, SKU |
| Tasso di click-through | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | unitId, SKU |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | unitId, SKU |

Se la vetrina è implementata con PWA Studio, consulta la [documentazione di PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se utilizzi una tecnologia front-end personalizzata come React o Vue JS, consulta la guida utente per scoprire come integrare [Product Recommendations in un ambiente headless](headless.md).

## Avvertenze

I blocchi degli annunci e le impostazioni della privacy possono impedire al modulo `magento/product-recommendations` di acquisire eventi e causare la mancata generazione di rapporti per [metriche](workspace.md) relative a coinvolgimento e ricavi.

Eventing non acquisisce ogni transazione che avviene sul sito del commerciante. L&#39;evento ha lo scopo di dare al mercante un&#39;idea generale degli eventi che stanno accadendo sul sito.

Le implementazioni headless devono implementare eventi per alimentare il dashboard di Product Recommendations.

>[!NOTE]
>
>Se è abilitata la modalità di restrizione dei cookie [](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html), Adobe Commerce non raccoglie i dati comportamentali fino a quando l&#39;acquirente non acconsente all&#39;utilizzo dei cookie. Se la modalità di restrizione dei cookie è disabilitata, Adobe Commerce raccoglie i dati comportamentali per impostazione predefinita.
