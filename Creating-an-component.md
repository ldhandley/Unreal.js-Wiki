```js
function compile(x) {
  return require('uclass')()(global,x)
}

class MyComponent /*EditInlineNew*/ extends ActorComponent {
  ctor() {
    this.Param1 = 23
    this.Param2 = {X:1,Y:2,Z:3}
  }

  properties() {
    this.Param1/*EditAnywhere+BlueprintReadOnly+Category:Javascript+int*/;
    this.Param2/*EditAnywhere+Category:Javascript+Vector*/;
  }
}

let MyComponent_C = compile(MyComponent)

class MyActor extends Actor {
  ctor() {
    this.MyComponent = MyComponent_C.CreateDefaultSubobject("MyComponent")
  }
  
  properties() {
    this.MyComponent/*VisibleAnywhere+Category:Javascript+MyComponent*/;
  }
}

let MyActor_C = compile(MyActor)
let actor = Actor.C(new MyActor_C(GWorld))
```