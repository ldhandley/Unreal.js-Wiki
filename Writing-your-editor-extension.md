Unreal.js executes automatically `editor.js` with editor enabled environment. 

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