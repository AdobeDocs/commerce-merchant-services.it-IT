---
title: Test in ambiente di staging
description: Scopri come utilizzare [!DNL Product Recommendations] dall’ambiente di produzione nell’ambiente di staging a scopo di test.
exl-id: 178ff2aa-7821-45f7-85f1-d490d8182817
source-git-commit: 3d0de3eeb4aa96c996bc9fa38cffd7597e89e7ca
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# Test in ambiente di staging

Prima di implementare i consigli nell’ambiente di produzione, è necessario eseguire il test in un ambiente non di produzione per assicurarsi che tutto funzioni come previsto.

[!DNL Product Recommendations] restituisce prodotti in base a [dati sul comportamento degli acquirenti](behavioral-data.md) raccolte dalla vetrina. In un ambiente non di produzione, tuttavia, è probabile che non siano presenti dati comportamentali provenienti dagli acquirenti. L’unico tipo di consiglio che puoi verificare senza dati comportamentali è `More like this`. Questo tipo di consiglio non richiede alcun dato di input, in quanto utilizza una corrispondenza diretta di somiglianza dei contenuti.

I seguenti tipi di consigli richiedono dati comportamentali:

- Articoli più visualizzati
- Ha visualizzato questo, ha visualizzato quello
- Ho comprato questo e quello

Come puoi testare i consigli in un ambiente non di produzione utilizzando i dati comportamentali? Ci sono un paio di opzioni.

## Recupera consigli dall’ambiente di produzione (scelta consigliata)

Adobe Commerce consente di recuperare i consigli dall’ambiente di produzione e di visualizzarli in anteprima in un ambiente non di produzione tramite [commutazione](settings.md) lo spazio dati SaaS.

Per recuperare i consigli dall’ambiente di produzione, è necessario assicurarsi che:

- La raccolta dati di Storefront è [configurato e abilitato](install-configure.md) sulla produzione.
- Il catalogo degli ambienti non di produzione è in gran parte lo stesso di quello esistente in produzione. L’utilizzo di cataloghi simili garantisce che i prodotti restituiti nelle unità di consigli rispecchino fedelmente quelli in produzione.

## Generare dati comportamentali in ambienti non di produzione

1. Distribuire `magento/product-recommendations` in un ambiente non di produzione in cui i dati del catalogo sono simili a quelli del catalogo di produzione.

1. Utilizza uno degli ID spazio dati non di produzione per [configurazione](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html) in Admin.

1. Genera i dati da solo facendo clic sulla vetrina per simulare il comportamento degli acquirenti effettivi (o crea uno script di automazione). Attraverso i test, puoi generare eventi comportamentali nell’ambiente non di produzione. Tali eventi vengono utilizzati per produrre affinità di prodotto che alimentano le raccomandazioni. Per le prove, [!DNL Commerce] consiglia di interagire con i seguenti tipi di consigli:

   - Più visualizzati: richiede un minimo di dati di input. Gli utenti devono visualizzare i prodotti.
   - Visualizzato questo, visto che - Richiede più utenti per visualizzare più prodotti.
   - Ha acquistato questo, acquistato che - Richiede più utenti per acquistare più prodotti.

### Avvertenze

- I dati comportamentali e di catalogo provenienti dallo spazio di dati SaaS non di produzione identificano un ambiente isolato in cui i consigli di prodotto risultanti si basano interamente sui dati comportamentali generati nella vetrina associata.

- Poiché non si dispone di grandi quantità di dati comportamentali, i dati di input per il calcolo delle associazioni di prodotti sono sparsi. Tuttavia, tali dati vengono comunque inviati a Sensei per calcolare i modelli di apprendimento automatico e fornire consigli in base ai dati generati in questo ambiente.
