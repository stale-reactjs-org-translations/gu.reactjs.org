---
id: lifting-state-up
title: Lifting State Up
permalink: docs/lifting-state-up.html
prev: forms.html
next: composition-vs-inheritance.html
redirect_from:
  - "docs/flux-overview.html"
  - "docs/flux-todo-list.html"
---

અમુક સમયે,ઘણા કોમ્પોનેન્ટને સમાન રીતે બદલતા ડેટાને રિફલેક્ટ કરવાની જરુર હોય છે. અમે વહેંચાયેલ સ્ટેટને તેમના નજીકના સામાન્ય સ્ટેટ સુધી વધારવાનું સુચન કરીએ છીએ. આ ક્રિયામાં કેવી રીતે કાર્ય થાય છે તે જોઇએ.

આ ભાગમાં, આપણે તાપમાન માટેનું calculator બનાવીશુ, જે નક્કી કરશે કે પાણી આપેલ તાપમાન સુધી ગરમ થયુ છે કે નહી.

આપણે `BoilingVerdict` નામનાં કોમ્પોનેન્ટથી ચાલુ કરશું. તે `celsuis` માં તાપમાન પ્રોપની કિમંત તરીકે સ્વિકારશે, અને તે પ્રિન્ટ કરશે કે તે પાણી ગરમ કરવા માટે પુરતું છે કે નહી.

```js{3,5}
function BoilingVerdict(props) {
  if (props.celsius >= 100) {
    return <p>The water would boil.</p>;
  }
  return <p>The water would not boil.</p>;
}
```

ત્યાર પછી આપણે `Calculator` નામનું કોમ્પોનેન્ટ બનાવીશું. તે `<input>` ને રેન્ડર કરશે અને તમને તાપમાન એન્ટર કરવા આપશે, અને તેની કિમંત `this.state.temperture` માં સાચવશે.

વધારેમાં, તે ઇનપુટ કરેલી કિમંત ને `BoilingVerdict` માં રેન્ડર કરશે.
```js{5,9,13,17-21}
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    return (
      <fieldset>
        <legend>Enter temperature in Celsius:</legend>
        <input
          value={temperature}
          onChange={this.handleChange} />
        <BoilingVerdict
          celsius={parseFloat(temperature)} />
      </fieldset>
    );
  }
}
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/ZXeOBm?editors=0010)

## Adding a Second Input {#adding-a-second-input}

આપણી નવી જરુરિયાત છે કે, સેલ્સિયસ ઇનપુટ ઉપરાંત ફેરનહિટ ઇનપુટ આપવું અને તેઓને સિનટેકસમાં સાથે રાખવામાં આવે.

આપણે `Calculator` કોમ્પોનેન્ટ પરથી `TemperatureInput` ને એક્સટ્રેટ કરી શકીએ. આપણે નવો `scale` પ્રોપ ઉમેરીશું જે `"c"` અથવા `"f"` હોઇ શકે.
:

```js{1-4,19,22}
const scaleNames = {
  c: 'Celsius',
  f: 'Fahrenheit'
};

class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    const scale = this.props.scale;
    return (
      <fieldset>
        <legend>Enter temperature in {scaleNames[scale]}:</legend>
        <input value={temperature}
               onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```

હવે અમે `Calculator` ને બે અલગ તાપમાન રેન્ડર કરવા માટે બદલશું. 
```js{5,6}
class Calculator extends React.Component {
  render() {
    return (
      <div>
        <TemperatureInput scale="c" />
        <TemperatureInput scale="f" />
      </div>
    );
  }
}
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/jGBryx?editors=0010)

હવે આપણી પાસે બે ઇનપુટ છે, પણ જ્યારે તમે બે માંથી એકનું તાપમાન બદલશો તો, તો બીજાનું બદલાશે નહી.આ આપણી જરુરિયાતને અલગ પાડે છે:આપણે તેને સિનટેક્સમાં સાથે રાખવાના છે.

આપણે `Calculator` માંથી `BoilingVerdict` ને દર્શાવી શકતા નથી.`Calculator` વર્તમાન તાપમાનને જાણતું નથી કારણ કે તે `TemperatureInput` ની અંદર હાઇડ થયેલું છે. 
## Writing Conversion Functions {#writing-conversion-functions}

