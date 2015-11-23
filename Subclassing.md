```js
class MyUObject extends UObject {
  ctor() {
    this.Prop = 'Good'
  }

  properties() {
    this.Prop/*EditAnyWhere+string*/;
  }
}
let MyUObject_C = require('uclass')()(global,MyUObject)
let instance = new MyUObject()
```

```js
class MyActor extends Actor {
  // overriding existing event
  // function signature is not needed for overriding; 
  // because we already know it!
  ReceiveBeginPlay() {
    super.ReceiveBeginPlay()
    console.log("Hello")
  }
}
let MyUObject_C = require('uclass')()(global,MyActor)
let actor = new MyActor(GWorld)
```