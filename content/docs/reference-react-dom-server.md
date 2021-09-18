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

તેના પ્રારંભિક HTML પર React element પ્રસ્તુત કરો। તે [વાંચવા યોગ્ય સ્ટ્રીમ](https://nodejs.org/api/stream.html#stream_readable_streams) આપે છે જે HTML શબ્દમાળાને ઉત્પાદન કરે છે। આ પ્રવાહ દ્વારા HTML આઉટપુટ બરાબર તેવું જ છે જે [`ReactDOMServer.renderToString`](#rendertostring) પાછું આપશે। તમે સર્વર પર HTML પેદા કરવા માટે આ પદ્ધતિનો ઉપયોગ કરી શકો છો અને ઝડપી પૃષ્ઠ લોડ માટે પ્રારંભિક વિનંતી પર માર્કઅપ મોકલી શકો છો અને શોધ એન્જિનને SEO હેતુ માટે તમારા પૃષ્ઠોને તપાસવાની મંજૂરી આપવા માટે। 

જો તમે પહેલાથી જ આ સર્વર માં પ્રસ્તુત કરેલું માર્કઅપ ધરાવતા નોડ પર [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate) ને call કરો છો, React તેને સાચવશે અને ફક્ત event handlers ને જોડશે, જે તમને ખૂબ પ્રદર્શનશીલ પ્રથમ લોડ અનુભવ મેળવવાની મંજૂરી આપે છે।

> નૉૅધ:
>
> માત્ર સર્વર। આ API Browser માં ઉપલબ્ધ નથી।
>
> આ પદ્ધતિથી પરત થયેલ પ્રવાહ utf-8 માં encoded કરેલ byte પ્રવાહ પાછો આવશે। જો તમને બીજા encoding માં પ્રવાહની જરૂર હોય, તો [iconv-lite](https://www.npmjs.com/package/iconv-lite) જેવા પ્રોજેક્ટ પર એક નજર નાખો, જે લખાણ રૂપાંતર માટે પ્રવાહ પરિવર્તન પ્રદાન કરે છે।

* * *

### `renderToStaticNodeStream()` {#rendertostaticnodestream}

```javascript
ReactDOMServer.renderToStaticNodeStream(element)
```

[`renderToNodeStream`](#rendertonodestream) જેવું જ, સિવાય કે આ વધારાના DOM attribute બનાવતું નથી જે React આંતરિક રીતે વાપરે છે, જેમ કે `data-reactroot`। જો તમે એક સરળ સ્થિર પૃષ્ઠ જનરેટર તરીકે React વાપરવા માંગતા હોવ તો આ ઉપયોગી છે, કારણ કે વધારાના attributes છીનવી લેવાથી કેટલાક bytes બચાવી શકાય છે।

આ પ્રવાહ દ્વારા HTML આઉટપુટ બરાબર તેવું જ છે જે [`ReactDOMServer.renderToStaticMarkup`](#rendertostaticmarkup) પાછું આપશે।

જો તમે માર્કઅપને ઇન્ટરેક્ટિવ બનાવવા માટે client પર React નો ઉપયોગ કરવાની યોજના ઘડી રહ્યા છો, તો પછી આ પદ્ધતિનો ઉપયોગ કરશો નહીં। તેના બદલે, server પર [`renderToNodeStream`](#rendertonodestream) ઉપયોગ કરો અને client પર [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate)।

> નૉૅધ:
>
> માત્ર સર્વર। આ API Browser માં ઉપલબ્ધ નથી।
>
> આ પદ્ધતિથી પરત થયેલ પ્રવાહ utf-8 માં encoded કરેલ byte પ્રવાહ પાછો આવશે। જો તમને બીજા encoding માં પ્રવાહની જરૂર હોય, તો [iconv-lite](https://www.npmjs.com/package/iconv-lite) જેવા પ્રોજેક્ટ પર એક નજર નાખો, જે લખાણ રૂપાંતર માટે પ્રવાહ પરિવર્તન પ્રદાન કરે છે।
