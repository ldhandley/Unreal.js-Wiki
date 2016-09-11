The code below create a custom actor (myTimeActor) that print "myTimeActor: Printing Message" every second.  This is done by using the SetTimerbyFunctionName().  More details is in the code.

```js
/// <reference path="typings/ue.d.ts">/>

/*
    Description: Create an actor that print a text to screen every second
    Detail: Implemented using Unreal Framework

*/

class myTimeActor extends Actor
{
    //overload Event Begin Play
    ReceiveBeginPlay()
    {
        //how often the timer will trigger in second
        let timeInterval = 1.0
        //set whether timer should loop
        let bLoop = true
        //set a timer on this actor
        this.SetTimerbyFunctionName('printMyText', timeInterval, bLoop)
    }

    //create a new UFUNCTION name printMyText
    //the /*BlueprintCallable*/ comment is a UFUNCTION specifier 
    //and must exist to create a new function from javascript
    
    //more UFUNCTION specifier can be found here 
    //https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/Reference/Functions/Specifiers/index.html
    printMyText() /*BlueprintCallable*/
    {
        //print a text to the screen
        GWorld.PrintText("myTimeActor: Printing Message", true, false, LinearColor.MakeColor(0,0,1,1), 3)
    }
}

//compile myTimeActor
let myTimeActor_C = require('uclass')()(global, myTimeActor) 

//create an actor into the world, can fail if collide at spawn point
let myActor = new myTimeActor_C(GWorld, Vector.MakeVector(0, 0, 10))

//need aliases.js for SetTimerbyFunctionName to be recognized
Context.RunFile('aliases.js')

```

Alternative way to create a timer in node.js/browser like way,
```js
setInterval( () => { console.log('hello') }, 1000 )
```