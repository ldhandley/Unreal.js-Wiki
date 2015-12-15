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


