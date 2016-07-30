```
UE4Editor <your uproject> -run=Javascript commandlet.js params
```

commandlet.js
```js
"use strict"

let log = JavascriptLibrary.CreateLogCategory("JS", 'Log')
log.Log('Log','Test')
console.log("Hello commandlet", Root.CmdLineTokens, Root.CmdLineSwitches)
```