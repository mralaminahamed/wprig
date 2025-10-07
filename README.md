<img align="right" width="90" height="90"
src="https://avatars1.githubusercontent.com/u/38340689"
title="WP Rig logo by Morten Rand-Hendriksen and Rob Ruiz">

# WP Rig: WordPress Theme Boilerplate

[![Build Status](https://github.com/wprig/wprig/workflows/Main/badge.svg)](https://github.com/wprig/wprig/actions)
[![License: GPL](https://img.shields.io/github/license/wprig/wprig)](/LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/wprig/wprig?include_prereleases)](https://github.com/wprig/wprig/releases)

## Your Performance-Focused Development Rig

A progressive theme development rig for WordPress, WP Rig is built to promote the latest best practices for progressive
web content and optimization. Creating a theme from WP Rig means adopting this approach and the core principles it is
built on:

- Accessibility
- Mobile-first
- Progressive enhancement
- [Resilient Web Design](https://resilientwebdesign.com/)
- Progressive Web App enabled

We are trying to be the starter theme for design-focused devs. If you have any ideas, questions, or suggestions for this
project or are seeking to get involved in contributing or maintaining, please check out
our [discussion board on Github](https://github.com/wprig/wprig/discussions) and
read [our contribute page](https://wprig.io/contribute/) on our website.

## Documentation

We have a new Documentation area that can be found on the [WP Rig website](https://wprig.io/documentation/).
If you would like to contribute to our documentation efforts, please submit a request on
our [contribute page](https://wprig.io/contribute/) on our website.

## Installation

WP Rig has been tested on Linux, Mac, and Windows.

### Requirements

WP Rig requires the following dependencies. Full installation instructions are provided at their respective websites.

- [PHP](http://php.net/) 8.1 or higher (PHP 8.3 recommended)
- [npm](https://www.npmjs.com/) or [bun](https://bun.com/)
- [Composer](https://getcomposer.org/) (installed globally)

### WP Rig and child themes

WP Rig is built to lay a solid theme foundation, which is excellent for a parent theme but not for a child theme. A
child theme is meant to only add on or modify the foundation. As such, WP Rig is not intended for making child themes to
extend any themes, whether they were originally built with WP Rig or not.

### How to install WP Rig:

1. Clone or download this repository to the themes folder of a WordPress site on your development environment.
	- DO NOT give the WP Rig theme directory the same name as your eventual production theme. Suggested directory names
	  are `wprig` or `wprig-themeslug`. For instance, if your theme will eventually be named “Excalibur” your
	  development directory could be named `wprig-excalibur`. The `excalibur` directory will be automatically created
	  during the production process and should not exist beforehand.
2. Configure theme settings, including the theme slug and name.
	- View `./config/config.default.json` for the default settings.
	- Place custom theme settings in `./config/config.json` to override default settings.
		- You do not have to include all settings from config.default.json. Just the settings you want to override.
	- Place local-only theme settings in `./config/config.local.json`, e.g. potentially sensitive info like the path to
	  your BrowserSync certificate.
		- Again, only include the settings you want to override.
3. In the command line, run `npm run rig-init` to install necessary node and Composer dependencies.
4. In the command line, run `npm run dev` to process source files, build the development theme, and watch files for
   subsequent changes.
	- `npm run build` can be used to process the source files and build the development theme without watching files
	  afterwards.
5. In WordPress admin, activate the WP Rig development theme.

#### Recommended Git Workflow
When working with WP Rig, it is important to understand the appropriate Git workflow depending on what you are working on.
If you are using WP Rig as a starting point for a new theme, you should use the following workflow:

[Recommended Git Workflow](https://wprig.io/documentation/recommended-git-workflow/)

It is also important to note that the main branch now ignores the package-lock.json file.
While this is ideal for how we distribute WP Rig, it can cause issues when working with a local development environment or on a team using a forked WP Rig.
If you are using a local development environment, you should add the package-lock.json file to the .gitignore file
with a ! in front to prevent ignoring the file in your new theme's repo.

#### Defining custom settings for the project

Here is an example of creating a custom theme config file for the project. In this example, we want a custom slug, name,
and author.

Place the following in your `./config/config.json` file. This config will be versioned in your repo, so all developers
use the same settings.

```
{
  "theme": {
    "slug": "newthemeslug",
    "name": "New Theme Name",
    "author": "Name of the theme author"
  }
}
```

#### Defining custom settings for your local environment

Some theme settings should only be set for your local environment. For example, if you want to set local information for
BrowserSync.

Place the following in your `./config/config.local.json` file. This config will not be tracked in your repo and will
only be executed in your local development environment.

```
{
  "browserSync": {
    "live": true,
    "proxyURL": "localwprigenv.test",
    "https": true,
    "keyPath": "/path/to/my/browsersync/key",
    "certPath": "/path/to/my/browsersync/certificate"
  }
}
```

If your local environment uses a specific port number, for example, `8888`, add it to the `proxyURL` setting as follows:

```
"proxyURL": "localwprigenv.test:8888"
```

## How to build WP Rig for production:

1. Follow the steps above to install WP Rig.
2. Run `npm run bundle` from inside the `wp-rig` development theme.
3. A new, production-ready theme will be generated in `wp-content/themes`.
4. The production theme can be activated or uploaded to a production environment.

### Wiki: Recommended code editor extensions

To take full advantage of the features in WP Rig, visit
the [Recommended code editor extensions Wiki page](https://github.com/wprig/wprig/wiki/Recommended-code-editor-extensions).

## Working with WP Rig

WP Rig can be used in any development environment. It does not require any specific platform or server setup. It also
does not have an opinion about what local or virtual server solution the developer uses.

Before the first run, visit the [BrowserSync wiki page](https://github.com/wprig/wprig/wiki/BrowserSync).

### Available Processes

#### `dev watch` process

`npm run dev` will run the default development task that processes source files. While this process is running, source
files will be watched for changes, and the BrowserSync server will run. This process is optimized for speed, so you can
iterate quickly.

#### `dev build` process

`npm run build` processes source files one-time. It does not watch for changes nor start the BrowserSync server.

#### `translate` process

The translation process generates a `.pot` file for the theme in the `./languages/` directory.

The translation process will run automatically during production builds unless the `export:generatePotFile`
configuration value in `./config/config.json` is set to `false`.

The translation process can also be run manually with `npm run translate`. However, unless `NODE_ENV` is defined
as `production`, the `.pot` file will be generated against the source files, not the production files.

#### `production bundle` process

`npm run bundle` generates a production-ready theme as a new theme directory and, optionally, a `.zip` archive. This
builds all source files, optimizes the built files for production, does a string replacement and runs translations.
Non-essential files from the `wp-rig` development theme are not copied to the production theme.

To bundle the theme without creating a zip archive, define the `export:compress` setting in `./config/config.json`
to `false`:

```javascript
export:
{
	compress: false
}
```

### Build process

WP Rig uses a fast end efficient build process to generate and optimize the code
for the theme. [Gulp 5](https://gulpjs.com/), [Lightning CSS](https://lightningcss.dev/), and [esbuid](https://esbuild.github.io/) are mainly used to provide the underlying functionality.
All development is done in the `wp-rig` development theme. Feel free to edit any `.php` files.
You should only edit the source asset files in the following
locations:

- CSS: `assets/css/src` (Processed by Lightning CSS)
- JavaScript/Typescript: `assets/js/src` (Processed by esbuild)
- images: `assets/images/src` (Processed by Gulp)

For more information about the Gulp processes, what processes are available, and how to run them individually, visit
the [Gulp Wiki page](https://github.com/wprig/wprig/wiki/Gulp).

### Browser Support

As WP Rig processes CSS and JavaScript, it will support the browsers listed in `.browserslistrc`. Note that WP Rig will
**not** add polyfills for missing browser support. WP Rig **will** add CSS prefixes and transpile JavaScript.

## Advanced Features

WP Rig gives the developer an out of the box environment with support for modern technologies, including ES2015, CSS
grid, CSS custom properties (variables), CSS nesting and more, without making any configurations. Just write code, and
WP Rig handles the heavy lifting for you.

Configuring the behavior of WP Rig is done by editing `./config/config.json`. Here the developer can set the theme name
and theme author name (for translation files) and local server settings for BrowserSync. Additionally, compression of
JavaScript and CSS files can be turned off for debugging purposes.

Place your custom theme settings in `./config/config.json` to override default settings, located
in `./config/config.default.json`. Place local-only/untracked theme settings in `./config/config.local.json`. For
example, if you want to set local information for BrowserSync.

WP Rig ships with advanced features, including:

- Easily add custom Customizer settings using .json file
- Progressive loading of CSS
- Modern CSS, custom properties (variables), autoprefixing, etc
- Modern layouts through CSS grid, flex, and float
- Component scaffolding system to easily create new theme components

### Component Scaffolding

WP Rig includes a component scaffolding system that makes it easy to create new PHP components under the `inc/` directory. This allows developers to quickly add new functionality to their theme following WP Rig's component architecture.

#### Usage

```bash
npm run create-rig-component "Component Name" [options]
```

#### Options

- `--templating`: Add Templating_Component_Interface and template_tags() method
- `--tests`: Create minimal PHPUnit test skeleton

#### Example

```bash
npm run create-rig-component "Related Posts" --templating --tests
```

This command will:
1. Create a new component at `inc/Related_Posts/Component.php`
2. Implement both Component_Interface and Templating_Component_Interface
3. Add an empty template_tags() method ready to be customized
4. Create a test file at tests/phpunit/unit/inc/Related_Posts/ComponentTest.php
5. Auto-register the component in Theme.php

For more information about the advanced features in WP Rig and how to use them, visit
the [Advanced Features Wiki page](https://github.com/wprig/wprig/wiki/Advanced-Features-(and-how-to-use-them)).

## License

WP Rig is released
under [GNU General Public License v3.0 (or later)](https://github.com/wprig/wprig/blob/master/LICENSE).
