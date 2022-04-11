---
id: conditional-rendering
title: Conditional Rendering
permalink: docs/conditional-rendering.html
prev: handling-events.html
next: lists-and-keys.html
redirect_from:
  - "tips/false-in-jsx.html"
---

રિએક્ટ માં, તમે વિશિષ્ટ કોમ્પોનેન્ટ બનાવી શકો છો જે તમને જરૂરી વર્તનને સમાવી લે છે. તે પછી, તમારા એપ્લિકેશન ના સ્ટેટે ને આધારે રેન્ડર કરાવી શકો છો.

રીએક્ટમાં શરતી રેંડરિંગ જાવાસ્ક્રિપ્ટમાં શરતો જેવું કાર્ય કરે છે તે જ રીતે કાર્ય કરે છે. જાવાસ્ક્રિપ્ટ ઓપરેટરો જેમ કે [`if`] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else) અથવા [કન્ડિશન્લ ઓપરેટર] (https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) ને પ્રતિક્રિયા આપવા, અને UI ને તેની સાથે મેચ કરવા અપડેટ કરવા દો.

આ બે કોમ્પોનેટ્સ ને ધ્યાન માં લો:

```js
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}
```

અમે એક `Greeting` કોમ્પોનેન્ટ બનાવશુ જે વપરાશકર્તા લોગીન છે કે નાઈ તેના આધારે દેખાશે.

```javascript{3-7,11,12}
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```

