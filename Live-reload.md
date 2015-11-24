Live reload is not a black magic. It just monitors files and triggers some action. You can limit live-reload scope by implementing your own logic. eg. `devjade.js` is monitoring jade files and refreshes only UI widgets.

main.js
```js
require('devrequire')('myApp')
```

myApp.js
```js
module.exports = function() {
  console.log("initializing")
  let actor = new Actor(GWorld)
  return function() {
    console.log("uninitializing")
    actor.DestroyActor()
  }
}
```

If `init/uninit` pair doesn't match, there will be `logic leakage`. 