2016-01-20 

- BlueprintLibraryFunction for UStruct is now accessible as a method of corresponding UStruct itself and its typing(*.d.ts) is auto-generated!
 * Before : `WidgetBlueprintLibrary.EndDragDrop(reply)` 
 * After : `reply.DragDrop()`
 * Before : `KismetMathLibrary.Add_VectorFloat(new Vector(),1)`
 * After : `new Vector().Add_VectorFloat(1)`

2016-01-18

- Animation driver module added for [[UMG animation]]
```js
  let ad = require('animation-driver')
  ad.apply(someWidget,{duration:0.25},{Color:t => ({R:t,A:1})})
```