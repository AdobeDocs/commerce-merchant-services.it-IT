---
title: Headless
description: Scopri come integrare [!DNL Product Recommendations] in una vetrina headless.
exl-id: 316d0b0c-5938-4e2f-9d0d-747746cf6056
source-git-commit: 521ea4fc2cce809fc12d3958e37089f3e34e1068
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Headless

È possibile integrare [!DNL Product Recommendations] in una vetrina headless utilizzando [PWA Studi](https://developer.adobe.com/commerce/pwa-studio/) o una tecnologia front-end personalizzata, ad esempio React o Vue JS.

Gli integratori personalizzati e headless devono fare riferimento a queste istruzioni Luma e PWA come implementazione suggerita. Esistono diversi modi per implementare Product Recommendations in soluzioni headless e questa documentazione non copre tutti gli scenari. Gli integratori devono occuparsi di eventi, progettazione e test per le loro implementazioni.

[!DNL Product Recommendations] richiedi [dati comportamentali e di catalogo](https://experienceleague.adobe.com/docs/commerce-merchant-services/product-recommendations/developer/development-overview.html) per il funzionamento. Il processo di sincronizzazione dei dati del catalogo rimane invariato in un’implementazione headless, ma sono necessarie modifiche per la raccolta dei dati comportamentali.

>[!NOTE]
>
>Le istanze headless devono implementare l’evento per alimentare il dashboard di Product Recommendations.

Per integrare [!DNL Product Recommendations] in una vetrina headless, devi:

1. Invia dati comportamentali ad Adobe Sensei per analizzare e calcolare i risultati dei consigli di prodotto. Puoi anche inviare dati aggiuntivi per abilitare i consigli sui prodotti [reporting delle metriche](workspace.md).

1. Recupera i risultati dei consigli di prodotto ed esegui il rendering di tali risultati sulla pagina.

Puoi eseguire entrambe queste azioni utilizzando gli SDK disponibili, come descritto nel seguente flusso di lavoro.

1. [Installa](install-configure.md) il [!DNL Product Recommendations] modulo.

1. Installare e utilizzare [SDK per eventi Adobe Commerce Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) per attivare [eventi comportamentali](https://experienceleague.adobe.com/docs/commerce-merchant-services/product-recommendations/developer/events.html).

   Numero minimo di eventi richiesti da restituire [!DNL Product Recommendations] risultati:

   | Evento | Categoria |
   |--- | ---|
   | `view` | prodotto |
   | `add-to-cart` | prodotto |
   | `place-order` | pagamento |

   Per abilitare [reporting delle metriche](workspace.md), sono necessari i seguenti eventi aggiuntivi:

   | Evento | Categoria |
   |--- | ---|
   | `impression-render` | unità-consiglio |
   | `view` | unità-consiglio |
   | `rec-click` | unità-consiglio |
   | `rec-add-to-cart-click` | unità di consigli (se nel modello di consigli è presente il pulsante &quot;Aggiungi al carrello&quot;) |

1. Quando gli eventi vengono attivati, utilizza [Raccolta eventi Adobe Commerce Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) per gestire gli eventi e inviarli ad Adobe Sensei.

1. Una volta raccolti i dati comportamentali, puoi [creare](create.md) [!DNL Product Recommendations] in Admin.

1. Utilizza il [SDK per Recommendations](https://developer.adobe.com/commerce/services/product-recommendations/) per recuperare le unità consigli sulla vetrina. L’SDK restituisce i dati del prodotto necessari per eseguire il rendering delle unità di consigli su una pagina.
