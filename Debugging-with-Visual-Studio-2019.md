1. In your script, call 
 - `Context.CreateInspector(9222)` 9229 is default port for Unreal.js, for Chrome devtools its 9222
2. `Attach To Process` in Visual Studio
 - Alt+Ctrl+P : Debug -> `Attach To Process`
 - Set `Connection Type` to `Chrome devtools protocol websocket (no authentication)`
 - Connection target: `ws://localhost[:{port}]` :{port} default is 9222
   - Type 'Enter' or Click `Refresh` to see available processes. 
 - Set `Attach To`: `JavasScript (Node.js 8+) code`
 - Select the `Webkit instance -` process
 - Click `Attach`
3. Set a breakpoint in your script
 - Save your script to force Unreal.js to reload
4. Start Debugging!