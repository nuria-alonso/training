# Installation and Customisation guide.
This guide will walk you through the installation, customisation.

- [About](#about)
- [Requirements](#requirements)
	- [For authoring content](#for-authoring-content)
	- [For local development / customisation](#for-local-development-customisation)
- [Installation](#installation)
- [Build the project](#build-the-project)
- [Content Management guidelines - The Data](#content-management-guidelines-the-data)
- [Managing languages](#managing-languages)
	- [The Data](#the-data)
	- [Setting the languages.](#setting-the-languages)
- [Customising the UI](#customising-the-ui)
- [Customising the base html, fonts and styles.](#customising-the-base-html-fonts-and-styles)
	- [HTML](#html)
	- [Fonts](#fonts)
	- [styles](#styles)


## About
CurryCooler consists of 2 components.

1. **The Data** - A collection of markdown files that consist of Workshops, Activities and Materials.
2. **The UI** - A web-based front end for users to browse, select and export units from **the data**

## Requirements
### For authoring content
- A text/markdown editor (recommended: [atom](https://atom.io) with markdown linting packages)

### For local development / customisation
- [Nodejs](https://nodejs.org/en/)


## Installation
- Clone this repository. `git clone https://github.com/decidim/training.git`
- navigate to the cloned repository. `cd training`
- run `npm install`

This will install all the dependencies that you need to **build** the project locally.

## Build the project
- `npm run build` will build the data and ui to the `_site/` folder which can be copied to a webserver or served locally
- 'npm run start' will start the development server on your computer. In this mode you can preview the final output live in a browser, make edits and preview them.
- see other build options by running `npm run`

## Content Management guidelines - The Data
This is **The Data**: All content resides in the `content` directory which has the following structure
```
content
├── en
│   ├── Activities
│   │   └── Activity-files.md
│   ├── Materials.md
│   └── Workshops
│       └── Workshop-files.md
└── es
    ├── Activities
    │   └── Activity-files.md
    ├── Materials.md
    └── Workshops
        └── Workshop-files.md

```
- The example above uses 2 languages - English and Spanish.
- The contents of each language should be in a sub-directory of the `content` directory.
- `Activities` and `Workshops` are organised in sub-directories within each language directory. To be compiled correctly, they have to strictly conform to the [template](https://github.com/decidim/training/blob/master/content/es/Template) provided.
- Materials are listing in a single file, one such file for each language.

## Managing languages
### The Data
The Data is organised primarily by languages [see here](#content-management-guidelines).

### Setting the languages.
While your project may have content for several languages, it has to be explicitly specified which languages are being published. This is configured in `config/base-settings.js` in the section of the file as shown in the example snippet below
```
const locales = [
  {
    code: 'es',
    name: 'Español',
  },
 {
   code: 'en',
   name: 'English',
  },
];
```

Set the default language in the same file in this section
```
const defaultLocale = {
  code: 'es',
  name: 'Español',
};
```
- The above example shows 2 languages - English and Spanish.
- The `code` and `name` have to be specified.
  - code: ISO 630-1 language code [see here](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)
  - name: ISO 630 Native name. This is the label displayed in the language switcher widget.

## Customising the UI
All UI strings can be translated. for each of the available languages please make sure a corresponding set of UI language customisations exist. These are organised in the `config` directory with a sub-directory for each language, each containing 2 files.
- `phrasing.json` - These are the section titles, sub-titles, button and link labels of the UI.
- `iconmap.json` - This contains a list of all tags used in the content, each mapped to an icon name from the [font-awesome](http://fontawesome.io/icons/) icon library. These icons are used as icons for the filters in the UI.
  - The labels are case sensitive and should match exactly the tags being used.
  - The icon eg. `fa-cogs` should match the icon class names as specified by font-awesome.

## Customising the base html, fonts and styles.
### HTML
- The base html template is in `public/index.html` file.
- Please ensure that a `<div id="curricula-ui"></div>` element exists.
- You can edit metadata, title, add external styles and js in here.

### Fonts
- Custom fonts for the UI can be added to the `public/assets/fonts`
- Please include fonts in `.eot, .svg, .woff, .woff2, .otf, .ttf` formats
- add a `@font-face` declaration for each font in `public/assets/css/typo.scss` (use one of the existing declarations as an example)

### styles
- In `public/assets/css/configuration.scss` you can override or customise the styles of the UI
- the stylesheet is in scss format.
