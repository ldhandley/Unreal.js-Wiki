UNDER CONSTRUCTION

```js
"use strict"

function main() {
    let extender = new JavascriptExtender
    let context = JavascriptMenuLibrary.NewBindingContext('MenuEx','Test menu','','EditorStyle');
    let commands = new JavascriptUICommands
    commands.BindingContext = context
    commands.Commands = [{
        Id: 'test',
        FriendlyName: 'Unreal.js',
        Description: 'world',
        ActionType: 'Button'
    }]
    commands.Initialize()

    let list = JavascriptMenuLibrary.CreateUICommandList()
    commands.Bind(list)

    console.log("HELO")

    extender.AddToolBarExtension('Content','After',list,builder => {
        console.log('toolbar!!')
        builder.AddToolBarButton(commands.CommandInfos[0])
    })
    let manager = JavascriptEditorLibrary.GetToolBarExtensibilityManager('LevelEditor') 
    manager.AddExtender(extender)
    return function () {
        manager.RemoveExtender(extender)        
        commands.Uninitialize()
        context.Destroy()
    }
}

main()
```