---
title: "Area di lavoro faceting"
description: "Scopri come utilizzare il [!DNL Live Search] area di lavoro di faceting."
exl-id: b47b5c19-59bb-41e4-9599-3b90cbc44b70
source-git-commit: 4978bdb5549f5df911863a23fdfbfc9ab9ad05df
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Area di lavoro di faceting

Il *Faceting* workspace elenca tutti i facet attualmente disponibili e fornisce accesso agli strumenti necessari per impostare e gestire i facet. I facet bloccati vengono visualizzati per primi nell&#39;elenco dei facet esistenti, seguiti dai facet dinamici. L’elenco può essere filtrato per mostrare tutti i facet oppure solo quelli bloccati o dinamici.

![Area di lavoro di sfaccettatura](assets/faceting-workspace.png)

## Impostare l&#39;ambito

Se l’installazione di Adobe Commerce include più visualizzazioni dello store, imposta **Ambito** al [visualizzazione store](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) dove si applicano le impostazioni facet.

## Filtrare l’elenco

1. Fai clic su **Filtra per** controllo.
1. Scegliere una delle opzioni seguenti:

   * Tutti i filtri
   * Bloccato
   * Dinamico

## Aggiungi un facet

1. Clic **Aggiungi facet**.
1. Consulta [Aggiungi facet](facets-add.md) per istruzioni dettagliate.

## Descrizioni delle colonne

| Colonna | Descrizione |
|--- |--- |
| (prima colonna) | Elenca i facet bloccati e dinamici dalla [etichetta](facets-type.md) visibile all’acquirente. |
| Tipo di ordinamento | Il [ordinamento](facets-type.md) dei valori facet. I facet sono ordinati alfabeticamente per tutti [!DNL Commerce] vetrine. Per [headless] implementazioni, i facet possono essere ordinati alfabeticamente o per conteggio. Opzioni: Alfabetico, Conteggio (solo headless) |
| Valore massimo | Il numero di valori di facet disponibili nella vetrina come filtri, con un massimo di 10. |

## Controlli

| Controllo | Descrizione |
|--- |--- |
| Aggiungi facet | Apre il [editor facet](facets-add.md). |
| Filtra per | Determina la [tipo di facet](facets-type.md) visualizzati nell&#39;elenco. Opzioni: Tutto, Bloccato, Dinamico |
