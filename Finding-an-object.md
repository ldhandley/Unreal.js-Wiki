```js
let worldDirect = World.Find(null,'/Temp/Untitled_1') 
let worldFromEditorContext = Root.GetEngine().GetEditorWorld()
let worldFromGameContext = GWorld
let coneMesh = StaticMesh.Load('/Engine/BasicShapes/Cone')
let PC = GWorld.GetPlayerController(0)
```