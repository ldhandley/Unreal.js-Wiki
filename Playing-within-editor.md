- [[Writing your editor extension]]

To play with editor you must have an access to `editor world`.

```js
let editorWorld = Root.GetEngine().GetEditorWorld()
let staticMeshActor = new StaticMeshActor(editorWorld)
staticMeshActor.SetStaticMesh(StaticMesh.Load('/SomeNiceMesh'))
```


