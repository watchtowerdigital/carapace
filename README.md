# <img src="carapace-logo.png" width="342" height="96" alt="Carapace">

[![npm](https://img.shields.io/npm/v/scarab-carapace/beta.svg)](https://www.npmjs.com/package/scarab-carapace) [![Build Status](https://travis-ci.org/watchtowerdigital/scarab-carapace.svg?branch=v4)](https://travis-ci.org/watchtowerdigital/scarab-carapace) 

**Highly configurable framework for generating single-purpose, functional CSS classes**

*Carapace* is a Sass framework which generates [functional/atomic CSS](https://css-tricks.com/lets-define-exactly-atomic-css/) classes based on user-defined configuration. It depends on the [`scarab-scss`](https://github.com/watchtowerdigital/scarab) Sass utility library for low-level functions and mixins.

Although Carapace provides some defaults, it is not an opinionated CSS library. Think of it instead as a tool for rapidly creating custom CSS libraries on a per-project basis.

## Table of contents
  - [Features](#features)
  - [Installation](#installation)
  - [Configuration](#configuration)
    - [Variable management](#variable-management)
    - [Naming convention](#naming-convention)
  - [Usage](#usage)
    - [Modules](#modules)
    - [Compiling CSS](#compiling-css)
  - [Documentation](#documentation)
  - [Related](#related)

## Features
- Functional CSS *(a.k.a. Atomic CSS)*
- Configuration-driven stylesheets
- Bring-your-own naming convention
- Responsive and mobile-first
- Optional CSS reset/normalize
- Easily achieve vertical rythmn
- Automatic styleguides for your project *(with [`scarab-styleguide`](https://github.com/watchtowerdigital/scarab-styleguide))*

## Installation
1. Install `scarab-carapace` as a dev-dependency in your project via npm:
```
npm install scarab-carapace --save-dev
```

2. Add your `node_modules` folder to your Sass [`includePaths`](https://github.com/sass/node-sass#includepaths).

3. Import the necessary files in your main stylesheet:
```scss
// IMPORTANT
// 
// Follow the import order below to ensure modules are generated properly.

@import 'scarab-scss/scarab';        // Imports scarab-scss, core utils & config
@import 'custom/config.scss';        // Your custom Scarab config
@import 'scarab-carapace/config';    // Imports default Carapace module config
@import 'custom/module-config.scss'; // Your custom Carapace module config
@import 'scarab-carapace/modules';   // Generates CSS classes
```

## Configuration

### Variable management
*Carapace* imports the `scarab-scss` utility library, exposing the `get()` function and `set()` mixin. These utilities allow you to configure the *Carapace* theme and modules. Refer to the [Configuration section](https://github.com/watchtowerdigital/scarab#configuration) of the `README` in `scarab-scss` for more information on `get()` and `set()`.

### Naming convention
With the default naming convention, class names that *Carapace* generates will look something like this:
```html
<section class="bgc:black c:white  m(bgc:white) m(c:black)  hv(c:grey) m(hv(c:dark-grey))">
	<p>This section has a 'black' background with 'white' text.
	When hovered, the text color changes to 'grey'.</p>
	<p>On 'medium'-sized screens, it has a 'white' background with 'black' text.
	When hovered, the text color changes to 'dark-grey'.</p>
</section>
```

The naming convention can be customized by changing the `namescheme` options in Scarab.

## Usage

### Modules
Modules are single-purpose, functional CSS classes. Module class names and values are dynamically generated by *Carapace*, depending on the values set in the global `$__SCARAB` variable.

Module class names consist of a `root`, and optionally: `variant`, `modifier`, `breakpoint` and `state`.

In Carapace, configuration for a module typically looks like this:
```scss
@include set(modules, 'opacity', (
  'root'        : 'o',                        // String which defines the module's "root"
  'group'       : 'base',                     // Group which the module belongs to
  'values'      : get(opacity),               // Map  of "modifier" names to CSS property values
  'states'      : option(namescheme, states), // Map of "state" shorthands to values
  'breakpoints' : get(breakpoint)             // Map of "breakpoint" names to values
));
```

Refer to the [`modules/`](lib/modules/) folder for more information on how to configure modules.

### Compiling CSS
*Carapace* does not include a build step to compile Sass to CSS. The following tasks are recommended for production:

- Prefix compiled CSS for cross-browser compatibility ([`autoprefixer`](https://github.com/postcss/autoprefixer))
- Minify compiled CSS ([`cssnano`](https://github.com/ben-eb/cssnano))
- Separate base CSS from styles in media queries ([`sakugawa`](https://github.com/paazmaya/sakugawa))
- Inline base CSS, and `<link>` media query styles

## Documentation
Documentation is a work-in-progress.

## Related
* [**scarab-scss**](https://github.com/watchtowerdigital/scarab.git) — Sass utility framework for rapid stylesheet development
* [**scarab-styleguide**](https://github.com/watchtowerdigital/scarab-styleguide.git) — Generate automatic styleguides from scarab-carapace configuration
* [**scarab-cli**](https://github.com/watchtowerdigital/scarab-cli.git) — Command-Line Interface for the Scarab Sass ecosystem
* [**scarab-snippets**](https://github.com/watchtowerdigital/scarab-snippets.git) — Sublime Text snippets for the Scarab Sass utility framework
