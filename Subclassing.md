- [[USTRUCT and UCLASS]]
- [[UPROPERTY]]
- [[Creating a component]]
- [[Creating a widget]]

You can subclass any UClass like creating a blueprint in the editor. Just like blueprints, given class is transformed into `JavascriptGeneratedClass` by `require('class')()(global,SourceClass)`. 

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

  Client_PlayFX(effect/*string*/) /*NetMulticast*/ {
    console.log("fire!")
  }
}
let MyUObject_C = require('uclass')()(global,MyActor)
let actor = new MyActor(GWorld)
```

You may create a class derived from a blueprint. 

```js
class MyBPChild extends Blueprint.Load('/Game/MyBP').GeneratedClass {
}
```

*CAUTION* Inheritance from Javascript class is not supported yet. 