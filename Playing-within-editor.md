To play with editor you must have an access to `editor world`.

```js
let editorWorld = GEngine.GetEditorWorld()
let staticMeshActor = new StaticMeshActor(editorWorld)
staticMeshActor.SetStaticMesh(StaticMesh.Load('/SomeNiceMesh'))
```