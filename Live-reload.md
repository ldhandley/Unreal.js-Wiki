Live reload is not a black magic. It just monitor files and trigger some action.

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