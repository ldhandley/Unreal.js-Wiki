With slate framework you can define your own modal/modeless window with just a few lines of code!

```js
let I = require('instantiator')
let UMG = require('UMG')
let design = UMG(JavascriptWindow, 
  {
    SizingRule:'AutoSized', 
    Title:'Hello Modal dialog'
  },
  UMG(Button, {},
    UMG.text({},"Content")
  )
)
I(design).TakeWidget().EditorAddModalWindow()
```