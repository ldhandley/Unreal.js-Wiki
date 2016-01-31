`Actor` can be spawned with `new operator` for convenience. You can also use `BeginSpawningActorFromClass` and `FinishSpawningActor`.

```js
let location = {X:10}
let actor = new Actor(GWorld, location)
function kill() {
  actor.DestroyActor()
}
setTimeout(kill,1000)
```

```js
let transform = {Translation:{X:1}}
let actor = GWorld.BeginSpawningActor(StaticMeshActor,transform)
actor.StaticMeshComponent.SetStaticMesh(StaticMesh.Load('/NiceMesh'))
actor.FinishSpawningActor(transform)
```