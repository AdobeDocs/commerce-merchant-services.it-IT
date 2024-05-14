---
title: 'Limiti e limiti'
description: Scopri i limiti e le limitazioni di [!DNL Live Search] per soddisfare le esigenze dell'azienda.
role: Admin, Developer
exl-id: ad6737f9-6ecd-4d82-89e7-d95425e4ba53
source-git-commit: 589475cfc695cefb727176ee772c8d0d07e8e0a2
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Limiti e limiti

Adobe Commerce offre diverse opzioni per la ricerca del sito. Rivedi i limiti e le limitazioni seguenti per assicurarti che [!DNL Live Search] e [!DNL Catalog Service] soddisfa le esigenze della tua azienda. Se hai bisogno di funzionalità di ricerca avanzate, ad esempio ricerca di contenuti, algoritmo BYOA (port-your-own-algorithm) o merchandising basato su attributi, considera una soluzione di ricerca di terze parti.

## Generale

- Il [Ricerca avanzata](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) il modulo è disattivato quando [!DNL Live Search] e il collegamento Ricerca avanzata nel piè di pagina della vetrina viene rimosso.
- [Determinazione prezzi livello](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier) e [Prezzi speciali](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) non sono supportati nella [!DNL Live Search] campo e widget pagina elenco prodotti.
- I prezzi dei prodotti non includono l&#39;imposta sul valore aggiunto (IVA).
- La ricerca dei contenuti non è supportata.
- Esiste un limite di 10.000 prodotti che possono essere impaginati.

## Indicizzazione

- [!DNL Live Search] [indici](indexing.md) fino a un totale di 450 attributi di prodotto per visualizzazione store. Questi sono distribuiti come segue:
   - 50 attributi ordinabili
   - 200 attributi filtrabili
   - 200 attributi ricercabili
- [!DNL Live Search] indicizza solo i prodotti dal database di Adobe Commerce.
- Le pagine CMS non sono indicizzate.

## Facet

- È possibile configurare un massimo di 100 attributi come facet dai 200 attributi filtrabili che possono essere indicizzati.
- All’interno di un facet, è possibile restituire un massimo di 30 bucket. Se devono essere restituiti più di 30 bucket, [creare un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) Adobe può quindi analizzare l’impatto sulle prestazioni e determinare se è possibile aumentare questo limite per il tuo ambiente.
- I facet dinamici possono causare problemi di prestazioni in indici e indici di grandi dimensioni con elevata ordinalità. Se hai creato facet dinamici e noti un deterioramento delle prestazioni o una pagina non caricata con errori di timeout, prova a modificare i facet in modo che siano bloccati per determinare se questo risolve il problema di prestazioni.
- Stato scorte (`quantity_and_stock_status`) non è supportato come facet. È possibile utilizzare `inStock: 'true'` per filtrare i prodotti di magazzino. Questa funzione è supportata come funzionalità integrata nella `LiveSearchAdapter` quando &quot;Display out of stock products&quot; è impostato su &quot;True&quot; nel [!DNL Commerce] Amministratore

## Query

- [!DNL Live Search] non ha accesso alla tassonomia completa dell’albero delle categorie, il che rende alcuni scenari di ricerca di navigazione a più livelli al di fuori della sua portata.
- [!DNL Live Search] utilizza un valore univoco [Endpoint GraphQL](https://developer.adobe.com/commerce/services/graphql/live-search/) per le query che supportano funzionalità quali il faceting dinamico e la ricerca in base alla digitazione. Anche se simile al [API GRAPHQL](https://developer.adobe.com/commerce/webapi/graphql/), esistono alcune differenze e alcuni campi potrebbero non essere completamente compatibili.
- Il numero massimo di risultati che è possibile restituire in una query di ricerca è 10.000.

## Regole

- Numero massimo di ricerche di merchandising [regole](rules.md) la visualizzazione per negozio è 50.
- Il merchandising per categoria può avere una regola per categoria.
- Il numero massimo di condizioni per regola è 10.
- Il numero massimo di eventi per regola è 25.

## Sinonimi

- [!DNL Live Search] può gestire fino a 200 [sinonimi](synonyms.md) per la visualizzazione store.
- I sinonimi con più parole non sono supportati.

## Merchandising categorie

- È possibile creare una regola per categoria per ogni visualizzazione store. Ogni regola può avere:
   - Fino a dieci condizioni
   - Fino a 25 eventi

## Autorizzazioni B2B e categoria

- I prodotti non vengono visualizzati se non vengono aggiunti a un catalogo condiviso predefinito.
- Per limitare i gruppi di clienti utilizzando le autorizzazioni del catalogo:
   - I prodotti devono essere assegnati alla categoria principale.
   - Al gruppo di clienti &quot;Non connesso&quot; devono essere assegnate autorizzazioni di navigazione &quot;Consenti&quot;.
   - Per limitare i prodotti al gruppo di clienti &quot;Non connesso&quot;, vai a ogni categoria e imposta le autorizzazioni per ogni gruppo di clienti.
- Al momento il supporto per B2B con Live Search for PWA Studi non è supportato.
