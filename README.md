![Cactus Logo](http://joedinsdale.co.uk/misc/cactus-logo.png)

# Cactus CSS Framework

Cactus is a very minimal but flexible CSS grid framework powered by Scss. Rather than defining a list of potential column widths, Cactus lets you define your own and automatically generates the classes for you.


## Cactus Classes
Cactus makes use of BEM like naming convention for classes making for far more readable markup, if you're not familiar it stands for Block Element Modifier. It follows this basic structure:

``` scss
.block {}
.block__element {}
.block--modifier {}
.block__element--modifier {}
```

For more information have a look at [MindBEMding - Getting your head round BEM syntax](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) by Harry Roberts, its a great read!

### Cactus wrapper
The Wrapper element sets the max width `$cactus-wrapper-width` of the content and centers it on the page, by default this is 60em (960px).

``` scss
.cactus__w
```

An optional wide modifier can be set `$cactus-wrapper-width-wide`, by default this is set to false.

``` scss
.cactus__w--wide
```

### Cactus Group
The Group element wraps Units, it also allows us to adjust the gutter on direct descendant `cactus__u` elements.

``` scss
.cactus__g // Default gutter width set by $cactus-gutter, 32px default.
.cactus__g--gutter-small // Sets gutter to value of $cactus-gutter-small, 8px default.
.cactus__g--gutter-none // Removes gutter.
```

### Cactus Unit
The Unit defines the ratios of your columns as well as breakpoints where it will become effective.

``` scss
.cactus__u--1-2 // 1/2 width unit with no specified breakpoint
.cactus__u--l-13-19 // 13/19 width unit at the large breakpoint (for some insane layouts)
.cactus__u--m-1-8 // 1/8 width at the medium breakpoint
```

### Markup example

``` html
<div class="cactus__w">
  <div class="cactus__g">
    <div class="cactus__u--3-4 cactus__u--m-1-2">
      <p>This content will be 3/4 width on large screens and 1/2 on medium screens.</p>
    </div>
    <div class="cactus__u--1-4 cactus__u--m-1-2">
      <p>This content will be 3/4 width on large screens and 1/2 on medium screens.</p>
    </div>
  </div>
</div>
```

## Cactus Grid Generator
There have been some major changes to how the settings for Cactus work. It will take me a while to re-write the documentation to account for this and add better tools for extending however for now heres a quick summary


### Cactus Unit Config
Here we can define each of the breakpoints we want to generate unit classes for and specify what those units should be:

``` scss
$cactus-unit-config: (
  default: (
    name: false,
    breakpoint: false,
    units: $cactus-unit-ratio-default
  ),
  medium: (
    name: m,
    breakpoint: 75em,
    units: $cactus-unit-ratio-default
  )
);
```

Here we have two breakpoints, `default` and `medium`. Each comprises of:

- **`name`** - The name which will be used for the class, for example giving a name of 'm' will result in a generated class of `.cactus__u--m-X`. Setting to `false` means this is the global breakpoint with no media query attached.
- **`breakpoint`** - This is the width at which the breakpoint should apply and should be set in em's. A breakpoint of `50em` would mean these classes only effect when the screen width is below `800px` etc.
- **`units`** - This should be set to a variable containing an array of fractions, for the correct format of these see below.

### Cactus Unit Ratios
These are the unit ratios we set for the various breakpoints. They currently need to be contained with in separate variables as sass maps don't support nested arrays. The benefit of this is that it potentially DRYs up our code:

``` scss
$cactus-unit-ratio-default: 1 1, 1 2, 1 3, 2 3, 1 4, 3 4;
```

The unit ratios are essentially fractions so `1 2` is the same as `1/2` or `50%`. There is no limit to how many you can have although it is recommended that you only include the ones you need.

### Cactus Breakpoint Config

Here we set which of the breakpoints we want to include in our project. The values in here must be the same as the maps nested within `$cactus-unit-config`.

``` scss
$cactus-breakpoint-config: (
  default,
  medium,
  small
);
```

### Using the generated class names
The classes and breakpoints we have defined will be exported in the following format:

``` scss
.cactus__u--1-4     // Quarter width
.cactus__u--3-4     // Three quarter width

.cactus__u--m-1-3   // Quarter width at medium breakpoint
.cactus__u--m-2-3   // Three quarter width at medium breakpoint

.cactus__u--s-1     // Full width at small breakpoint
```


<!-- The Cactus Grid is defined by `$cactus-grid-generator`. It consists of an array of data for each breakpoint:

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

The resulting Unit class will be named `cactus__u--` followed by the breakpoint name (if set) and the ratios supplied. The example above would provide the following:

``` scss
.cactus__u--1-4
.cactus__u--3-4

.cactus__u--m-1-3
.cactus__u--m-2-3

.cactus__u--s-1
```

If the same innumerator and denominator are passed as a ratio it will automatically export the ratio as 1. So `1 1`, `2 2`, `3 3` etc would all convert to `.cactus__u--1`, for this reason you should only ever declare one full width ratio or you will end up with duplicate classes.


The breakpoint name can be set to anything you want, I tend to stick to `m` for medium and `l` for large etc however you could pass the breakpoint name `ipad2` and get the class:

``` scss
.cactus__u--ipad2-1-4
```

With this control you can set as many breakpoints as you want while only adding minimal weight to your CSS by only outputting the classes you want. -->


This is very much a work in progress and highly likely to change drastically over the next few months. I also have a lot of refactoring for naming conventions of variables etc. If you have any suggestions or improvements feel free to let me know :D
