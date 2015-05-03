![Cactus Logo](http://joedinsdale.co.uk/misc/cactus-logo.png)

# Cactus
_**So DRY it chafes.**_

Cactus is a very minimal but flexible CSS grid framework powered by Scss. Rather than defining a list of potential column widths, Cactus lets you define your own and automatically generates the classes for you.


## Cactus Classes
Cactus makes use of BEM like naming convention for classes making for far more readible markup:

### Cactus wrapper
The Wrapper element sets the max width `$cactus-wrapper-width` of the content and centers it on the page, by default this is 60em (960px).

``` scss
.cactus__wrapper
```

An optional wide modifier can be set `$cactus-wrapper-width-wide`, by default this is set to false.

``` scss
.cactus__wrapper--wide
```

### Cactus Group
The Group element wraps Units, it also allows us to adjust the gutter on direct descendant `cactus__unit` elements.

``` scss
.cactus__group // Default gutter width set by $cactus-gutter, 32px default.
.cactus__group--gutter-small // Sets gutter to value of $cactus-gutter-small, 8px default.
.cactus__group--gutter-none // Removes gutter.
```

### Cactus Unit
The Unit defines the ratios of your columns as well as breakpoints where it will become effective.

``` scss
.cactus__unit--1-2 // 1/2 width unit with no specified breakpoint
.cactus__unit--l-13-19 // 13/19 width unit at the large breakpoint (for some insane layouts)
.cactus__unit--m-1-8 // 1/8 width at the medium breakpoint
```

### Markup example

``` html
<div class="cactus__wrapper">
  <div class="cactus__group">
    <div class="cactus__unit--3-4 cactus__unit--m-1-2">
      <p>This content will be 3/4 width on large screens and 1/2 on medium screens.</p>
    </div>
    <div class="cactus__unit--1-4 cactus__unit--m-1-2">
      <p>This content will be 3/4 width on large screens and 1/2 on medium screens.</p>
    </div>
  </div>
</div>
```

## Cactus Grid Generator
The Cactus Grid is defined by `$cactus-grid-generator`. It consists of an array of data for each breakpoint:

'$breakpoint-name $breakpoint-width $array-of-unit-ratios'

The array of ratios for each breakpoint width is defined with comma separated numerator and denominator pairs such as `1 2, 1 3, 2 3, 1 4...`. Heres an example of all this working together:

``` scss
// Base grid generator
$cactus-unit-ratios-base: 1 4, 3 4;

$break-m: 767px;
$cactus-unit-ratios-m: 1 3, 2 3;

$break-s: 420px;
$cactus-unit-ratios-s: 1 1;

// Build loop for Grid Generator
$cactus-grid-generator: false false $cactus-unit-ratios-base, m $break-m $cactus-unit-ratios-m, s $break-s $cactus-unit-ratios-s;
```

Passing `false` to the name and width properties will remove any breakpoint so any relevant Unit classes will not be wrapped in media queries.

The resulting Unit class will be named `cactus__unit--` followed by the breakpoint name (if set) and the ratios supplied. The example above would provide the following:

``` scss
.cactus__unit--1-4
.cactus__unit--3-4

.cactus__unit--m-1-3
.cactus__unit--m-2-3

.cactus__unit--s-1-1
```

The breakpoint name can be set to anything you want, I tend to stick to `m` for medium and `l` for large etc however you could pass the breakpoint name `ipad2` and get the class:

``` scss
.cactus__unit--ipad2-1-4
```

With this control you can set as many breakpoints as you want while only adding minimal weight to your CSS by only outputting the classes you want.


This is very much a work in progress and highly likely to change drastically over the next few months. I also have a lot of refactoring for naming conventions of variables etc. If you have any suggestions or improvements feel free to let me know :D
