1. Open the `YourUEProject/Content/Scripts` folder in the Visual Studio Code Explorer (Ctrl+Shift+E, or first button on the left toolbar)
2. Go to debug view (Ctrl+Shift+D or last button in left toolbar)
3. Click on the Configure gear icon on the Debug view top bar, choose your debug environment and VS Code will generate a launch.json file under your workspace's .vscode folder.
4. The default settings should be fine. There must be two configurations, the second one is what we need:


        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "localhost",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }

5. Let your JavascriptContext to be set as debug context (in UE Javascript console) with `Context.SetAsDebugContext()`
 - Warning: you should set the correct javascript console.
 - To debug a game: 
 - Start your game (Play button) 
 - _Shift + F1_ to have access to the mouse, type `Context.SetAsDebugContext()` in the correct javascript console
6. Start your debug session with F5 or the play button.

That's all!