[**તેને કોડપેન પર અજમાવો**] (https://codepen.io/gaearon/pen/ZpVxNq?editors=0011)

આ ઉદાહરણ માં `isLoggedIn` પ્રોપ ની વૅલ્યુ ના આધારે ગ્રીટિંગ્સ રેન્ડર થાય છે.

### એલિમેન્ટ વેરીએબલ {#element-variables}

તમે એલિમેન્ટ ને સ્ટોર કરવા વેરીએબલ નો ઉપયોગ કરી શકો છો. તે તમને કોમ્પોનેન્ટ ના એક ભાગ ને શરતો પર રેન્ડર કરવામાં મદદ કરે છે, બાકીના આઉટપુટ ને બદલ્યા વગર.

આ બે નવા કોમ્પોનેન્ટ ને જોવો, જે લોગીન અને લોગૉઉટ બટન ને રજુ કરે છે:

```js
function LoginButton(props) {
  return (
    <button onClick={props.onClick}>
      Login
    </button>
  );
}

function LogoutButton(props) {
  return (
    <button onClick={props.onClick}>
      Logout
    </button>
  );
}
```

નીચેના ઉદાહરણ માં, `LoginControl` નામના [સ્ટેટેફૂલ કોમ્પોનેન્ટ] (/docs/state-and-lifecycle.html#adding-local-state-to-a-class) બનાવશુ.

તે તેના સ્ટેટ ના આધારે યા તો `<LoginButton />` અને યા તો `<LogoutButton />` રેન્ડર કરશે. તે આગળ ના ઉદાહરણ માંથી `<Greeting />` પણ રેન્ડર કરશે.

```javascript{20-25,29,30}
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;

    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);
```

[**તેને કોડપેન પર અજમાવો**](https://codepen.io/gaearon/pen/QKzAgB?editors=0010)


જ્યારે કોઈ વેરીએબલ જાહેર કરવું અને `if` સ્ટેટમેન્ટનો ઉપયોગ કરવો એ શરતી રૂપે કોમ્પોનેન્ટ ને રેન્ડર કરવા માટે એક સરસ રીત છે, કેટલીકવાર તમે ટૂંકા વાક્યરચનાનો ઉપયોગ કરી શકો છો. નીચે જણાવેલ jsx માં શરતોને ઇનલાઇન કરવાના કેટલાક રસ્તાઓ છે.


### ઇનલાઇન ઇફ લોજિકલ && ઓપરેટર સાથે {#inline-if-with-logical--operator}


તમે [jsx માં કોઈપણ એક્સપ્રેસ્સ્ન એમ્બેડ કરી શકો છો] (/docs/introducing-jsx.html#embedding-expressions-in-jsx) તેમને કર્લી કૌંસમાં લપેટીને. આમાં જાવાસ્ક્રિપ્ટ લોજિકલ `&&` ઓપરેટર શામેલ છે. તે એલિમેન્ટ સહિતના શરતી સ્થિતિ માટે સરળ હોઈ શકે છે:

```js{6-10}
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

[**તેને કોડપેન પર અજમાવો**](https://codepen.io/gaearon/pen/ozJddz?editors=0010)

તે જાવાસ્ક્રિપ્ટમાં કાર્ય કરે છે કારણ કે જાવાસ્ક્રિપ્ટમાં, `true && expression` હંમેશાં "true" `એક્સપ્રેસ્સ્ન` નું મૂલ્યાંકન કરે છે, અને `false && expression` - હંમેશાં "false" નું મૂલ્યાંકન કરે છે.


<<<<<<< HEAD
તેથી, જો સ્થિતિ `true` છે, તો `&&` after પછીનું એલિમેન્ટ આઉટપુટમાં દેખાશે. જો તે `false` છે, તો રિએક્ટ તેને અવગણશે અને જતું કરશે.
=======
Note that returning a falsy expression will still cause the element after `&&` to be skipped but will return the falsy expression. In the example below, `<div>0</div>` will be returned by the render method.

```javascript{2,5}
render() {
  const count = 0;
  return (
    <div>
      {count && <h1>Messages: {count}</h1>}
    </div>
  );
}
```

### Inline If-Else with Conditional Operator {#inline-if-else-with-conditional-operator}
>>>>>>> 84ad3308338e2bb819f4f24fa8e9dfeeffaa970b

### કન્ડિશન્લ ઓપરેટર સાથે ઇનલાઇન If-Else {#inline-if-else-with-conditional-operator}


કન્ડિશન્લ એલિમેન્ટ ઇનલાઇન રેન્ડર કરવા માટેની બીજી પદ્ધતિ જાવાસ્ક્રિપ્ટ કન્ડિશન્લ ઓપરેટરનો ઉપયોગ છે [`condition ? true : false`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Conditional_Operator).


નીચેના ઉદાહરણ માં અમે તેનો ઉપયોગ એક નાના બ્લોક ને કોંડિશનલ રેન્ડર કરવા મારે કર્યો છે.

```javascript{5}
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
    </div>
  );
}
```

તેનો ઉપયોગ મોટા એક્સપ્રેસ્સ્ન માટે પણ થઈ શકે છે, તેમ છતાં શું ચાલી રહ્યું છે તે સ્પષ્ટ નથી:

```js{5,7,9}
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn
        ? <LogoutButton onClick={this.handleLogoutClick} />
        : <LoginButton onClick={this.handleLoginClick} />
      }
    </div>
  );
}
```

જાવાસ્ક્રિપ્ટ ની જેમ, આ તમારા પર આધાર રાખે છે કે તમને અને તામ્રરી ટીમ ને સરળ પડે એવી સ્ટાઇલ પસંદ કરો। પણ યાદ રાખો જયારે કન્ડિશન જટિલ બને છે ત્યારે આ સારો સમય છે કોમ્પોનેન્ટ એક્સટ્રેક્ટ કરવા [extract a component](/docs/components-and-props.html#extracting-components).


### કોમ્પોનેન્ટ ને રેન્ડર થતા અટકાવા {#preventing-component-from-rendering}


કોઈ સમયે તમારે કોમ્પોનેન્ટ ને પોતાને હાઇડ કરવાનો હોય છે, જયારે તે બીજા કોમ્પોનેન્ટ દ્વારા રેન્ડર થતો હોય. એવું કરવા મારે રેન્ડર આઉટપુટ ની જગ્યા એ null રીટર્ન કરવો.


નીચેના ઉદાહરણ માં, `<WarningBanner />` `warn` નામના પ્રોપ ની વૅલ્યુ ઉપર આધાર રાખી રેન્ડર થાય છે. જો પ્રોપ્સ ની વૅલ્યુ `false` હશે તો કોમ્પોનેન્ટ રેન્ડર નાઈ થાય. 

```javascript{2-4,29}
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {showWarning: true};
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState(state => ({
      showWarning: !state.showWarning
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Hide' : 'Show'}
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Page />,
  document.getElementById('root')
);
```

[**તેને કોડપેન પર અજમાવો**](https://codepen.io/gaearon/pen/Xjoqwm?editors=0010)


કોમ્પોનેન્ટ ના રેન્ડર થી null રીટર્ન કરવું એ કોમ્પોનેન્ટ ની લાઈફસાયક્લ મેથોડ ને કોઈ અસર નાઈ કરે. ઉદાહરણ તરીકે `componentDidUpdate` કોલ થાય છે.
