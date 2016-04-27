- [[Writing your editor extension]]

To play with editor you must have an access to `editor world`.

#### Get the World
```js
let editorWorld = Root.GetEngine().GetEditorWorld()
```

#### Creating an actor
```js
let actor = new StaticMeshActor(editorWorld)
let cubeMesh = StaticMesh.Load('/Engine/BasicShapes/Cube')
actor.RootComponent.SetWorldLocation({Z:123})
actor.StaticMeshComponent.StaticMesh = cubeMesh
```

#### Editor script execution guard
```js
$execEditor( () => {
  // your code goes here to prevent exec-blocking
} )
```

#### Transaction for undo/redo
```js
$execTransaction( "Important operation!", () => {
  yourPreciousTarget.ModifyObject(true)
  yourPreciousTarget.yourPreciousProperty = "ALTERED"
  yourPreciousTarget.yourPreciousMethod()
})
```

### Warning
Editor context is not being cleaned up before map load. So every references to actors belonging to previous map should be cleaned up before map load triggered.
