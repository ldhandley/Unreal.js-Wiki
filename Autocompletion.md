Autocompletion support is a huge time-saver of dev. Due to nature of being dynamic-typed language, most of javascript editor doesn't provide full level of support like as C++ has in Visual Studio. 

However, Visual Studio Code provides auto completion for Javascript, only when typing information are given. So Unreal.js has built-in feature which generates typing information of all UnrealEngine entities which are accessible. You can regenerate typings by calling `Context.WriteDTS(path)`.

```js
Context.WriteDTS(Context.Paths[0] + 'typings/ue.d.ts')
```

Once you have got typings, the only thing to have auto completion is adding a line to top of your JS code.

```js
/// <reference path="typings/ue.d.ts">/>
```
