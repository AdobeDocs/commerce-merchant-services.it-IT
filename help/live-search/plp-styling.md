---
title: Widget pagina elenco prodotti
description: "Abilitazione e formattazione di [!DNL Live Search Product Listing Page Widget]"
source-git-commit: c4bca0c7238be653dd13b051634c662e5891767d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Widget pagina elenco prodotti

Il [!DNL Live Search Product Listing Page Widget] (PLP) utilizza la piattaforma Commerce Services per fornire una pagina di elenco dei prodotti performante, ricercabile e facet-able. In questo argomento viene descritto come abilitare e assegnare uno stile al widget PLP.

## Abilitazione del widget PLP

Quando [!DNL Live Search] è installato, la funzionalità di ricerca predefinita viene convertita in [!DNL Live Search] automaticamente.
Il widget PLP deve essere abilitato in Admin.

1. Vai a **Negozi** > Impostazioni > **Configurazione** > **[!DNL Live Search]** > **Funzioni vetrina** e imposta **Abilita widget elenco prodotti** a &quot;Sì&quot;.
1. Seleziona **Salva configurazione** per salvare l&#39;impostazione.

## Esempio di stile

È possibile personalizzare l&#39;aspetto del widget PLP in modo che corrisponda al sito utilizzando [CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/).

>[!NOTE]
>
>Gli elementi con classi personalizzate all’interno di un tema Adobe Commerce non vengono ereditati. Questi elementi devono essere oggetto di targeting da parte della classe specifica per corrispondere alle classi personalizzate; le classi di azione primarie non funzioneranno su un pulsante widget.
>Verranno ereditati gli elementi mirati generici all’interno del CSS; `button` verrà applicato ai pulsanti widget.

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

* `.ds-sdk-product-list`: div esterno
* `.ds-sdk-product-list__grid`: div interno

![Paginazione](assets/plp-css-product-list.png)

#### Paginazione elenco prodotti

* `.ds-plp-pagination`

![Paginazione](assets/plp-css-pagination.png)

* `.ds-plp-pagination_item`

![Elemento di paginazione](assets/plp-css-pagination-item.png)

* `.ds-plp-pagination_item--current`

![Impaginazione elemento corrente](assets/plp-css-pagination-item-current.png)

### Widget

* `.ds-widgets`: div esterno
* `.ds-widgets__actions`: div interno lato sinistro
* `.ds-widgets__results`: div interno lato destro

![Risultati widget](assets/plp-css-widgets.png)

### Menu a discesa Ordina

* `.ds-sdk-sort-dropdown`

![Menu a discesa Ordina](assets/plp-css-dropdown.png)

* `.ds-sdk-sort-dropdown__button`

![Pulsante a discesa](assets/plp-css-dropdown-button.png)

* `.ds-sdk-sort-dropdown__items`

![Elementi a discesa](assets/plp-css-dropdown-items.png)

* `.ds-sdk-sort-dropdown__items--item`

![Elemento a discesa](assets/plp-css-dropdown-item.png)

* `.ds-sdk-sort-dropdown__items--item-selected`

![Elemento selezionato a discesa](assets/plp-css-dropdown-selected.png)

* `.ds-sdk-sort-dropdown__items--item-active`

![Selezione attiva a discesa](assets/plp-css-dropdown-active.png)

### Facet

* `.ds-plp-facets`
* `.ds-plp-facets__header`
* `.ds-plp-facets__header_title`
* `.ds-plp-facets__header__clear-all`

![Titolo intestazione facet](assets/plp-css-facets-title-clear.png){width="350"}

* `.ds-plp-facets__pills`
* `.ds-sdk-pill`

![Pillole sfaccettate](assets/plp-css-facets-pill.png){width="350"}

* `.ds-sdk-pill__label`
* `.ds-sdk-pill__cta`

![Etichetta facet](assets/plp-css-pill-label-cta.png){width="350"}

* `.ds-plp-facets__list`

![Elenco facet](assets/plp-css-facets-list.png){width="350"}

* `.ds-sdk-input`
* `.ds-sdk-input__label`
* `.ds-sdk-input__options`
* `.ds-sdk-input_fieldset_show-more`

![Input](assets/plp-css-sdk-input.png)

* `.ds-sdk-labelled-input`

![Input con etichetta](assets/plp-css-labelled-input.png)

* `.ds-sdk-labelled-input__input`
* `.ds-sdk-labelled-input__label`

![Etichetta di input](assets/plp-css-labelled-input-label.png)

### Elemento prodotto

* `.ds-sdk-product-item`
* `.ds-sdk-product-item__image`
* `.ds-sdk-product-item__product-name`
* `.ds-sdk-product-item__product-options`
* `.ds-sdk-product-price`
   * `.ds-sdk-product-price--no-discount`
   * `.ds-sdk-product-price--grouped`
   * `.ds-sdk-product-price--bundle`
   * `.ds-sdk-product-price--discount`

![Prodotto](assets/plp-css-product.png)

### Caricamento

* `.ds-sdk-loading`
* `.ds-sdk-loading__spinner`
* `.ds-sdk-loading__spinner-label`

![Indicatore di caricamento](assets/plp-css-loading.png)
