# ember-froalacharts

Simple and lightweight Ember component for FroalaCharts. `ember-froalacharts` enables you to add JavaScript charts in your Ember application or project without any hassle.

- Github Repo: [https://github.com/froala/ember-froalacharts](https://github.com/froala/ember-froalacharts)
- Documentation: [https://froala.com/charts/docs/frameworks/ember/](https://froala.com/charts/docs/frameworks/ember/)
- Support: [support@froala.com](support@froala.com)
- FroalaCharts
  - Official Website: [https://froala.com/](https://froala.com/)
  - Official NPM Package: [https://www.npmjs.com/package/froalacharts](https://www.npmjs.com/package/froalacharts)
- Issues: [https://github.com/froala/ember-froalacharts/issues](https://github.com/froala/ember-froalacharts/issues)

---

## Table of Contents

- [Getting Started](#getting-started)
  - [Requirements](#requirements)
  - [Installation](#installation)
- [Quick Start](#quick-start)
- [For Contributors](#for-contributors)
- [Licensing](#licensing)

## Getting Started

### Requirements

- **Node.js**, **NPM/Yarn** installed globally in your OS.
- **FroalaCharts** and **Ember** installed in your project, as detailed

## Installation

**Direct Download**
All binaries are located on our [github repository](https://github.com/froala/ember-froalacharts/).

**Install from NPM**

To install `ember-froalacharts` to any existing ember project, run:

For Modern Ember CLI:

```bash
$ npm install ember-froalacharts --save
```

For Earlier Ember CLI (and addon developers):

```bash
$ npm install ember-froalacharts --save-dev
$ ember g ember-froalacharts
```

Then install `froalacharts` to your project:

```bash
$ npm install froalacharts --save
```

Then import `froalacharts` library to your `ember-cli-build.js` build file:

```javascript
/* eslint-env node */
'use strict';

const EmberApp = require('ember-cli/lib/broccoli/ember-app');

module.exports = function(defaults) {
  let app = new EmberApp(defaults, {
    // Add options here
  });

  // Import froalacharts library
  app.import('node_modules/froalacharts/froalacharts.js');
  app.import('node_modules/froalacharts/themes/froalacharts.theme.froala.js');

  // Use `app.import` to add additional libraries to the generated
  // output files.
  //
  // If you need to use different assets in different
  // environments, specify an object as the first parameter. That
  // object's keys should be the environment name and the values
  // should be the asset to use in that environment.
  //
  // If the library that you are including contains AMD or ES6
  // modules that you would like to import into your application
  // please specify an object with the list of modules as keys
  // along with the exports of each module as its value.

  return app.toTree();
};
```

## Quick Start

After installing `ember-froalacharts`, create a simple component(e.g. `chart-viewer`, also you can use it anywhere in your application) to show your interactive charts, run:

```bash
$ ember g component chart-viewer
```

Write your chart logic in `chart-viewer.js` file:

```javascript
import Component from '@ember/component';

const myDataSource = {
  chart: {
    caption: "Harry's SuperMart",
    subCaption: 'Top 5 stores in last month by revenue',
    numberPrefix: '$',
    theme: 'fint'
  },
  data: [
    {
      label: 'Bakersfield Central',
      value: '880000'
    },
    {
      label: 'Garden Groove harbour',
      value: '730000'
    },
    {
      label: 'Los Angeles Topanga',
      value: '590000'
    },
    {
      label: 'Compton-Rancho Dom',
      value: '520000'
    },
    {
      label: 'Daly City Serramonte',
      value: '330000'
    }
  ]
};

export default Component.extend({
  title: 'Ember FroalaCharts Sample',
  width: 600,
  height: 400,
  type: 'pie',
  dataFormat: 'json',
  dataSource: myDataSource
});
```

And use `froalacharts` component in your `chart-viewer.hbs` template to show your charts:

```html
<h1>{{ title }}</h1>

{{froalacharts-xt width=width height=height type=type dataFormat=dataFormat
dataSource=dataSource}}
```

Then, use `chart-viewer` component in your `application.hbs` template:

```html
{{chart-viewer}} {{outlet}}
```

## For Contributors

- Clone the repository.
- Install dependencies.
- Run `npm start` to start the dev server.
- Open `http://localhost:4200/` in your browser.

```sh
$ git clone https://github.com/froala/ember-froalacharts.git
$ cd ember-froalacharts
$ npm i && bower install
$ npm start
```

To build, run:

```sh
$ npm run build
```

## Licensing

The FroalaCharts Ember component is open-source and distributed under the terms of the MIT/X11 License. However, you will need to download and include FroalaCharts library in your page separately, which has a [separate license](https://www.ideracorp.com/Legal/Froala/FroalaChartsLicenseAgreement).