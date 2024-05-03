---
title: "Impostazioni"
description: "Configurare le impostazioni per [!DNL Live Search] servizio."
exl-id: a0b63116-4b8f-490c-a54e-e21f1b02b634
source-git-commit: 4978bdb5549f5df911863a23fdfbfc9ab9ad05df
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Impostazioni

Utilizza il *Impostazioni* workspace per configurare gli intervalli e gli intervalli del facet di prezzo e la lingua predefinita per l&#39;indice.

Fatturazione prezzo specifica il numero di gruppi di intervalli di prezzi e il modo in cui i valori di prezzo vengono distribuiti tra di essi.

L’impostazione della lingua comunica al [!DNL Live Search] indica la lingua prevista durante la scrittura dell&#39;indice.

![Impostazioni](assets/settings.png)

## Fatturazione del prezzo

È possibile specificare il numero di gruppi di intervalli di prezzi e il modo in cui i valori di prezzo vengono distribuiti tra di essi. Ogni fascia di prezzo si sovrappone al gruppo precedente di uno. Ad esempio, cinque gruppi con un intervallo di 20 creano le seguenti fasce di prezzo: 0-20, 20-40, 40-60, 60-80 e >80. Se il catalogo non contiene un numero di prodotti sufficiente per riempire tutti gli intervalli definiti, la visualizzazione dei gruppi disponibili viene regolata di conseguenza. Ad esempio: 0-20, 60-80, >80.

1. In Admin (Amministrazione), vai a **Marketing** > *SEO e ricerca* > **[!DNL Live Search]**.
1. Il giorno **Impostazioni** workspace in *Fatturazione del prezzo*, eseguire le operazioni seguenti:
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

Le lingue hanno diversi insiemi di regole per la grammatica: come le parole vengono separate, tempi dei verbi e forme delle parole, ad esempio.
L’impostazione Lingua assicura che al meccanismo di indicizzazione venga applicato l’insieme corretto di regole.

Impostare l&#39;impostazione Lingua sulla lingua principale del catalogo. Quando si modifica la lingua dell’indice, possono essere necessari da 5 a 60 minuti per riflettere la modifica nella vetrina, a seconda delle dimensioni e della complessità del catalogo.

| Lingua | Codice |
|----|----|
| Arabo | ar |
| Armeno | hy |
| Basco | eu |
| Bengalese | bn |
| Brasiliano | pt-br |
| Bulgaro | bg |
| Catalano | ca |
| Cinese (semplificato) | zh-cn |
| Cinese (tradizionale) | zh-tw |
| Ceco | cs |
| Danese | da |
| Olandese | nl |
| Inglese | it |
| Estone | et |
| Finlandese | fi |
| Francese | fr |
| Galiziano | gl |
| Tedesco | de |
| Greco | el |
| Hindi | ciao |
| Ungherese | hu |
| Indonesiano | id |
| Irlandese | ga |
| Italiano | it |
| Giapponese | ja |
| Coreano | ko |
| Lettone | lv |
| Lituano | lt |
| Norvegese | no |
| Persiano | fa |
| Portoghese | pt |
| Rumeno | ro |
| Russo | ru |
| Sorani | ku |
| Spagnolo | es |
| Svedese | sv |
| Turco | tr |
| Thailandese | th |
