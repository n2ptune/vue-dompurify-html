# vue-dompurify-html

[![npm](https://img.shields.io/npm/v/vue-dompurify-html)](https://www.npmjs.com/package/vue-dompurify-html)
[![Build Status](https://travis-ci.com/LeSuisse/vue-dompurify-html.svg?branch=master)](https://travis-ci.com/LeSuisse/vue-dompurify-html)
[![Code Coverage](https://codecov.io/gh/LeSuisse/vue-dompurify-html/branch/master/graph/badge.svg)](https://codecov.io/gh/LeSuisse/vue-dompurify-html)

A "safe" replacement for the `v-html` directive. The HTML code is
sanitized with [DOMPurify](https://github.com/cure53/DOMPurify) before being interpreted.

This is only a small wrapper around DOMPurify to ease its usage in a Vue app.
You should take a look at the 
[DOMPurify Security Goals & Threat Model](https://github.com/cure53/DOMPurify/wiki/Security-Goals-&-Threat-Model)
to understand what are the limitations and possibilities.

## Installation

```
npm install vue-dompurify-html
```

## Usage

```js
import Vue from 'vue'
import VueDOMPurifyHTML from 'vue-dompurify-html'

Vue.use(VueDOMPurifyHTML)

new Vue({
  el: '#app',
  data: {
    rawHtml: '<span style="color: red">This should be red.</span>'
  }
})
```

In your template:
```html
<div id="app">
    <div v-dompurify-html="rawHtml"></div>
</div>
```

You can also define your [DOMPurify configurations](https://github.com/cure53/DOMPurify#can-i-configure-dompurify):
```js
import Vue from 'vue'
import VueDOMPurifyHTML from 'vue-dompurify-html'

Vue.use(VueDOMPurifyHTML, {
  namedConfigurations: {
    'svg': {
      USE_PROFILES: { svg: true }
    },
    'mathml': {
      USE_PROFILES: { mathMl: true }
    },
  }
});

new Vue({
  el: '#app',
  data: {
    rawHtml: '<span style="color: red">This should be red.</span>',
    svgContent: '<svg><rect height="50"></rect></svg>'
  }
})
```

Your configuration keys can then be used as an argument of the directive:
```html
<div id="app">
    <div v-dompurify-html="rawHtml"></div>
    <div v-dompurify-html:svg="svgContent"></div>
</div>
```

Alternatively, you can define a default [DOMPurify configuration](https://github.com/cure53/DOMPurify#can-i-configure-dompurify):
```js
import Vue from 'vue'
import VueDOMPurifyHTML from 'vue-dompurify-html'

Vue.use(VueDOMPurifyHTML, {
  default: {
    USE_PROFILES: { html: false }
  }
});

new Vue({
  el: '#app',
  data: {
    rawHtml: '<span style="color: red">This should not be red.</span>'
  }
})
```

The `default` [DOMPurify configuration](https://github.com/cure53/DOMPurify#can-i-configure-dompurify) will be used:
```html
<div id="app">
    <div v-dompurify-html="rawHtml"></div>
</div>
```
