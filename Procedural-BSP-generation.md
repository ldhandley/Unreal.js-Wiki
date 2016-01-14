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
    
    function pointlight(P, radius = 160) {
        let t = {
            Translation : P
        }
        let light = world.BeginSpawningActorFromClass(PointLight, t, true)
        light.LightComponent.AttenuationRadius = radius
        light.FinishSpawningActor(t)
    }
    
    function selectOne(obj) {
        engine.GetSelectedObjects().DeselectAll()
        engine.GetSelectedObjects().Select(obj)
    }
    
    function material(path) {
        let mtrl = Material.Load(path)
        
        function create() {
            let mi = world.CreateDynamicMaterialInstance(mtrl)
            let context = {
                vector: (param,value) => {
                    mi.SetVectorParameterValue(param,value)
                    return context        
                },
                selectOne: _ => {
                    selectOne(mi)
                    return context
                }
            }
            return context
        }
        
        return {
            spawn: create,
            selectOne: _ => selectOne(mtrl)
        }            
    }
    
    function transaction(name,fn) {
        (global[name] || []).forEach(actor => {
            try {
                if (actor.IsValid()) {
                    world.EditorDestroyActor(actor)   
                }
            } catch (e)
            {}                
        })
        
        let _ = require('lodash')
        let prev_actors = world.GetAllActorsOfClass(Actor).OutActors
            
        fn()
        
        let new_actors = world.GetAllActorsOfClass(Actor).OutActors
        global[name] = _.difference(new_actors,prev_actors)
        engine.RedrawAllViewports()
    }
    
    function test() {
        const size = 300
        const padding = 10
        const hole = 250;
        
        let mtrl = material('/Game/Color.Color')
        
        let _ = require('lodash')
        _.range(0,10).forEach(i => {                
            mtrl.spawn()
                .vector('color',{
                    R:Math.random(),G:Math.random(),G:Math.random(),
                    A:1})
                .selectOne()
        
            let P = {X:i * (size+padding),Y:i * padding,Z:i * padding}
            cube(size,size,size).moveto(P).add()
            cube(size,hole,hole).moveto(P).subtract()
            
            pointlight(P,80)
        })     
    }
            
    transaction('bspActors',test)   
}    
```