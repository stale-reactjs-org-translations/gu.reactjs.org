---
id: add-react-to-a-website
title: Add React to a Website
permalink: docs/add-react-to-a-website.html
redirect_from:
  - "docs/add-react-to-an-existing-app.html"
prev: getting-started.html
next: create-a-new-react-app.html
---


તમારે જરૂરીયાત હોય તેટલું અથવા તેના કરતાં વધારે react વાપરો.

React ને ક્રમશ: અપનાવવા માટે શરૂઆતથી બનાવવામાં આવી છે,અને **you can use as little or as much React as you need**. કદાચ તમે અસ્તિત્વમાનાં પેજ પર
 "sprinkles of interactivity" એડ કરવા માંગતા હોય તો. React કોમ્પોનેન્ટ એ આમ કરવા માટે સારો રસ્તો છે.

મોટાભાગની વેબસાઇટ્સ સિંગલ-પેજ એપ્લિકેશનો હોતી નથી, અને તે હોવાની જરૂર પણ નથી. **a few lines of code and no build tooling** સાથે, તમારી વેબસાઇટના અમુક ભાગ પર React ને વાપરવાનો પ્રયાસ કરો.પછી ધીમે ધીમે તમે તેની હાજરી ને વધારી શકો છે, અથવા તેને તમે અમુક ડાયનામિક વિજેટ્સમાં સમાવી શકો છો.
---

