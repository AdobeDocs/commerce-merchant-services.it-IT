---
title: Widget pagina elenco prodotti
description: Abilitazione e formattazione di [!DNL Live Search Product Listing Page Widget]
exl-id: f7346a06-a8c7-4a33-8437-ea4f61d9281f
source-git-commit: faf217486d57588d8535c1d605e963c91ec3ee68
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Widget pagina elenco prodotti

Il [!DNL Live Search Product Listing Page Widget] (PLP) utilizza la piattaforma Commerce Services per fornire una pagina di elenco dei prodotti performante, ricercabile e facet-able. In questo argomento viene descritto come abilitare e assegnare uno stile al widget PLP.

## Abilitazione del widget PLP

Quando [!DNL Live Search] è installato, la funzionalità di ricerca predefinita viene convertita in [!DNL Live Search] automaticamente.

Il [!DNL Live Search] Il widget PLP è abilitato per impostazione predefinita per le nuove installazioni. Se si esegue l&#39;aggiornamento [!DNL Live Search] e il widget PLP è già stato disattivato, rimarrà così.

>[!IMPORTANT]
>
>Quando [!DNL Live Search Product Listing Page Widget] è attivato, non è possibile modificare la direzione dell’ordinamento in una pagina di elenco dei prodotti.

## Funzioni widget

Il widget PLP fornisce le seguenti funzioni predefinite:

- Pulsanti Aggiungi al carrello - Disponibile solo per prodotti semplici.
- Più immagini per prodotto: l’immagine può cambiare quando si sceglie un colore diverso per un prodotto configurabile.
- Supporto per i campioni colore: l’attributo colore deve essere scritto `color` affinché il codice possa essere convalidato correttamente.

### Personalizzazione del widget

Oltre alle funzioni predefinite del widget PLP, potete personalizzare ulteriormente il widget per includere le seguenti funzioni:

- Filtraggio per attributi
- Supporto di più lingue
- Cursori prezzo

Per informazioni su come personalizzare il widget PLP per gestire le funzioni di cui sopra, vedere `storefront-product-listing-page` leggimi nei seguenti [repository](https://github.com/adobe/storefront-product-listing-page/).

>[!WARNING]
>
>Se personalizzi il widget PLP utilizzando il codice disponibile nell’archivio, sei responsabile della manutenzione e di tutti gli aggiornamenti necessari. Eventuali nuove funzioni del widget PLP di cui agli Adobi rilasci potrebbero essere incompatibili con l’implementazione personalizzata.

## Esempio di stile

È possibile personalizzare l&#39;aspetto del widget PLP in modo che corrisponda al sito utilizzando [CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/).

>[!NOTE]
>
>Gli elementi con classi personalizzate all’interno di un tema Adobe Commerce non vengono ereditati. Questi elementi devono essere oggetto di targeting da parte della classe specifica per corrispondere alle classi personalizzate; le classi di azione primarie non funzioneranno su un pulsante widget. Vengono ereditati gli elementi mirati generici all’interno del CSS; `button` si applica ai pulsanti widget.

I div evidenziati contengono la classe target `ds-sdk-product-item__product-name`.

![Paginazione](assets/plp-css-example.png)

Personalizza il nome del prodotto aggiungendo una regola per renderli maiuscoli.

```css
.ds-sdk-product-item__product-name {
 text-transform: uppercase;
}
```

![Paginazione](assets/plp-css-example-after.png)

## Classi CSS

### Elenco prodotti

- `.ds-sdk-product-list`: div esterno
- `.ds-sdk-product-list__grid`: div interno

![Paginazione](assets/plp-css-product-list.png)

#### Paginazione elenco prodotti

- `.ds-plp-pagination`

![Paginazione](assets/plp-css-pagination.png)

- `.ds-plp-pagination_item`

![Elemento di paginazione](assets/plp-css-pagination-item.png)

- `.ds-plp-pagination_item--current`

![Impaginazione elemento corrente](assets/plp-css-pagination-item-current.png)

### Widget

- `.ds-widgets`: div esterno
- `.ds-widgets__actions`: div interno lato sinistro
- `.ds-widgets__results`: div interno lato destro

![Risultati widget](assets/plp-css-widgets.png)

### Menu a discesa Ordina

- `.ds-sdk-sort-dropdown`

![Menu a discesa Ordina](assets/plp-css-dropdown.png)

- `.ds-sdk-sort-dropdown__button`

![Pulsante a discesa](assets/plp-css-dropdown-button.png)

- `.ds-sdk-sort-dropdown__items`

![Elementi a discesa](assets/plp-css-dropdown-items.png)

- `.ds-sdk-sort-dropdown__items--item`

![Elemento a discesa](assets/plp-css-dropdown-item.png)

- `.ds-sdk-sort-dropdown__items--item-selected`

![Elemento selezionato a discesa](assets/plp-css-dropdown-selected.png)

- `.ds-sdk-sort-dropdown__items--item-active`

![Selezione attiva a discesa](assets/plp-css-dropdown-active.png)

### Facet

- `.ds-plp-facets`
- `.ds-plp-facets__header`
- `.ds-plp-facets__header_title`
- `.ds-plp-facets__header__clear-all`

![Titolo intestazione facet](assets/plp-css-facets-title-clear.png){width="350"}

- `.ds-plp-facets__pills`
- `.ds-sdk-pill`

![Pillole sfaccettate](assets/plp-css-facets-pill.png){width="350"}

- `.ds-sdk-pill__label`
- `.ds-sdk-pill__cta`

![Etichetta facet](assets/plp-css-pill-label-cta.png){width="350"}

- `.ds-plp-facets__list`

![Elenco facet](assets/plp-css-facets-list.png){width="350"}

- `.ds-sdk-input`
- `.ds-sdk-input__label`
- `.ds-sdk-product-item__product-swatch-group`
- `ds-sdk-product-item__product-swatch-item`
- `.ds-sdk-input_fieldset_show-more`

![Input](assets/plp-css-sdk-input.png)

- `.ds-sdk-labelled-input`

![Input con etichetta](assets/plp-css-labelled-input.png)

- `.ds-sdk-labelled-input__input`
- `.ds-sdk-labelled-input__label`

![Etichetta di input](assets/plp-css-labelled-input-label.png)

### Elemento prodotto

- `.ds-sdk-product-item`
- `.ds-sdk-product-item__image`
- `.ds-sdk-product-item__product-name`
- `.ds-sdk-product-item__product-options`
- `.ds-sdk-product-price`
   - `.ds-sdk-product-price--no-discount`
   - `.ds-sdk-product-price--grouped`
   - `.ds-sdk-product-price--bundle`
   - `.ds-sdk-product-price--discount`

![Prodotto](assets/plp-css-product.png)

### Caricamento

- `.ds-sdk-loading`
- `.ds-sdk-loading__spinner`
- `.ds-sdk-loading__spinner-label`

![Indicatore di caricamento](assets/plp-css-loading.png)

## Disattivazione del widget PLP

Per disattivare il widget PLP:

1. Vai a **Negozi** > Impostazioni > **Configurazione** > **[!DNL Live Search]** > **Funzioni vetrina** e imposta **Abilita widget elenco prodotti** a &quot;No&quot;.
1. Seleziona **Salva configurazione** per salvare l&#39;impostazione.
