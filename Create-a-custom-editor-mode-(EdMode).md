To create a custom [editor mode](https://docs.unrealengine.com/latest/INT/Engine/UI/LevelEditor/Modes/index.html):

```
const StyleSetName = 'JSEdmode'
const UMG = require('UMG')
const instantiator = require('instantiator')

module.exports = function () {
	console.log("HELLO")
	let edmode = new JavascriptEdMode()
	edmode.ModeId = "JSMode"
	edmode.ModeName = "JSMode"
	edmode.SlateIcon = {
		StyleSetName : 'UnrealJS',
		StyleName : 'SpiralGenerator.Purge',
	} 
	edmode.bVisible = true
	edmode.PriorityOrder = 999
	edmode.OnGetContent = _ => {
		var design = UMG.div({},
			UMG.text({},"Hello UMG 123"),
			UMG(Button,{OnClicked:_ => console.log("CLICK")},"Hello")
		)
		return instantiator(design)
	}
	edmode.Register()
	global.edmode = edmode
	console.log("HELLO")
	return _ => { 
		edmode.Unregister()
	}
}
```
Look at [JavascriptEdMode.h](https://github.com/ncsoft/Unreal.js-core/blob/1f86fa5a324a3e9f317cb4a775b1b9ec62249e35/Source/JavascriptEditor/JavascriptEdMode.h) and [JavascriptEdMode.cpp](JavascriptEdMode.cpp) to learn more about creating custom EdModes.