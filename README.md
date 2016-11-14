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
.o-cactus__w
```

An optional wide modifier can be set `$cactus-wrapper-width-wide`, by default this is set to false.

``` scss
.o-cactus__w--wide
```

### Cactus Group
The Group element wraps Units, it also allows us to adjust the gutter on direct descendant `cactus__u` elements.

``` scss
.o-cactus__g                // Default gutter width set by $cactus-gutter, 32px default.
.o-cactus__g--gutter-small  // Sets gutter to value of $cactus-gutter-small, 8px default.
.o-cactus__g--gutter-none   // Removes gutter.
.o-cactus__g--reverse       // Reverse child unit elements.
```

### Cactus Unit
The Unit defines the ratios of your columns as well as breakpoints where it will become effective.

``` scss
.o-cactus__u--1-2       // 1/2 width unit with no specified breakpoint
.o-cactus__u--l-13-19   // 13/19 width unit at the large breakpoint (for some insane layouts)
.o-cactus__u--m-1-8     // 1/8 width at the medium breakpoint
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

- **`name`** - The name which will be used for the class, for example giving a name of 'm' will result in a generated class of `.o-cactus__u--m-X`. Setting to `false` means this is the global breakpoint with no media query attached.
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
.o-cactus__u--1-4     // Quarter width
.o-cactus__u--3-4     // Three quarter width

.o-cactus__u--m-1-3   // Quarter width at medium breakpoint
.o-cactus__u--m-2-3   // Three quarter width at medium breakpoint

.o-cactus__u--s-1     // Full width at small breakpoint
```