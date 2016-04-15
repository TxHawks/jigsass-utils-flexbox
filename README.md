# JigSass Utils Flexbox
[![NPM version][npm-image]][npm-url]  [![Dependency Status][daviddm-image]][daviddm-url]   

  > A collection of dynamically generated flexbox-related utility classes.

Class names follow the [Emmet](http://docs.emmet.io/cheat-sheet/) abbreviation
syntax, with colons (':') replaced by two dashes (`--`) to follow BEM naming
conventions.
E.g., the `justify-content: space-around` utility class name is `.u-jc--sa`.


## Installation

Using npm:

```sh
npm i -S jigsass-utils-flexbox
```


## Available classes

Class names follow the [Emmet](http://docs.emmet.io/cheat-sheet/) abbreviation
syntax, with colons (':') replaced by two dashes (`--`) to follow BEM naming
conventions.
E.g., the `justify-content: space-around` utility class name is `.u-jc--sa`.

  - `.u-ac--c` (align-content: center)
  - `.u-ac--fe` (align-content: flex-end)
  - `.u-ac--fs` (align-content: flex-start)
  - `.u-ac--s` (align-content: stretch)
  - `.u-ac--sa` (align-content: space-around)
  - `.u-ac--sb` (align-content: space-between)


  - `.u-ai--b` (align-items: baseline)
  - `.u-ai--c` (align-items: center)
  - `.u-ai--fe` (align-items: flex-end)
  - `.u-ai--fs` (align-items: flex-start)
  - `.u-ai--s` (align-items: stretch)


  - `.u-as--a` (align-self: auto)
  - `.u-as--b` (align-self: baseline)
  - `.u-as--c` (align-self: center)
  - `.u-as--fe` (align-self: flex-end)
  - `.u-as--fs` (align-self: flex-start)
  - `.u-as--s` (align-self: stretch)


  - `.u-jc--c` (justify-content: center)
  - `.u-jc--fe` (justify-content: flex-end)
  - `.u-jc--fs` (justify-content: flex-start)
  - `.u-jc--sa` (justify-content: space-around)
  - `.u-jc--sb` (justify-content: space-between)


  - `.u-fb--a` (flex-basis: auto)
  - `.u-fb--<width>` (flex-basis: &lt;width>)


  - `.u-fxg--<number>` (flex-grow: &lt;number>)
  - `.u-fxsh--<number>` (flex-shrink: &lt;number>)


  - `.u-fxw--n` (flex-wrap: nowrap)
  - `.u-fxw--w` (flex-wrap: wrap)
  - `.u-fxw--wr` (flex-wrap: wrap-reverse)


  - `.u-fxd--c` (flex-direction: column)
  - `.u-fxd--cr` (flex-direction: column-reverse)
  - `.u-fxd--r` (flex-direction: row)
  - `.u-fxd--rr` (flex-direction: row-reverse)


  - `.u-ord--<number>` (order: &lt;number>)
  - `.u-ord--min-<number>` (order: -&lt;number>)


## Usage

Import JigSass Utils Flexbox into your main scss file near its very end, together with all
other utilities (utilities should always be the last to be imported).

```scss
@import 'path/to/jigsass-utils-flexbox/scss/index';
```

Like all other JigSass Utils, JigSass Flexbox does not automatically generate any CSS
when imported. You would need to explicitly indicate that each individual flexbox
class should actually be generated in each component or object it is used in
(clarification: This will include style declarations inside `.foo` and .`bar`):

```scss
// _c.foo.scss
.foo {
  @include jigsass-util(u-ord, $modifier: 1); // <-- order: 1

  ...
}
```

```scss
// _c.bar.scss
.bar {
  @include jigsass-util(u-jc, $modifier: fe);  // <-- justify-content: flex-end
  @include jigsass-util(u-ord, $modifier: min-1, $from: large); // <-- ordr: -1 from large bp and on.

  ...
}
```

Doing so helps us a great deal with portability, as no matter where we import component or object
partials, the correct utility classes will be generated. Think of it as a poor man's dependency
management.

Developer communication is also assisted by including "dependencies" wherever they are required,
as anyone going through a partial, can easily understand how it should be marked up with just a
glance.

As far as bloat goes, just don't worry about it - the actual styles will only be generated once,
at the location in the cascade where the Jigsass Flexbox partial was imported into the main file.


JigSass Flexbox classes are responsive-enabled, using [JigSass MQ](https://txhawks.github.io/jigsass-tools-mq/)
and the breakpoints defined in the [$jigsass-breakpoints](https://txhawks.github.io/jigsass-tools-mq/#variable-jigsass-breakpoints) variable.

Based on the breakpoint arguments passed to `jigsass-util` when including a flexbox class, responsive
modifiers are generated according to the following logic:

```scss
.u-<util>--<modifier>[-[-from-<breakpoint-name>][-until-<breakpoint-name>][-misc-<breakpoint-name>]]
```

So, assuming the `medium`, `large` and `landscape` breakpoints are defined in `$jigsass-breakpoints`
as `600px`, `1024px` and `(orientation: landscape)` respectively,

```scss
@include jigsass-util(u-ord, $modifier: 2);
```
will generate the `.u-ord--2` class, which is not limited to any media-query.

```scss
@include jigsass-util(u-ord, $modifier: 2, $until: medium);
```

will generate the `.u-ord--2--until-medium` class, which will be in effect at
`(max-width: 37.49em)` and will override styles in the default class until that point.

```scss
@include jigsass-util(u-ord, $modifier: min2, $from: large, $misc: landscape);
```

will generate the `.u-ord-min2--from-large-when-landscape` class, which will go into
effect at `(min-width: 64em) and (orientation: landscape)` and will override styles in the default
class under these  conditions.


## Documentation

The full documentation was generated using mdcss, and is available at 
[https://txhawks.github.io/jigsass-utils-flexbox/](https://txhawks.github.io/jigsass-utils-flexbox/)

## Contributing

It is a best practice for JigSass modules to *not* automatically generate css on `@import`, but 
rather have the user explicitly enable the generation of specific styles from the module.

Contributions in the form of pull-requests, issues, bug reports, etc. are welcome.
Please feel free to fork, hack or modify JigSass Flexbox in any way you see fit.

#### Writing documentation

Good documentation is crucial for usability, scalability and maintainability. When 
contributing, please do make sure that both its Sass functionality (functions, mixins, 
variables and placeholder selectors), as well as the CSS it generates (selectors, 
concepts, usage exmples, etc.) are well documented.

Jigsass Flexbox uses Jonathan Neal's [mdcss](//github.com/jonathantneal/mdcss).

When styles and documentation comments are not automatically generated by your module on `@import`,
please use the `sgSrc/sg.scss` file to enable their generation.

In addition, any file in `sgSrc/assets` will be available for use in the style guide.



## File structure
```bash
┬ ./
│
├─┬ scss/ 
│ └─ index.scss # The module's importable file.
│
├─┬ sgSrc/      # Style guide sources
│ │
│ ├── sg.scc    # It is a best practice for JigSass 
│ │             # modules to not automatically generate 
│ │             # css and documentation on `@import.` 
│ │             # Please use this file to enable css
│ │             # and documentation comments) generation.
│ │
│ └── assets/   # Files in `sgSrc/assets` will be 
│               # available for use in the style guide
│
└─┬ docs/      # Documention
  │
  └── styleguide/ # Generated documentation 
                  # of the module's CSS
```





**License:** MIT



[npm-image]: https://badge.fury.io/js/jigsass-utils-flexbox.svg
[npm-url]: https://npmjs.org/package/jigsass-utils-flexbox

[daviddm-image]: https://david-dm.org/TxHawks/jigsass-utils-flexbox.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/TxHawks/jigsass-utils-flexbox