- [Add React in One Minute](#add-react-in-one-minute)
- [Optional: Try React with JSX](#optional-try-react-with-jsx) (no bundler necessary!)

## Add React in One Minute {#add-react-in-one-minute}
 
આ ભાગમાં, અમે તમને બતાવી રહ્યા છી કે જૂના HTML પેજમાં React કોમ્પોનેન્ટ કેવી રીતે એડ કરવું. તમે તમારી પોતાની વેબસાઇટ સાથે અનુસરણ કરી શકો, અથવા પ્રેક્ટિસ માટે ખાલી HTML ફાઇલ બનાવી શકો છો.  

ત્યાં કોઈ કોમ્પલીકેટેડ ટૂલ્સ કે ઇન્સ્ટોલ ની જરૂરિયાત નથી -- **to complete this section, you only need an internet connection, and a minute of your time.**

ઓપ્શનલ:[Download the full example (2KB zipped)](https://gist.github.com/gaearon/6668a1f6986742109c00a581ce704605/archive/f6c882b6ae18bde42dcf6fdb751aae93495a2275.zip)

### Step 1: Add a DOM Container to the HTML {#step-1-add-a-dom-container-to-the-html}

પ્રથમ,તમારે જે HTML પેજ ને એડિટ કરવાનું હોય તેને ઓપન કરો.જ્યાં તમે React વડે કઇંક બતાવવા માંગો છો તે સ્થાનને સ્પોટ કરવા માટે ખાલી `<div>` ટેગ ઉમેરો. ઉદાહરણ તરીકે 
```html{3}
<!-- ... existing HTML ... -->

<div id="like_button_container"></div>

<!-- ... existing HTML ... -->
```

અમે આ `<div>` ને યુનિક HTML એટ્રિબ્યુટ `id` આપેલું છે.આ અમને તે પછીથી જાવાસ્ક્રિપ્ટ કોડમાંથી શોધવા અને તેની અંદર React કોમ્પોનેન્ટ ડિસ્પ્લે કરવાની મંજૂરી આપશે.

>ટીપ
>
> તમે "container" `<div>` ને `<body>` ટેગમાં આની જેમ **anywhere** મૂકી શકો છો.તમે એક પેજ પર તમારે જરૂર હોય તેટલા સ્વત્રંત DOM કન્ટેનર ઉમેરી શકો છો.તે સામાન્ય રીતે ખાલી હોય છે - React DOM કન્ટેનર ની અંદર ગમે તે કન્ટેન્ટને રિપ્લેસ કરી શકે છે.
### Step 2: Add the Script Tags {#step-2-add-the-script-tags}

ત્યાર પછી, ત્રણ `<script>` ટેગને HTML પેજમાં `</body>` ટેગ ક્લોઝ થાય તે પેલા ઉમેરો:

```html{5,6,9}
  <!-- ... other HTML ... -->

  <!-- Load React. -->
  <!-- Note: when deploying, replace "development.js" with "production.min.js". -->
  <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>

  <!-- Load our React component. -->
  <script src="like_button.js"></script>

</body>
```

પેલી બે ટેગ React ને લોડ કરે છે.અને ત્રીજી ટેગ તમારા કોમ્પોનેન્ટના કોડને લોડ કરે છે.

### Step 3: Create a React Component {#step-3-create-a-react-component}

HTML પેજ પછી `like_button.js` નામની ફાઇલ બનાવો.

આને **[this starter code](https://gist.github.com/gaearon/0b180827c190fe4fd98b4c7f570ea4a8/raw/b9157ce933c79a4559d2aa9ff3372668cce48de7/LikeButton.js)** ખોલો અને તેને તમે બનાવેલ ફાઈલમાં પેસ્ટ કરો.

>ટીપ
>
>આ કોડમાં Reactનું `LikeButton` નામનું કોમ્પોનેન્ટ ડિફાઇન કરેલ છે. ચિંતા ન કરો જો તમે હમણાં તેને સમજી શકતા નથી -- પછીનાં અમારા [hands-on tutorial](/tutorial/tutorial.html) અને [main concepts guide](/docs/hello-world.html)માં Reactના બિલ્ડીંગ બ્લોક્સને કવર કરી લેશું. હમણાં માટે,
ચાલો તેને સ્ક્રીન પર બતાવીએ !

ત્યાર પછી **[the starter code](https://gist.github.com/gaearon/0b180827c190fe4fd98b4c7f570ea4a8/raw/b9157ce933c79a4559d2aa9ff3372668cce48de7/LikeButton.js)**, `like_button.js`માં છેલ્લે આ બે લાઇન ઉમેરો:

```js{3,4}
// ... the starter code you pasted ...

const domContainer = document.querySelector('#like_button_container');
ReactDOM.render(e(LikeButton), domContainer);
```

આ બે લાઇનનો કોડ પેલા તો `<div>` ને શોધશે જે અમે HTMLમાં એડ કર્યું હતું, અને ત્યાર પછી તેની અંદર React કોમ્પોનેન્ટનું "Like" બટન ડિસ્પ્લે કરશે.
### That's It! {#thats-it}

ત્યાં હવે ચોથુ સ્ટેપ નથી.**You have just added the first React component to your website.**

React ને ઇન્ટિગ્રેટ કરવા માટેની વધુ ટિપ્સ માટે આગળના વિભાગો તપાસો.

**[View the full example source code](https://gist.github.com/gaearon/6668a1f6986742109c00a581ce704605)**

**[Download the full example (2KB zipped)](https://gist.github.com/gaearon/6668a1f6986742109c00a581ce704605/archive/f6c882b6ae18bde42dcf6fdb751aae93495a2275.zip)**

### Tip: Reuse a Component {#tip-reuse-a-component}
 
સામાન્ય રીતે,તમે HTML પેજ પર એક થી વધારે સ્થાને React કોમ્પોનેન્ટ ડિસ્પ્લે કરવા માંગો છો. અહિયાં તેનું ઉદાહરણ છે જે 3 વખત "Like" બટન ડિસ્પ્લે કરે છે અને તેમાં થોડો ડેટા પાસ કરે છે:

[View the full example source code](https://gist.github.com/gaearon/faa67b76a6c47adbab04f739cba7ceda)

[Download the full example (2KB zipped)](https://gist.github.com/gaearon/faa67b76a6c47adbab04f739cba7ceda/archive/9d0dd0ee941fea05fd1357502e5aa348abb84c12.zip)

>નોંધ
>
> આ સ્ટ્રેટજી વધારે ઉપયોગી છે જયારે પેજના React-powered ભાગો એકબીજાથી અલગ છે. React કોડની અંદર,[component composition](/docs/components-and-props.html#composing-components)નો ઉપયોગ કરવો સહેલો છે.

### Tip: Minify JavaScript for Production {#tip-minify-javascript-for-production}

તમારી વેબસાઇટને પ્રોડકશનમાં ડિપ્લોય કરતાં પહેલા, ધ્યાનમાં રાખો કે અનમિનિફાઇડ જાવાસ્ક્રિપ્ટ તમારા યુઝર્સ માટે પેજને નોંધપાત્ર રીતે ધીમું કરી શકે છે.

જો તમે પહેલેથી જ એપ્લિકેશન સ્ક્રિપ્ટને મિનિફાઇ કરેલ છે, **your site will be production-ready** જો તમે એનસ્યોર કરો કે ડિપ્લોય કરેલી HTML `production.min.js` સમાપ્ત થતાં React ના વર્જન લોડ કરે છે:

```js
<script src="https://unpkg.com/react@16/umd/react.production.min.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js" crossorigin></script>
```

જો તમારી પાસે સ્ક્રિપ્ટ મિનીફિકશન માટેના સ્ટેપ નથી તો,[here's one way to set it up](https://gist.github.com/gaearon/42a2ffa41b8319948f9be4076286e1f3).

## Optional: Try React with JSX {#optional-try-react-with-jsx}

ઉપરના આ ઉદાહરણમાં, અમે ફક્ત એવા ફીચર્સ બતાવ્યા છે જે બ્રાઉઝર દ્વારા મૂળ રૂપે સપોર્ટેડ છે.આથી જ જાવાસ્ક્રિપ્ટ ફંક્શન કોલનો ઉપયોગ કરીને આપણે શું દર્શવાવું તે React ને કહેવામાં આવ્યું છે:

```js
const e = React.createElement;

// Display a "Like" <button>
return e(
  'button',
  { onClick: () => this.setState({ liked: true }) },
  'Like'
);
```

જોકે, React તેના કરતાં આનો ઉપયોગ કરવાનો પણ [JSX](/docs/introducing-jsx.html) વિકલ્પ આપે છે:

```js
// Display a "Like" <button>
return (
  <button onClick={() => this.setState({ liked: true })}>
    Like
  </button>
);
```

આ બંને કોડના સ્નિપેસ્ટ સમાન છે. જ્યારે **JSX is [completely optional](/docs/react-without-jsx.html)**, ઘણા લોકોને આ UI કોડ લખવા માટે મદદ રૂપ લાગે છે --બંને React અને બીજી લાઈબ્રેરી સાથે.

You can play with JSX using [this online converter](https://babeljs.io/en/repl#?babili=false&browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=DwIwrgLhD2B2AEcDCAbAlgYwNYF4DeAFAJTw4B88EAFmgM4B0tAphAMoQCGETBe86WJgBMAXJQBOYJvAC-RGWQBQ8FfAAyaQYuAB6cFDhkgA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=es2015%2Creact%2Cstage-2&prettier=false&targets=&version=7.4.3).

અહીંથી તમે JSX નો ઉપયોગ કરી શકો છો [this online converter](https://babeljs.io/en/repl#?babili=false&browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=DwIwrgLhD2B2AEcDCAbAlgYwNYF4DeAFAJTw4B88EAFmgM4B0tAphAMoQCGETBe86WJgBMAXJQBOYJvAC-RGWQBQ8FfAAyaQYuAB6cFDhkgA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=es2015%2Creact%2Cstage-2&prettier=false&targets=&version=7.4.3).

### Quickly Try JSX {#quickly-try-jsx}

તમારા પ્રોજેકટના પેઝમાં  `<script>` ટેગ ઉમેરવી એ JSX try કરવાની સૌથી ઝડપી રીત છે. 

```html

<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

```

હવે તમે `<script>` ટેગમાં `type="text/babel"` એટ્રિબ્યુટનો ઉપયોગ કરીને JSXનો ઉપયોગ કરી શકો છો. અંહીથી તમે [an example HTML file with JSX](https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html) તેને ડાઉનલોડ કરી શકો છો.

આ એપ્રોચ શીખવા અને સિમ્પલ ડેમો create કરવા માટે સારું છે.જો કે તે તમારી વેબસાઇટને ધીમી બનાવે છે અને **isn't suitable for production**. જ્યારે તમે આગળ વધવા માટે તૈયાર હોવ, ત્યારે તમે એડ કરેલા `<script>` ટેગ અને `type="text/babel"` એટ્રિબ્યુટને રીમુવ કરો. તેના બદલે, આગલા વિભાગમાં તમે તમારા બધા `<script>` ટેગ્સ ને ઓટોમેટિક કન્વર્ટ કરવા માટે JSX પ્રોસેસર સેટ કરશો.

### Add JSX to a Project {#add-jsx-to-a-project}

પ્રોજેકટમાં JSX ઉમેરવાથી તેમાં કોમ્પિકેટેડ ટૂલ જેવાકે બન્ડલ અથવા ડેવલપમેન્ટ સર્વરની જરૂર પડતી નથી.જરૂરિયાત મુજબ ,JSX ઉમેરવાથી **is a lot like adding a CSS preprocessor.** તમારા કમ્યુટર પર એકમાત્ર [Node.js](https://nodejs.org/) ઇનસ્ટોલ કરવાની આવશ્યકતા છે.

ટર્મિનલમાંથી તમારા પ્રોજેકટ ફોલ્ડરમાં જાઓ, અને આ બે કમાન્ડ પેસ્ટ કરો:

1. **Step 1:** `npm init -y` રન કરો (જો તે નિષ્ફળ થાય તો [here's a fix](https://gist.github.com/gaearon/246f6380610e262f8a648e3e51cad40d))
2. **Step 2:** `npm install babel-cli@6 babel-preset-react-app@3` રન કરો

>ટીપ
>
>આપણે **using npm here only to install the JSX preprocessor;** તમારે તેની બીજા કોઇ કામ માટે જરૂર નહીં પડે. React અને એપ્લીકેશન કોડ એમ બંને  કોઈ ફેરફાર વગર `<script>` તરીકે રહેશે.

અભિનંદન! તમે તમારા પ્રોજેકટમાં હમણાં જ **production-ready JSX setup**  ઉમેર્યું છે.

### Run JSX Preprocessor {#run-jsx-preprocessor}

`src` નામનું ફોલ્ડર બનાવો અને આ ટર્મિનલ કમાન્ડ રન કરો::
```
npx babel --watch src --out-dir . --presets react-app/prod 
```

>નોંધ 
>
> `npx` એ ટાયપો નથી -- તે આ [package runner tool that comes with npm 5.2+](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) છે.

>જો તમને એરર મેસેજ મળતો હોય જેમાં કહેલું હોય કે "You have mistakenly installed the `babel` package", તો તમે કદાચ પેલું સ્ટેપ ભૂલી ગયા છો    [the previous step]. તેને સેમ ફોલ્ડરમાં પરફોર્મ કરો, અને પાછો પ્રયાસ કરો.
>

તેના સમાપ્ત થવા માટેની રાહ ન જોવો -- આ કમાન્ડ JSX માટે ઓટોમેટેડ વોચર ચાલુ કરે છે.

જો તમે હવે આ `src/like_button.js` નામની ફાઇલ બનાવો છો આની સાથે **[JSX starter code](https://gist.github.com/gaearon/c8e112dc74ac44aac4f673f2c39d19d1/raw/09b951c86c1bf1116af741fa4664511f2f179f0a/like_button.js)**, તો વોચર બ્રાઉઝર માટે યોગ્ય એવા સાદા જાવાસ્ક્રિપ્ટ કોડ સાથે પ્રિપ્રોસેસ્ડ `like_button.js` બનાવશે.

બોનસ તરીકે, આ જૂના બ્રાઉઝરની ચિંતા કર્યા વગર તમને મોર્ડન જાવાસ્ક્રિપ્ટ સિન્ટેક્સ સુવિધાઓનો ઉપયોગ કરવા દે છે.આપણે હમણાં જે ટૂલ વાપર્યુ તેને બેબલ કહે છે, અને તમે તેના વિષે અહીંથી [its documentation](https://babeljs.io/docs/en/babel-cli/) વધારે જાણી શકો છો.

If you notice that you're getting comfortable with build tools and want them to do more for you, [the next section](/docs/create-a-new-react-app.html) describes some of the most popular and approachable toolchains. If not -- those script tags will do just fine!

જો તમે નોટિસ કર્યું હોય કે તમે હવે બિલ્ડ ટૂલ્સ થી કમ્ફર્ટેબલ છો અને તમે તેમાં આગળ વધી શકો છો, તો અહીં [the next section](/docs/create-a-new-react-app.html) કેટલીક સૌથી વધુ પ્રચલિત અને એપ્રોચ કરવા યોગ્ય ટૂલ ચેનનું વર્ણન કરેલ છે. જો ના -- તો આ સ્ક્રિપ્ટ ટેગ તમારા માટે સારું છે!
