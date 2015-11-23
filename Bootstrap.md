An actor with `JavascriptComponent` has its own V8 instance. In general there is no need to spawn multiple `JavascriptComponent`. 

`JavascriptComponent` has `ScriptSourceFile` property in which you can specify which `*.js` file to run.