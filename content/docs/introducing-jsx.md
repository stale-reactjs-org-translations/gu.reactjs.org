---
id: introducing-jsx
title: JSX નો પરિચય
permalink: docs/introducing-jsx.html
prev: hello-world.html
next: rendering-elements.html
---

આ વેરિયેબલ ડેકલેરેશન ધ્યાનમાં લો:

```js
const element = <h1>Hello World</h1>;
```

આ ફની ટેગ સિન્ટેક્સ ન તો string કે HTML છે.

તેને JSX કહેવામાં આવે છે, અને તે વિસ્તૃત JavaScript સિન્ટેક્સ છે. UI એ કેવું હોવું જોઈએ તેનું વર્ણન કરવા માટે, અમે તેને React સાથે ઉપયોગ કરવાની ભલામણ કરીએ છીએ. JSX તમને ટેમ્પલેટ ભાષાની યાદ અપાવી શકે છે, પરંતુ તે JavaScript ની સંપૂર્ણ ક્ષમતાઓ સાથે આવે છે.

JSX React "એલિમેન્ટ્સ" બનાવે છે. આપણે તેમને [આગલા વિભાગમાં](/docs/rendering-elements.html) DOMમાં રેન્ડર કરવાનું શીખીશું. આપને પ્રારંભ કરવા માટે JSX ની પ્રાથમિક જરૂરી બાબતો નીચે મુજબ છે 

### શા માટે JSX? {#why-jsx}

React એ હકીકતને સ્વીકારે છે કે લોજિકને રજૂ કરવું મૂળ રીતે અન્ય UI લોજિક સાથે જોડાયેલું છે. જેમ કે, events કેવી રીતે હૅન્ડલ થાય છે, state સમય સાથે કેવી રીતે બદલાય છે અને ડિસ્પ્લે માટે ડેટા કેવી રીતે તૈયાર કરવામાં આવે છે.

અલગ ફાઇલોમાં માર્કઅપ અને લૉજિકને મૂકીને આર્ટીફિશ્યલ રીતે *ટેક્નોલોજીઓ* ને અલગ કરવાને બદલે, React, ઢીલી રીતે જોડાયેલા એવા "કોમ્પોનેન્ટ્સ" કે જેમાં બંને શામેલ છે એના દ્વારા [*કન્સર્નસ* અલગ](https://en.wikipedia.org/wiki/Separation_of_concerns) પાડે છે. અમે [આગળના ભાગમાં](/docs/components-and-props.html) કોમ્પોનેન્ટ્સ પર પાછા આવીશું, પરંતુ જો તમે JSમાં માર્કઅપ લખવા હજી સુધી કમ્ફર્ટેબલ નથી, તો [આ વાત](https://www.youtube.com/watch?v=x7cQ3mrcKaY) તમને સમજાવી શકે છે.

JSXનો ઉપયોગ કરવો એ Reactમાં [જરૂરી નથી](/docs/react-without-jsx.html), પરંતુ મોટાભાગના લોકોને JavaScript કોડની અંદર UI સાથે કામ કરતી વખતે વિઝ્યુઅલ સહાય તરીકે સહાયરૂપ લાગે છે. તે Reactને વધુ ઉપયોગી એરર અને વોર્નિંગ સૂચનો બતાવવામાં પણ મદદ કરે છે.

તે સાથે, ચાલો શરૂ કરીએ!

### JSXમાં એક્સપ્રેશન એમ્બેડ કરવું {#embedding-expressions-in-jsx}

નીચેનાં ઉદાહરણમાં, અમે `name` વેરિયેબલને ડિક્લેર કરીએ છીએ અને પછી તેને JSXની અંદર છગડીયા કૌંસમાં લખીને તેનો ઉપયોગ કરીએ છીએ:

```js{1,2}
const name = 'ગુણવંત શાહ';
const element = <h1>Hello World, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

તમે JSXમાં છગડીયા કૌંસની અંદર કોઈપણ માન્ય [JavaScript એક્સપ્રેશન](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) લખી શકો છો. ઉદાહરણ તરીકે, `2 + 2`, `user.firstName`, અથવા `formatName(user)` એ બધી માન્ય JavaScript એક્સપ્રેશન છે.

નીચેનાં ઉદાહરણમાં, આપણે JavaScript `formatName(user)` ફંકશનનું પરિણામ `<h1>` એલિમેન્ટમાં એમ્બેડ કરીશું.

```js{12}
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'નયન',
  lastName: 'શાહ'
};

