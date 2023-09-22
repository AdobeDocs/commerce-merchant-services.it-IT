---
title: "[!DNL Live Search] Settings"
description: "Configurare le impostazioni per [!DNL Live Search] servizio."
exl-id: a0b63116-4b8f-490c-a54e-e21f1b02b634
source-git-commit: d367fdb0cb0ddf67ee1ce31b178fcb29ec5283ad
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Impostazioni

Utilizza il *Impostazioni* per configurare gli intervalli e gli intervalli del facet di prezzo e la lingua predefinita per l&#39;indice.

Fatturazione prezzo specifica il numero di gruppi di intervalli di prezzi e il modo in cui i valori di prezzo vengono distribuiti tra di essi.

Le impostazioni della lingua indicano a [!DNL Live Search] indica la lingua prevista durante la scrittura dell&#39;indice.

![Impostazioni](assets/settings.png)

## Fatturazione del prezzo

È possibile specificare il numero di gruppi di intervalli di prezzi e il modo in cui i valori di prezzo vengono distribuiti tra di essi. Ogni fascia di prezzo si sovrappone al gruppo precedente di uno. Ad esempio, cinque gruppi con un intervallo di 20 creano le seguenti fasce di prezzo: 0-20, 20-40, 40-60, 60-80 e >80. Se il catalogo non contiene un numero di prodotti sufficiente per riempire tutti gli intervalli definiti, la visualizzazione dei gruppi disponibili viene regolata di conseguenza. Ad esempio: 0-20, 60-80, >80.

1. In Admin (Amministrazione), vai a **Marketing** > *SEO e ricerca* > **[!DNL Live Search]**.
1. Il giorno **Impostazioni** scheda in *Fatturazione del prezzo*, eseguire le operazioni seguenti:
   * Inserisci il **Numero di selezioni** o gruppi di prezzi. È possibile definire fino a 50 raggruppamenti di prezzi.
   * Inserisci il **Valore intervallo**, o fascia di prezzo per ciascun gruppo. Il valore massimo è 10.000.
1. Clic **Salva**.

   La disponibilità delle impostazioni aggiornate nella vetrina richiede circa 15 minuti.

### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Numero di selezioni | Specifica il numero di raggruppamenti di intervalli di prezzi che possono essere utilizzati come filtri di ricerca nella vetrina. Valore predefinito: 8, valore massimo: 50 |
| Valore intervallo | Specifica l&#39;intervallo di prezzo per ogni gruppo. Ad esempio, cinque selezioni con un valore di intervallo pari a 20 creano cinque raggruppamenti di 0-20, 20-40, 40-60, 60-80 e >80. Valore predefinito: 5, valore massimo: 10.000 |

## Lingua

L’impostazione della lingua comunica [!DNL Live Search] quale lingua aspettarsi durante la lettura del catalogo e la scrittura dell’indice.

Le lingue hanno diversi insiemi di regole per la grammatica: come vengono separate le parole, tempi dei verbi e sinonimi, ad esempio.
L’impostazione Lingua assicura che al meccanismo di indicizzazione venga applicato l’insieme corretto di regole.

Le impostazioni della lingua devono essere impostate sulla lingua principale del catalogo.
