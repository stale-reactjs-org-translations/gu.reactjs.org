---
id: rendering-elements
title: રેન્ડરિંગ Elements
permalink: docs/rendering-elements.html
redirect_from:
  - "docs/displaying-data.html"
prev: introducing-jsx.html
next: components-and-props.html
---

Elements એ React એપ્લિકેશન્સના નાનામાં નાના બિલ્ડિંગ બ્લોક્સ છે.

Element, તમે સ્ક્રીન પર શું જોવા માંગો છો તેનું વર્ણન કરે છે:

```js
const element = <h1>Hello World</h1>;
```

React Elements સાદા ઑબ્જેક્ટ્સ છે અને તે બનાવવા સરળ છે, જે બ્રાઉઝર DOM Elements થી અલગ છે. React DOMએ React Elements સાથે મેચ કરવા માટે DOM ને અપડેટ કરવાની કાળજી લે છે.

> **નૉૅધ:**
>
> લોકો elements ને ખુબજ પ્રચલિત એવો કોન્સેપટ "components" સમજી કન્ફુઝ થઇ શકે છે. અમે [આગામી વિભાગ](/docs/components-and-props.html) માં components નો પરિચય આપીશું. Components એ Elements થી "બને છે" અને આગળ વધતા પહેલાં અમે તમને આ વિભાગ વાંચવા માટે પ્રોત્સાહિત કરીએ છીએ.

## DOM માં element રેન્ડર કરવું {#rendering-an-element-into-the-dom}

ચાલો ધારીએ કે તમારી HTML ફાઇલમાં ક્યાંક `<div>` છે.

```html
<div id="root"></div>
```

અમે તેને "root" DOM node કહીએ છીએ કારણ કે તેની અંદરની દરેક વસ્તુ React DOM દ્વારા સંચાલિત કરવામાં આવશે.

React થી બનેલી એપ્લિકેશન્સમાં સામાન્ય રૂપે એક જ `root` DOM node હોય છે. જો તમે હાલની એપ્લિકેશનમાં React ને સંકલિત કરી રહ્યાં હોવ, તો તમે ઈચ્છો એટલા અલગ અલગ `root` DOM nodes હોઈ શકે છે.

