```js
class TestWidget extends JavascriptWidget {
    OnPaint(context) {
        let start = {X:0,Y:0}
        let r = 300
        let t = (new Date() | 0) / 1000
        let end = {X:Math.cos(t)*r,Y:Math.sin(t)*r}
        WidgetBlueprintLibrary.DrawLine(context,start,end,{R:1,A:1},true)                    
    }
}
let TestWidget_C = require('uclass')()(global,TestWidget)
let widget = GWorld.CreateWidget(TestWidget_C)
widget.AddToViewport()
```

You can embed your custom widget into another UMG as a child widget.

```js
let UMG = require('UMG')
let design = UMG(TestWidget_C,{})
```