પહેલા, આપણે Celsius ને Fahrenheit માં બદલવા માટે બે ફંકશન બનાવીશુ.
```js
function toCelsius(fahrenheit) {
  return (fahrenheit - 32) * 5 / 9;
}

function toFahrenheit(celsius) {
  return (celsius * 9 / 5) + 32;
}
```

આ બે ફંકશન નંબરને કનવર્ટ કરશે.આપણે બીજુ ફંકશન બનવીશુ જે આર્ગુમેન્ટ તરીકે સ્ટ્રીંગ `temperature` અને કનવર્ટર ફંકશનને લેશે અને સ્ટ્રીંગ પરત કરશે.આપણે તેનો ઉપયોગ અન્ય ઇનપુટ આધરિત એક ઇનપુટની કિમંતની ગણતરી કરવા માટે કરીશું.

તે અમાન્ય ઇનપુટ પર ખાલી સ્ટ્રિંગ પરત કરશે,અને તે આઉટપુટને ત્રીજા દશાંશ સ્થાને રાખે છે:
```js
function tryConvert(temperature, convert) {
  const input = parseFloat(temperature);
  if (Number.isNaN(input)) {
    return '';
  }
  const output = convert(input);
  const rounded = Math.round(output * 1000) / 1000;
  return rounded.toString();
}
```

ઉદાહરણ તરીકે, આ `tryConvert('abc', toCelsius)` ખાલી સ્ટ્રિંગ પરત કરશે, અને આ `tryConvert('10.22', toFahrenheit)` પરત કરશે `'50.396'`.
## Lifting State Up {#lifting-state-up}

હાલમાં, બંને `TemperatureInput` કોમ્પોનેન્ટ સ્વત્રંત રીતે પોતાની વેલ્યુને સામાન્ય સ્ટેટમાં રાખે છે.

```js{5,9,13}
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    // ...  
```
જ્યારે, આપણે ઇચ્છતા હોય કે બંને ઇનપુટ એકબીજા સાથે વાક્યરચનામાં રહે.જ્યારે આપણે સેલ્સિયસ ઇનપુટને સુધારીએ,ત્યારે ફેરનહિટ ઇનપુટ કનવર્ટ કરેલા તાપમાને રિફ્લેકટ કરવું જોઇએ. vice versa 

React માં, સ્ટેટને વહેંચવાની ક્રિયા તેને જરુરી કોમ્પોનેન્ટને તેની નજીકના કોમ્પોનેન્ટ પર ખસેડીને પુરી થાય છે.આ ક્રિયાને "lifting state up" કહે છે. આપણે લોકલ સ્ટેટમાંથી `TemperatureInput` ને કાઢી નાખશું અને તેને `Calculator` માં મુવ કરીશુ.

જો શેર થયેલ સ્ટેટ `Calculator` નું પોતાનું હોય,તો તે આપેલા બંને ઇનપુટ માટે "source of truth" બને છે.તે આપેલ બંને ઇનપુટ એકબીજા સાથે વય્વહારમાં રહે તે માટેનું સુચન કરી શકે છે.બંને `TemperatureInput` કોમ્પોનેન્ટના પ્રોપ્સ એક જ મુખ્ય  `Calculator` કોમ્પોનેન્ટમાંથી આવતા હોવાથી બંને ઇનપુટ હમેંશા એક જ સાથે સુમેળમાં રહેશે.

ચાલો તે કેવી રીતે કામ કરે છે તેના સ્ટેપ જોઇએ.

પહેલાતો, આપણે `TemperatureInput` કોમ્પોનેન્ટમાં `this.state.temperature` ને `this.props.temperature`માં ફેરવીશું.અત્યાર માટે, માની લઇએ કે `this.props.temperature` એ પહેલેથી જ બનાવેલ છે, કારણ કે આગળ જતા આપણે તેને `Calculator` માં પાસ કરવાની જરૂર પડશે.

```js{3}
  render() {
    // Before: const temperature = this.state.temperature;
    const temperature = this.props.temperature;
    // ...
```

