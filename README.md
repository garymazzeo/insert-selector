# insert-selector

SCSS mixin for adding a selector into a nested list.

It automatically adds class, ID, attribute, and pseudo selectors to the end of the target. It adds elements to the front.

## Requirements

Dart Sass >=1.23.0 for `@use` [module syntax](https://css-tricks.com/introducing-sass-modules/)

## Install

`npm install insert-selector`

`yarn add insert-selector`

## Usage

Import the mixin at the top of your `.scss` file.

If using [module syntax](https://sass-lang.com/documentation/at-rules/use) (it's the future)(and also the default):

```scss
@use "insert-selector" as *;

// You will probably need to use a path to you node_modules
@use "../../../../node_modules/insert-selector/insert-selector" as *;
```
*You can also use a [load path](https://sass-lang.com/documentation/at-rules/use/#load-paths) to make it cleaner. ([Load path in CLI docs](https://sass-lang.com/documentation/cli/dart-sass/#load-path))*

If using `@import` syntax:

```scss
@import "insert-selector-import";
```

```scss
/// @param {string} $target
///   the target element in the tree
/// @param {string} $insert
///   the element or modifier you want to insert
/// @param {boolean} $child, default false
///   if true, the $insert is a separate child element in the selector tree
/// @return {string}
///   full new element tree

@include insert-selector("#target", ".insert");
@include insert-selector("#target", ".insert", true);
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

        @include insert-selector(".row-fluid", ".outOfStock", true) {
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
.product-info .row-fluid .outOfStock .price-info .buy-info {
  grid-column: 2;
}
```

## Why would I want this?

You're probably on a legacy system that has difficult to navigate element trees for selectors. Ideally, the markup doesn't look like this, but sometimes it's out of your hands. Hopefully this helps!

This also acts like a parent selector, giving you access to change the parent from the nested child selector.
