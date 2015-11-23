You can activate/deactivate `JavascriptConsole` by clicking `Windows - Developer Tools - JavascriptConsole`. This window implements basic functions of modern browser's console. There can be one or more `JavascriptContext` running, so you can select `JavascriptContext` in dropdown list.

*TIP*
You may pass an object which needs to be inspected run-time by exposing it as a global var.

```js
global.XYZ = 'This is the magic string I want to inspect'
```

And then you can inspect the object by typing 'XYZ' in console window.