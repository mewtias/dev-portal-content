---
title: "FRN Minicart free shipping bar"
slug: "fabiolamolina-frn-minicart-bar"
excerpt: "fabiolamolina.frn-minicart-bar@4.1.0"
hidden: true
createdAt: "2022-08-08T18:04:28.079Z"
updatedAt: "2022-08-08T18:04:28.079Z"
---
## Config app

To config app navigate to `ACCOUNT SETTINGS` -> `apps` -> `My Apps` -> `Minicart Bar`

## custom app

Class | local
-- | --
`freigthScaleContainer` | css class
`emptyOrderForm` | css class
`sliderText` | css class
`valueLessTheMinimumToFreeFhipping` | css class
`currencyContainer` | css class
`freeShippingTitle` | css class
`haveFreeFhipping` | css class
`sliderContainer` | css class
`sliderContainerFull` | css class
`barContainer` | css class
`barIconContainer` | css class
`barIcon` | css class

## Custom icon

1. To change icon use the [VTEX guide](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-customizing-your-stores-icons) to custom store icons

2. Add a new icon in `iconpack.svg` com `id="minicart-free-shipping"` in store-theme

*note* To icon correct size icon, export the icon with size `16x16px`

Exemplo:

```svg
<svg className="dn" height="0" version="1.1" width="0" xmlns="http://www.w3.org/2000/svg">
  <defs>
    ...
    <g id="minicart-free-shipping">
      <path
        d="M15.6486 10.9286C15.6486 11.1034 15.504 11.2425 15.3286 11.2425H14.6806C14.5052 11.2425 14.3618 11.1003 14.3618 10.9255C14.3618 10.7508 14.5052 10.6086 14.6806 10.6086H15.0129L15.0357 6.2677L12.9545 4.55447H10.3809V10.6142H11.0228C11.1988 10.6142 11.3428 10.7569 11.3428 10.9317C11.3428 11.1059 11.1988 11.2486 11.0228 11.2486H7.12615C6.95077 11.2486 6.80739 11.1059 6.80739 10.9317C6.80739 10.7569 6.95077 10.6142 7.12615 10.6142H9.74339V3.09539H2.25046V5.0997C2.25046 5.27386 2.10708 5.41662 1.93046 5.41662C1.75508 5.41662 1.61169 5.27386 1.61169 5.0997V2.77847C1.61169 2.6037 1.75508 2.46155 1.93046 2.46155H10.0591C10.2357 2.46155 10.3785 2.6037 10.3785 2.77847V3.92062H13.0658C13.1428 3.92062 13.2129 3.94586 13.2708 3.99324L15.5557 5.87386C15.6295 5.93416 15.6702 6.02586 15.6745 6.12124L15.6486 10.9286ZM5.48923 5.6677C5.664 5.6677 5.808 5.81047 5.808 5.98463C5.808 6.15939 5.664 6.30155 5.48923 6.30155H1.61785C1.44246 6.30155 1.29846 6.15939 1.29846 5.98463C1.29846 5.81047 1.44246 5.6677 1.61785 5.6677H5.48923ZM5.16123 7.44986C5.15754 7.62462 5.01354 7.76432 4.83815 7.76432L0.968 7.74216C0.791385 7.74216 0.648 7.59878 0.650462 7.42155C0.650462 7.24678 0.795077 7.1077 0.969846 7.1077H0.973539L4.84492 7.12986C5.01969 7.12986 5.16369 7.27201 5.16123 7.44986V7.44986ZM4.51077 8.88616C4.51077 9.06401 4.36615 9.20309 4.19015 9.20309H0.319385C0.144 9.20309 0 9.06093 0 8.88616C0 8.71201 0.144 8.56924 0.319385 8.56924H4.19015C4.36615 8.56924 4.51077 8.71201 4.51077 8.88616ZM1.93046 9.45416C2.10708 9.45416 2.25046 9.59693 2.25046 9.77109V10.6142H2.89169C3.06646 10.6142 3.21108 10.7569 3.21108 10.9317C3.21108 11.1059 3.06646 11.2486 2.89169 11.2486H1.93046C1.75508 11.2486 1.61169 11.1059 1.61169 10.9317V9.77109C1.61169 9.59693 1.75508 9.45416 1.93046 9.45416V9.45416ZM5.01969 10.2246C5.80492 10.2246 6.44369 10.8652 6.44369 11.6511C6.44369 12.4382 5.80492 13.0788 5.01969 13.0788C4.63631 13.0788 4.27692 12.9292 3.99877 12.6603C3.72185 12.3877 3.57169 12.0326 3.57169 11.6511C3.57169 11.2714 3.72492 10.9163 3.99877 10.6437C4.27323 10.3735 4.63631 10.2246 5.01969 10.2246V10.2246ZM5.01969 12.4449C5.45292 12.4449 5.80492 12.0892 5.80492 11.6511C5.80492 11.2142 5.45292 10.8591 5.01969 10.8591C4.57969 10.8591 4.20923 11.2203 4.20923 11.6511C4.20923 12.0831 4.57969 12.4449 5.01969 12.4449ZM13.9311 8.62339H11.3317C11.1582 8.62339 11.0135 8.48124 11.0135 8.30647V5.70586C11.0135 5.53109 11.1582 5.3877 11.3317 5.3877H12.9698C13.0498 5.3877 13.1268 5.41663 13.184 5.47078L14.1458 6.32986C14.2123 6.39078 14.2505 6.4757 14.2505 6.56493V8.30647C14.2505 8.48124 14.1065 8.62339 13.9311 8.62339V8.62339ZM13.6117 6.70463L12.8455 6.0197H11.6523V7.98893H13.6117V6.70463V6.70463ZM12.8135 10.2246C13.5994 10.2246 14.2375 10.8652 14.2375 11.6511C14.2375 12.4382 13.5994 13.0788 12.8135 13.0788C12.4314 13.0788 12.0702 12.9292 11.792 12.6603C11.5151 12.3877 11.3655 12.0326 11.3655 11.6511C11.3655 11.2714 11.5188 10.9163 11.792 10.6437C12.0671 10.3735 12.4314 10.2246 12.8135 10.2246V10.2246ZM12.8135 12.4449C13.2474 12.4449 13.5994 12.0892 13.5994 11.6511C13.5994 11.2142 13.2474 10.8591 12.8135 10.8591C12.3735 10.8591 12.0031 11.2203 12.0031 11.6511C12.0031 12.0831 12.3735 12.4449 12.8135 12.4449Z"
        fill="currentCollor" />
    </g>
    ...
  </defs>
</svg>
```

## Internacionalization

To translate and localizate messages use this ids to react-intl

```json
{
  "store/minicartbar.freeShippingTitleDefault": "Free Shipping",
  "store/minicartbar.emptyOrderForm": "We have free shipping from: ",
  "store/minicartbar.valueLessTheMinimumToFreeFhipping": "Only left {valueToFreeShiping} to ",
  "store/minicartbar.haveFreeFhipping": "You won free shipping"
}
```

*note:* in `store/minicartbar.valueLessTheMinimumToFreeFhipping` use `{valueToFreeShiping}` to replace per value at to get free shipping
![Free shipping Bar](./images/freeShippingBar.png)