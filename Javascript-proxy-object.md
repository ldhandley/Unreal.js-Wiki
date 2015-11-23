`UObject`s are living in UnrealEngine and being reflected into JavaScript as `proxy` objects. Every instance you access in JavaScript is a proxy object which holds a reference to a underlying `UObject`. But even proxy object is capable of having extra data because it is a form of JavaScript `object`.

```js
let obj = new USomeUnrealObject()
obj.NotDeclaredWithinEngine = { x:1, y:2 }

let parent = new USomeParentUnrealObject()
parent.ObjectPropertyVar = obj

// This works!
console.log(parent.ObjectProperty.NotDeclaredWithinEngine) 
```

Proxy objects are mortal by design(to save memory footprint), so it can be GC'ed at any time. This may introduce some chaos.

```js
let parent = null

(function() {
  let obj = new USomeUnrealObject()
  obj.NotDeclaredWithinEngine = { x:1, y:2 }

  parent = new USomeParentUnrealObject()
  parent.ObjectPropertyVar = obj
})()

// Hey V8, please gc!
gc()

// This doesn't work!
console.log(parent.ObjectProperty.NotDeclaredWithinEngine) 
```

To avoid this inconsistency, proxy objects should be kept in somewhere to tell V8 that these objects cannot be GC'ed.

```js
let parent = null
let precious = []

(function() {
  let obj = new USomeUnrealObject()
  obj.NotDeclaredWithinEngine = { x:1, y:2 }

  precious.push(obj)

  parent = new USomeParentUnrealObject()
  parent.ObjectPropertyVar = obj
})()

// Hey V8, please gc!
gc()

// This works again!
console.log(parent.ObjectProperty.NotDeclaredWithinEngine) 
```