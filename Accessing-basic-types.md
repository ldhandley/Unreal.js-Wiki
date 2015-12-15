```js
let actor = new StaticMeshActor(GWorld)

// structs(vector)
let loc = actor.GetActorLocation()
console.log(loc.X, loc.Y, loc.Z)
console.log(JSON.stringify(loc,null,2))
actor.SetActorLocation({Z:100})

// enum
actor.NavigationGeometryGathingMode = ENavDataGatheringMode.Instant
actor.NavigationGeometryGathingMode = 'default'
console.log(ENavDataGatheringMode.map((x) => `Enums! ${x}`))
```