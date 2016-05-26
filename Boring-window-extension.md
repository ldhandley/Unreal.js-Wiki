`extension-boring.js`

```js
/// <reference path="typings/ue.d.ts" />
"use strict"

function main() {
    const _ = require('lodash')
    const UMG = require('UMG')
    const I = require('instantiator')
    
    let window
    let widget = I(
        UMG(JavascriptWindow,
            {
                SizingRule:'AutoSized', 
                Title:'Hello JS',
                $link:elem => window = elem
            }, 
            UMG(Button,
                {
                    OnClicked: finish
                },
                UMG.text({},"Hello World")
            )
        ) 
    )
    JavascriptSlateWidget.C(widget.TakeWidget()).AddWindow()
    
    function finish() {
        if (window) {
            window.RequestDestroyWindow()
            window = null
        }       
    }
    
    return finish        
}

module.exports = function() {
    try {
        return main()
    } catch (e) {
        console.error(String(e))
        return _ => null
    }    
}
```