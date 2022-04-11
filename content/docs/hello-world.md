---
id: hello-world
title: Hello World
permalink: docs/hello-world.html
prev: cdn-links.html
next: introducing-jsx.html
---

સૌથી નાનો React ઉદાહરણ આના જેવો દેખાય છે.

<<<<<<< HEAD
```js
ReactDOM.render(
  <h1>Hello World</h1>,
  document.getElementById('root')
);
=======
```jsx
ReactDOM
  .createRoot(document.getElementById('root'))
  .render(<h1>Hello, world!</h1>);
>>>>>>> 84ad3308338e2bb819f4f24fa8e9dfeeffaa970b
```

તે પેજ પર "Hello World" લખેલું શીર્ષક દર્શાવે છે.

**[Try it on CodePen](https://codepen.io/gaearon/pen/rrpgNB?editors=1010)**

ઑનલાઇન એડિટર ખોલવા માટે ઉપરની લિંકને ક્લિક કરો. નિશ્ચિન્ત રહી કેટલાક ફેરફારો કરો, અને જુઓ કે કેવી રીતે તે આઉટપુટ પર અસર કરે છે. આ ગાઇડમાં મોટાભાગના પેજમાં આના જેવા એડિટેબલ ઉદાહરણો હશે.


## ગાઇડ કેવી રીતે વાંચશો {#how-to-read-this-guide}


આ ગાઇડમાં, આપણે React એપ્સના બિલ્ડિંગ બ્લોક્સ વિશે જાણીશું: Elements અને Components. એકવાર તમે તેમને શીખ્યા પછી, તમે નાના, ફરીથી વાપરી શકાય તેવા કોમ્પોનેન્ટ્સનો ઉપયોગ કરીને જટિલ એપ્લિકેશનો બનાવી શકો છો.

>ટિપ
>
>આ ગાઇડ એવા લોકો માટે બનાવવામાં આવી છે જે **ક્રમશઃ શીખવાનું** પસંદ કરે છે. જો તમે વ્યવહારુ ઉદાહરણો દ્વારા શીખવાનું પસંદ કરો છો, તો અમારા [પ્રેકટિકલ ટ્યૂટોરિઅલ](/tutorial/tutorial.html) જુઓ. તમને આ ગાઇડ અને ટ્યુટોરીયલ એકબીજાનાં પૂરક લાગશે.


આ ક્રમશઃ ગાઇડમાં પ્રથમ પ્રકરણ છે React ના મેઈન કોન્સેપ્ટ્સ. તમે નેવિગેશન સાઇડબારમાં તેના બધા પ્રકરણોનું લિસ્ટ જોઈ શકો છો. જો તમે મોબાઇલથી આ વાંચી રહ્યાં છો, તો તમે તમારી સ્ક્રીનની જમણી બાજુ નીચે આપેલા બટનને દબાવી નેવિગેશનને ઍક્સેસ કરી શકો છો.


આ ગાઇડમાં દરેક પ્રકરણ અગાઉના પ્રકરણોમાં રજૂ કરેલા નોલેજ પર આધારિત છે. **સાઇડબારમાં દેખાતા "મેઈન કોન્સેપ્ટ્સ" પ્રકરણો ક્રમમાં વાંચીને જ, તમે મોટા ભાગનું React શીખી શકો છો.** ઉદાહરણ તરીકે, [“JSX નો પરિચય”](/docs/introducing-jsx.html) એ આ પછીનું પ્રકરણ છે.

## નોલેજ લેવલની ધારણાઓ {#knowledge-level-assumptions}

React JavaScript Library છે, અને તેથી અમે માનીએ છીએ કે તમને JavaScript ભાષાની મૂળભૂત સમજ છે. **જો તમને આત્મવિશ્વાસ ન હોય, તો અમે ભલામણ કરીએ છીએ કે [આ JavaScript ટ્યુટોરીયલ વાંચી](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript) તમારા નોલેજ લેવલને ચકાસો** અને કોઈપણ ગૂંચવણો વગર આ ગાઇડને અનુસરવા માટે તમને સક્ષમ બનાવશો. તમે 30 મિનિટ અને એક કલાકની વચ્ચે પૂર્ણ કરી શકો છો, અને પરિણામે તમને એવું લાગશે નહીં કે તમે એક જ સમયે React અને JavaScript બંને શીખી રહ્યાં છો.

>નૉૅધ
>
<<<<<<< HEAD
>આ ગાઇડ, ક્યારેક ઉદાહરણોમાંના કેટલાક નવા JavaScript સિન્ટેક્ષનો ઉપયોગ કરે છે. જો તમે છેલ્લા થોડા વર્ષોમાં JavaScript સાથે કામ કર્યું ન હોય, તો [આ ત્રણ મુદ્દાઓ](https://gist.github.com/gaearon/683e676101005de0add59e8bb345340c) તમને વધુ પરિચિત બનાવશે.
=======
>This guide occasionally uses some newer JavaScript syntax in the examples. If you haven't worked with JavaScript in the last few years, [these three points](https://gist.github.com/gaearon/683e676101005de0add59e8bb345340c) should get you most of the way.
>>>>>>> 84ad3308338e2bb819f4f24fa8e9dfeeffaa970b


## ચાલો, શરુ કરીએ! {#lets-get-started}

નીચે સ્ક્રોલ કરવાનું ચાલુ રાખો, અને વેબસાઇટ ફૂટરની પહેલાં તમને [આ ગાઇડના આગલા પ્રકરણ](/docs/introducing-jsx.html) ની લિંક મળશે.


