---
id: cdn-links
title: CDN Links
permalink: docs/cdn-links.html
prev: create-a-new-react-app.html
next: release-channels.html
---

<!-- Both React and ReactDOM are available over a CDN. -->
React અને ReactDOM બન્ને હવે CDN પર ઉપલબ્ધ છે.

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
```

<!-- The versions above are only meant for development, and are not suitable for production. Minified and optimized production versions of React are available at: -->
ઉપર આપેલા બન્ને આવ્રુતીઓ ફ્ક્ત ડેવેલોપમેંટ માટે જ છે, અને પ્રોડ્ક્શન માટે યોગ્ય નથી. React ની સંકુચીત અને ઉત્તમ આવ્રુતી નીચે મુજબ ઉપલબ્ધ છે:

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
```

<!-- To load a specific version of `react` and `react-dom`, replace `16` with the version number. -->
React અને ReactDOM ની ચોક્ક્સ આવ્રુતી માટે, ‘16’ ને આવ્રુતી અંક સાથે બદલો.

<!-- ### Why the `crossorigin` Attribute? {#why-the-crossorigin-attribute} -->
### `crossorigin` લાક્ષણીકતા કેમ? {#why-the-crossorigin-attribute}

<!-- If you serve React from a CDN, we recommend to keep the [`crossorigin`](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes) attribute set: -->
જો તમે React CDN પરથી વાપરો છો તો, અ‍મે તમને સલાહ આપીએ છીએ કે તમે [`crossorigin`](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes) લક્ષણીકતા સેટ કરો.

```html
<script crossorigin src="..."></script>
```

<!-- We also recommend to verify that the CDN you are using sets the `Access-Control-Allow-Origin: *` HTTP header: -->
અમે તે પણ ચકસવાની સલાહ આપીએ છીએ કે તમે જે CDN વાપરો છો તે `Access-Control-Allow-Origin: *` HTTP header સેટ કરે છે.

![Access-Control-Allow-Origin: *](../images/docs/cdn-cors-header.png)

<!-- This enables a better [error handling experience](/blog/2017/07/26/error-handling-in-react-16.html) in React 16 and later. -->
આ React 16 અને તેના પછીની આવ્રુતીઓમા સારી રીતે [error handling અ‍નુભવ](/blog/2017/07/26/error-handling-in-react-16.html) આપે છે.
