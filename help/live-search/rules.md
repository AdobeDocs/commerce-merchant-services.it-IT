---
title: "Ricerca merchandising"
description: "[!DNL Live Search] le regole di merchandising combinano la logica con le azioni per modellare l’esperienza di acquisto."
exl-id: d06a3040-6987-4813-90ae-2f7b3ad0b232
source-git-commit: 888b81683a4e139a35b771d9c573f1f5f0c3b902
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# Cerca nel merchandising

Per &quot;Search Merchandising&quot; si intende un insieme di regole che combinano logica e azioni per dare forma all’esperienza di ricerca di un acquirente nel tuo negozio. Puoi utilizzare le regole di merchandising per promuovere, seppellire, fissare o nascondere i prodotti per calibrare i risultati della ricerca in tempo reale per supportare gli obiettivi aziendali.

Ogni regola ha tre componenti principali:

* Condizioni: le condizioni che attivano un’azione.
* Eventi: le azioni che hanno luogo quando vengono soddisfatte le condizioni.
* Dettagli: il nome della regola, l’intervallo di tempo facoltativo e la descrizione.

È possibile combinare più condizioni e azioni e pianificare una regola affinché sia attiva per un periodo.

## Requisiti

Una regola di ricerca semplice può avere una singola condizione e un singolo evento, mentre una regola complessa può avere fino a dieci condizioni che attivano fino a 25 eventi.
Le regole possono avere:

* Fino a dieci condizioni
* Fino a 25 eventi

Il testo della query può contenere:

* Caratteri alfanumerici (lettere e numeri)
* Caratteri maiuscoli o minuscoli. L&#39;iniziale maiuscola viene ignorata.

## Operatori logici

Operatori logici `AND` e `OR` unisci due condizioni e restituisce risultati diversi. Tutti gli operatori logici utilizzati in una regola con più condizioni sono gli stessi. Non è possibile utilizzare entrambi `AND` e `OR` nella stessa regola.

### Operatori di corrispondenza

Operatori di corrispondenza `All` e `Any` determina l’operatore logico utilizzato per unire più condizioni nella regola e può essere utilizzato per modificare l’operatore esistente.

* `All` - Utilizza il `AND` per unire più condizioni. Una regola che utilizza `All` L’operatore di corrispondenza può avere un solo operatore `Search query is` condizione.
* `Any` - Utilizza il `OR` per unire più condizioni.

Durante la composizione di una regola complessa, può essere utile scriverla con un rientro per descrivere le condizioni, gli eventi associati e i nomi dei prodotti o gli SKU necessari per restituire i risultati desiderati. Quindi, crea la regola e verifica il risultato.

## Ordine di precedenza con più regole

A un termine di ricerca viene applicata una sola regola di ricerca alla volta.
Se a una frase di ricerca sono applicabili più regole, vengono applicate tutte queste regole. In caso di conflitto tra due regole:`rule 1` che migliora sku1 ma `rule 2` nasconde lo stesso SKU, quindi la regola applicata più di recente (`rule 2`) ha la precedenza.

* Le regole vengono ordinate in base alla marca temporale &quot;Ultima modifica&quot;. La regola modificata più di recente viene applicata per prima, e le regole precedenti vengono applicate in seguito, in ordine di marca temporale.
* Il `query is` condizione ha la precedenza rispetto ad altre condizioni. Se una regola più recente contiene `query contains` condizione, ma una regola precedente ha `query is` condizione, la `query is` regola applicata.

### Richieste Storefront

Se una regola attiva contiene `query is` corrisponde alla frase di ricerca, viene applicata. Se sono presenti più regole di corrispondenza con un `query is` condizione, viene applicata la regola attiva aggiornata più di recente.
In caso contrario, viene applicata la regola attiva aggiornata più di recente.

### Anteprima richieste

La richiesta effettuata nell’amministratore funziona in modo leggermente diverso. Quando visualizzi l’anteprima in Amministrazione, vengono applicate tutte le regole, incluse quelle scadute e pianificate.

* Se la regola visualizzata in anteprima presenta `query is` condizione, viene applicata.
* Se la regola visualizzata in anteprima non ha un `query is` e una successiva regola attiva corrispondente con un `query is` condizione trovata, il `query is` regola applicata.
* Se la regola visualizzata in anteprima non ha un `query is` e nessun&#39;altra regola con un `query is` viene trovata, viene applicata la regola visualizzata in anteprima.

## Assegnazioni di prodotti di categoria e merchandising categorie

[!DNL Live Search] consente di filtrare per Categorie. Consulta [Merchandising categorie](category-merch.md) per ulteriori informazioni.
Tuttavia, in Adobe Commerce puoi creare una categoria virtuale con [Assegnazioni prodotti categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/products-in-category/categories-product-assignments.html). Questo tipo di categoria viene creato in fase di esecuzione e non esiste nel database delle categorie. Pertanto, [!DNL Live Search] impossibile leggere o utilizzare questo tipo di categoria.
