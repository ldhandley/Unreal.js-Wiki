`Actor` can be spawned with `new operator` for convenience. You can also use `BeginSpawningActorFromClass` and `FinishSpawningActor`.

```js
let location = {X:10}
let actor = new Actor(GWorld, location)
function kill() {
  actor.DestroyActor()
}
setTimeout(kill,1000)
```

#### Make your own `AActor`
```js
const uclass = require('uclass')().bind(this,global)
class MySMA extends StaticMeshActor {
  ctor() {
    this.StaticMeshComponent.SetStaticMesh(StaticMesh.Load('/Engine/BasicShapes/Cube.Cube'))
  }
}      
let MySMA_C = uclass(MySMA) 
new MySMA_C(GWorld,{Z:100})
```


**Note**: you can use `process.nextTick(tick)` instead of the `Actor::Tick()` event:

```js
function tick() {
    // do something every tick
    // reschedule it
    process.nextTick(tick)
}

```