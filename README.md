# insert-selector

SCSS mixin for adding a selector into a nested list.

It automatically adds class, ID, attribute, and pseudo selectors to the end of the target. It adds elements to the front.

## Requirements
Dart Sass >=1.23.0 for `@use` [module syntax](https://css-tricks.com/introducing-sass-modules/)

## Install

`npm install insert-selector`

`yarn add insert-selector`

If using [module syntax](https://sass-lang.com/documentation/at-rules/use) (it's the future):
```scss
@use "~insert-selector/insert-selector:insert-selector";
```

If using `@import` syntax:
```scss
@import "~insert-selector/insert-selector";
```

## Usage
```scss
/// @param {string} $target
///   the target element in the tree
/// @param {string} $insert
///   the element or modifier you want to insert
/// @return {string} 
///   full new element tree

@include insert-selector("#target", ".insert")
```

## Examples
```scss
.product-info {

  .row-fluid {

    .price-info {
      display: grid;

      .buy-info {
        grid-column: 1;

        @include insert-selector(".row-fluid", ".active") {
          grid-column: 3;
        }

        @include insert-selector(".row-fluid", ".outOfStock") {
          grid-column: 2;
        }
      }
    }
  }
}
```
compiles to
```scss
.product-info .row-fluid .price-info {
  display: grid;
}
.product-info .row-fluid .price-info .buy-info {
  grid-column: 1;
}
.product-info .row-fluid.active .price-info .buy-info {
  grid-column: 3;
}
.product-info .row-fluid.outOfStock .price-info .buy-info {
  grid-column: 2;
}
```


## Why would I want this?
Todo
