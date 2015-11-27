```js
class MyBox extends StaticMeshActor {
  ctor() {
    this.StaticMeshComponent.SetStaticMesh(StaticMesh.Load('/Game/Geometry/Meshes/1M_Cube.1M_Cube'))
    this.StaticMeshComponent.SetMobility('Movable')
  }
  ReceiveActorBeginCursorOver() {
    super.ReceiveActorBeginCursorOver() // not necessary
    let pos = this.GetActorLocation()
    pos.Z += 10
    this.SetActorLocation(pos)
  }
}

function test() {
  let MyBox_C = require('uclass')()(global,MyBox)
  let box = new MyBox_C(GWorld)
  let PC = GWorld.GetAllActorsOfClass(PlayerController).OutActors[0]
  PC.bEnableMouseOverEvents = true
  PC.bShowMouseCursor = true
  return function () {
    box.DestroyActor()
  }
}
```