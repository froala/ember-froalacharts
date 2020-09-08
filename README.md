# Ember-FroalaCharts

A lightweight EmberJS component which provides bindings for FroalaCharts JavaScript Charting Library. It easily adds rich and interactive charts to any ambitious Ember application.

## [Demo](https://fusioncharts.github.io/ember-fusioncharts/)

- Github Repo: [https://github.com/froala/ember-froalacharts](https://github.com/froala/ember-froalacharts)
- Documentation: [https://www.fusioncharts.com/dev/getting-started/ember/your-first-chart-using-ember](https://www.fusioncharts.com/dev/getting-started/ember/your-first-chart-using-ember)
- Support: [https://www.fusioncharts.com/contact-support](https://www.fusioncharts.com/contact-support)
- FroalaCharts
  - Official Website: [https://www.fusioncharts.com/](https://www.fusioncharts.com/)
  - Official NPM Package: [https://www.npmjs.com/package/fusioncharts](https://www.npmjs.com/package/fusioncharts)
- Issues: [https://github.com/fusioncharts/ember-fusioncharts/issues](https://github.com/fusioncharts/ember-fusioncharts/issues)

---

## Table of Contents

- [Getting Started](#getting-started)
  - [Requirements](#requirements)
  - [Installation](#installation)
- [Quick Start](#quick-start)
  - [Working with APIs](#working-with-apis)
  - [Working with events](#working-with-events)
- [Going Beyond Charts](#going-beyond-charts)
- [Usage and Integration of FroalaTime](#usage-and-integration-of-froalatime)
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

## Working with APIs

In your component file:

```javascript
import Component from '@ember/component';

export default Component.extend({
  width: 600,
  height: 400,
  type: 'pie',
  dataFormat: 'json',
  dataSource: {
    chart: {
      caption: 'Countries With Most Oil Reserves [2017-18]',
      subCaption: 'In MMbbl = One Million barrels',
      xAxisName: 'Country',
      yAxisName: 'Reserves (MMbbl)',
      numberSuffix: 'K',
      theme: 'froala'
    },
    data: [
      {
        label: 'Venezuela',
        value: '290'
      },
      {
        label: 'Saudi',
        value: '260'
      },
      {
        label: 'Canada',
        value: '180'
      },
      {
        label: 'Iran',
        value: '140'
      },
      {
        label: 'Russia',
        value: '115'
      },
      {
        label: 'UAE',
        value: '100'
      },
      {
        label: 'US',
        value: '30'
      },
      {
        label: 'China',
        value: '30'
      }
    ]
  },
  events: null,
  message: 'Hover on the plot to see the value along with the label',

  init() {
    this._super(...arguments);
    const self = this;
    this.set('events', {
      dataplotRollOver: function(eventObj, dataObj) {
        self.set(
          'message',
          'You are currently hovering over ' +
            dataObj.categoryLabel +
            ' whose value is ' +
            dataObj.displayValue
        );
      },
      dataPlotRollOut: function(eventObj, dataObj) {
        self.set(
          'message',
          'Hover on the plot to see the value along with the label'
        );
      }
    });
  }
});
```

In your template file:

```html
{{froalacharts-xt width=width height=height type=type dataFormat=dataFormat
dataSource=dataSource events=events}}

<p>{{ message }}</p>
```

Using this example when you hover on a dataplot you will get to see the value and label of the dataplot underneath the chart.

## Working with events

To attach event listeners to FroalaCharts, you can use the `events` attribute in the `froalacharts` template.

In your template file:

```html
{{froalacharts-xt width=width height=height type=type dataFormat=dataFormat
dataSource=dataSource events=events}}
```

## Usage and integration of FroalaTime

From `froalacharts@1.0.4` and `ember-froalacharts@1.0.0`, You can visualize timeseries data easily with vue.

Learn more about FroalaTime [here](https://www.fusioncharts.com/fusiontime).

import `FroalaTime` library to your `ember-cli-build.js` build file:

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

Create a simple component(e.g. `timeseries-viewer`, also you can use it anywhere in your application) to show your interactive charts, run:

```bash
$ ember g component chart-viewer
```

Write your chart logic in `timeseries-viewer.js` file:

```javascript
import Component from '@ember/component';

const dataSource = {
  data: null,
  caption: {
    text: 'Sales Analysis'
  },
  subcaption: {
    text: 'Grocery & Footwear'
  },
  series: 'Type',
  yAxis: [
    {
      plot: 'Sales Value',
      title: 'Sale Value',
      format: {
        prefix: '$'
      }
    }
  ]
};

const jsonify = res => res.json();
// This is the remote url to fetch the data.
const dataFetch = fetch(
  'https://s3.eu-central-1.amazonaws.com/fusion.store/ft/data/plotting-multiple-series-on-time-axis-data.json'
).then(jsonify);
const schemaFetch = fetch(
  'https://s3.eu-central-1.amazonaws.com/fusion.store/ft/schema/plotting-multiple-series-on-time-axis-schema.json'
).then(jsonify);

export default Component.extend({
  title: 'TimeSeries Example',
  width: 600,
  height: 400,
  type: 'timeseries',
  dataFormat: null,
  dataSource: null,
  // timeSeriesDS: null,

  init() {
    this._super(...arguments);
    this.set('dataFormat', 'json');
    this.createDataTable();
  },

  createDataTable() {
    Promise.all([dataFetch, schemaFetch]).then(res => {
      const data = res[0];
      const schema = res[1];
      // First we are creating a DataStore
      const froalaDataStore = new FroalaCharts.DataStore();
      // After that we are creating a DataTable by passing our data and schema as arguments
      const froalaDataTable = froalaDataStore.createDataTable(data, schema);
      // Afet that we simply mutated our timeseries datasource by attaching the above
      // DataTable into its data property.
      dataSource.data = froalaDataTable;
      this.set('dataSource', dataSource);
    });
  }
});
```

And use `froalacharts` component in your `timeseries-viewer.hbs` template to show your charts:

```html
<h1>{{ title }}</h1>

{{froalacharts-xt width=width height=height type=type dataFormat=dataFormat
dataSource=dataSource}}
```

Then, use `timeseries-viewer` component in your `application.hbs` template:

```html
{{timeseries-viewer}} {{outlet}}
```

## Going beyond Charts

- Explore 20+ pre-built business specific dashboards for different industries like energy and manufacturing to business functions like sales, marketing and operations [here](https://www.fusioncharts.com/explore/dashboards).
- See [Data Stories](https://www.fusioncharts.com/explore/data-stories) built using FroalaCharts’ interactive JavaScript visualizations and learn how to communicate real-world narratives through underlying data to tell compelling stories.

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

The FroalaCharts Ember component is open-source and distributed under the terms of the MIT/X11 License. However, you will need to download and include FroalaCharts library in your page separately, which has a [separate license](https://www.fusioncharts.com/buy).