2019-09-07
 - Update to support 4.23

2019-05-03
 - V8-7.4.288 (Win64, Mac, Linux, Android, iOS)
   - Jit-less V8 (Support iOS)

2019-04-04
 - Update to support 4.22
   - modified v8 library (Need to download a new v8 library)
     - unreal.js uses the UnrealEngine allocator, and due to changes in the implementation of TBB, v8 had to be fixed.

2018-12-04
 - Update to support 4.21

2018-08-30
 - Update to support 4.20

2018-03-31
- Fix for Property Name Issue (FName)
  - https://github.com/ncsoft/Unreal.js/wiki/Access-Property

2018-03-21
- Update to support 4.19
- V8-6.5.254 (Win64, Mac, Linux)
  - Starting with V8 6.1, the Console is built in and provides faster logging. However, because it is not logging through a Global Object created in Unreal.js, a single Isolate does not provide more than one Logger. **So you can not log Inspector and Editor at the same time.**

2017-10-30
- Updated to support 4.18.

2017-09-13
- Temporary downgrade v8 version (6.1 -> 5.9) (Builtin Console Issue)

2017-09-08
- Updated to support 4.16, 4.17 (Marketplace)

2017-08-26
- V8-6.1.534 (Win64, Mac, Linux)

2017-08-17
- Updated to support 4.17.

2017-05-28
- Updated to support 4.16. 

2017-04-30
- V8-5.9.221 (Win64, Mac)

2017-04-19

- Updated to support 4.15. (Marketplace)

2017-04-05

- UEnumProperty (4.15)

2017-02-17

- Updated to support 4.15.

2016-12-24

- Chrome Inspector is now available for non editor build.

2016-12-23

- Add graph editor library. 

2016-12-12

- V8 5.7.201. 
- Fix [[inspector | V8 inspector]] for Mac, which has 4-bytes TCHAR!

2016-12-05

- [[V8 inspector]]. (https://github.com/ncsoft/Unreal.js-core/tree/v8inspector)

2016-12-03

- Made use of function parameter default value specified in C++.

2016-11-30

- Added `FJavascriptRef` which contains reference to Javascript object, so you can safely keep reference to js-object.

2016-11-28

- Added stats. (STAT_xxx)

2016-11-19

- Added naive support for Map/Set property.

2016-11-17

- Updated to support 4.14.
- Switched back to 5.5-lkgr.
- Removed JavascriptWebSocket.

2016-10-26

- Updated V8 to 5.6.140(Chrome canary).
- Switched to static v8 libraries for MacOS.

2016-09-17

- Merged PR from [@arthursw](https://github.com/arthursw)
 - Added bindings to JavascriptEditorViewport 
- Added new branch [V8 5.5.225](https://github.com/ncsoft/Unreal.js-core/tree/V8-5.5.225).

2016-09-07

- Fixed GC crash. (4.13)

2016-08-31

- Missing [[UPROPERTY]] decorators added.

2016-07-29

- JavascriptAutomatedTest added. [[Automated test]]
- Package find, load, save, delete added.

2016-07-28

- JavascriptCommandlet added. [[Commandlet]]
  * `UE4Editor.exe <your-project> -run=Javascript commandlet.js`

2016-07-27

- Uncaught exceptions are routed to `global.$uncaughtException`.
- VS2015 Update 2 compilation issue resolved.

2016-07-23

- Shell scripts added for easy installation of v8 libraries. `install-v8-libs.sh`, `install-v8-libs.bat`.
- UI Extender exposed. (Currently, `LevelEditor` is the only available end-point.) [Wiki](https://github.com/ncsoft/Unreal.js/wiki/Extending-editor-toolbar-menu-...)

2016-07-22

- Experimental V8 5.3.332.19 (in V8-5.3.332.19 branch)
- Call by ref(UStruct) [[Call by reference]]
- Can specify return value(by ref) not to allocate temporary variables.

2016-07-19

- 'v8' module exposed, which has only one method `v8.setFlagsFromString`.
- Bug fix: JavascriptActor can have JavascriptComponent subobjects.
- FJavascriptFunction can be called outside normal javascript context.
- FJavascriptStreamableManager exposed.

2016-07-14

- Smoother GC (supports IdleTask to enable hitch-aware GC)

2016-07-02

- V8 heapsnapshot dump by `memory.takeSnapshot(filename)`. See [[Heap profiling]]

2016-06-07

- Fixed a crash related to debugging.

2016-06-06

- Added directory manipulation ops.
- Added experimental package control. [source](https://github.com/ncsoft/Unreal.js/blob/master/Examples/Content/Scripts/extension-exampleWindow.js)

2016-06-04

- Added compatibility for 4.11.2

2016-06-02

- Migrated to 4.12.

2016-05-31

- Switched to MIT License.

2016-05-26

- [Ractive.js](https://github.com/ncsoft/Unreal.js/blob/master/Examples/Content/Scripts/helloRactive.js) dynamic binding example added.

2016-05-25

- [[Modal-dialog-in-Editor]]: `SWindow` for modal/modeless dialog. 

2016-05-24

- V8 5.1.300

2016-05-17

- Fixed a bug which was introduced during support for JS class inheritance.
- [[StaticMeshEdit]]: Added support for StaticMesh creation.
- [[Huge array fast access]]: Typed array access added.

2016-05-15

- Upgrading V8 to 5.1.300
 * https://github.com/ncsoft/Unreal.js-core/tree/V8-5.1.300
 * https://github.com/ncsoft/Unreal.js-core/releases/tag/v8-5.1.300-win64

2016-05-11

- Decorators(instanced, editinline, ...) for array inner property.
- inheritance from JS class(experimental).

2016-05-06

- Fix for V8 5.0: @HACK for Weird JS inheritance. instance of inherited class has invalid `__proto__`. This fixes #72(Mac build).

2016-05-01

- Now supports mac. (V8 4.8.271)
- `FJavascriptFunction` added which allows callback js func from C++/BP. This is needed for scoped struct instance. (eg. FMultiBoxBuilder, ...)

2016-04-28

- Binary updated

2016-04-26

- EdMode can be extended with Javascript! 

2016-04-22

- JavascriptTreeView retains GC-ref for generated UWidgets not to cause a crash. (JavascriptListView isn't fixed yet)

2016-04-21

- Update build for 4.11.2
- Features to build editor extension added.

2016-04-16

- Editor tab improvements (Mostly about GC, crashes)

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