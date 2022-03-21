---
id: lists-and-keys
title: Lists and Keys
permalink: docs/lists-and-keys.html
prev: conditional-rendering.html
next: forms.html
---

સૌ પ્રથમ, ચાલો JavaScript માં યાદીઓને કેવી રીતે રૂપાંતરિત કરી તેની સમીક્ષા કરીએ.

નીચે કોડ આપેલા છે, અમે નકશાઓની શ્રેણી લેવા અને તેમના વૅલ્યુઝને બમણી કરવા માટે ['નકશા () '] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) ફંકશનનો ઉપયોગ કરીએ છીએ. અમે 'નકશા()' દ્વારા 'બમણા' વેરિયેબલ પર પાછા આપેલા નવા એરેને સોંપી અને તેને લૉગ ઇન કરીએ છીએ:

```javascript{2}
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
```

આ કોડ કન્સોલ પર `[2, 4, 6, 8, 10]` લોગ કરે છે.

રિએક્ટ માં, Elements સૂચિમાં [elements](/docs/rendering-elements.html) પરિવર્તન એરે લગભગ સમાન છે.

### બહુવિધ Components ને રેંડરિંગ {#rendering-multiple-components}

તમે elements ના સંગ્રહનું નિર્માણ કરી શકો છો અને તેમને કર્લી કૌંસ `{}` દ્વારા [JSX માં શામેલ](/docs/introducing-jsx.html#embedding-expressions-in-jsx) કરી શકો છો.

નીચે, અમે JavaScript ['નકશા () '] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) ફંકશનનો ઉપયોગ કરીને 'સંખ્યાઓ' એરેથી લૂપ કરીએ છીએ. અમે દરેક વસ્તુ માટે `<li>` element પરત કરીએ છીએ. છેવટે, આપણે સૂચિના પરિણામી એરેને યાદીમાં 'સૂચિબદ્ધ' કરીએ છીએ:

```javascript{2-4}
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
```

