You can access huge array within UStruct/UClass as an array buffer.

```js
let mesh = StaticMesh.Load('/Game/Assets/Meshes/SM_Arch.SM_Arch').LoadRawMesh(0).OutMesh
mesh.$memaccess('VertexPositions',ab => {
  let fa = new Float32Array(ab)
  console.log('you have float32 typed array',fa)
})
```

## See also
- [[StaticMeshEdit]]