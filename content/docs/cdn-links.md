---
id: cdn-links
title: CDN Links
permalink: docs/cdn-links.html
prev: create-a-new-react-app.html
next: hello-world.html
---

React અને ReactDOM બંને CDN ઉપર પણ ઉપલબ્ધ છે.

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
```

ઉપરના આ વર્જન ખાલી ડેવલપમેન્ટ માટે જ છે, અને તે પ્રોડક્શન માટે યોગ્ય નથી.React ના મિનિફાઇડ અને ઓપટીમાઈઝ્ડ પ્રોડકશન વર્જન અહી ઉપલબ્ધ છે::

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
```

`react` અને `react-dom` ના ચોક્કસ વર્જન ને લોડ કરવા,વર્જન નંબર ને `16` સાથે બદલો..


### Why the `crossorigin` Attribute? {#why-the-crossorigin-attribute}


જો તમે CDN પરથી React ને ડાઉનલોડ કરો છો તો, અમે આ [`crossorigin`](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes) એટ્રિબ્યુટને સેટ કરવાની સલાહ આપીએ છીએ::


```html
<script crossorigin src="..."></script>
```

અમે તમે જે CDN નો ઉપયોગ કરી રહ્યા છો તેનું `Access-Control-Allow-Origin: *` HTTP હેડર ચકાસવાની પણ સલાહ આપીએ છીએ:


![Access-Control-Allow-Origin: *](../images/docs/cdn-cors-header.png)


આ React 16 અને તેના પછી ને વધુ સારૂ [error handling experience](/blog/2017/07/26/error-handling-in-react-16.html) બનાવે છે.