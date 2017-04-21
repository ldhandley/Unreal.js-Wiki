https://github.com/ncsoft/Unreal.js/issues/111

```js
let Compile = function(x) {  
    return require('uclass')()(global, x);
}

class CustomComponent extends MeshComponent {
    ctor() { }

    properties() {
        this.X /*EditAnywhere+int*/;
    }
}

let CustomComponentClass = Compile(CustomComponent)

class CustomActor extends Actor {
    ctor() {
        console.log("CustomActor ctor")

        this.Root = SceneComponent.CreateDefaultSubobject("ActorRootComponent")
        this.SetRootComponent(this.Root)

        this.CustomComponent = CustomComponentClass.CreateDefaultSubobject("CustomComponent")
        this.CustomComponent.AttachTo(this.Root)
    }

    properties() {
        this.Root /*VisibleAnywhere+BlueprintReadOnly+SceneComponent*/;
        this.CustomComponent /*VisibleAnywhere+BlueprintReadOnly+MeshComponent*/;
    }
}
```