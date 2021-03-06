Unreal.js loads extensions automatically. Extension should be devrequired and have name with prefix 'extension'. Unreal.js searches `GameContent/Scripts` recursively to find extensions. 

```js
"use strict"

module.exports = () => {
  console.log("Hello my first editor extension")
  class MyDelegates extends JavascriptGlobalDelegates {
    OnObjectModified(obj) {
      console.log("You just modified",obj.GetName())
    }
  }
  let MyDelegates_C = require('uclass')()(global,MyDelegates)
  let instance = new MyDelegates_C()
  instance.Bind('OnObjectModified')

  return () => {
    instance.UnbindAll()
    console.log("Bye, editor")
  }
}
```

And your `JavascriptComponent` can be running within editor by checking `bActiveWithinEditor`.

There can be several worlds so there is no `GWorld` exposed. Instead of accessing `GWorld`, you can retrieve by calling `Root.GetEngine().GetEditorWorld()`.

### See also

[[EdMode]]
[[EditorViewport]]