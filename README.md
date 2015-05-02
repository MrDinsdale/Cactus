# Cactus
_**So DRY it chafes.**_

Cactus is a very minimal but flexible CSS grid framework powered by Scss. Rather than defining a list of potential column widths, Cactus lets you define your own and automatically generates the classes for you.


## Cactus Classes
Cactus makes use of BEM like naming convention for classes making for far more readible markup:

### Cactus wrapper
The Wrapper element sets the max width `$cacti-wrapper-width: 960px;` of the content and centers it on the page:

    .cacti__wrapper

An optional wide modifier can be set `$cacti-wrapper-width-wide: 1200px;`:

    .cacti__wrapper--wide

### Cactus Group
The Group element wraps out Units and is required to offset outer most gutter and set gutter modifiers to adjust their width.

    .cacti__group
    .cacti__group--gutter-small
    .cacti__group--gutter-none

### Cactus Unit
The Unit defines the ratios of your columns aswell as breakpoints where it will become effective.

    .cacti__unit--1-2
    .cacti__unit--l-13-19
    .cacti__unit--m-1-8


## Cactus Grid Generator
The Cactus Grid is defined by `$cacti-grid-generator`. It consits of an array of data for each breakpoint:

'$breakpoint-name $breakpoint-width $array-of-unit-ratios'

The array of ratios for each breakpoint width is defined with comma seperated numerator and denominator pairs such as `1 2, 1 3, 2 3, 1 4...`. Heres an example of all this working together:

    // Base grid generator
    $cacti-unit-ratios-base: 1 1, 1 2, 1 4, 3 4;

    $break-m: 767px;
    $cacti-unit-ratios-m: 1 1, 1 2, 1 3, 2 3;

    $break-s: 420px;
    $cacti-unit-ratios-s: 1 1, 1 2;

    // Build loop for Grid Generator
    $cacti-grid-generator: false false $cacti-unit-ratios-base, m $break-m $cacti-unit-ratios-m, s $break-s $cacti-unit-ratios-s;

Passing `false` to the name and width properties will remove any breakpoint so any relevant Unit classes will not be wrapped in media queries.

The resulting Unit class will be named `cacti__unit--` followed by the breakpoint name (if set) and the ratios supplied:

    .cacti__unit--3-4
    .cacti__unit--m-2-3
    .cacti__unit--s-1-2
