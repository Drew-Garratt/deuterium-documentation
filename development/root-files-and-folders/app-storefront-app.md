---
description: Explains the folders and files found at the root of storefront-app.
---

# app/storefront-app

## Introduction

* Besides the _src_ folder you will find numerous files at the storefront-app root (outside the _src_ folder), below are explanations for what they do

## Folders

* _.next -_ Contains the built Next.js application. Is only generated on build (also used in tests)
* _**.storybook**_ - Contains Storybook assets and configuration
* _**e2e**_ - Contains Playwright end to end tests and configuration
* _**public**_ - Next.js static assets folder [see here](https://nextjs.org/docs/basic-features/static-file-serving)

## Files

* _**.env**_** ** - Contains public variables such as Shopify URL and Storefront access token
* _**.example.env.local**_ - Example env file for private variables such asmultipass secret
* _**.escheckrc**_ - ES version checker config
* _**.eslintrc.js**_ - ESLint (JS linting) config. Config extends ES Monorepo base config and includes jsx-a11y and next/core-web-vitals.
* _**.size-limit.js**_ - Enforces size limits to the built Next.js app. (used in CI tests)
* _**babel.config.js**_** ** - Babel config
* _**codegen.js**_ - GraphQL Codgen configuration
* _**jest.config.js** _ - Jest configuration
* _**lingui.config.js** _ - Lingui configuration [lingui.md](../../features/libraries/lingui.md "mention")
* _**lint-staged.config.js**_ - Lint staged config [see here](https://github.com/okonet/lint-staged)
* _**next.config.js**_ - Next.js config file
* _**next-env.d.ts**_ - Next typescript enable file
* _**next-i18next.config.js**_ - i18next config used in concert with Lingui
* _**package.json** _ - Name, version, dependencies, and commands for storefront-app
* _**playwright.config.ts**_ - Playwright configuration
* _**README.md**_ - storefront-app read me
* _**tsconfig.jest.json**_ - Jest specific typescript config
* _**tsconfig.json**_** ** - Typescript config



