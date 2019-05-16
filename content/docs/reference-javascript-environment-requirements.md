---
id: javascript-environment-requirements
title: JavaScript એન્વાયર્નમેન્ટ ની આવશ્યકતાઓ
layout: docs
category: Reference
permalink: docs/javascript-environment-requirements.html
---

React 16 એ [મેપ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) અને [સેટ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) ના સંગ્રહ પ્રકારો પર આધાર રાખે છે. 
જો તમે જૂના બ્રાઉઝર્સ અને ઉપકરણોને સમર્થન આપો છો, જે હજી સુધી આ નેચરલ (દા.ત. IE <11) પ્રદાન કરી શકતા નથી અથવા જેની પાસે બિન-સુસંગત અમલીકરણો (દા.ત. IE 11) છે, તો તમારા બંડલ કરેલ એપ્લિકેશનમાં વૈશ્વિક પોલિફિલનો સમાવેશ કરો, જેમ કે [core-js](https://github.com/zloirock/core-js) or [babel-polyfill](https://babeljs.io/docs/usage/polyfill/).

જૂના બ્રાઉઝર્સને સમર્થન આપવા માટે core-js નો ઉપયોગ કરીને React 16 માટે પોલિફિલ્ડ એન્વાયર્નમેન્ટ આના જેવું લાગે છે:

```js
import 'core-js/es6/map';
import 'core-js/es6/set';

import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <h1>નમસ્તે</h1>,
  document.getElementById('root')
);
```

React આના પણ પર આધાર રાખે છે `requestAnimationFrame` (પરીક્ષણ એન્વાયર્નમેન્ટ માં પણ).  
તમે ઉપયોગ કરી શકો છો [raf](https://www.npmjs.com/package/raf) પેકેજ ને પાતળું કરવા માટે `requestAnimationFrame`:

```js
import 'raf/polyfill';
```