અમે સમગ્ર 'સૂચિબદ્ધ' એરેને `<ul>` element અંતર્ગત શામેલ કરીએ છીએ અને તેને [DOM માં render કરીએ છીએ ](/docs/rendering-elements.html#rendering-an-element-into-the-dom):

```javascript{2}
ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```

[**કોડપેન પર પ્રયત્ન કરો**](https://codepen.io/gaearon/pen/GjPyQr?editors=0011)

આ કોડ 1 અને 5 ની વચ્ચેની સંખ્યાઓની બુલેટ સૂચિ પ્રદર્શિત કરે છે.

### મૂળભૂત સૂચિ Component {#basic-list-component}

સામાન્ય રીતે તમે [component](/docs/components-and-props.html) ની અંદર સૂચિ render કરશો.

અમે પાછલા ઉદાહરણને એવા component માં રિફૅક્ટર કરી શકીએ જે 'સંખ્યાઓ' ની અરે સ્વીકારે છે અને elements ની સૂચિ આઉટપુટ કરે છે.

```javascript{3-5,7,13}
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

જ્યારે તમે આ કોડ ચલાવો છો, ત્યારે તમને ચેતવણી આપવામાં આવશે કે સૂચિ વસ્તુઓ માટે કી પ્રદાન કરવી જોઈએ. "કી" વિશિષ્ટ શબ્દ લક્ષણ છે જે તમારે elements ની સૂચિ બનાવતી વખતે શામેલ કરવાની જરૂર છે. અમે ચર્ચા કરીશું કે આગલા વિભાગમાં શા માટે મહત્વપૂર્ણ છે.

ચાલો `numbers.map()` માં અમારી સૂચિ વસ્તુઓની `કી` આપીએ અને ગુમ થયેલ મુખ્ય સમસ્યાને ઠીક કરીએ.

```javascript{4}
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

[**કોડપેન પર પ્રયત્ન કરો**](https://codepen.io/gaearon/pen/jrXYRR?editors=0011)

## કીઝ {#keys}

કીઝ જે વસ્તુઓ બદલાયેલ છે, ઉમેરવામાં આવે છે અથવા દૂર કરવામાં આવે છે તે ઓળખવામાં સહાય કરે છે. elements ને એક સ્થિર ઓળખ આપવા માટે એરેની અંદરના elements ને કીઝ આપવી જોઈએ:

```js{3}
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

કી પસંદ કરવાનો શ્રેષ્ઠ માર્ગ તે શબ્દનો ઉપયોગ કરવો છે જે વિશિષ્ટ રીતે તેના ભાઈબહેનો વચ્ચે સૂચિ આઇટમને ઓળખે છે. મોટેભાગે તમે તમારા ડેટામાંથી ID તરીકે કીઝનો ઉપયોગ કરશો:

```js{2}
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

જ્યારે તમારી પાસે પ્રસ્તુત વસ્તુઓ માટે સ્થિર ID ન હોય, ત્યારે તમે વસ્તુઓ અનુક્રમણિકાના છેલ્લા ઉપાય તરીકે કી નો ઉપયોગ કરી શકો છો:

```js{2,3}
const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
);
```

વસ્તુઓના ક્રમમાં ફેરફાર થઈ શકે તો અમે કીઝ માટે અનુક્રમણિકાનો ઉપયોગ કરવાની ભલામણ કરીએ છીએ. આ પ્રભાવ પર નકારાત્મક અસર કરી શકે છે અને Component state સાથે સમસ્યાઓ ઊભી કરી શકે છે. [ચાવીરૂપ અનુક્રમણિકાનો ઉપયોગ કીની જેમ નકારાત્મક અસરો પર ઊંડાણપૂર્વક સમજૂતી માટે](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318) રોબિન પોકોર્નીના લેખને તપાસો. જો તમે વસ્તુઓ સૂચિબદ્ધ કરવા માટે કોઈ સ્પષ્ટ કી અસાઇન કરવાનું પસંદ ન કરો તો, રીકેટ્સ કીઓ તરીકે અનુક્રમણિકાનો ઉપયોગ કરવા માટે ડિફોલ્ટ કરશે.

જો તમને [વધુ શીખવામાં રસ હોય તો શા માટે કીઝ આવશ્યક છે](/docs/reconciliation.html#recursing-on-children) તે વિશેની એક વિગતવાર સમજણ અહીં છે.

### કીઝ સાથે components કાઢવી {#extracting-components-with-keys}

કીઝ આસપાસના એરેના સંદર્ભમાં ફક્ત અર્થપૂર્ણ બનાવે છે.

ઉદાહરણ તરીકે, જો તમે `સૂચિ` component [કાઢો](/docs/components-and-props.html#extracting-components) છો, તો તમારે સૂચિમાં `<ListItem />` elements ને સૂચિમાં `<li>` element ની જગ્યાએ રાખવું જોઈએ.

**ઉદાહરણ: ખોટી કી વપરાશ**

```javascript{4,5,14,15}
function ListItem(props) {
  const value = props.value;
  return (
    // Wrong! There is no need to specify the key here:
    <li key={value.toString()}>
      {value}
    </li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Wrong! The key should have been specified here:
    <ListItem value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

**ઉદાહરણ: યોગ્ય કી વપરાશ**

```javascript{2,3,9,10}
function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()} value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

[**કોડપેન પર પ્રયત્ન કરો**](https://codepen.io/gaearon/pen/ZXeOGM?editors=0010)

અંગૂઠાનો સારો નિયમ એ છે કે 'નકશા()' ની અંદરના elements ને કીઝ કૉલની જરૂર છે.

### કીઝ માત્ર ભાઈબહેનો વચ્ચે જ અનન્ય હોવું જોઈએ {#keys-must-only-be-unique-among-siblings}

<<<<<<< HEAD
એરેમાં વપરાતી કીઝ તેમના ભાઈબહેનો વચ્ચે અનન્ય હોવી જોઈએ. જો કે તેઓ વૈશ્વિક રીતે અનન્ય હોવા જરૂરી નથી. જ્યારે આપણે બે ભિન્ન એરે પેદા કરીએ છીએ ત્યારે આપણે સમાન કીઝનો ઉપયોગ કરી શકીએ છીએ:
=======
Keys used within arrays should be unique among their siblings. However, they don't need to be globally unique. We can use the same keys when we produce two different arrays:
>>>>>>> 1e3b023d3192c36a2da7b72389debee2f0e0e8b0

```js{2,5,11,12,19,21}
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
  <Blog posts={posts} />,
  document.getElementById('root')
);
```

[**કોડપેન પર પ્રયત્ન કરો**](https://codepen.io/gaearon/pen/NRZYGN?editors=0010)

કીઝ પ્રતિક્રિયા આપવા માટે સંકેત આપે છે પરંતુ તે તમારા components પર પસાર થઈ નથી. જો તમને તમારા components માં સમાન વેલ્યુની આવશ્યકતા હોય, તો તેને સ્પષ્ટ રૂપે અલગ નામ સાથેના prop તરીકે પસાર કરો:

```js{3,4}
const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
```

ઉપરોક્ત ઉદાહરણ સાથે, `પોસ્ટ` component `props.id` વાંચી શકે છે, પરંતુ `props.key` નથી.

### JSXમાં નકશો() એમ્બેડ  કરવો {#embedding-map-in-jsx}

ઉપરોક્ત ઉદાહરણોમાં અમે એક અલગ `સૂચિબદ્ધ` વેરીએબલ જાહેર કર્યું છે અને તેને JSX માં શામેલ કર્યું છે:

```js{3-6}
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

JSX કર્લી કૌંસમાં [કોઈપણ અભિવ્યક્તિને એમ્બેડ] (/docs/introducing-jsx.html#embedding-expressions-in-jsx) કરવાની મંજૂરી આપે છે જેથી અમે `નકશા()` પરિણામ એક લાઈનમાં કરી શકીએ:

```js{5-8}
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```

[**કોડપેન પર પ્રયત્ન કરો**](https://codepen.io/gaearon/pen/BLvYrB?editors=0010)

કેટલીકવાર આ સ્પષ્ટ કોડમાં પરિણમે છે, પરંતુ આ શૈલીનો પણ દુરુપયોગ થઈ શકે છે. JavaScriptની જેમ, તે તમારા પર નિર્ધારિત છે કે તે વાંચી શકાય તેવું એક વેરિયેબલ કાઢવા માટે યોગ્ય છે કે નહીં. ધ્યાનમાં રાખો કે જો 'નકશા()' શરીર ખૂબ નિભાવ્યું હોય, તો તે [component કાઢવા માટે](/docs/components-and-props.html#extracting-components) સારો સમય હોઈ શકે છે.