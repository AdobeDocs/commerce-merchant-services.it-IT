---
title: Raccogli dati
description: Scopri come gli eventi raccolgono i dati per i consigli di prodotto.
exl-id: b827d88c-327f-4986-8239-8f1921d8383c
feature: Services, Recommendations, Eventing
source-git-commit: 87db52e0c851b56c9a8ceba1bf25c222c6d63cda
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 0%

---

# Raccogli dati

Quando installi e configuri funzionalità di Adobe Commerce basate su SaaS come [Product Recommendations](install-configure.md) o [Live Search](../live-search/install.md), i moduli distribuiscono la raccolta di dati comportamentali nella vetrina. Questo meccanismo raccoglie dati comportamentali anonimi dai tuoi acquirenti e alimenta i consigli sui prodotti e i risultati di [Live Search](../live-search/overview.md). Ad esempio, l&#39;evento `view` viene utilizzato per calcolare il tipo di consiglio `Viewed this, viewed that` e l&#39;evento `place-order` per calcolare il tipo di consiglio `Bought this, bought that`.

>[!NOTE]
>
>La raccolta dei dati ai fini delle raccomandazioni sui prodotti non include informazioni personali identificabili (PII, personally identifiable information). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi. Ulteriori informazioni [su](https://www.adobe.com/privacy/experience-cloud.html).

## Tipi di dati ed eventi

Esistono due tipi di dati utilizzati in Product Recommendations:

- **Comportamento**: dati del coinvolgimento di un acquirente sul tuo sito, ad esempio visualizzazioni di prodotti, elementi aggiunti a un carrello e acquisti.
- **Catalogo** - Metadati del prodotto come nome, prezzo, disponibilità e così via.

Quando installi il modulo `magento/product-recommendations`, Adobe Sensei aggrega i dati comportamentali e di catalogo, creando Product Recommendations per ogni tipo di consiglio. Il servizio Recommendations del prodotto distribuisce quindi tali consigli nella vetrina sotto forma di un widget contenente il prodotto consigliato _elementi_.

Alcuni tipi di consigli utilizzano i dati comportamentali dei tuoi acquirenti per addestrare modelli di apprendimento automatico per creare consigli personalizzati. Altri tipi di consigli utilizzano solo i dati di catalogo e non utilizzano dati comportamentali. Se desideri iniziare rapidamente a utilizzare Product Recommendations sul tuo sito, puoi utilizzare i seguenti tipi di consigli solo catalogo:

- `More like this`
- `Visual similarity`

### Avvio a freddo

Quando puoi iniziare a utilizzare i tipi di consigli che utilizzano dati comportamentali? Dipende. Questo problema è denominato _Avvio a freddo_.

Il problema di _Avvio a freddo_ si riferisce al tempo necessario per l&#39;addestramento e l&#39;efficacia di un modello. Per i consigli di prodotto, significa attendere che Adobe Sensei raccolga dati sufficienti per addestrare i suoi modelli di apprendimento automatico prima di distribuire unità di consigli sul sito. Maggiore è il numero di dati di cui dispongono i modelli, più accurati e utili sono i consigli. Poiché la raccolta dati viene eseguita su un sito attivo, è consigliabile avviare questo processo in anticipo installando e configurando il modulo `magento/production-recommendations`.

La tabella seguente fornisce alcune indicazioni generali sul tempo necessario per raccogliere dati sufficienti per ogni tipo di consiglio:

| Tipo di consiglio | Tempo di formazione | Note |
|---|---|---|
| Basato sulla popolarità (`Most viewed`, `Most purchased`, `Most added to cart`) | Varia | Dipende dal volume degli eventi: le visualizzazioni sono più comuni e quindi apprende più rapidamente; quindi aggiunge al carrello, quindi acquista |
| `Viewed this, viewed that` | Richiede più formazione | Il volume delle visualizzazioni dei prodotti è decisamente elevato |
| `Viewed this, bought that`, `Bought this, bought that` | Richiede il massimo della formazione | Gli eventi di acquisto sono gli eventi più rari su un sito di e-commerce, in particolare rispetto alle visualizzazioni di prodotto |
| `Trending` | Richiede tre giorni di dati per stabilire una baseline di popolarità | Il trend è una misura dello slancio recente nella popolarità di un prodotto rispetto alla sua linea di base di popolarità. Il punteggio di tendenza di un prodotto viene calcolato utilizzando un set in primo piano (popolarità recente superiore a 24 ore) e un set in background (linea di base di popolarità superiore a 72 ore). Se la popolarità di un elemento aumenta in modo significativo entro un periodo di 24 ore rispetto alla popolarità al basale, allora riceve un punteggio di tendenza elevato. Ogni prodotto ha questo punteggio e gli elementi con il punteggio più alto in qualsiasi momento comprendono il set di prodotti con tendenze migliori. |

Altre variabili che possono influire sul tempo necessario per la formazione:

- Un volume di traffico più elevato contribuisce a un apprendimento più rapido
- Alcuni tipi di consigli si addestrano più rapidamente di altri
- Adobe Commerce ricalcola i dati comportamentali ogni quattro ore. Recommendations diventa più preciso quanto più a lungo vengono utilizzati sul tuo sito.

Per aiutarti a visualizzare l&#39;avanzamento della formazione di ciascun tipo di consiglio, la pagina [crea consiglio](create.md#readiness-indicators) visualizza gli indicatori di preparazione.

Durante la raccolta dei dati sul sito live e l’apprendimento dei modelli di apprendimento automatico, puoi completare altre attività di test e configurazione necessarie per impostare i consigli. Al termine di questo lavoro, i modelli avranno a disposizione dati sufficienti per creare consigli utili e distribuirli nella vetrina.

Se il sito non riceve abbastanza traffico (visualizzazioni, acquisti, tendenze) per la maggior parte delle SKU di prodotto, potrebbero non esserci dati sufficienti per completare il processo di apprendimento. In questo modo l’indicatore di preparazione nell’amministratore potrebbe sembrare bloccato. Gli indicatori di preparazione hanno lo scopo di fornire agli esercenti un altro punto di dati nella scelta del tipo di consigli migliore per il negozio. I numeri sono una guida e potrebbero non raggiungere mai il 100%. [Ulteriori informazioni](create.md#readiness-indicators) sugli indicatori di preparazione.

### Raccomandazioni per il backup {#backuprecs}

Se i dati di input sono insufficienti per fornire tutti gli elementi dei consigli richiesti in un&#39;unità, Adobe Commerce fornisce consigli di backup per popolare le unità dei consigli. Ad esempio, se distribuisci il tipo di consiglio `Recommended for you` nella tua home page, un acquirente sul tuo sito non ha generato abbastanza dati comportamentali per consigliare accuratamente prodotti personalizzati. In questo caso, Adobe Commerce fa emergere a questo acquirente gli elementi in base al tipo di consiglio `Most viewed`.

In caso di raccolta dati di input insufficiente, i seguenti tipi di consigli eseguono il fallback al tipo di consiglio `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

### Eventi

L&#39;[Agente di raccolta eventi Adobe Commerce Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start) elenca tutti gli eventi distribuiti nella vetrina. Da tale elenco, tuttavia, è disponibile un sottoinsieme di eventi specifici per Product Recommendations. Questi eventi raccolgono dati quando gli acquirenti interagiscono con le unità di consigli sulla vetrina e alimentano le metriche utilizzate per aiutarti ad analizzare le prestazioni dei consigli.

| Evento | Descrizione |
| --- | --- | --- |
| `impression-render` | Inviato quando viene eseguito il rendering dell’unità di consigli sulla pagina. Se una pagina ha due unità di consigli (acquistate, visualizzate), vengono inviati due eventi `impression-render`. Questo evento viene utilizzato per tenere traccia della metrica delle impression. |
| `rec-add-to-cart-click` | L&#39;acquirente fa clic sul pulsante **Aggiungi al carrello** per un elemento nell&#39;unità di consigli. |
| `rec-click` | L’acquirente fa clic su un prodotto nell’unità di consigli. |
| `view` | Inviata quando l’unità di consigli diventa visualizzabile per almeno il 50%, ad esempio scorrendo la pagina verso il basso. Ad esempio, se un&#39;unità di consigli ha due righe, viene inviato un evento `view` quando una riga più un pixel della seconda diventa visibile all&#39;acquirente. Se l&#39;acquirente scorre la pagina verso l&#39;alto o verso il basso più volte, l&#39;evento `view` viene inviato tante volte quante volte vede l&#39;intera unità di consigli sulla pagina. |

>[!NOTE]
>
>Le metriche di consigli del prodotto sono ottimizzate per le vetrine di Luma. Se la vetrina è implementata con PWA Studio, consulta la [documentazione di PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se utilizzi una tecnologia front-end personalizzata come React o Vue JS, scopri come integrare [Product Recommendations in un ambiente headless](headless.md).

#### Eventi dashboard richiesti

Per popolare il [[!DNL Product Recommendations] dashboard](workspace.md) sono necessari i seguenti eventi

| Colonna del dashboard | Eventi | Unisci campo |
| ---------------- | --------- | ----------- |
| Impression | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| Visualizzazioni | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| Clic | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| Ricavi | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| Retribuzioni LT | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| Tasso di click-through | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

I seguenti eventi non sono specifici di Product Recommendations, ma sono necessari per consentire ad Adobe Sensei di interpretare correttamente i dati degli acquirenti:

- `view`
- `add-to-cart`
- `place-order`

#### Tipo di consiglio

Questa tabella descrive gli eventi utilizzati da ogni tipo di consiglio.

| Tipo di consiglio | Eventi | Pagina |
| --- | --- | --- | ---|
| Articoli più visualizzati | `page-view`<br>`product-view` | Pagina dettagli prodotto |
| Più acquistati | `page-view`<br>`complete-checkout` | Carrello/Pagamento |
| Più aggiunti al carrello | `page-view`<br>`add-to-cart` | Pagina dettagli prodotto<br>Pagina elenco prodotti<br>Carrello<br>Elenco desideri |
| Ha visualizzato questo, ha visualizzato quello | `page-view`<br>`product-view` | Pagina dettagli prodotto |
| Ho visto questo, ho comprato quello | Registrazioni dei prodotti | `page-view`<br>`product-view` | Pagina dettagli prodotto<br>Carrello/Pagamento |
| Ho comprato questo e quello | Registrazioni dei prodotti | `page-view`<br>`product-view` | Pagina dettagli prodotto |
| Di tendenza | `page-view`<br>`product-view` | Pagina dettagli prodotto |
| Conversione: Visualizza per acquisto | Registrazioni dei prodotti | `page-view`<br>`product-view` | Pagina dettagli prodotto |
| Conversione: Visualizza per acquisto | Registrazioni dei prodotti | `page-view`<br>`complete-checkout` | Carrello/Pagamento |
| Conversione: Visualizza in carrello | Registrazioni dei prodotti | `page-view`<br>`product-view` | Pagina dettagli prodotto |
| Conversione: Visualizza in carrello | Registrazioni dei prodotti | `page-view`<br>`add-to-cart` | Pagina dettagli prodotto<br>Pagina elenco prodotti<br>Carrello<br>Elenco desideri |

#### Avvertenze

- Gli ad blocker e le impostazioni di privacy possono impedire l&#39;acquisizione degli eventi e causare la mancata generazione di rapporti per [metriche](workspace.md#column-descriptions) relative a coinvolgimento e ricavi. Inoltre, alcuni eventi potrebbero non essere inviati a causa di acquirenti che abbandonano la pagina o di problemi di rete.
- [Le implementazioni headless](headless.md) devono implementare eventi per alimentare il dashboard di Product Recommendations.
- Per i prodotti configurabili, Product Recommendations utilizza l’immagine del prodotto principale nell’unità di consigli. Se per il prodotto configurabile non è stata specificata un’immagine, l’unità di consigli sarà vuota per quel prodotto specifico.

>[!NOTE]
>
>Se è abilitata la modalità di restrizione dei cookie [](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html), Adobe Commerce non raccoglie i dati comportamentali fino a quando l&#39;acquirente non acconsente all&#39;utilizzo dei cookie. Se la modalità di restrizione dei cookie è disabilitata, Adobe Commerce raccoglie i dati comportamentali per impostazione predefinita.
