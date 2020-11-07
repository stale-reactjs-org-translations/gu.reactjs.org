---
id: react-dom-server
title: ReactDOMServer
layout: docs
category: Reference
permalink: docs/react-dom-server.html
---

`ReactDOMServer` object તમને સ્થિર માર્કઅપમાં ઘટકો પ્રસ્તુત કરવા માટે સક્ષમ બનાવે છે। લાક્ષણિક રીતે, તેનો ઉપયોગ Node server પર થાય છે:

```js
// ES modules
import ReactDOMServer from 'react-dom/server';
// CommonJS
var ReactDOMServer = require('react-dom/server');
```

## ઝાંખી {#overview}

નીચેની પદ્ધતિઓનો ઉપયોગ server અને browser બંને વાતાવરણમાં થઈ શકે છે:

- [`renderToString()`](#rendertostring)
- [`renderToStaticMarkup()`](#rendertostaticmarkup)

આ વધારાની પદ્ધતિઓ (`stream`) પેકેજ પર આધારીત છે જે ફક્ત server પર ઉપલબ્ધ છે, અને browser માં કાર્ય કરશે નહીં।

- [`renderToNodeStream()`](#rendertonodestream)
- [`renderToStaticNodeStream()`](#rendertostaticnodestream)

* * *

## સંદર્ભ {#reference}

### `renderToString()` {#rendertostring}

```javascript
ReactDOMServer.renderToString(element)
```

તેના પ્રારંભિક HTML પર React element પ્રસ્તુત કરો। React HTML string પરત કરશે। તમે સર્વર પર HTML પેદા કરવા માટે આ પદ્ધતિનો ઉપયોગ કરી શકો છો અને ઝડપી પૃષ્ઠ લોડ માટે પ્રારંભિક વિનંતી પર માર્કઅપ મોકલી શકો છો અને શોધ એન્જિનને SEO હેતુ માટે તમારા પૃષ્ઠોને તપાસવાની મંજૂરી આપવા માટે।

જો તમે પહેલાથી જ આ સર્વર માં પ્રસ્તુત કરેલું માર્કઅપ ધરાવતા નોડ પર [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate) ને call કરો છો, React તેને સાચવશે અને ફક્ત event handlers ને જોડશે, જે તમને ખૂબ પ્રદર્શનશીલ પ્રથમ લોડ અનુભવ મેળવવાની મંજૂરી આપે છે।

* * *

### `renderToStaticMarkup()` {#rendertostaticmarkup}

```javascript
ReactDOMServer.renderToStaticMarkup(element)
```

[`renderToString`](#rendertostring) જેવું જ, સિવાય કે આ વધારાના DOM attribute બનાવતું નથી જે React આંતરિક રીતે વાપરે છે, જેમ કે `data-reactroot`। જો તમે એક સરળ સ્થિર પૃષ્ઠ જનરેટર તરીકે React વાપરવા માંગતા હોવ તો આ ઉપયોગી છે, કારણ કે વધારાના attributes છીનવી લેવાથી કેટલાક bytes બચાવી શકાય છે।

જો તમે માર્કઅપને ઇન્ટરેક્ટિવ બનાવવા માટે client પર React નો ઉપયોગ કરવાની યોજના ઘડી રહ્યા છો, તો પછી આ પદ્ધતિનો ઉપયોગ કરશો નહીં। તેના બદલે, server પર [`renderToString`](#rendertostring) ઉપયોગ કરો અને client પર [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate)।

* * *

### `renderToNodeStream()` {#rendertonodestream}

```javascript
ReactDOMServer.renderToNodeStream(element)
```

Render a React element to its initial HTML. Returns a [Readable stream](https://nodejs.org/api/stream.html#stream_readable_streams) that outputs an HTML string. The HTML output by this stream is exactly equal to what [`ReactDOMServer.renderToString`](#rendertostring) would return. You can use this method to generate HTML on the server and send the markup down on the initial request for faster page loads and to allow search engines to crawl your pages for SEO purposes.

If you call [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate) on a node that already has this server-rendered markup, React will preserve it and only attach event handlers, allowing you to have a very performant first-load experience.

> Note:
>
> Server-only. This API is not available in the browser.
>
> The stream returned from this method will return a byte stream encoded in utf-8. If you need a stream in another encoding, take a look at a project like [iconv-lite](https://www.npmjs.com/package/iconv-lite), which provides transform streams for transcoding text.

* * *

### `renderToStaticNodeStream()` {#rendertostaticnodestream}

```javascript
ReactDOMServer.renderToStaticNodeStream(element)
```

Similar to [`renderToNodeStream`](#rendertonodestream), except this doesn't create extra DOM attributes that React uses internally, such as `data-reactroot`. This is useful if you want to use React as a simple static page generator, as stripping away the extra attributes can save some bytes.

The HTML output by this stream is exactly equal to what [`ReactDOMServer.renderToStaticMarkup`](#rendertostaticmarkup) would return.

If you plan to use React on the client to make the markup interactive, do not use this method. Instead, use [`renderToNodeStream`](#rendertonodestream) on the server and [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate) on the client.

> Note:
>
> Server-only. This API is not available in the browser.
>
> The stream returned from this method will return a byte stream encoded in utf-8. If you need a stream in another encoding, take a look at a project like [iconv-lite](https://www.npmjs.com/package/iconv-lite), which provides transform streams for transcoding text.
