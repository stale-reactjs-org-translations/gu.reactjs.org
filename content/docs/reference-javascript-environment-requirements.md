---
id: javascript-environment-requirements
title: JavaScript એન્વાયર્નમેન્ટ ની આવશ્યકતાઓ
layout: docs
category: Reference
permalink: docs/javascript-environment-requirements.html
---

<<<<<<< HEAD
React 16 એ [મેપ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) અને [સેટ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) કલેકશન ટાઈપ્સ  પર આધાર રાખે છે. 
જો તમે જૂના બ્રાઉઝર્સ અને ઉપકરણોને સપોર્ટ આપો છો, જે હજી સુધી આ પ્રાકૃતિક રીતે  પ્રદાન ન કરતા હોય (દા.ત. IE <11) અથવા એની પાસે બિન-સુસંગત અમલીકરણો છે (દા.ત. IE 11), તો તમારા બંડલ કરેલ એપ્લિકેશનમાં ગ્લોબલ polyfill નો સમાવેશ કરો, જેમ કે [core-js](https://github.com/zloirock/core-js) અથવા  [babel-polyfill](https://babeljs.io/docs/usage/polyfill/).
=======
React 16 depends on the collection types [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) and [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set). If you support older browsers and devices which may not yet provide these natively (e.g. IE < 11) or which have non-compliant implementations (e.g. IE 11), consider including a global polyfill in your bundled application, such as [core-js](https://github.com/zloirock/core-js).
>>>>>>> f0a9793dff9f8e86ec365bfadb0b4b23c6f618ce

જૂના બ્રાઉઝર્સને સમર્થન આપવા માટે, React 16 નું polyfilled એન્વાયર્નમેન્ટ core-js નો ઉપયોગ કરે છે જે નીચે મુજબ જેવું લાગે છે :

```js
import 'core-js/es/map';
import 'core-js/es/set';

import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

React `requestAnimationFrame` પર પણ આધાર રાખે છે (ટેસ્ટ એન્વાયર્નમેન્ટ માં પણ).  
`requestAnimationFrame` ને shim કરવા માટે તમે [raf](https://www.npmjs.com/package/raf) પેકેજ નો ઉપયોગ કરી શકો છો:

```js
import 'raf/polyfill';
```
