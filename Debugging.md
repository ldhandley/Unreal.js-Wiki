Unreal.js implements debuggee feature which allows to be debugged remotely. You can debug live unreal.js code with Visual Studio Code. 

First, tag JavascriptContext which you want to debug by calling `Context.SetAsDebugContext()`.
Then, launch a remote debug remote session in Visual Studio Code by connecting `localhost:5858`.

You can also debug your application in UE4Editor. Within `JavascriptConsole` you can freely evaluate your global scope variables, so just expose your debuggee variable into global scope like below.

```js
(function (global) {
  let actor = new Actor(GWorld)
  global.my_debuggee = actor
})(this)
```

You can inspect `my_debuggee` in your `JavascriptConsole`, which can be opened with `Tools - Developer - JavascriptConsole`.

```js
> my_debuggee.ToString()
< "Actor_1"
```