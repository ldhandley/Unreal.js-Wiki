2016-02-05

- WebSocket added
- `memory.exec(array-buffer, transaction-fn)` added. Old `memory.bind` and `memory.unbind` are deprecated now for cleaner api.

2016-01-26

- $execEditor added
 * `FEditorScriptExecutionGuard` equivalent in JS.
   - `$execEditor(_ => your_secret_editor_code_goes_here)`

2016-01-25

- Animation driver updates
 * `animdriver.apply(,{warm:true},...)` for warm start, which calls apply(t=0) immediately.
 * `animdriver.apply(,{$access:(target,key) => return target.yourOwnSetFunction.bind(target,key)},...)`
   * This update enables animation driver support non UMG targets.
- `require` bug fix.
 * `package.json` can point entry javascript file without `.js` extension.

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