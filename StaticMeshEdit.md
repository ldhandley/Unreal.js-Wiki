* Requires WITH_EDITOR

```js
let mesh = StaticMesh.Load('/Game/Assets/Meshes/SM_Arch.SM_Arch')
let raw = mesh.LoadRawMesh(0).OutMesh

let package = mesh.GetOuter()
let newMesh = new StaticMesh(package, 'TestMesh', 0x3) // RF_Public | RF_Standalone
newMesh.SourceModels = [{}] // add a model
newMesh.SaveRawMesh(0,raw)
newMesh.Materials  = mesh.Materials
newMesh.Build()
newMesh.MarkPackageDirty()
newMesh.BroadcastAssetCreated()
```