```
let UMG = require('UMG')
let instantiator = require('instantiator')

class MyAppWidget extends JavascriptWidget {
  ctor() {
    this.JavascriptContext = this
    this.bSupportsKeyboardFocus = true
  }
}
let MyAppWidget_C = require('uclass')()(global,MyAppWidget)
let PC = GWorld.GetAllActorsOfClass(PlayerController).OutActors[0]
let widget = GWorld.CreateWidget(MyAppWidget_C, PC)
let page = instantiator(UMG.text({},"Hello Unreal.js"))

widget.SetRootWidget(page)
widget.AddToViewport()    
```