const element = (
  <h1>
    Hello World, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

[](codepen://introducing-jsx)

વાંચી શકાય તે માટે અમે બહુવિધ લાઇન્સમાં JSXને વિભાજિત કર્યું છે. તે કરવું આવશ્યક નથી, પરંતુ જો કરો, તો તેને [ઓટોમેટિક સેમિકોલોન ઇન્સેરશન](https://stackoverflow.com/q/2846283) ની ભૂલોને ટાળવા માટે, કૌંસમાં`()` આવરવાની અમે ભલામણ કરીએ છીએ.

### JSX એક એક્સપ્રેશન પણ છે {#jsx-is-an-expression-too}

કંપાયલેશન પછી, JSX એક્સપ્રેશન નિયમિત JavaScript ફંક્શન કોલ્સ બની જાય છે અને JavaScript ઑબ્જેક્ટ્સનું મૂલ્યાંકન કરે છે.

આનો અર્થ એ છે કે તમે `if` સ્ટેટમેન્ટ્સ અને `for` loops ની અંદર JSXનો ઉપયોગ કરી શકો છો, તેને વેરીએબલોને અસાઈન કરી શકો છો, તેને આરગ્યુમેન્ટ્સ તરીકે સ્વીકારી શકો છો, અને તેને ફંકશનમાંથી રીટર્ન કરી શકો છો:

```js{3,5}
function getGreeting(user) {
  if (user) {
    return <h1>Hello World, {formatName(user)}!</h1>;
  }
  return <h1>Hello World, અપરિચિત.</h1>;
}
```

### JSXમાં અટ્ટ્રીબ્યુટસ સ્પેસિફાય કરવા {#specifying-attributes-with-jsx}

તમે string લિટરલ્સને અટ્ટ્રીબ્યુટસ તરીકે સ્પેસિફાય કરવા માટે અવતરણ ચિન્હોનો ઉપયોગ કરી શકો છો:

```js
const element = <div tabIndex="0"></div>;
```

તમે અટ્ટ્રીબ્યુટમાં JavaScript એક્સપ્રેશનને એમ્બેડ કરવા માટે છગડીયા કૌંસનો પણ ઉપયોગ કરી શકો છો:

```js
const element = <img src={user.avatarUrl}></img>;
```

એટ્રિબ્યુટમાં JavaScript એક્સપ્રેશનને એમ્બેડ કરતી વખતે છગડીયા કૌંસની આસપાસ અવતરણ ચિન્હો મૂકવું નહીં. તમારે અવતરણ ચિન્હો (string વૅલ્યુ માટે) અથવા છગડીયા કૌંસ (એક્સપ્રેશન માટે) નો ઉપયોગ કરવો જોઈએ, પરંતુ બંને સમાન અટ્ટ્રીબ્યુટમાં નહીં.

>**ચેતવણી:**
>
>JSX, HTML કરતા JavaScriptની નજીક છે, જેથી React DOM, HTML એટ્રિબ્યુટ નામોની જગ્યાએ `camelCase` પ્રોપર્ટી નૅમિંગ પ્રણાલીનો ઉપયોગ કરે છે.
>
>ઉદાહરણ તરીકે, `class` JSXમાં બને છે [`className`](https://developer.mozilla.org/en-US/docs/Web/API/Element/className), અને `tabindex` બને છે [`tabIndex`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/tabIndex).

### JSXમાં ચિલડ્રન સ્પેસિફાય કરવા {#specifying-children-with-jsx}

જો ટૅગ ખાલી હોય, તો તમે તેને તરત જ `/>` દ્વારા XML ની જેમ બંધ કરી શકો છો:

```js
const element = <img src={user.avatarUrl} />;
```

JSX ટૅગ્સમાં ચિલડ્રન શામેલ હોઈ શકે છે:

```js
const element = (
  <div>
    <h1>Hello World</h1>
    <h2>તમને અહીં મળીને આનંદ થયો.</h2>
  </div>
);
```

### JSX ઇન્જેક્શન એટેક્સ અટકાવે છે {#jsx-prevents-injection-attacks}

JSX માં યુઝર ઇનપુટ એમ્બેડ કરવું સલામત છે:

```js
const title = response.potentiallyMaliciousInput;
// આ સુરક્ષિત છે:
const element = <h1>{title}</h1>;
```

મૂળભૂત રીતે, React DOM રેન્ડરિંગ કરતા પહેલા JSXમાં એમ્બેડ કરેલી કોઈપણ વૅલ્યુઝ [છોડી દે](https://stackoverflow.com/questions/7381974/which-characters-need-to-be-escaped-on-html) છે. આથી તે સુનિશ્ચિત કરે છે કે તમે એવી કોઈપણ વસ્તુને ઇન્જેક્ટ કરી શકતા નથી જે તમારી એપ્લિકેશનમાં સ્પષ્ટ રીતે લખાઈ નથી. રેન્ડર કરવામાં આવે તે પહેલાં બધું જ stringમાં રૂપાંતરિત થાય છે. આ [XSS (ક્રોસ-સાઇટ-સ્ક્રિપ્ટીંગ)](https://en.wikipedia.org/wiki/Cross-site_scripting) એટેક્સને અટકાવવામાં મદદ કરે છે.

### JSX ઓબ્જેક્ટો રજૂ કરે છે {#jsx-represents-objects}

Babel JSX ને `React.createElement()` કૉલ્સ માં કંપાયલ કરે છે.

આ બે ઉદાહરણો સરખા છે:

```js
const element = (
  <h1 className="greeting">
    Hello World
  </h1>
);
```

```js
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello World'
);
```

બગ-ફ્રી(ક્ષતિ રહિત) કોડ લખવા માટે `React.createElement()` કેટલાક તપાસ કરે છે પરંતુ આવશ્યક રીતે તે આના જેવો ઑબ્જેક્ટ બનાવે છે:

```js
// નોંધ: આ માળખું સરળ છે
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello World'
  }
};
```

આ ઑબ્જેક્ટ્સને "React elements" કહેવામાં આવે છે. તમે તેમનો આ રીતે વિચાર કરી શકો છો કે સ્ક્રીન પર તમે જે જોવા માંગો છો તે તેનું વર્ણન છે. React આ ઓબ્જેક્ટો વાંચે છે અને DOM બનાવવા અને તેને અપ ટુ ડેટ રાખવા માટે તેનો ઉપયોગ કરે છે.

આપણે [આગલા વિભાગમાં](/docs/rendering-elements.html) DOM પર React elements રેન્ડર કરતા શીખીશું.

>**ટિપ:**
>
<<<<<<< HEAD
>અમે તમારા પસંદગીના એડિટર માટે ["babel" language definition](https://babeljs.io/docs/editors) નો ઉપયોગ કરવાની ભલામણ કરીએ છીએ જેથી ES6 અને JSX કોડ બંને યોગ્ય રીતે હાઈલાઈટ થઇ શકે.
=======
>We recommend using the ["Babel" language definition](https://babeljs.io/docs/en/next/editors) for your editor of choice so that both ES6 and JSX code is properly highlighted.
>>>>>>> ec2d0adcb44d6394f4e6282d8bf52f0e25dbfec3
