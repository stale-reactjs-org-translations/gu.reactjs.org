---
title: એક Stateful Component
order: 1
domid: timer-example
---

ઇનપુટ ડેટા (`this.props` દ્વારા મેળવેલ) લેવા ઉપરાંત, component આંતરિક state ડેટા (`this.state` દ્વારા મેળવેલ) જાળવી શકે છે. જ્યારે કોઈ component ના state ડેટા બદલાશે, ત્યારે   `render()` ફરીથી ઈન્વોક થઇ રેન્ડર કરેલ માર્કઅપને અપડેટ કરશે.