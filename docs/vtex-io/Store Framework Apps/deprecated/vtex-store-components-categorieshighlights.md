---
title: "Categories Highlights"
slug: "vtex-store-components-categorieshighlights"
excerpt: "vtex.store-components@3.132.2"
hidden: false
createdAt: "2020-06-03T16:04:30.355Z"
updatedAt: "2021-11-03T14:49:38.636Z"
---
![https://img.shields.io/badge/-Deprecated-red](https://cdn.jsdelivr.net/gh/vtexdocs/dev-portal-content@main/images/vtex-store-components-categorieshighlights-0.png)

>⚠️ Warning
>
> The Categories Highlights has been deprecated. Despite this, support for it is still granted.

Categories Highlights is a banner which shows two or four categories in a highlighted position in the store. This Component can be imported and used by any VTEX App.

> 📢 Disclaimer 
> 
> Don't fork this project, use, contribute, or open issue with your feature request.

## Usage

You should follow the usage instruction in the main [README](https://github.com/vtex-apps/store-components/blob/master/README.md#usage).

To import it into your code: 
```js
import CategoriesHighlights from 'vtex.store-components/CategoriesHighlights'
```

You can use it in your code like a React component with the jsx tag: `<CategoriesHighlights />`. 
```jsx
<CategoriesHighlights
    categoriesHighlighted={ 
        categoryX: { name: 'X', image: 'Image X' }, 
        categoryY: { name: 'Y', image: 'Image Y' } 
    }
/>
```

## Configuration

| Prop name                           | Type       | Description                                                                               | Default value
| ----------------------------------- | ---------- | ----------------------------------------------------------------------------------------- |---------------- |
| `categoriesHighlighted`             |`Object!`| Categories highlighted in the department                                                     | {}
| `showCategoriesHighlighted`         | `Boolean!` | Flag which indicates if the categories highlighted should be displayed or not             | false
| `quantityOfItems`                   | `Number!`  | Number of categories highlighted to be displayed (it should be 2 or 4)                    | 2
| `boxShape`                          | `String!`  | Shape of the card box which wraps each category (it should be 'squared' or 'rectangular') | `squared`                              

Category Highlight:

| Prop name                           | Type       | Description                                                                               |
| ----------------------------------- | ---------- | ----------------------------------------------------------------------------------------- |
| `name`                              | `String!`  | Name of the category                                                                      |
| `image`                             | `String`   | Image of the category                                                                     |

## Styles API

This app provides some CSS classes as an API for style customization. You should follow the Styles API instruction in the main [README](https://github.com/vtex-apps/store-components/blob/master/README.md#styles-api).

### CSS namespaces
Below, we describe the namespaces that are defined in the categories highlights.

Class name        | Description                    | Component Source        
----------------- | ------------------------------ | ------------------------
`squaredCategoriesHighlights`| The properties to be applied to a squared container | [index](index.js)|
`rectangularCategoriesHighlights`| The properties to be applied to a rectangular container | [index](index.js)|
`rectangularCard`| The properties to be applied to a rectangular card container | [CategoryCard](./components/CategoryCard.js)|
`squaredCard`| The properties to be applied to a squared card container | [CategoryCard](./components/CategoryCard.js)|
`squaredCardImage`| The properties to be applied to the image inside a squared card | [CategoryCard](./components/CategoryCard.js)|
`rectangularCardImage`| The properties to be applied to the image inside a rectangular card | [CategoryCard](./components/CategoryCard.js)|