# insert-selector

SCSS mixin for adding a selector into a nested list.

It automatically adds class, ID, attribute, and pseudo selectors to the end of the target. It adds elements to the front.

## Requirements
Dart Sass 1.23.0 for `@use` module syntax

## Usage

`npm install insert-selector`

`yarn add insert-selector`

```scss
@use "insert-selector:insert-selector";
```

## Examples
```scss
.product-info {

  .row-fluid {

    .price-info {
      display: grid;
      grid-gap: 0.5rem 1.5rem;

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
  grid-gap: 0.5rem 1.5rem;
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
