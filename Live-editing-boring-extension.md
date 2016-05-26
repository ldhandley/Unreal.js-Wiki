`extension-live-boring.js`

```js
/// <reference path="typings/ue.d.ts" />
"use strict"

function main() {
    const UMG = require('UMG')
     
    makeWindow("$window2",
    {
        SizingRule:'AutoSized',  
        Title:'Hello Extension' 
    })(finish => 
    UMG.div({},
        UMG.text({},"Happy hacking"),
        [1,2,3].map(x => UMG.text({},`count ${x}`)),
        UMG(Button,
            {
                OnClicked: finish
            },
            UMG.text({},"Hello Live!") 
        )),        
        null        
    )
    
    return _ => 0         
}  
 
function makeWindow(key,opts) {
    const _ = require('lodash')
    const UMG = require('UMG')
    const I = require('instantiator')
     
    if (!global[key]) {
        let window
        let container
        let widget = I(
            UMG(JavascriptWindow,_.extend(
                {
                    $link:elem => window = elem
                },opts),
                UMG(SizeBox,{$link:elem => container = elem})           
            )  
        )
        widget.TakeWidget().AddWindow()       
         
        let prev
        function add(child) {
            if (prev) {
                container.remove_child(prev) 
            }
            prev = container.add_child(child(finish))
            process.nextTick(_ => window.BringToFront())  
        }       
        
        global[key] = add 
        
        function finish() {
            if (window) {
                window.RequestDestroyWindow()
                window = null
                global[key] = null
            }
        }
    }
    
    return global[key]
}

module.exports = function() {
    try {
        return main()
    } catch (e) {
        console.error(String(e),'got error')
        return _ => null
    }    
}
```