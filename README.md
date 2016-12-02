![Cactus Logo](http://joedinsdale.co.uk/misc/cactus-logo.png)

# Cactus CSS Framework

Cactus is a very minimal but flexible CSS grid framework powered by Scss. Rather than defining a list of potential column widths, Cactus lets you define your own and automatically generates the classes for you.

## Installation
To include in your project run the following:
`npm install cactus-framework --save`

Then integrate in to your build pipeline.

## Testing
Cactus has a suite of automated tests, to run:
`npm run test`

For linting run:
`npm run lint`

## Building
To build a static CSS version of Cactus run:
`npm run build`


## Cactus Structure
Cactus is structured acording to ITCSS, this allows separation of concerns and gives greater context for what each class is used for. For more information checkout this [blog post on ITCSS](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture). The framework is split up into the following categories:

* **Settings** - Settings contains all of the configuration settings for Cactus. These should never be overwritten directly.

* **Tools** - Tools contains functions and mixins required for Cactus.

* **Generic** - Generic is used for any generic global styling, this should be avoided where possible.

* **Elements** - Elements contains styling for HTML elements such as `<img>`.

* **Objects** - Objects contains class-based styling for non-cosmetic design patterns such as containers and layout.

* **Debug** - Debug is an optional set of styling which enables some debug styling to highlight incorrect grid usage.


## Cactus Classes
Cactus makes use of BEM like naming convention for classes making for far more readable markup, if you're not familiar it stands for Block Element Modifier. It follows this basic structure:

``` scss
.prefix-block {}
.prefix-block__element {}
.prefix-block--modifier {}
.prefix-block__element--modifier {}
```

For more information have a look at [MindBEMding - Getting your head round BEM syntax](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) by Harry Roberts, it's a great read!

### Cactus wrapper
The Wrapper element sets the a max-width constraint. The wrapper widths are define in`$cactus-wrapper-config` which expects a map:

``` scss
$cactus-wrapper-config: (
  sizes: (
    default: 48em,
    large: 56em,
    small: 40em
  )
);
```

This will create the following classes:

``` scss
.o-cactus__w
.o-cactus__w--large
.o-cactus__w--small
```

### Cactus Group
The Group element wraps Units and adds essential margins and offsets to create the layouts. All immediately nested elements should be cactus unit classes.

``` scss
.o-cactus__g                // Default gutter width.
.o-cactus__g--gutter-small  // Optional modifier for gutter width.
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
There have been some major changes to how the settings for Cactus work. It will take me a while to re-write the documentation to account for this and add better tools for extending however for now here's a quick summary

### Cactus Wrapper Config
The Cactus wrapper is an optional element which sets a maximum width constraint, by default this is centrally aligned in the page. You can define


### Cactus Unit Config
Here we can define each of the breakpoints we want to generate unit classes for and specify what those units should be:

``` scss
$cactus-unit-config: (
  default: (
    name: false,
    breakpoint: false,
    units: (1 1, 1 2, 1 4, 3 4)
  ),
  medium: (
    name: m,
    breakpoint: 75em,
    units: (1 1, 1 2, 1 3, 2 3)
  )
);
```

Here we have two breakpoints, `default` and `medium`. Each comprises of:

- **`name`** - The name which will be used for the class, for example giving a name of 'm' will result in a generated class of `.o-cactus__u--m-X`. Setting to `false` means this is the global breakpoint with no media query attached.
- **`breakpoint`** - This is the width at which the breakpoint should apply and should be set in em's. A breakpoint of `50em` would mean these classes only effect when the screen width is below `800px` etc.
- **`units`** - Units expects an array of space separated fractions, so `1 2` is the same as `1/2` or `50%`. This lets us tailor the exact unit widths we want to include.


### Using the generated class names
The classes and breakpoints we have defined will be exported in the following format:

``` scss
.o-cactus__u--1-4     // Quarter width
.o-cactus__u--3-4     // Three quarter width

.o-cactus__u--m-1-3   // Quarter width at medium breakpoint
.o-cactus__u--m-2-3   // Three quarter width at medium breakpoint

.o-cactus__u--s-1     // Full width at small breakpoint
```

## Customising
To customise the default grid settings include your own overrides file and include before Cactus. You can include your own `$cactus-unit-config` or `$cactus-gutter-config` etc as your project requires. To see what options are available check `settings/_grid.scss`.

## License

See the [LICENSE file](https://github.com/MrDinsdale/Cactus/blob/master/LICENSE.md) for license text and copywrite information.
