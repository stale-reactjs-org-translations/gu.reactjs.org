---
id: create-a-new-react-app
title: ન​વો React App બનાવો
permalink: docs/create-a-new-react-app.html
redirect_from:
  - "docs/add-react-to-a-new-app.html"
prev: add-react-to-a-website.html
next: cdn-links.html  
---
શ્રેષ્ઠ વપરાશ અને વિકાસ ના અનુભવ માટે integrated toolchain નો ઉપયોગ કરો.

આ page કેટલીક લોકપ્રિય React toolchains નુ વર્ણન છે જે નીચે અપેલ​ જેવા કાર્યોમા સહાય કરે છે:

* અનેક files અને components ની ગોઠવણ.
* npm તરફ થી third-party libraries વપર​વા માટે.
* સામાન્ય ભૂલો ને વહેલી તકે શોધી કાઢવા .
* Development સમયે CSS અને JS નુ live-editing.
* Production માટે output નુ optimizing.

આ page પર સૂચવેલ toolchains **પ્રારંભ કરવા માટે ગોઠવણીની જરૂર નથી**.

## તમને કોઈ toolchain ની જરૂર નથી {#you-might-not-need-a-toolchain}

જો તમે ઉપર વર્ણવેલ સમસ્યાઓનો અનુભવ કરતા નથી અથવા JavaScript tools નો ઉપયોગ કરીને હજી સુધી આરામદાયક નથી અનુભવતા, તો [React ને plain `<script>` tag તરિકે HTML page મા ઉમેરો ](/docs/add-react-to-a-website.html)અથ​વા [JSX સાથે ](/docs/add-react-to-a-website.html#optional-try-react-with-jsx).

આ **વર્તમાન Website મા React ને એકીકૃત સૌથી સહેલો રસ્તો છે.** જો તમને મદદરૂપ લાગે તો તમે હંમેશાં એક મોટી toolchain ઉમેરી શકો છો!

## ભલામણ કરેલ Toolchains {#recommended-toolchains}

React ટીમ મુખ્યત્વે આ ઉકેલોની ભલામણ કરે છે:

- જો તમે **React શીખી રહ્યા છો** અથ​વા **ન​વો  [single-page](/docs/glossary.html#single-page-application) app બનાવી રહ્યા છો,** તો વપરો [React App બનાવો](#create-react-app).
- જો તમે **Node.js સાથે server-rendered કરેલી website બનાવી રહ્યા છો**, તો [Next.js](#nextjs). નો પ્રયાસ કરો
- જો તમે **સ્થિર content-oriented website બનાવી રહ્યા છો, તો** [Gatsby](#gatsby) અજમાવો.
- જો તમે **component library બનાવી રહ્યા છો**  અથવા **અસ્તિત્વમાંના codebase સાથે સંકલન કર​વા**, [More Flexible Toolchains](#more-flexible-toolchains) અજમાવો.

### React App બનાવો {#create-react-app}

[Create React App](https://github.com/facebookincubator/create-react-app)  **React શીખવા** માટે આરામદાયક વાતાવરણ છે, અને React મા **નવી [single-page](/docs/glossary.html#single-page-application) Application** બનાવવાનું પ્રારંભ કરવાનો શ્રેષ્ઠ માર્ગ છે

તે તમારા development environment સેટ કરે છે જેથી તમે નવીનતમ JavaScript સુવિધાઓનો ઉપયોગ કરી શકો, એક સરસ developer અનુભવ પ્રદાન કરી શકો અને production માટે તમારી એપ્લિકેશનને optimizes કરી શકો. તમારે તમારા machine પર [Node>= 8.10 અને npm>= 5.6](https://nodejs.org/en/) રાખવાની જરૂર પડશે. પ્રોજેક્ટ બનાવવા માટે, ચલાવો:

<<<<<<< HEAD
=======
It sets up your development environment so that you can use the latest JavaScript features, provides a nice developer experience, and optimizes your app for production. You’ll need to have [Node >= 14.0.0 and npm >= 5.6](https://nodejs.org/en/) on your machine. To create a project, run:
>>>>>>> 17ad2cbc71f4c1fcc3f3f9ae528bfd292a9fced7

```bash
npx create-react-app my-app
cd my-app
npm start
```

>નોંધ
>
>પ્રથમ લાઇન પરનો `npx` typo નથી -- તે એક [package runner tool છે જે npm 5.2+ સાથે આવે છે](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b).

React App backend logic અથવા database ને નિયંત્રિત કરતી નથી; તે ફક્ત frontend build pipeline બનાવે છે, જેથી તમે તેનો ઉપયોગ કોઈપણ backend સાથે કરી શકો. hood હેઠળ, તે [Babel](https://babeljs.io/) અને [webpack](https://webpack.js.org/) ઉપયોગ કરે છે, પરંતુ તમારે તેમના વિશે કંઈપણ જાણવાની જરૂર નથી.

જ્યારે તમે production deploy કર​વા માટે તૈયાર છો, ત્યારે `npm run build`ચલાવ​વા થી `build` folder મા તમારા app માટે optimized build બન​વી દેશે. તમે React application બનાવવા વિશે વધુ શીખી શકો છો [તેના README માંથી](https://github.com/facebookincubator/create-react-app#create-react-app--) અને તેની [User Guide માંથી](https://facebook.github.io/create-react-app/)

### Next.js {#nextjs}

[Next.js](https://nextjs.org/) એક React સાથે **static અને server‑rendered applications** સાથે માટે ની એક લોકપ્રિય અને lightweigth framwork છે. તેમાં **styling અને routing solutions** out of the box છે, અને ધારે છે કે તમે [Node.js](https://nodejs.org/) ને server environment તરીકે ઉપયોગ કરી રહ્યાં છો.

શીખો Next.js [તેની official guide](https://nextjs.org/learn/) માંથી.

### Gatsby {#gatsby}

React સાથે static website બનાવવાનો શ્રેષ્ઠ માર્ગ [Gatsby](https://www.gatsbyjs.org/) છે. તે તમને React components નો ઉપયોગ કરવા દે છે, પરંતુ ઝડપી લોડ સમયની બાંયધરી આપવા માટે પ્રી રેન્ડર કરેલા HTML અને CSS ને આઉટપુટ આપે છે.

શીખો Gatsby [તેની official guide](https://www.gatsbyjs.org/docs/) અથવા [gallery of starter kits](https://www.gatsbyjs.org/docs/gatsby-starters/) માંથી.

### વધુ Flexible Toolchains {#more-flexible-toolchains}

નીચે આપેલ toolchains વધુ સુગમતા અને પસંદગી પ્રદાન કરે છે. અમે તેમને વધુ અનુભવી વપરાશકર્તાઓ માટે ભલામણ કરીએ છીએ:

- **[Neutrino](https://neutrinojs.org/)** preset ની સરળતા સાથે [webpack](https://webpack.js.org/) ની શક્તિને જોડે છે, અને તેમાં [React apps](https://neutrinojs.org/packages/react/) અને [React components](https://neutrinojs.org/packages/react-components/) માટેનો preset શામેલ છે.

- React, Next.js, [Express](https://expressjs.com/) અને વધુ માટે built-in support સાથે, **[Nx](https://nx.dev/react)** એક full-stack monorepo developmentસ માટે toolkit છે.

<<<<<<< HEAD
- **[Parcel](https://parceljs.org/)** એ એક ઝડપી, શૂન્ય રૂપરેખાંકન web application bundler છે જે React સાથે કાર્ય કરે છે.
=======
- **[Parcel](https://parceljs.org/)** is a fast, zero configuration web application bundler that [works with React](https://parceljs.org/recipes/react/).
>>>>>>> 17ad2cbc71f4c1fcc3f3f9ae528bfd292a9fced7

- **[Razzle](https://github.com/jaredpalmer/razzle)** એ server-rendering framework છે જેને કોઈ પણ ગોઠવણીની જરૂર નથી, પરંતુ Next.js કરતા વધુ સુગમતા આપે છે.

## શરૂઆતથી toolchain બનાવવી {#creating-a-toolchain-from-scratch}

Javascript build toolchain સામાન્ય રીતે શામેલ છે:

* [Yarn](https://yarnpkg.com/) અથવા [npm](https://www.npmjs.com/) જેવા **package manager**. તે તમને third-party packages ના વિશાળ ecosystem લાભ લઈ શકે છે અને તેમને સરળતાથી install અથવા update કરી શકે છે.

* **bundler**, જેમ કે [webpack](https://webpack.js.org/) અથવા [Parcel](https://parceljs.org/). તે તમને modular cod લખવા અને લોડ ટાઇમને optimize કરવા માટે તેને નાના packages bundle કરવા દે છે.

* [Babel](https://babeljs.io/) જેવા **compiler**. તે તમને આધુનિક JavaScript code લખવા દે છે જે હજી પણ જૂના browsers કાર્ય કરે છે.

જો તમે શરૂઆતથી જ Javascript toolchain set કરવાનું પસંદ કરો છો, તો [આ માર્ગદર્શિકા તપાસો](https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658) કે જે કેટલાક બનાવો React applicationન કાર્યક્ષમતાને ફરીથી બનાવે છે.

તમારું custom toolchain [ઉત્પાદન માટે યોગ્ય રીતે સેટ કરેલું છે](/docs/optimizing-performance.html#use-the-production-build) તેની ખાતરી કરવાનું ભૂલશો નહીં.
