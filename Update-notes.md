2016-04-10

- JavascriptEditorViewport provides basic editor viewport functionality to JS env.
- Fixed crashes, GC bugs related to Editor tab.

2016-04-09

- [json2u](https://github.com/ncsoft/Unreal.js/blob/master/Examples/Content/Scripts/json2u.js) generates corresponding USTRUCT/UCLASS from json-schema, you can edit your favorite json object with PropertyEditor.
- Prebuilt binaries for 4.11.1.

2016-04-08

- Editor extension example updated. (No more jade)

2016-04-03

- Main plugin has been split as a [submodule](https://github.com/ncsoft/Unreal.js-core)

2016-04-01

- Prebuilt binaries for 4.11.0.
- Video tutorial(by [@youdaman](https://twitter.com/Youdaman)) added. [Link to video](https://www.youtube.com/watch?v=QDEy71oiHOg)

2016-03-28

- Prebuilt binaries for 4.11 preview 8.
- Examples updated.

2016-03-27

- Added a new sample 'helloGame', which demonstrates making a multiplayer game with Unreal.js.
- Video tutorial(by [@keyle](https://twitter.com/keyle)) added. [Link to video](https://www.youtube.com/watch?v=XxPSLjBg7DU)

2016-03-12

- Added a new sample 'helloSnippet'. [Link to video](https://youtu.be/Kl4LVaiHqGw) [Link to binary](https://github.com/ncsoft/Unreal.js/archive/snippet-editor.zip)

2016-03-05

- New casting operators which behave like Unreal's `Cast<>`. `Vector({X:1})` gives valid vector struct instance. `Pawn(GWorld)` gives `undefined`. 
```js
Vector({X:1}).Lerp(Vector({Y:1}),0.5).ToLinearColor()
```

- UMG: `JavascriptMultiLineEditableTextBox` added.
```js
UMG(JavascriptMultiLineEditableTextBox, {
    'slot.size.size-rule':'Fill',
    AlwaysShowScrollbars:true, 
    IsReadOnly:true,
    $link:elem =>{
        let layout
        let style = TextBlockStyle({
            Font:{Size:20},
            ColorAndOpacity:{
                SpecifiedColor:{R:1,G:1,B:1,A:1} 
            }
        })
        let style2 = TextBlockStyle({
            Font:{Size:30},
            ColorAndOpacity:{
                SpecifiedColor:{R:1,G:0,B:1,A:1} 
            }
        })
        elem.SetTextDelegate = (text,_layout) => {
            layout = _layout
            _.range(100).forEach(x => {
                let msg = "TESTworld " + x
                let model = new JavascriptTextModel()
                model.SetString(msg)
                
                layout.AddLine(model,[
                    model.CreateRun(style,0,4),
                    model.CreateRun(style2,4,msg.length)
                    ])
            })                        
        }
        let timer = null
        elem.OnVScrollBarUserScrolled = offset => {
            if (timer) {
                clearTimeout(timer)
                timer = null
            }
            timer = setTimeout(_ => {
                timer = null
                elem.ScrollTo(99)
            },500)
        }
    }
})
```

2016-02-29

- No more `git-lfs`.

2016-02-21

- JavascriptProfile added for profiling V8. [[Profiling V8]]
- JavascriptSettings(config) added. V8 flags are configurable!

2016-02-16

- BlueprintLibrary functions with alias for ScriptStructs are now supported. For an example, `KeyEvent.IsAltDown` is now available instead of `KeyEvent.KeyEvent_IsAltDown`.
- BlueprintLibrary factory function is supported. For an example, `EventReply.Handled()` is now available instead of `WidgetBlueprintLibrary.Handled()`.

2016-02-13

- AutoReimport is automatically suppressed not to try to import *.json under Scripts/ folder.

2016-02-10

- FObjectInitializer::SetDefaultSubobjectClass reflected. You can access it within your `prector`. Please check out an example: `helloCharacter.js`.

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