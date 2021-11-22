---
id: forms
title: Forms
permalink: docs/forms.html
prev: lists-and-keys.html
next: lifting-state-up.html
redirect_from:
  - "tips/controlled-input-null-value.html"
  - "docs/forms-in-GJ.html"

---

<<<<<<< HEAD
HTML ફોર્મના એલિમેન્ટ, react ના અન્ય DOM એલિમેન્ટથી અલગ કામ કરે છે, કારણ કે ફોર્મ એલિમેન્ટ કુદરતી રીતે થોડી આંતરિક સ્થિતિ ધરાવે છે. ઉદાહરણ તરીકે, સાદા HTML માં આ ફોર્મ એક નામ સ્વીકારે છે:
=======
HTML form elements work a bit differently from other DOM elements in React, because form elements naturally keep some internal state. For example, this form in plain HTML accepts a single name:
>>>>>>> 17ad2cbc71f4c1fcc3f3f9ae528bfd292a9fced7

```html
<form>
  <label>
    Name:
    <input type="text" name="name" />
  </label>
  <input type="submit" value="Submit" />
</form>
```

જ્યારે ઉપયોગકર્તા ફોર્મ સબમિટ કરે ત્યારે ફોર્મને નવા પેજ પર મોકલવું એ HTMLની મૂળભૂત લાક્ષણિકતા છે. જો તમારે આ લાક્ષણિકતા Reactમાં  જોઈએ છે, તો તે ફકત કાર્ય કરે છે. પરંતુ મોટાભાગના કિસ્સાઓમાં, જાવાસ્ક્રિપ્ટમાં કાર્ય કરવું તે યોગ્ય છે જે ફોર્મ સબમિશનને હેન્ડલ કરે છે અને ઉપયોગકર્તાએ ફોર્મમાં દાખલ કરેલા ડેટાનો ઉપયોગ પણ કરી શકે છે. આમ કરવાની પ્રમાણભૂત રીતને "contorlled components" કહે છે..

## Controlled Components {#controlled-components}

HTML માં, ફોર્મ એલિમેન્ટ જેમ કે `<input>` , `<textarea>`, અને `<select>` સામાન્ય રીતે પોતાનું state જાળવી રાખે છે અને ઉપયોગકર્તા ઈનપુટને આધારે તેને અપડેટ કરે છે. React માં mutable state ને ખાસ કરીને property ના state માં રખવામાં આવે છે, અને તેને [`setState()`](/docs/react-component.html#setstate). સાથે અપડેટ કરવામાં આવે છે.

આપણે આ બે પ્રતિક્રિયાને react state "single source of truth" થી જોડી શકીએ. પછી તે React કોમ્પોનેટ જે ફોર્મ ને રેન્ડર કરે છે તે ઉપયોગકર્તાના ઈનપુટ કરવાથી તે ફોર્મમાં શું થાય છે તેને પણ નિયંત્રિત કરે છે. ઈનપુટ ફોર્મ એલિમેન્ટ જેની value આ પ્રકિયા દ્વારા નિયંત્રિત થાય છે તેને "controlled component" કહેવામાં આવે છે..

<<<<<<< HEAD
ઉદાહરણ તરીકે, જો આપણે પહેલાંના ઉદાહરણ પર જ્યારે નામ સબમિટ કરીએ ત્યારે log દર્શાવવા માંગતા હોય, તો આપણે ફોર્મને controlled component તરીકે લખી શકીએ..
```javascript{4,10-12,24}
=======
```javascript{4,10-12,21,24}
>>>>>>> 17ad2cbc71f4c1fcc3f3f9ae528bfd292a9fced7
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/VmmPgp?editors=0010)

જયારે `value` attribute ફોર્મ એલિમેન્ટ પર સેટ કરેલું છે, તેની પ્રદર્શિત કિમંત હમેંશા `this.state.value` રહેશે, જે તેને React state source of truth બનાવે છે. React state ને અપડેટ કરવા માટે `handleChange` દરેક keystroke પર ચાલતું હોવાથી, પ્રદશિત કિમંત ઉપયોગકર્તાના પ્રકાર તરીકે અપડેટ થશે.

controlled component સાથે, દરેક state પરિવર્તનમાં તેની સાથે સંકળાયેલ હેન્ડલર ફંક્શન હશે.આ ઉપયોગકર્તાના ઇનપુટને સીધી રીતે બદલવા અથવા માન્ય કરવા માટે તેને સરળ બનાવે છે.ઉદાહરણ તરીકે, જો આપણે લખેલા બધા નામો કેપિટલ અક્ષરોમાં જોતાં હોય, તો આપણે `હેન્ડલ ચેંજ` આ રીતે લખી શકીએ: 

