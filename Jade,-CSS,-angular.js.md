**Pseudo angular is deprecated. Stay tuned for React-UMG.**

Creating UI for massive multiplayer games are cumbersome because there are so many pages and controls to create and maintain. UI is the domain of Web technologies. Just imagine modern web tech + UMG.

Unreal.js provides `jade-umg`, so you can layout UMG with jade. :+1: Furthermore, Unreal.js has `pseudo-angular.js`, which is a (imperfect) clone of angular.js for UMG. Because Unreal.js doesn't have DOM which all browsers have, the wheel was needed to be reinvented. 

```jade
div(fn.init="value = false")
  text your value is {{value}}
  Button(fn.on-clicked="value = !value")
    Border(BrushColor=({R:0.5,G:0.5,A:0.9})
      text This is a nice button
```
