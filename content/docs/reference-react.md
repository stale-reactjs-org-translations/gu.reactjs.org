---
id: react-api
title: React Top-Level API
layout: docs
category: Reference
permalink: docs/react-api.html
redirect_from:
  - "docs/reference.html"
  - "docs/clone-with-props.html"
  - "docs/top-level-api.html"
  - "docs/top-level-api-ja-JP.html"
  - "docs/top-level-api-ko-KR.html"
  - "docs/top-level-api-zh-CN.html"
---

`React` એ React પુસ્તકાલયનો પ્રવેશ પોઇન્ટ છે. જો તમે React `<script>` ટેગ પરથી લોડ કરો છો, તો આ top-level APIs `React` ગ્લોબલ પર ઉપલબ્ધ છે. જો તમે npm સાથે ES6 ઉપયોગ કરો છો, તો તમે `import React from 'react'` લખી શકો છો. જો તમે npm સાથે ES5 ઉપયોગ કરો છો, તો તમે `var React = require('react')` લખી શકો છો.

## ઓવરવ્યૂ {#overview}

### Components {#components}

React components તમને UI ને સ્વતંત્ર, રીયુઝએબલ ટુકડાઓમાં વહેંચવા દે છે, અને દરેક ટુકડા વિશે એકાંતમાં વિચારવા દે છે. React components ને `React.Component` અથવા `React.PureComponent` સબક્લાસીંગ મા ડીફાઇન કરી શકાય છે.

 - [`React.Component`](#reactcomponent)
 - [`React.PureComponent`](#reactpurecomponent)

જો તમે ES6 ક્લાસીસ નો ઉપયોગ કરતા નથી, તો તમે તેના બદલે `create-react-class` મોડ્યુલનો ઉપયોગ કરી શકો છો. વધુ માહિતી માટે [React ES6 વિના વાપરવું](/docs/react-without-es6.html) એ જુઓ.

React components ને ફંકશન્સ તરીકે પણ ડીફાઇન કરી શકાય છે જે આવરિત કરેલું છે:

- [`React.મેમો`](#reactmemo)

### React Elements બનાવવા {#creating-react-elements}

અમે [JSX વાપરવા](/docs/introducing-jsx.html) ભલામણ કરીએ છીએ તમારું UI કેવું હોવું જોઈએ તે વર્ણવવા. દરેક JSX element [`React.createElement()`](#createelement) કોલ કરવા માટે ફક્ત સિન્ટેક્ટિક સુગર છે. જો તમે JSX નો ઉપયોગ કરી રહ્યાં હોવ તો સામાન્ય રીતે તમારે નીચેની પદ્ધતિઓ ઈન્વોક કરવો નહીં.

- [`createElement()`](#createelement)
- [`createFactory()`](#createfactory)

વધુ માહિતી માટે [React JSX વિના વાપરવું](/docs/react-without-jsx.html) એ જુઓ.

### Elements પરિવર્તન કરવા {#transforming-elements}

`React` થોડી APIs આપે છે elements બદલવા:

- [`cloneElement()`](#cloneelement)
- [`isValidElement()`](#isvalidelement)
- [`React.ચિલ્ડ્રન`](#reactchildren)

### ફ્રેગમેન્ટ્સ {#fragments}

`React` રેપર વિના પણ ઘણા elements રેન્ડર કરવા એક component આપે છે.

- [`React.ફ્રેગમેન્ટ્`](#reactfragment)

### Refs {#refs}

- [`React.createRef`](#reactcreateref)
- [`React.forwardRef`](#reactforwardref)

### સસ્પેન્સ {#suspense}

સસ્પેન્સ કંઇક રેન્ડર કરતા પહેલા components ને "રાહ" જોવા દે છે. આજે, સસ્પેન્સ ફક્ત એક જ યુઝ કેસ ને સપોર્ટ કરે છે: [`React.લેઝી` થી ડાઈનામેટીકલી components લોડ કરવા](/docs/code-splitting.html#reactlazy). ભવિષ્યમાં, તે ડેટા ફૅચિંગ જેવા અન્ય યુઝ કેસીસ ને સપોર્ટ કરશે.

- [`React.લેઝી`](#reactlazy)
- [`React.સસ્પેન્સ`](#reactsuspense)

### હુક્સ {#hooks}

*હુક્સ* React 16.8 માં એક નવો ઉમેરો છે. તેઓ તમને ક્લાસ લખ્યા વિના સ્ટેટ અને અન્ય React ફીચર્સ ઉપયોગ કરવા દે છે. હુક્સ ની એક [સમર્પિત માર્ગદર્શિકા વિભાગ](/docs/hooks-intro.html) અને એક અલગ API રેફરન્સ છે:

- [પાયાના હુક્સ](/docs/hooks-reference.html#basic-hooks)
  - [`useState`](/docs/hooks-reference.html#usestate)
  - [`useEffect`](/docs/hooks-reference.html#useeffect)
  - [`useContext`](/docs/hooks-reference.html#usecontext)
- [વધારાના હુક્સ](/docs/hooks-reference.html#additional-hooks)
  - [`useReducer`](/docs/hooks-reference.html#usereducer)
  - [`useCallback`](/docs/hooks-reference.html#usecallback)
  - [`useMemo`](/docs/hooks-reference.html#usememo)
  - [`useRef`](/docs/hooks-reference.html#useref)
  - [`useImperativeHandle`](/docs/hooks-reference.html#useimperativehandle)
  - [`useLayoutEffect`](/docs/hooks-reference.html#uselayouteffect)
  - [`useDebugValue`](/docs/hooks-reference.html#usedebugvalue)

* * *

## રેફરન્સ {#reference}

### `React.Component` {#reactcomponent}

`React.Component` એ React components નો બેઝ ક્લાસ છે જ્યારે તેને [ES6 classes](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) સાથે ડીફાઇન કરેલું હોય:

```javascript
class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

બેઝ `React.Component` ક્લાસથી સંબંધિત મેથડ્સ અને પ્રોપર્ટીઝની સૂચિ માટે [React.Component API રેફરન્સ](/docs/react-component.html) જુઓ.

* * *

### `React.PureComponent` {#reactpurecomponent}

`React.PureComponent` એ [`React.Component`](#reactcomponent) જેવું છે. તેમની વચ્ચેનો તફાવત એ છે કે [`React.Component`](#reactcomponent) [`shouldComponentUpdate()`](/docs/react-component.html#shouldcomponentupdate) ઈમ્પ્લીમેન્ટ કરતુ નથી, પરંતુ `React.PureComponent` તેને શૅલૉ પ્રોપ અને સ્ટેટ સરખામણીથી ઈમ્પ્લીમેન્ટ કરે છે.

જો તમારા React component નુ `render()` ફંક્શન સમાન પ્રોપ્સ અને સ્ટેટ જોતા સમાન પરિણામ આપે છે, તો તમે કેટલાક કેસોમાં પ્રભાવ વધારવા માટે `React.PureComponent` નો ઉપયોગ કરી શકો છો.

> નોંધ
>
> `React.PureComponent` ની `shouldComponentUpdate()` ફક્ત ઓબ્જેક્ટની શેલોલી તુલના કરે છે. જો આમાં જટિલ ડેટા સ્ટ્રક્ચર્સ શામેલ છે, તો તે ઊંડા તફાવતો માટે ફોલ્સ-નેગેટીવ્સ પેદા કરી શકે છે. જો તમારી પાસે સરળ પ્રોપ્સ અને સ્ટેટની અપેક્ષા હોય ત્યારે ફક્ત `PureComponent` એક્સટેન્ડ કરવું, અથવા જ્યારે તમે જાણો છો કે ઊંડા જટિલ ડેટા સ્ટ્રક્ચર્સ બદલાયા છે ત્યારે [`forceUpdate()`](/docs/react-component.html#forceupdate) નો ઉપયોગ કરો. અથવા, પુનરાવર્તિત ડેટાની ઝડપી તુલનાને સુવિધા આપવા માટે [અપરિવર્તીત ઓબ્જેક્ટસ](https://facebook.github.io/immutable-js/) નો ઉપયોગ કરો.
>
> તદુપરાંત, `React.PureComponent` ની `shouldComponentUpdate()` પુરી component સબટ્રી માટે પ્રોપ અપડેટ્સ છોડે છે. ખાતરી કરો કે બધા ચિલ્ડ્રન components પણ "પ્યોર" છે.

* * *

### `React.મેમો` {#reactmemo}

```javascript
const MyComponent = React.memo(function MyComponent(props) {
  /* render using props */
});
```

`React.મેમો` એ એક [ઉચ્ચ ક્રમ component](/docs/higher-order-components.html) છે. તે [`React.PureComponent`](#reactpurecomponent) જેવું છે પણ કલાસીસના બદલે ફંકશન માટે છે.

જો તમારું ફંકશન component સમાન પ્રોપ્સ અને સ્ટેટ જોતા સમાન પરિણામ રેન્ડર કરે છે, તો તમે કેટલાક કેસોમાં પ્રભાવ વધારવા માટે `React.મેમો` નો ઉપયોગ પરિણામ સંસ્મરણ દ્વારા કરી શકો છો. આનો અર્થ એ છે કે React component ને રેન્ડર કરવાનું છોડશે, અને છેલ્લા રેન્ડર કરેલા પરિણામનો ફરીથી ઉપયોગ કરશે.

`React.મેમો` ફક્ત પ્રોપ ચેન્જીસ ચેક કરે છે. જો તમારા `React.મેમો` માં આવરિત ફંકશન component પાસે એક [`useState`](/docs/hooks-state.html) અથવા [`useContext`](/docs/hooks-reference.html#usecontext) હુક એના ઈમ્પ્લીમેન્ટેશનમાં છે, તો તે રીરેન્ડર થશે જયારે સ્ટેટ અથવા કોન્ટેક્સટ બદલાશે.

તે મૂળભૂત રીતે પ્રોપ્સ ઓબ્જેક્ટમાં ફક્ત જટિલ ઓબ્જેક્ટ્સની શેલોલી તુલના કરે છે. જો તમે તુલના પર નિયંત્રણ રાખવા માંગો છો, તો તમે બીજા આર્ગ્યુમેન્ટમાં કસ્ટમ તુલનાત્મક ફંકશન આપી પણ શકો છો.

```javascript
function MyComponent(props) {
  /* render using props */
}
function areEqual(prevProps, nextProps) {
  /*
  return true if passing nextProps to render would return
  the same result as passing prevProps to render,
  otherwise return false
  */
}
export default React.memo(MyComponent, areEqual);
```

આ મેથડ ફક્ત એક **[પરફોર્મન્સ ઓપ્ટિમાઇઝેશન](/docs/optimizing-performance.html)** તરીકે અસ્તિત્વમાં છે. રેન્ડરને "અટકાવવા" માટે તેના પર આધાર રાખશો નહીં, કારણ કે આ બગ્સ તરફ દોરી શકે છે.

> નોંધ
>
> કલાસ components પર [`shouldComponentUpdate()`](/docs/react-component.html#shouldcomponentupdate) મેથડથી વિપરીત, `areEqual` ફંકશન `true` રિટર્ન કરશે જો પ્રોપ્સ સમાન હોય અને `false` જો પ્રોપ્સ સમાન ના હોય. આ `shouldComponentUpdate`થી વિપરિત છે.

* * *

### `createElement()` {#createelement}

```javascript
React.createElement(
  type,
  [props],
  [...children]
)
```

આપેલ પ્રકારનું એક નવું [React element](/docs/rendering-elements.html) બનાવો અને રિટર્ન કરો. ટાઈપ આર્ગ્યુમેન્ટ કાં તો એક ટેગ નામની સ્ટ્રીંગ (જેમ કે `'div'` અથવા `'span'`), એક [React component](/docs/components-and-props.html) ટાઈપ (એક ક્લાસ અથવા એક ફંકશન), અથવા એક [React ફ્રેગમેન્ટ્](#reactfragment) ટાઈપ હોય શકે.

[JSX](/docs/introducing-jsx.html) સાથે લખેલા કોડને `React.createElement()` ઉપયોગ કરવા માટે બદલવામાં આવશે. જો તમે JSX ઉપયોગ કરો છો, તો તમે સીધું ખાસ કરીને `React.createElement()` ઈન્વોક ના કરો. વધુ માહિતી માટે [React JSX વિના વાપરવું](/docs/react-without-jsx.html) એ જુઓ.

* * *

### `cloneElement()` {#cloneelement}

```
React.cloneElement(
  element,
  [props],
  [...children]
)
```

 સ્ટાર્ટિંગ પોઇન્ટ તરીકે `element` થી એક નવું React element ક્લોન અને રિટર્ન કરો. પરિણામી element ને મૂળ element ની પ્રોપ્સ સાથે નવા પ્રોપ્સ જોડે શેલોલી મર્જ થશે. નવા ચિલ્ડ્રન હાલના ચિલ્ડ્રન બદલશે. `key` અને `ref` મૂળ element ના સાચવેલા રહેશે.

`React.cloneElement()` લગભગ સમાન છે:

```js
<element.type {...element.props} {...props}>{children}</element.type>
```

પણ, તે `ref` ને પણ સાચવી રાખે છે. આનો અર્થ એ છે કે જો તમને કોઈ ચાઈલ્ડ તેના પર `ref` મળે છે, તો તમે તેને આકસ્મિક રીતે તમારા પૂર્વજ પાસેથી ચોરી નહીં કરો. તમને તમારા નવા element માં સમાન `ref` જોડાયેલ મળશે.

આ API નકારેલા `React.addons.cloneWithProps()` ની બદલીમાં રજુઆત થયેલું હતું.

* * *

### `createFactory()` {#createfactory}

```javascript
React.createFactory(type)
```

આપેલ ટાઈપ React elements ઉત્પન્ન કરતું ફંક્શન રિટર્ન કરો. [`React.createElement()`](#createelement) ની જેમ, ટાઈપ આર્ગ્યુમેન્ટ કાં તો એક ટેગ નામની સ્ટ્રીંગ (જેમ કે `'div'` અથવા `'span'`), એક [React component](/docs/components-and-props.html) ટાઈપ (એક ક્લાસ અથવા એક ફંકશન), અથવા એક [React ફ્રેગમેન્ટ્](#reactfragment) ટાઈપ હોય શકે.

આ હેલ્પર લેગસી માનવામાં આવે છે, અને અમે તમને કાં તો JSX અથવા `React.createElement()` સીધું વાપરવા પ્રોત્સાહિત કરીએ છીએ.

જો તમે JSX ઉપયોગ કરો છો, તો તમે સીધું ખાસ કરીને `React.createElement()` ઈન્વોક ના કરો. વધુ માહિતી માટે [React JSX વિના વાપરવું](/docs/react-without-jsx.html) એ જુઓ.

* * *

### `isValidElement()` {#isvalidelement}

```javascript
React.isValidElement(object)
```

ઓબ્જેક્ટ એક React element છે એની ચકાસણી કરે છે. `true` અથવા `false` રિટર્ન કરે છે.

* * *

### `React.ચિલ્ડ્રન` {#reactchildren}

`React.ચિલ્ડ્રન` `this.props.ચિલ્ડ્રન` સાથેના અપારદર્શક ડેટા સ્ટ્રક્ચર વ્યવહાર માટે ઉપયોગિતાઓ આપે છે.

#### `React.ચિલ્ડ્રન.મેપ` {#reactchildrenmap}

```javascript
React.Children.map(children, function[(thisArg)])
```

`ચિલ્ડ્રન` ની અંદર સમાયેલ દરેક તાત્કાલિક ચાઈલ્ડ પર `this`ને `thisArg` જોડે સેટ કરીને એક ફંકશન ઈન્વોક કરે છે. જો `ચિલ્ડ્રન` એક એરે છે તો તે ટ્રાવર્સ કરે છે અને એરેના દરેક ચાઈલ્ડ માટે ફંક્શન કોલ કરે છે. જો ચિલ્ડ્રન `નલ` અથવા `અંડિફાઈન્ડ` છે, આ મેથડ એરેના બદલે `નલ` અથવા `અંડિફાઈન્ડ` રિટર્ન કરે છે.

> નોંધ
>
> જો `ચિલ્ડ્રન` એક `ફ્રેગમેન્ટ્` છે તો તે એકલા ચાઈલ્ડની જેમ વર્તાશે અને ટ્રાવર્સ નહિ થાય.

#### `React.ચિલ્ડ્રન.forEach` {#reactchildrenforeach}

```javascript
React.Children.forEach(children, function[(thisArg)])
```

[`React.ચિલ્ડ્રન.મેપ()`](#reactchildrenmap) જેવું પણ એરે રિટર્ન ના કરે.

#### `React.ચિલ્ડ્રન.count` {#reactchildrencount}

```javascript
React.Children.count(children)
```

`ચિલ્ડ્રન`માં components ની કુલ સંખ્યા રિટર્ન કરે છે, `મેપ`ને પસાર કરેલા callbackની સંખ્યા બરાબર અથવા `forEach` ઈન્વોક થશે.

#### `React.ચિલ્ડ્રન.only` {#reactchildrenonly}

```javascript
React.Children.only(children)
```

`ચિલ્ડ્રન`ને ફક્ત એક ચાઈલ્ડ (એક React element) છે તેની ચકાસણી કરે છે અને રિટર્ન કરે છે. અન્યથા આ મેથડ એરર થ્રો કરે છે.

> નોંધ:
>
>`React.ચિલ્ડ્રન.only()` એ [`React.ચિલ્ડ્રન.મેપ()`](#reactchildrenmap)ની રિટર્ન વૅલ્યુ સ્વીકારતું નથી કારણ કે તે એક React element ના બદલે એક એરે છે.

#### `React.ચિલ્ડ્રન.toArray` {#reactchildrentoarray}

```javascript
React.Children.toArray(children)
```

Returns the `ચિલ્ડ્રન` opaque data structure as a flat array with keys assigned to each child. Useful if you want to manipulate collections of ચિલ્ડ્રન in your render methods, especially if you want to reorder or slice `this.props.ચિલ્ડ્રન` before passing it down.

> Note:
>
> `React.ચિલ્ડ્રન.toArray()` changes keys to preserve the semantics of nested arrays when flattening lists of ચિલ્ડ્રન. That is, `toArray` prefixes each key in the returned array so that each element's key is scoped to the input array containing it.

* * *

### `React.ફ્રેગમેન્ટ્` {#reactfragment}

The `React.ફ્રેગમેન્ટ્` component lets you return multiple elements in a `render()` method without creating an additional DOM element:

```javascript
render() {
  return (
    <React.Fragment>
      Some text.
      <h2>A heading</h2>
    </React.Fragment>
  );
}
```

You can also use it with the shorthand `<></>` syntax. For more information, see [React v16.2.0: Improved Support for ફ્રેગમેન્ટ્સ](/blog/2017/11/28/react-v16.2.0-fragment-support.html).


### `React.createRef` {#reactcreateref}

`React.createRef` creates a [ref](/docs/refs-and-the-dom.html) that can be attached to React elements via the ref attribute.
`embed:16-3-release-blog-post/create-ref-example.js`

### `React.forwardRef` {#reactforwardref}

`React.forwardRef` creates a React component that forwards the [ref](/docs/refs-and-the-dom.html) attribute it receives to another component below in the tree. This technique is not very common but is particularly useful in two scenarios:

* [Forwarding refs to DOM components](/docs/forwarding-refs.html#forwarding-refs-to-dom-components)
* [Forwarding refs in higher-order-components](/docs/forwarding-refs.html#forwarding-refs-in-higher-order-components)

`React.forwardRef` accepts a rendering function as an argument. React will call this function with `props` and `ref` as two arguments. This function should return a React node.

`embed:reference-react-forward-ref.js`

In the above example, React passes a `ref` given to `<FancyButton ref={ref}>` element as a second argument to the rendering function inside the `React.forwardRef` call. This rendering function passes the `ref` to the `<button ref={ref}>` element.

As a result, after React attaches the ref, `ref.current` will point directly to the `<button>` DOM element instance.

For more information, see [forwarding refs](/docs/forwarding-refs.html).

### `React.lazy` {#reactlazy}

`React.lazy()` lets you define a component that is loaded dynamically. This helps reduce the bundle size to delay loading components that aren't used during the initial render.

You can learn how to use it from our [code splitting documentation](/docs/code-splitting.html#reactlazy). You might also want to check out [this article](https://medium.com/@pomber/lazy-loading-and-preloading-components-in-react-16-6-804de091c82d) explaining how to use it in more detail.

```js
// This component is loaded dynamically
const SomeComponent = React.lazy(() => import('./SomeComponent'));
```

Note that rendering `lazy` components requires that there's a `<React.Suspense>` component higher in the rendering tree. This is how you specify a loading indicator.

> **Note**
>
> Using `React.lazy`with dynamic import requires Promises to be available in the JS environment. This requires a polyfill on IE11 and below.

### `React.Suspense` {#reactsuspense}

`React.Suspense` lets you specify the loading indicator in case some components in the tree below it are not yet ready to render. Today, lazy loading components is the **only** use case supported by `<React.Suspense>`:

```js
// This component is loaded dynamically
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    // Displays <Spinner> until OtherComponent loads
    <React.Suspense fallback={<Spinner />}>
      <div>
        <OtherComponent />
      </div>
    </React.Suspense>
  );
}
```

It is documented in our [code splitting guide](/docs/code-splitting.html#reactlazy). Note that `lazy` components can be deep inside the `Suspense` tree -- it doesn't have to wrap every one of them. The best practice is to place `<Suspense>` where you want to see a loading indicator, but to use `lazy()` wherever you want to do code splitting.

While this is not supported today, in the future we plan to let `Suspense` handle more scenarios such as data fetching. You can read about this in [our roadmap](/blog/2018/11/27/react-16-roadmap.html).

>Note:
>
>`React.lazy()` and `<React.Suspense>` are not yet supported by `ReactDOMServer`. This is a known limitation that will be resolved in the future.