<<<<<<< HEAD
<<<<<<< HEAD
React Element ને `root` DOM node માં રેન્ડર કરવા માટે, બંનેને `ReactDOM.render()` માં પસાર કરો:
=======
To render a React element into a root DOM node, pass both to [`ReactDOM.render()`](/docs/react-dom.html#render):
>>>>>>> b3c7f041586b71b31f556403426fcd7cab342535
=======
To render a React element, first pass the DOM element to [`ReactDOM.createRoot()`](/docs/react-dom-client.html#createroot), then pass the React element to `root.render()`:
>>>>>>> 84ad3308338e2bb819f4f24fa8e9dfeeffaa970b

`embed:rendering-elements/render-an-element.js`

**[Try it on CodePen](https://codepen.io/gaearon/pen/ZpvBNJ?editors=1010)**

તે પેજ પર "Hello, world" દર્શાવે છે.

## Rendered Element ને અપડેટ કરવું {#updating-the-rendered-element}

React elements [અપરિવર્તીત](https://en.wikipedia.org/wiki/Immutable_object) છે. એકવાર તમે element બનાવી લો, પછી તમે તેના children કે attributes ને બદલી શકતા નથી. એક elementએ ફિલ્મમાં એક ફ્રેમ જેવું છે: તે એક ચોક્કસ ક્ષણનું UI રજૂ કરે છે.

<<<<<<< HEAD
<<<<<<< HEAD
અત્યાર સુધીના આપણા જ્ઞાન મુજબ, UI ને અપડેટ કરવાની એકમાત્ર રીત એ એક નવું element બનાવવું અને તેને `ReactDOM.render ()` માં પસાર કરવું છે.
=======
With our knowledge so far, the only way to update the UI is to create a new element, and pass it to [`ReactDOM.render()`](/docs/react-dom.html#render).
>>>>>>> b3c7f041586b71b31f556403426fcd7cab342535
=======
With our knowledge so far, the only way to update the UI is to create a new element, and pass it to `root.render()`.
>>>>>>> 84ad3308338e2bb819f4f24fa8e9dfeeffaa970b

આ ટિકિંગ ઘડિયાળનું ઉદાહરણ ધ્યાનમાં લો:

`embed:rendering-elements/update-rendered-element.js`

**[Try it on CodePen](https://codepen.io/gaearon/pen/gwoJZk?editors=1010)**

<<<<<<< HEAD
<<<<<<< HEAD
તે પ્રત્યેક સેકન્ડે [SetInterval()](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) દ્વારા `ReactDOM.render()` ને કૉલ કરે છે.
=======
It calls [`ReactDOM.render()`](/docs/react-dom.html#render) every second from a [`setInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) callback.
>>>>>>> b3c7f041586b71b31f556403426fcd7cab342535
=======
It calls [`root.render()`](/docs/react-dom.html#render) every second from a [`setInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) callback.
>>>>>>> 84ad3308338e2bb819f4f24fa8e9dfeeffaa970b

> **નૉૅધ:**
>
<<<<<<< HEAD
<<<<<<< HEAD
> વ્યવહારમાં, મોટાભાગના React એપ્લિકેશનો ફક્ત એક વાર `ReactDOM.render()` ને કૉલ કરે છે. આગલા વિભાગોમાં આપણે જાણીશું કે આવા કોડને [stateful components](/docs/state-and-lifecycle.html) માં કઈ રીતે સામેલ કરવા.
=======
>In practice, most React apps only call [`ReactDOM.render()`](/docs/react-dom.html#render) once. In the next sections we will learn how such code gets encapsulated into [stateful components](/docs/state-and-lifecycle.html).
>>>>>>> b3c7f041586b71b31f556403426fcd7cab342535
=======
>In practice, most React apps only call `root.render()` once. In the next sections we will learn how such code gets encapsulated into [stateful components](/docs/state-and-lifecycle.html).
>>>>>>> 84ad3308338e2bb819f4f24fa8e9dfeeffaa970b
>
> અમારી તમને ભલામણ છે કે, તમે મુદ્દાઓને કુદાવસો નહિ, કારણકે તેઓ એકબીજા પાર આધારિત છે

## React ફક્ત શું જરૂરી છે એ ને અપડેટ કરે છે {#react-only-updates-whats-necessary}

React DOM એ element અને તેના childrenની સરખામણી તેમની આગળની સ્તિથી સાથે કરે છે, અને DOM ને ઇચ્છિત સ્થિતિમાં લાવવા માટે જરૂરી DOM અપડેટ્સને જ લાગુ કરે છે.

<<<<<<< HEAD
તમે બ્રાઉઝર ટુલ્સ વડે [છેલ્લા ઉદાહરણને ](codepen://rendering-elements/update-rendered-element) inspect કરી ચકાશી શકો છો.
=======
You can verify by inspecting the [last example](https://codepen.io/gaearon/pen/gwoJZk?editors=1010) with the browser tools:
>>>>>>> 84ad3308338e2bb819f4f24fa8e9dfeeffaa970b

![DOM inspector showing granular updates](../images/docs/granular-dom-updates.gif)

<<<<<<< HEAD
ભલે આપણે દરેક ટિક પર સંપૂર્ણ UI tree નું વર્ણન કરતુ element બનાવીએ, પરંતુ ફક્ત text node કે જેનો content બદલાઈ ગયો છે તે જ React DOM દ્વારા અપડેટ થાય છે.

અમારા અનુભવમાં, સમયાંતરે UIને કેવી રીતે બદલવું તેના કરતા UI એ કોઈપણ એક ક્ષણે કેવું દેખાવું જોઈએ તે વિશે વિચારીને બગ્સ(bugs) ની સંપૂર્ણ શ્રેણીને દૂર કરી શકાય છે.
=======
Even though we create an element describing the whole UI tree on every tick, only the text node whose contents have changed gets updated by React DOM.

In our experience, thinking about how the UI should look at any given moment, rather than how to change it over time, eliminates a whole class of bugs.
>>>>>>> b3c7f041586b71b31f556403426fcd7cab342535
