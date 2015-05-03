![Cactus Logo](http://joedinsdale.co.uk/misc/cactus-logo.png)

# Cactus
_**So DRY it chafes.**_

Cactus is a very minimal but flexible CSS grid framework powered by Scss. Rather than defining a list of potential column widths, Cactus lets you define your own and automatically generates the classes for you.


## Cactus Classes
Cactus makes use of BEM like naming convention for classes making for far more readible markup:

### Cactus wrapper
The Wrapper element sets the max width `$cactus-wrapper-width: 960px;` of the content and centers it on the page:

    .cactus__wrapper

An optional wide modifier can be set `$cactus-wrapper-width-wide: 1200px;`:

    .cactus__wrapper--wide

### Cactus Group
The Group element wraps out Units and is required to offset outer most gutter and set gutter modifiers to adjust their width.

    .cactus__group
    .cactus__group--gutter-small
    .cactus__group--gutter-none

### Cactus Unit
The Unit defines the ratios of your columns aswell as breakpoints where it will become effective.

    .cactus__unit--1-2
    .cactus__unit--l-13-19
    .cactus__unit--m-1-8


## Cactus Grid Generator
The Cactus Grid is defined by `$cactus-grid-generator`. It consits of an array of data for each breakpoint:

'$breakpoint-name $breakpoint-width $array-of-unit-ratios'

The array of ratios for each breakpoint width is defined with comma seperated numerator and denominator pairs such as `1 2, 1 3, 2 3, 1 4...`. Heres an example of all this working together:

    // Base grid generator
    $cactus-unit-ratios-base: 1 1, 1 2, 1 4, 3 4;

    $break-m: 767px;
    $cactus-unit-ratios-m: 1 1, 1 2, 1 3, 2 3;

    $break-s: 420px;
    $cactus-unit-ratios-s: 1 1, 1 2;

    // Build loop for Grid Generator
    $cactus-grid-generator: false false $cactus-unit-ratios-base, m $break-m $cactus-unit-ratios-m, s $break-s $cactus-unit-ratios-s;

Passing `false` to the name and width properties will remove any breakpoint so any relevant Unit classes will not be wrapped in media queries.

The resulting Unit class will be named `cactus__unit--` followed by the breakpoint name (if set) and the ratios supplied:

    .cactus__unit--3-4
    .cactus__unit--m-2-3
    .cactus__unit--s-1-2

This is very much a work in progress, if you have any suggestions or improvements feel free to let me know :D
