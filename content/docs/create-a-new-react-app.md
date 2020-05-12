---
id: create-a-new-react-app
title: Create a New React App
permalink: docs/create-a-new-react-app.html
redirect_from:
  - "docs/add-react-to-a-new-app.html"
prev: add-react-to-a-website.html
next: cdn-links.html
---


યુઝર અને ડેવલપરના શ્રેષ્ઠ અનુભવ માટે ટૂલચેન નો ઉપયોગ કરો.

આ પેજમાં કેટલીક પોપ્યુલર React ટૂલચેનનું વર્ણન છે જે નીચે આપેલા કાર્યોમાં મદદરૂપ થશે:


* ફાઈલો અને કોમ્પોનેન્ટ પર સ્કેલિંગ કરવા.
* npm થી third-party લાઇબ્રેરીનો ઉપયોગ કરવા.
* વહેલી તકે સામાન્ય ભૂલો શોધી કાઢવા.
* ડેવલોપમેન્ટમાં css અને JS નું Live-editing કરવા.
* પ્રોડકશન માટે આઉટપુટને ઓપટીમાઇઝ કરવા.

આ પેજ પર આ **don't require configuration to get started** ટૂલચેનની ભલામણ કરવામાં આવી છે. 
## You Might Not Need a Toolchain {#you-might-not-need-a-toolchain}

