TL;DR
```js
let ad = require('animation-driver')
ad.apply(someWidget,{duration:0.25},{Color:t => ({R:t,A:1})})
```

```js
let UMG = require('UMG')
let instantiator = require('instantiator')
let animationDriver = require('animation-driver')

let design = UMG.span({},				
    UMG(Button,{id:'test'},UMG.text({id:'text',Font:{Size:150}},"Hello"))									
)
let page = instantiator(design)
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