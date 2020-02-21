1. In your script, call 
 - `Context.CreateInspector(9222)` 9229 is default port for Unreal.js, for Chrome devtools its 9222
2. Attach in Visual Studio
 - Debug -> `Attach To Process`
 - Set `Connection Type` to `Chrome devtools protocol websocket (no authentication)`
 - Connection target: `ws://localhost[:{port}]` :{port} is optional if CreateInspector was set to 9222
 - Click `Refresh`
 - Set `Attach To`: `JavasScript (Node.js 8+) code`
 - Select the `Webkit instance -` process
 - Click `Attach`
3. Set a breakpoint in your script
 - Save your script to force Unreal.js to reload
4. Start Debugging!