આપણે જાણીએ છી કે [props are read-only](/docs/components-and-props.html#props-are-read-only).જ્યારે `temperature` લોકલ સ્ટેટમાં હોય ત્યારે, `TemperatureInput` ને બદલવા માટે `this.setState()` ને કોલ કરી શકશે.જો કે હવે `temperature` પેરેન્ટ પ્રોપ તરફથી આવતું હોવાથી,`TemperatureInput` તેને કંટ્રોલ કરી શકશે નહી.

React માં, આ ને સામાન્ય રીતે "controlled" કોમ્પોનેન્ટથી સોલ્વ કરી શકાય છે. જેવી રીતે DOM માં `<input>` ટેગ `value` અને `onChange` ને પ્રોપ તરીકે સ્વિકારે છે, તે જ રીતે `TemperatureInput` તેના મુખ્ય `Calculator` કોમ્પોનેન્ટમાંથી `temperature` અને `onTemperatureChange` એમ બંને પ્રોપ્સ ને સ્વિકારી શકે છે.


હવે, જ્યારે `TemperatureInput` નું તાપમાન બદલાવવાની જરૂર પડે ત્યારે, `this.props.onTemperatureChange` ને કોલ કરે છે.
```js{3}
  handleChange(e) {
    // Before: this.setState({temperature: e.target.value});
    this.props.onTemperatureChange(e.target.value);
    // ...
```

>નોંધ:
>
>કસ્ટમ કોમ્પોનેન્ટમાં `temperature` અને `onTemperatureChange` એમ પ્રોપ્સના આવા નામ રાખવાનો કોઇ ખાસ અર્થ થતો નથી.આપણે તેને બીજા નામ સાથે પણ કોલ કરી શકીએ, જેવા કે `value` અને `onChange` આ એક સામાન્ય રસ્તો છે.

પેરેન્ટ `Calculator` કોમ્પોનેન્ટ દ્વારા `onTemperatureChange` પ્રોપ સાથે `temperature` પ્રોપ પણ આપવામાં આવશે.તે પોતાના લોકલ સ્ટેટમાં ફેરફાર કરશે અને તે કરેલા ફેરફાર ને હેન્ડલ પણ કરશે, આમ નવી વેલ્યુ સાથે બંને ઇનપુટ ફરીથી રેન્ડર થાસે. આપણે હવે જલ્દી નવા `Calculator` ને ઇમ્પ્લિમેન્ટ કરવામાં ધ્યાન આપીશું.

`Calculator`માં બદલાવ કરતા પહેલા,ચાલો `TemperatureInput` કોમ્પોનેન્ટમાં કરેલા ફેરફારોને જોઇએ. આપણે તેમાંથી લોકલ સ્ટેટને કાઢી નાખ્યુ છે, અને `this.state.temperature` ના અમલ ને બદલે, આપણે હવે `this.props.temperature` ને અમલમાં લેશુ. જ્યારે આપણે કોઇ બદલાવ કરવા માંગતા  હોય ત્યારે `this.setState()` ને બદલે, `this.props.onTemperatureChange()` કોલ કરીએ છીએ, જે  `Calculator` દ્વારા પ્રોવાઇડ કરવામાં આવી છે.

```js{8,12}
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.props.onTemperatureChange(e.target.value);
  }

  render() {
    const temperature = this.props.temperature;
    const scale = this.props.scale;
    return (
      <fieldset>
        <legend>Enter temperature in {scaleNames[scale]}:</legend>
        <input value={temperature}
               onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```

હવે `Calculator` કોમ્પોનેન્ટ તરફ આવીએ.

આપણે વર્તમાન ઇનપુટનું `temperature` અને `scale` તેના લોકલ સ્ટેટમાં સ્ટોર કરીશુ. આ તે સ્ટેટ છે જેને આપણે ઇનપુટમાંથી "lifted up" કર્યુ છે, અને તે તે બંને માટે "source of truth" તરીકે કામ કરશે.આ બંને ઇનપુટને રેન્ડર કરવા માટે આપણે તે ડેટાને જાણવાની જરૂર છે આ તે માટેની ન્યુનતમ રજુઆત છે.


ઉદાહરણ તરીકે, જ્યારે આપણે સેલ્સિયસ ઇનપુટ તરીકે 37 લઇએ, ત્યારે `Calculator` કોમ્પોનેન્ટનું સ્ટેટ આવું હશે:

```js
{
  temperature: '37',
  scale: 'c'
}
```


જો આપણે પછી ફેરનહિટ ફિલ્ડને 212 કરીશું, તો ત્યારે `Calculator` કોમ્પોનેન્ટનું સ્ટેટ આવું હશે:

```js
{
  temperature: '212',
  scale: 'f'
}
```

We could have stored the value of both inputs but it turns out to be unnecessary. It is enough to store the value of the most recently changed input, and the scale that it represents. We can then infer the value of the other input based on the current `temperature` and `scale` alone.

ઇનપુટસ એકબીજા સાથે સુમેળમાં રહે છે કારણ કે તેની વેલ્યુ સરખા સ્ટેટમાંથી લેવામાં આવી છે:

```js{6,10,14,18-21,27-28,31-32,34}
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleCelsiusChange = this.handleCelsiusChange.bind(this);
    this.handleFahrenheitChange = this.handleFahrenheitChange.bind(this);
    this.state = {temperature: '', scale: 'c'};
  }

  handleCelsiusChange(temperature) {
    this.setState({scale: 'c', temperature});
  }

  handleFahrenheitChange(temperature) {
    this.setState({scale: 'f', temperature});
  }

  render() {
    const scale = this.state.scale;
    const temperature = this.state.temperature;
    const celsius = scale === 'f' ? tryConvert(temperature, toCelsius) : temperature;
    const fahrenheit = scale === 'c' ? tryConvert(temperature, toFahrenheit) : temperature;

    return (
      <div>
        <TemperatureInput
          scale="c"
          temperature={celsius}
          onTemperatureChange={this.handleCelsiusChange} />
        <TemperatureInput
          scale="f"
          temperature={fahrenheit}
          onTemperatureChange={this.handleFahrenheitChange} />
        <BoilingVerdict
          celsius={parseFloat(celsius)} />
      </div>
    );
  }
}
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/WZpxpz?editors=0010)


હવે, તમે `this.state.temperature` અને `this.state.scale` માંથી ગમે તે ઇનપુટને બદલશો તો `Calculator` માં પણ ફેરફાર થાશે.અને ઇનપુટમાંથી એકને જ તે વેલ્યુ મળે છે અને અન્ય ઇનપુટને હમેંશા તેની વેલ્યુ ને આધારે ફરીથી ગણતરી કરવામાં આવે છે.
Let's recap what happens when you edit an input:

* React calls the function specified as `onChange` on the DOM `<input>`. In our case, this is the `handleChange` method in the `TemperatureInput` component.
* The `handleChange` method in the `TemperatureInput` component calls `this.props.onTemperatureChange()` with the new desired value. Its props, including `onTemperatureChange`, were provided by its parent component, the `Calculator`.
* When it previously rendered, the `Calculator` had specified that `onTemperatureChange` of the Celsius `TemperatureInput` is the `Calculator`'s `handleCelsiusChange` method, and `onTemperatureChange` of the Fahrenheit `TemperatureInput` is the `Calculator`'s `handleFahrenheitChange` method. So either of these two `Calculator` methods gets called depending on which input we edited.
* Inside these methods, the `Calculator` component asks React to re-render itself by calling `this.setState()` with the new input value and the current scale of the input we just edited.
* React calls the `Calculator` component's `render` method to learn what the UI should look like. The values of both inputs are recomputed based on the current temperature and the active scale. The temperature conversion is performed here.
* React calls the `render` methods of the individual `TemperatureInput` components with their new props specified by the `Calculator`. It learns what their UI should look like.
* React calls the `render` method of the `BoilingVerdict` component, passing the temperature in Celsius as its props.
* React DOM updates the DOM with the boiling verdict and to match the desired input values. The input we just edited receives its current value, and the other input is updated to the temperature after conversion.

* React DOM `BoilingVerdict` ને ઇચ્છિત ઈનપુટ વેલ્યુ સાથે મેચ કરવા માટે DOM ને અપડેટ કરે છે.આપણે હમણાં ફેરફાર કરેલું ઈનપુટ તેની વર્તમાન વેલ્યુ મેળવે છે, અને અન્ય ઈનપુટને ફેરફાર પછી તાપમાનમાં ફેરવવામાં આવે છે.

દરેક અપડેટ સમાન પગલાઓમાંથી પસાર થાય છે જેનાથી ઇનપુટ સુમેળમાં રાખી શકાય.


## Lessons Learned {#lessons-learned}

React એપ્લિકેશનમાં બદલાતા કોઈ પણ ડેટા માટે એક જ "source of truth" હોવું જોઈએ.સામાન્ય રીતે,સ્ટેટને પહેલા તે કોમ્પોનેન્ટમાં ઉમેરાવામાં આવે છે જેને રેન્ડર કરવા માટે તેની જરૂર છે.પછી,જો બીજા કોમપોનેન્ટને પણ તેની જરૂર હોય તો, તમે તેને તેમના નજીક ના સામાન્ય કોમ્પોનેન્ટ સુધી લઈ જઈ શકો છો. સ્ટેટને વિવિધ કોમ્પોનેન્ટ વચ્ચે સુમેળ કરવાનો પ્રયાસ કરવાને બદલે તમારે આ [top-down data flow](/docs/state-and-lifecycle.html#the-data-flows-down) જોવું જોઈએ.

લિફ્ટિંગ સ્ટેટમાં ટુ-વે બાઇંડિંગ એપ્રોચસ કરતાં પણ વધુ "boilerplate" માં કોડ લખવાનો સમાવેશ થાય છે,પરંતુ તેનો લાભ એ છે કે તે ભૂલો શોધવા અને અલગ કરવા માટે ઓછો સમય લે છે. કોઈપણ સ્ટેટ કેટલા કોમ્પોનેન્ટમાં લાઈવ છે અને તે કોમ્પોનેન્ટ જ તેને બદલી સકે છે, તેથી ભૂલો માટેના ક્ષેત્રમાં મોટો ઘટાડો થાય છે.આ ઉપરાંત, તમે યુઝરના ઈનપુટને નકારવા અથવા રૂપાંતર કરવા માટે કોઈ પણ લૉજિકને લાગું કરી શકો છો.

જો કઇં પણ પ્રોપ્સ અથવા સ્ટેટમાંથી ડીરાઇવડ થઈ શકતું હોય તો તે સ્ટેટમાં હોવું જોઈએ નહીં.ઉદાહરણ તરીકે,`celsiusValue` અને `fahrenheitValue` બંને સ્ટોર કરવાને બદલે, આપણે ફક્ત બદલાયેલું `temperature` અને તેના `scale` નો સંગ્રહ કરશું. અન્ય ઈનપુટ વેલ્યુની ગણતરી હમેંશા તેની `render()` મેથડ પરથી કરી શકાય છે. આ આપણને યુઝરના ઈનપુટની ચોકસાઇ ગુમાવ્યા વગર અન્ય સ્ટેટમાં વેલ્યુને ક્લિયર અથવા લાગું કરવા દે છે.

<<<<<<< HEAD
જ્યારે તમને UI માં કઈ ખોટું દેખાય, ત્યારે તમે props નિરીક્ષણ કરવા અને સ્ટેટને અપડેટ કરવા જવાબદાર કોમ્પોનેન્ટ ન મળે ત્યાં સુધી તમે આનો [React Developer Tools](https://github.com/facebook/react/tree/master/packages/react-devtools) ઉપયોગ કરી શકો છે.અહી તમે તેમના સોર્સ ઉપરથી ભૂલો ટ્રેસ કરી શકો છો.
=======
When you see something wrong in the UI, you can use [React Developer Tools](https://github.com/facebook/react/tree/main/packages/react-devtools) to inspect the props and move up the tree until you find the component responsible for updating the state. This lets you trace the bugs to their source:
>>>>>>> 951fae39f0e12dc061f1564d02b2f4707c0541c4

<img src="../images/docs/react-devtools-state.gif" alt="Monitoring State in React DevTools" max-width="100%" height="100%">

