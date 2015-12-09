Unreal.js executes automatically `editor.js` with editor enabled environment, so you may put your own `editor.js` in `/Game/Content/Scripts`. 

```js
(function (global) {
  "use strict"
  function main() {
    try {
      console.log("Hello editor")
      return function () {}
    } catch (e) {
      console.error(String(e))
      return function () {}
    }
  }
  try {
    module.exports = () => {
      let cleanup = null
      process.nextTick(() => cleanup = main())
      return () => cleanup()
    }
  } catch(e) {
    require('bootstrap')('editor')
  }
})(this)
```

And your `JavascriptComponent` can be running within editor by checking `bActiveWithinEditor`.

There can be several worlds so there is no `GWorld` exposed. Instead of accessing `GWorld`, you can retrieve by calling `Root.GetEngine().GetEditorWorld()`.