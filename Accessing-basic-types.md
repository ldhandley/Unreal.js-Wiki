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

Note: many useful enums are already available in Unreal.js. There are no clever way to add other UE enums: Grab code and paste it guarded with UENUM (for example: [EJavascriptWidgetMode](https://github.com/ncsoft/Unreal.js-core/blob/master/Source/JavascriptEditor/JavascriptEditorLibrary.h#L8)).