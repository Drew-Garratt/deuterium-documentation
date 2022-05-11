---
description: >-
  Lingui is an easy yet powerful internationalisation framework for global
  projects.
---

# Lingui

## Introduction

Lingui is a lightweight library (3.1 kBs gzipped) that provides clean and readable functions and helpers for working with translations.

* Lingui handles the output of all translated strings in the application
* Translation changes are automatically loaded into the client while in dev mode
* Translation extraction is manged via the CLI (you don't have to populate your JSON files to read the default language)

## Usage in storefront-app

The most basic interaction you will have in the application is via the one of Lingui's string translate methods. These strings can be imidately used remain readable in components. Once translation strings have been added/updated the CLI then allows us to extract and compile these translations for production.

### Macros

`@lingui/macro` package provides [babel macros](https://github.com/kentcdodds/babel-plugin-macros) which transforms JavaScript objects and JSX elements into messages in ICU MessageFormat.

```
import { t, plural } from '@lingui/macro';

// Translated string
t`Close`

// Macro with manual ID
t({
    id: 'accessibility.close',
    message: 'Close',
})

// Plural Macro
plural(count, {
   one: 'Message',
   other: 'Messages'
})
```

### Extraction and Compliation

Lingui's messages.json files are createad automatically by extracting translation strings from the application. To perform this extraction run the following from the the `apps/storefront-app` folder.

`yarn lingui extract`

```bash
Catalog statistics for public/locales/{locale}/messages: 
┌─────────────┬─────────────┬─────────┐
│ Language    │ Total count │ Missing │
├─────────────┼─────────────┼─────────┤
│ en (source) │      4      │    -    │
│ fr          │      4      │    4    │
│ es          │      4      │    4    │
│ pseudo      │      4      │    4    │
└─────────────┴─────────────┴─────────┘

(use "yarn extract" to update catalogs with new messages)
(use "yarn compile" to compile catalogs for production)T
```

The output of this command allows us to see how many strings total have been extracted and which languge files are currently missing translations.\
\
The storefront application uses a plain JSON format to store these translations. The output of this file is flat, however by utilising the `t({id: '', message:''})` form of the translation macros the output can be made descriptive.

```
{
  "accessibility.close": "Close",
  "general.site_header.cart": "Cart",
  "general.site_header.menu": "Menu",
  "main.explanation": "This is it!"
}
```

Prior to release the command `yarn lingui compile` must be run in order for the translations to be made available to the final application.\
\
Any strings not translated will simply display their fallback(source) lanague when that language is loaded.

## Further Reading

* Lingui Docs - React [https://lingui.js.org/tutorials/react-patterns.html](https://lingui.js.org/tutorials/react-patterns.html)
* LogRocket guide to translation with Lingui [https://blog.logrocket.com/complete-guide-internationalization-nextjs/](https://blog.logrocket.com/complete-guide-internationalization-nextjs/)

## Technical details

* Lingui's config is controlled from the root of the `storefront-app` by the `lingui.config.js`
*   Lingui provides a pseudo local for testing purposes. When switching to this local the output is automatically created to show a string has been translated&#x20;

    ```
    Account Settings --> [!!! Àççôûñţ Šéţţîñĝš !!!]
    ```
* Next's own i18next config is used in concert with Lingui to control output. This config can be found at the root of the `storefront-app` in `next-i18next.config.js`
* As with other global scopped functions Lingui is loaded into the applicatin via [app-provider.md](../../components/default-components/app-provider.md "mention")\


