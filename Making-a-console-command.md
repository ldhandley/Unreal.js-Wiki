```js
class YourPC extends PlayerController {
  GodMode(args/*string*/) /*Exec*/ {
    console.log("YOU ARE A GOD", args)
  }
}

let YourPC_C = require('uclass')()(global.YourPC)
Root.GetOuter().PlayerControllerClass = YourPC_C
```