<<<<<<< HEAD

```javascript{2}
handleChange(event) {
  this.setState({value: event.target.value.toUpperCase()});
}
```
=======
With a controlled component, the input's value is always driven by the React state. While this means you have to type a bit more code, you can now pass the value to other UI elements too, or reset it from other event handlers.
>>>>>>> b3c7f041586b71b31f556403426fcd7cab342535

## The textarea Tag {#the-textarea-tag}

HTML માં, `<textarea>` એલિમેન્ટ તેના children દ્વારા લખાણને દર્શાવે છે:

```html
<textarea>
  Hello there, this is some text in a text area
</textarea>
```
React માં, `<textarea>` તેના બદલે `value` એટ્રિબ્યુટનો ઉપયોગ કરે છે. આ રીતે, `<textarea>` નો ઉપયોગ કરીને ફોર્મ, જે single line ઈનપુટનો ઉપયોગ કરે છે તેવી સમાન રીતે લખી શકાય છે..
```javascript{4-6,12-14,26}
class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 'Please write an essay about your favorite DOM element.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('An essay was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Essay:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
ધ્યાનમાં લેવા જેવું `this.state.value` કન્સ્ટ્રક્ટરમાં initialized થયેલું છે, જેથી ટેક્સ્ટએરિયા તેની અંદર કેટલાક લખાણથી ચાલુ થાશે..
## The select Tag {#the-select-tag}

HTML માં, `<select>` ડ્રોપ-ડાઉન લિસ્ટ બનાવે છે. ઉદાહરણ તરીકે, આ HTML flavours માટેનું ડ્રોપ-ડાઉન લિસ્ટ બનાવશે.. 

```html
<select>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option selected value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

ધ્યાનમાં લેવાનું કે coconut ઓપ્શન શરૂઆતથીજ પસંદ થયેલો છે, કારણ તેના `selected` એટ્રિબ્યુટનાં લીધે. React `selected` એટ્રિબ્યુટનો ઉપયોગ કરવાને બદલે `value` એટ્રિબ્યુટનો ઉપયોગ `select` નાં root tag પર કરે છે. આ controlled component માં વધુ અનુકૂળ છે કારણ કે તમારે તેને ફક્ત એક જ જગ્યાએ અપડેટ કરવાની જરૂર છે. ઉદાહરણ તરીકે::

