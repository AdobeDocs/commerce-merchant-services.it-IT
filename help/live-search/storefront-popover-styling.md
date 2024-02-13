---
title: "Stile [!DNL Popover] Elementi"
description: "Note tecniche sulla personalizzazione di [!DNL Live Search storefront popover]"
exl-id: 033049f2-976e-4299-b026-333ac4b481a3
source-git-commit: 67da9016d4bca9750fa9e440cce08ad1ae7100e2
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Stile [!DNL Popover] Elementi

Il [[!DNL storefront popover]](storefront-popover.md) visualizza sempre il prodotto `name` e `price`e la selezione dei campi non è configurabile. Tuttavia, [!DNL popover] Gli elementi possono essere formattati utilizzando le classi CSS. Ad esempio, le seguenti dichiarazioni modificano il colore di sfondo del [!DNL popover] contenitore e piè di pagina.

```css
.livesearch.popover-container {
    background-color: lavender;
}

.livesearch.view-all-footer {
    background-color: magenta;
}
```

## Visibilità contenitore

Il componente principale del `.livesearch.popover-container` è `.search-autocomplete`.  Il `.active` La classe indica la visibilità del contenitore. Il `.active` viene aggiunta in modo condizionale quando [!DNL popover] è aperto.

```css
.search-autocomplete.active   /* visible */
.search-autocomplete          /* not visible */
```

Per ulteriori informazioni sullo stile degli elementi della vetrina, consulta [Fogli di stile CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/) nel [Guida per gli sviluppatori di front-end](https://developer.adobe.com/commerce/frontend-core/guide/).

## Selettori di classi

I seguenti selettori di classe possono essere utilizzati per assegnare uno stile al contenitore e agli elementi di prodotto nel [!DNL popover].

* `.livesearch.popover-container`
* `.livesearch.view-all-footer`
* `.livesearch.products-container`
* `.livesearch.product-result`
* `.livesearch.product-name`
* `.livesearch.product-price`

### Selettori di classi contenitore

#### .livesearch.popover-container

![[!DNL Popover] contenitore](assets/livesearch-popover-container.png)

#### .livesearch.view-all-footer

![Visualizza tutto il piè di pagina](assets/livesearch-view-all-footer.png)

### Selettori di classi di prodotto

#### .livesearch.products-container

![Contenitore prodotto](assets/livesearch-product-container.png)

#### .livesearch.product-result

![Risultato prodotto](assets/livesearch-product-result.png)

#### .livesearch.product-name

![Nome del prodotto](assets/livesearch-product-name.png)

#### .livesearch.product-price

![Prezzo del prodotto](assets/livesearch-product-price.png)

#### .livesearch product-link

![Risultato prodotto](assets/livesearch-product-link.png)

## Utilizzo di un tema modificato {#working-with-modified-theme}

Il [!DNL storefront popover] può essere utilizzato con un [tema](https://developer.adobe.com/commerce/frontend-core/guide/themes/) che eredita i file richiesti da *Luma*. Il `top.search` blocco in `header-wrapper` del `Magento_Search` non deve essere modificato.

```html
<referenceContainer name="header-wrapper">
   <block class="Magento\Framework\View\Element\Template" name="top.search" as="topSearch" template="Magento_Search::form.mini.phtml">
      <arguments>
         <argument name="configProvider" xsi:type="object">Magento\Search\ViewModel\ConfigProvider</argument>
      </arguments>
   </block>
</referenceContainer>
```

## Disattivazione di [!DNL popover]

Per disattivare [!DNL popover] e ripristinare lo standard [Ricerca rapida](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search) , immetti il comando seguente:

```bash
bin/magento module:disable Magento_LiveSearchStorefrontPopover
```