જો તમે ઉપર જણાવેલ સમસ્યાનો અનુભવ કર્યો નથી અથવા જાવાસ્ક્રિપ્ટ ટૂલ્સનો ઉપયોગ કરવો એ તમને પસંદ નથી,તો આ [adding React as a plain `<script>` tag on an HTML page](/docs/add-react-to-a-website.html) ધ્યાનમાં લો, અથવા [with JSX](/docs/add-react-to-a-website.html#optional-try-react-with-jsx).

આ પણ **the easiest way to integrate React into an existing website.** છે જો તમને મદરૂપ લાગે તો તમે હમેંશા એક મોટી ટૂલચેન ઉમેરી શકો છો.

## Recommended Toolchains {#recommended-toolchains}

React ટીમે ખાસ કરીને નીચેનાં સોલ્યુશન માટે ભલામણ કરી છે:

- જો તમે **learning React** અથવા **creating a new [single-page](/docs/glossary.html#single-page-application) app,** તો તમે આ [Create React App](#create-react-app) નો ઉપયોગ કરી શકો.
- જો તમે **server-rendered website with Node.js,** બનાવો છો તો આનો [Next.js](#nextjs) ઉપયોગ કરો.
- જો તમે **static content-oriented website,** બનાવો છો તો આનો [Gatsby](#gatsby) ઉપયોગ કરો.
- જો તમે **component library** અથવા **integrating with an existing codebase**, બનાવો છો તો આનો [More Flexible Toolchains](#more-flexible-toolchains) ઉપયોગ કરો. 


### Create React App {#create-react-app}

[Create React App](https://github.com/facebookincubator/create-react-app) એ **learning React** માટેનું સહાયકારી વાતાવરણ છે,અને Reactમાં આમ કરવા માટેનો આ **a new [single-page](/docs/glossary.html#single-page-application) application**  ક્ષ્રેષ્ઠ વિકલ્પ છે.

તે તમારા ડેવલોપમેન્ટ માટેનું વાતાવરણ નિશ્ચિત કરે છે,જેથી તમે જાવાસ્ક્રિપ્ટની નવી સુવિધાનો ઉપયોગ કરી શકો છો, સારા ડેવલપમેન્ટ માટેનો અનુભવ કરી શકો, અને તે તમારા એપના પ્રોડકશન ને ઓપટીમાઈઝ કરે છે. તમારે તમારા મશીન પર Node >= 8.10 અને npm >= 5.6 જરૂર પડશે. પ્રોજેકટ બનાવવા માટે, રન કરો::


```bash
npx create-react-app my-app
cd my-app
npm start
```

>નોંધ
>
> પ્રથમ લાઇન `npx` એ ટાઇપો નથી -- તે એક [package runner tool that comes with npm 5.2+](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) છે.

Create React App બેકેન્ડ લોજિક અથવા ડેટાબેજને હેન્ડલ કરતી નથી; તે ફક્ત frontend build માટે પાઇપલાઇન બનાવે છે,જેથી તમે તેમનો ઉપયોગ કોઈ પણ બેકેન્ડ સાથે કરી શકો. hood નીચે તે આનો [Babel](https://babeljs.io/) અને [webpack](https://webpack.js.org/) ઉપયોગ કરે છે, પણ તમારે તેના વિષે કઈ જાણવાની જરૂર નથી.

જ્યારે તમે પ્રોડકશન ને ડિપ્લોય કરવા માટે તૈયાર છો ત્યારે `npm run build` રન કરવાથી ત્યારે તે એપ `build` ફોલ્ડરમાંથી ઓપટીમાઈઝ બિલ્ડ બનાવશે.તમે Create React App વિષે વધારે શીખી શકો [from its README](https://github.com/facebookincubator/create-react-app#create-react-app--) and the [User Guide](https://facebook.github.io/create-react-app/).

### Next.js {#nextjs}

[Next.js](https://nextjs.org/) એ **static and server‑rendered applications** માટેનું પોપ્યુલર અને લાઇટવેઇટ React સાથે બનાવેલું ફ્રેમવર્ક છે.તેની અંદર **styling and routing solutions** તેની બોક્સ બહારનું છે, અને ધારો કે  તમે [Node.js](https://nodejs.org/) નો ઉપયોગ સર્વર એન્વાયરીમેન્ટ તરીકે કરી રહ્યા છો.

Next.js અહીંથી [its official guide](https://nextjs.org/learn/) શીખો..

### Gatsby {#gatsby}

[Gatsby](https://www.gatsbyjs.org/) એ React સાથે **static websites** બનાવાનો સૌથી સારો રસ્તો છે.તે તમને React કોમ્પોનેન્ટનો ઉપયોગ કરવા આપે છે,પણ આઉટપુટના ફાસ્ટ લોડીંગ માટે તે HTML અને  CSS ને પ્રિ-રેન્ડર કરે છે.

Gatsby અહીંથી [its official guide](https://www.gatsbyjs.org/docs/) અને અહીંથી [gallery of starter kits](https://www.gatsbyjs.org/docs/gatsby-starters/) શીખો.

### More Flexible Toolchains {#more-flexible-toolchains}

નીચે આપેલા ટૂલચેન્સ વધારે સારી ફ્લેક્સીબિલિટી અને ચોઇસ આપે છે, અમે તેમને વધુ અનુભવી યુઝર્સ માટે ભલામણ કરીએ છીએ..

- **[Neutrino](https://neutrinojs.org/)** એ [webpack](https://webpack.js.org/)ના પાવર ને પ્રિસેટ્સની સિમ્પલિસીટી સાથે જોડે છે,અને તે [React apps](https://neutrinojs.org/packages/react/) અને [React components](https://neutrinojs.org/packages/react-components/) માં પ્રિસેટને સામેલ કરે છે.

- **[Parcel](https://parceljs.org/)** એ ઝડપી, ઝીરો ક્નફીગ્રેશન વેબ એપ્લીકેશન બન્ડલર છે જે [works with React](https://parceljs.org/recipes.html#react).

- **[Razzle](https://github.com/jaredpalmer/razzle)** એ સર્વર-રેન્ડરીંગ ફ્રેમવર્ક છે જેના માટે એક પણ ક્નફીગ્રેશનની જરૂર નથી, પણ તે Next.js કરતાં પણ વધારે ફ્લેક્સીબિલિટી આપે છે. 

## Creating a Toolchain from Scratch {#creating-a-toolchain-from-scratch}

જાવાસસ્ક્રિપ્ટમાં બનેલ ટૂલચેનમાં સામાન્ય રીતે નીચેનું સામેલ છે:

* **package manager**,જેવા કે [Yarn](https://yarnpkg.com/) અથવા [npm](https://www.npmjs.com/). તે તમને થર્ડ-પાર્ટી પેકેજોની વિશાળ ઇકોસિસ્ટમ નો લાભ આપે છે અને તેમને સરળતાથી ઇનસ્ટોલ અને અપડેટ કરી શકાય છે.

* **bundler**, જેવા કે [webpack](https://webpack.js.org/) અથવા [Parcel](https://parceljs.org/). તે તમને મોડયુલર કોડ લખવા અને લોડ ટાઇમને ઓપટીમાઇઝ કરવા માટે નાના પેકેજોને એક બંડલ કરે છે.

* **compiler** જેવું કે [Babel](https://babeljs.io/).તે તમને મોર્ડન જાવાસ્ક્રિપ્ટ માટેનો કોડ લખવા આપે છે જે હજી જૂના બ્રાઉઝર પર વર્ક કરે છે.

જો તમે શરૂઆતથી જ તમારી પોતાની જાવાસ્ક્રિપ્ટ ટૂલચેનનું સેટ અપ માં કરવા માંગો છો, તો [check out this guide](https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658)  તે Create React App ની અમુક ફંકશનાલીટી ને re-create કરે છે.

તમારી કષ્ટમ ટૂલચેનની ખાતરી કરવાનું ભૂલશો નહીં [is correctly set up for production](/docs/optimizing-performance.html#use-the-production-build).