```javascript{4,10-12,24}
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Your favorite flavor is: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Pick your favorite flavor:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">Grapefruit</option>
            <option value="lime">Lime</option>
            <option value="coconut">Coconut</option>
            <option value="mango">Mango</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/JbbEzX?editors=0010)

કુલ મળીને, આ તે બનાવે છે જેથી `<input type="text">`, `<textarea>`, and `<select>` બધાજ એક સરખી રીતે કાર્ય કરી શકે છે  - તે બધા એક value સ્વીકારે છે કે જેનો ઉપયોગ તમે controlled component નાં અમલ માટે કરી શકો છો. 

> નોંધ
>
> તમે array ને પણ `value` એટ્રિબ્યુટમાં પાસ કરી શકો છો, જે તમને `select` ટેગમાં મલ્ટીપલ વિકલ્પો પસંદ કરવાની પરવાનગી આપે છે:
>
>```js
><select multiple={true} value={['B', 'C']}>
>```

## The file input Tag {#the-file-input-tag}

HTMLમાં, `<input type="file">` ઉપયોગકર્તાને તેમની ડિવાઇસ સ્ટોરેજ માંથી સર્વર પર એક કે તેથી વધારે ફાઇલ જવાસ્ક્રિપ્ટની મદદ થી અપલોડ કરવા દે છે. via [File API](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications).

```html
<input type="file" />
```

કારણ તેની value રીડ ઓન્લી છે, તે React નાં **uncontrolled** કોમ્પોનેન્ટ છે.તેની ચર્ચા અન્ય uncontrolled components સાથે કરવામાં આવશે.[later in the documentation](/docs/uncontrolled-components.html#the-file-input-tag).

## Handling Multiple Inputs {#handling-multiple-inputs}

જ્યારે તમારે વધારે નિયંત્રિત `input` એલિમેન્ટ ને હેન્ડલ કરવાની જરુર છે, ત્યારે તમે દરેક એલિમેન્ટમાં `name` એટ્રિબ્યુટ ઉમેરી શકો છો અને હેન્ડલર ફંક્શનન  `event.target.name` ની value ને આધારે શું કરવું તે નક્કી કરી શકે છે.
For example:

```javascript{15,18,28,37}
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```

[**Try it on CodePen**](https://codepen.io/gaearon/pen/wgedvV?editors=0010)

નોંધ લો કેવી રીતે અમે ES6 નો ઉપયોગ કરેલો [computed property name](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Object_initializer#Computed_property_names) આપેલ ઇનપુટ નામને તેને અનુરૂપ state કી સાથે અપડેટ કરવા માટેની syntax

```js{2}
this.setState({
  [name]: value
});
```

It is equivalent to this ES5 code:

```js{2}
var partialState = {};
partialState[name] = value;
this.setState(partialState);
```

ઉપરાંત, `setState()` ઓટોમેટિક હોવાથી,[આંશિક સ્થિતિને વર્તમાન સ્થિતિમાં મર્જ કરે છે](/docs/state-and-lifecycle.html#state-updates-are-merged),આપણે તેને ફક્ત ચેન્જ થયેલા ભાગ સાથે કોલ કરવાની જરૂર હોય છે.
## Controlled Input Null Value {#controlled-input-null-value}

<<<<<<< HEAD
[controlled component](/docs/forms.html#controlled-components) value prop ની કિમંત સ્પષ્ટ કરવી એ વપરાશકર્તાને ઇનપુટ બદલતા અટકાવે છે , જ્યાં સુધી તમે ઇચ્છો નહીં ત્યાં સુધી ઉપયોગકર્તાને ઇનપુટ બદલતા અટકાવે છે. જો તમે `value` ઉલ્લેખિત કરેલ છે, પરંતુ ઇનપુટ હજી પણ સુધારવા યોગ્ય છે, તો તમે આકસ્મિક રીતે ` value ` `undefined`  અથવા `null` પર સેટ કર્યું હશે.
=======
Specifying the `value` prop on a [controlled component](/docs/forms.html#controlled-components) prevents the user from changing the input unless you desire so. If you've specified a `value` but the input is still editable, you may have accidentally set `value` to `undefined` or `null`.

>>>>>>> 17ad2cbc71f4c1fcc3f3f9ae528bfd292a9fced7
The following code demonstrates this. (The input is locked at first but becomes editable after a short delay.)
નીચેનો કોડ આ દર્શાવે છે.(આ ઈનપુટ પહેલાથી લોક છે પરંતુ ટૂંક સમયમાં સુધારવા યોગ્ય બનશે..)
```javascript
ReactDOM.render(<input value="hi" />, mountNode);

setTimeout(function() {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);

```

## Alternatives to Controlled Components {#alternatives-to-controlled-components}

controlled components નો ઉપયોગ કરવો તે અમુક સમયે કંટાળાજનક હોઈ શકે છે, કારણ કે તમારે દરેક વખતે event handler લખવાની જરૂર પડે છે જ્યાં તમારો ડેટા બદલી શકાય અને જ્યાં ઈનપુટની સ્થિતિ ને React કોમ્પોનેન્ટથી પાઇપ કરી શકાય.જ્યારે તમે preexisting કોડબેઝને React માં રૂપાંતરિત કરી રહ્યાં હોવ અથવા React એપ્લિકેશનને non-React લાઇબ્રેરી સાથે integrate કરી રહ્યાં હોવ ત્યારે આ ત્રાંસજનક બની શકે છે.આવી પરિસ્થિતિમાં, તમે check કરી શકો છો [uncontrolled components](/docs/uncontrolled-components.html), ફોર્મ ઈનપુટના અમલીકરણ માટેની વૈકલ્પિક ટેક્નિક છે.
 
## Fully-Fledged Solutions {#fully-fledged-solutions}

જો તમે વેલિડેશન, મુલાકાત લીધેલ ફીલ્ડ્સને track કરવા, અને ફોર્મનાં સબમિશન સંભાળવા સહિતના સંપૂર્ણ સમાધાનની શોધ કરી રહ્યાં છો, તો [Formik] (https://jaredpalmer.com/formik) એ લોકપ્રિય પસંદગીઓમાંની એક છે. જો કે, તે controlled components and managing state નાં સમાન સિદ્ધાંતો પર બનાવવામાં આવ્યું છે - તેથી તેમને શીખવાની અવગણના ન કરો.