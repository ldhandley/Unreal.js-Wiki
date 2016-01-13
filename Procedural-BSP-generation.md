```js
function bsp() {
    let engine = Root.GetEngine()
    let world = engine.GetEditorWorld() 
    
    function brushbuilder(type) {
        let builder = engine.FindBrushBuilder(type)
        let context = { fn:_ => _ }
        function prepare() {
            if (world.$lastBrushBuilder == context) return
            context.fn(builder)
            builder.Build(world)
            world.$lastBrushBuilder = context
        }
        function exec(command) {
            prepare()
            engine.Exec(world,`brush ${command}`)
            return context
        }
        context.moveto = location => exec(`moveto x=${location.X || 0} y=${location.Y || 0} z=${location.Z || 0}`)
        context.add = _ => exec('add')
        context.subtract = _ => exec('subtract')
        context.set = fn => {
            context.fn = fn
            return context
        }
        return context
    } 
    
    function cube(x,y,z) {
        return brushbuilder(CubeBuilder).set(bb => {
            bb.X = x
            bb.Y = y
            bb.Z = z
        })              
    }       
    
    function test() {
        const size = 300
        const padding = 10
        const hole = 250; 
        
        (global.bspActors || []).forEach(actor => {
            try {
                if (actor.IsValid()) {
                    world.EditorDestroyActor(actor)   
                }
            } catch (e)
            {}                
        })
            
        let mtrl = Material.Load('/Game/Color.Color')
        
        let _ = require('lodash')
        let prev_actors = world.GetAllActorsOfClass(Actor).OutActors
        _.range(0,10).forEach(i => {
            let mi = world.CreateDynamicMaterialInstance(mtrl)
            let color = {R:Math.random(),G:Math.random(),G:Math.random(),A:1}
            mi.SetVectorParameterValue('color', color)
            engine.GetSelectedObjects().DeselectAll()
            engine.GetSelectedObjects().Select(mi)
        
            let P = {X:i * (size+padding),Y:i * padding,Z:i * padding}
            cube(size,size,size).moveto(P).add()
            cube(size,hole,hole).moveto(P).subtract()
            
            let t = {
                Translation : P
            }
            let light = world.BeginSpawningActorFromClass(PointLight, t, true)
            light.LightComponent.AttenuationRadius = 160
            light.FinishSpawningActor(t)
        })     
        let new_actors = world.GetAllActorsOfClass(Actor).OutActors
        global.bspActors = _.difference(new_actors,prev_actors)
        engine.RedrawAllViewports()
    }
            
    test()   
}
```