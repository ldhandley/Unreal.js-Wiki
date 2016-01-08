```js
class TestWidget extends JavascriptWidget {
  ctor() {
    this.Test = _ => console.log("default delegate")
  }
  AddChild(x) {
    this.SetRootWidget(x)
    return {}
  }
  OnMouseMove() {
    this.Test()
  }
}

let TestWidget_C = require('uclass')()(global,TestWidget)
let UMG = require('UMG')
function controller(scope) {
  scope.test_func = (arg) => console.log('hello from jade',arg)
}
let page = UMG.app(design,controller)
...
```

```jade
TestWidget(fn.Test="test_func(1)")
  div Hello Test
```