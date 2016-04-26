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

### Function not being called?
```js
$execEditor( () => {
  // your code goes here to prevent exec-blocking
} )

### Warning
Editor context is not being cleaned up before map load. So every references to actors belonging to previous map should be cleaned up before map load triggered.
