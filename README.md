# dictator-cypress

[![NPM](https://img.shields.io/npm/v/dictator-cypress.svg?style=flat-square)](https://www.npmjs.com/package/dictator-cypress)
[![Build Status](https://travis-ci.org/tomasbjerre/dictator-cypress.svg?branch=master)](https://travis-ci.org/tomasbjerre/dictator-cypress)

An example dictator created with [dictator-builder](https://github.com/tomasbjerre/dictator-builder).

The [cypress binaries](https://download.cypress.io/desktop.json) are not small enough to be published to `registry.npm.org`. This repository shows how to package your own NPM package that you can published to your internal NPM registry.

This is just an example of how to package cypress to use it inside firewalls where you cannot download from the cypress public [download mirror](https://docs.cypress.io/guides/getting-started/installing-cypress.html).

# Using it with an application

Se example usage in [dictator-cypress-example](https://github.com/tomasbjerre/dictator-cypress-example).

When added to your `package.json` like this:

```json
{
  "scripts": {
    "preinstall": "npx dictator-cypress@a.b.c"
  }
}
```

And when `npm install` is performed in that repository, it will:

- Determine your platform
- Add **cypress binary** for your platform as `/cypress.zip`
- Make sure `.npmrc` contains `CYPRESS_INSTALL_BINARY=${PWD}/cypress.zip`

# Publishing this repository to use it in application

You need to get the binaries from the [Cypress download mirror](https://docs.cypress.io/guides/getting-started/installing-cypress.html). Only pick the ones you need, perhaps:

- https://cdn.cypress.io/desktop/4.5.0/win32-x64/cypress.zip
- https://cdn.cypress.io/desktop/4.5.0/linux-x64/cypress.zip

Replace the fake zip-binaries in [/dictatables](/dictatables) folders with the real ones you downloaded.

Perhaps you want to commit the binaries to Git and release with a CI environment like Jenkins. Or publish the package from your local machine without committing to Git. This repository has a `release` script that you may want to use `npm run release`.
