---
id: rendering-elements
title: રેન્ડરિંગ તત્વો
permalink: docs/rendering-elements.html
redirect_from:
  - "docs/displaying-data.html"
prev: introducing-jsx.html
next: components-and-props.html
---

તત્વો(Elements) એ React એપ્લિકેશન્સના નાના બિલ્ડિંગ બ્લોક્સ છે.

તમે સ્ક્રીન પર શું જોવા માંગો છો તેનું એક તત્વ(Element) વર્ણન કરે છે:

```js
const element = <h1>Hello, world</h1>;
```

React Elements સાદા ઑબ્જેક્ટ્સ છે અને તે બનાવવા માટે સસ્તા છે, જે બ્રાઉઝર DOM Elements થી વિપરીત છે. React DOM,React Elements સાથે મેચ કરવા માટે DOM ને અપડેટ કરવાની કાળજી લે છે.

>**નૉૅધ:**
>
>એક "components" ની વધુ જાણીતી ખ્યાલ સાથે elements ને ભ્રમિત કરી શકે છે. અમે [આગામી વિભાગ](/docs/components-and-props.html) માં components રજૂ કરીશું. Elements એ છે કે કયા components "બનેલા છે" અને આગળ વધતા પહેલાં અમે તમને આ વિભાગ વાંચવા માટે પ્રોત્સાહિત કરીએ છીએ.

## DOM માં એલિમેન્ટ રેંડરિંગ {#rendering-an-element-into-the-dom}

ચાલો કહીએ કે તમારી HTML ફાઇલમાં ક્યાંક `<div>` છે.

```html
<div id="root"></div>
```

અમે તેને "root" DOM node કહીએ છીએ કારણ કે તેની અંદરની દરેક વસ્તુ React DOM દ્વારા સંચાલિત કરવામાં આવશે.

React સાથે બનેલી એપ્લિકેશન્સમાં સામાન્ય રૂપે એક જ root DOM node હોય છે. જો તમે અસ્તિત્વમાં છે તે એપ્લિકેશનમાં React ને સંકલિત કરી રહ્યાં છો, તો તમને ગમે તેટલા અલગ root DOM nodes હોઈ શકે છે.

React Element ને root DOM node માં રેન્ડર કરવા માટે, બંનેને `ReactDOM.render ()` માં પસાર કરો:

`embed:rendering-elements/render-an-element.js`

[](codepen://rendering-elements/render-an-element)

તે પૃષ્ઠ પર "Hello, world" દર્શાવે છે.

## Rendered Element ને અપડેટ કરી રહ્યું છે {#updating-the-rendered-element}

React elements [અવ્યવસ્થિત](https://en.wikipedia.org/wiki/Immutable_object) છે. એકવાર તમે element બનાવી લો, પછી તમે તેના children અથવા attributes ને બદલી શકતા નથી. એક element મૂવીમાં એક ફ્રેમ જેવું છે: તે ચોક્કસ સમયે UI રજૂ કરે છે.

અત્યાર સુધીના અમારા જ્ઞાનથી, UI ને અપડેટ કરવાની એકમાત્ર રીત એ એક નવું element બનાવવું છે અને તેને `ReactDOM.render ()` પર પસાર કરવું છે.

આ ટિકિંગ ઘડિયાળનું ઉદાહરણ ધ્યાનમાં લો:

`embed:rendering-elements/update-rendered-element.js`

[](codepen://rendering-elements/update-rendered-element)

તે [SetInterval()](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) કૉલબૅકથી પ્રત્યેક સેકન્ડમાં `ReactDOM.render()` ને કૉલ કરે છે.

>**નૉૅધ:**
>
>વ્યવહારમાં, મોટાભાગના React એપ્લિકેશનો ફક્ત એક વાર `ReactDOM.render ()` ને કૉલ કરે છે. આગલા વિભાગોમાં આપણે જાણીશું કે આવા કોડને [stateful components](/docs/state-and-lifecycle.html) માં શામેલ કરવામાં આવે છે.
>
>તમે વિષયોને અવગણો નહીં કારણ કે તેઓ એક બીજા પર આધાર રાખે છે.

## React ફક્ત શું જરૂરી છે એ ને અપડેટ કરે છે {#react-only-updates-whats-necessary}

React DOM તત્વ અને તેના children ની તુલના પહેલાની સરખામણીમાં કરે છે, અને DOM ને ઇચ્છિત સ્થિતિમાં લાવવા માટે જરૂરી DOM અપડેટ્સને લાગુ કરે છે.

તમે બ્રાઉઝર inspecting સાથે [છેલ્લું ઉદાહરણ](codepen://rendering-elements/update-rendered-element) નું નિરીક્ષણ કરીને ચકાસી શકો છો:

![DOM inspector showing granular updates](../images/docs/granular-dom-updates.gif)

ભલે આપણે દરેક ટિક પર સંપૂર્ણ UI tree નું વર્ણન કરતી element બનાવીએ, ફક્ત text node જેનો સમાવિષ્ટો બદલાઈ ગયો છે તે React DOM દ્વારા અપડેટ થાય છે.

અમારા અનુભવમાં, સમયાંતરે તેને કેવી રીતે બદલવું તેના બદલે UI એ કોઈપણ ક્ષણને કેવી રીતે જોવું જોઈએ તે વિશે વિચારીને બગ્સ(bugs) ની સંપૂર્ણ શ્રેણીને દૂર કરે છે.
