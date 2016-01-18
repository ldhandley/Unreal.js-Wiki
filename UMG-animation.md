```js
let UMG = require('UMG')
let design = UMG.span({},				
    UMG(Button,{id:'test'},UMG.text({id:'text',Font:{Size:150}},"Hello"))									
)

let instantiator = require('instantiator')
let page = instantiator(design)

let animationDriver = require('animation-driver')

let ad = animationDriver()

ad.apply(page.find('test'),{duration:1,loop:1},{
    BackgroundColor : t => ({R:0.5+0.5*Math.sin(Math.PI * 2 * t),A:1}) 
})
ad.apply(page.find('text'),{duration:0.25,loop:5},{
    ColorAndOpacity : t => ({SpecifiedColor:{B:0.5+0.5*Math.sin(3.7*t),A:0.5}}),
    Text : t => t > 0.5 ? "ABC" : "DEF",
    RenderScale : t => ({X:Math.sin(t*Math.PI*2)*0.25+1,Y:Math.sin(t*Math.PI*2)*0.25+1})
})

page.Visibility = 'Visible'

widget.SetRootWidget(page)
widget.AddToViewport()    

return function () {			
    ad.destroy()
    widget.RemoveFromViewport()            	
}
```