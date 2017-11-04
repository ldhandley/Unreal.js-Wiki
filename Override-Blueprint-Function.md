```js
// "MyActor" should be replaced with the Blueprint that you want

class MyActor extends Blueprint.Load('/Game/MyActor').GeneratedClass { 
    // "/Game/(Path to BP)" "/Game/" can be seen as Content in Unreal's browser

    Function_To_Override() {

        return; 
    }
}

var MyActor_C = require('uclass')()(global, MyActor);

function main() { //main function thats defined at buttom
    if (GWorld.IsServer) { //executes only on server / host
        var actor = new MyActor_C(GWorld, { X: 1 }); //creates the actor

        return () => {
            actor.DestroyActor();
        }
    }
}

try { //setup / init
    module.exports = () => {
        var t = main();

        return function () {
            t();
        }
    }
}
catch (e) {
    require('bootstrap')('BP_Function_Override'); // replace "BP_Function_Override" with the js file name
}
```