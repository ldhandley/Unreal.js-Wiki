```js
class YourPC extends PlayerController {
  GodMode() /*Exec*/ {
    console.log("YOU ARE A GOD")
  }
}

let YourPC_C = require('uclass')()(global.YourPC)
Root.GetOuter().PlayerControllerClass = YourPC_C
```

