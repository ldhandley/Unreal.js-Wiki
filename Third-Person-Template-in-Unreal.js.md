Here is the Third Person Template rewritten in Unreal.js.  The example is very close to Unreal C++ format.  There are two files needed for this to work bootstrap.js and zThirdPerson.js.  This code require game assets from ThirdPerson Blueprint template i.e. SK_Mannequin and animations.
  
I'll include the code below.  I have a small post on Unreal forum with pictures how to install.  https://forums.unrealengine.com/showthread.php?122377-Default-Game-Template-using-Unreal-JS


**zThirdPerson.js**

```js
/// <reference path="typings/ue.d.ts">/>

/*
 *  Author: Kiet Khong
 *  Version: UE4 style programming, 
 *  License: MIT, no warranty
 *  Description: This JavaScript file is to implement ThirdPerson Character similar to the engine game template.  
 *  Implement Details: 
 * 
 * 
 */

//  "(function (global){your codes}) (this)" implement closure for zThirdPerson.js script.  
//  It is a cross between private variable and namespace in C++/C#---I think
//  More info at https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

(function (global) 
{
    //Disable some unsafe JavaScript programming practices. 
    //More info at https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode
    "use strict"

    //create Third Person Character from base Character class
    class MyThirdPerson extends Character
    {
        properties()
        {
            //example variables definitions (don't do anything ingame yet')
            this.MyTest /*EditAnywhere+int*/
            this.myArm /*EditAnywhere+SpringArmComponent*/
            this.myCamera /*EditAnywhere+CameraComponent*/
        }

        //constructor for class (this is similar to c++ constructor). Very different from 'Blueprint Construction Script'
        ctor()
        {
            //Set size for collision capsule
            this.CapsuleComponent.CapsuleRadius = 42.0
            this.CapsuleComponent.CapsuleHalfHeight = 96.0
            //this.CapsuleComponent.bVisible = true
            //this.CapsuleComponent.bHiddenInGame = false

            // Don't rotate when the controller rotates. Let that just affect the camera.
            this.bUseControllerRotationPitch = false
            this.bUseControllerRotationRoll = false
            this.bUseControllerRotationYaw = false

            // Configure character movement
            this.CharacterMovement.bOrientRotationToMovement = true // Character moves in the direction of input...
            this.CharacterMovement.RotationRate = Rotator.MakeRotator(0, 0, 540)
            this.CharacterMovement.JumpZVelocity = 600
            this.CharacterMovement.AirControl = 0.2
            
            // Create a camera boom (pulls in towards the player if there is a collision)
            let tempArm = SpringArmComponent.CreateDefaultSubobject("SpringArm")            
            //attach spring arm to character capsule.  Replace SetupAttachment()       
            tempArm.AttachParent = this.CapsuleComponent 
            // The camera follows at this distance behind the character
            tempArm.TargetArmLength = 300.0  
            // Rotate the arm based on the controller 
            tempArm.bUsePawnControlRotation = true        
            //assign spring arm to properties variable 'myArm' for use at runtime
            this.myArm = tempArm   

            //// Create a follow camera named 'TP_Camera'
            let tempCamera = CameraComponent.CreateDefaultSubobject("TP_Camera")  
            //attach 'TP_Camera' to spring arm
            tempCamera.AttachParent = this.myArm
            // Camera does not rotate relative to arm
            tempCamera.bUsePawnControlRotation = false 
            //assign camera to properties variable 'myCamera'
            this.myCamera = tempCamera                                   
            
            //We can load asset directly into JavaScript.  Can be positive or negative depend on your style
            //Load skeletal mesh and animation blueprint from ThirdPerson sample into JavaScript
            //Require assets from ThirdPerson template either Blueprint or C++ will do
            let SK_mesh = SkeletalMesh.Load('/Game/Mannequin/Character/Mesh/SK_Mannequin.SK_Mannequin')
            let ANI_AnimationBP = AnimBlueprint.Load('/Game/Mannequin/Animations/ThirdPerson_AnimBP.ThirdPerson_AnimBP').GeneratedClass

            //set character mesh to the SK_Mannequin
            this.Mesh.SetSkeletalMesh(SK_mesh)

            //set animation class to ThirdPerson_AnimBP
            this.Mesh.SetAnimInstanceClass(ANI_AnimationBP)
           
           //rotate the skeletal mesh so it is facing front
            this.Mesh.RelativeRotation = Rotator.MakeRotator(0, 0, 270)

            //lower the skeletal mesh to the ground
            this.Mesh.RelativeLocation = Vector.MakeVector(0, 0, -96)

        }

        //Event Begin Play
        ReceiveBeginPlay()
        {
            //run any code from base Character class
            super.ReceiveBeginPlay()
            //debug message
            console.log("Begin Play")

            //----force the player controller to possess this pawn    
            //get the current player controller at index 0
            let myPlayerController = GWorld.GetPlayerController(0)

            //possess the MyThirdPerson character that just spawned
            myPlayerController.Possess(this)            
        }

        //spawn new MyThirdPerson when press 't' key
        SpawnNewUnit() /*KeyBinding[t]*/
        {   
            console.log("Spawning new MyThirdPerson character")

            //define spawn location using vector
            let mySpawnLocation = Vector.MakeVector(0, 0, 200)

            //spawn the MyThirdPerson character.  Will fail if there is collision at spawn point
            let myChar = new MyThirdPerson_C(GWorld, mySpawnLocation)   

        }

        //---Input binding start
        Turn(value /*float*/) /*AxisBinding[Turn, -bConsumeInput]*/
        {
            //check if value is valid
            if (value)
            {
                //console.log("Turn", value)
                //add Turn value to controller yaw input
                this.AddControllerYawInput(value)
            }
        }

        LookUp(value /*float*/) /*AxisBinding[LookUp, -bConsumeInput]*/
        {
            if (value)
            {
                //console.log("LookUp", value)
                //add LookUp value to controller pitch input
                this.AddControllerPitchInput(value)
            }
        }

        MoveForward(value /*float*/) /*AxisBinding[MoveForward, -bConsumeInput]*/
        {
            if (value)
            {
                //console.log("MoveForward", value)
                //get pawn control rotation
                let tPawnRotator = this.GetControlRotation()

                //zero out roll and pitch, leaving yaw untouched
                tPawnRotator.Pitch = 0
                tPawnRotator.Roll = 0

                //find forward vector from rotation 
                let tForwardVector = tPawnRotator.GetForwardVector()
                
                //move pawn forward (value > 0) or backward(value < 0)
                this.AddMovementInput(tForwardVector, value, false)

            }
        }

        MoveRight(value /*float*/) /*AxisBinding[MoveRight, -bConsumeInput]*/
        {
            if (value)
            {
                //console.log("MoveRight", value)
                //get pawn control rotation
                let tPawnRotator = this.GetControlRotation()

                //zero out roll and pitch, leaving yaw untouched
                tPawnRotator.Pitch = 0
                tPawnRotator.Roll = 0

                //find right vector from rotation
                let tRightVector = tPawnRotator.GetRightVector()

                //move pawn right (value > 0) or left (value < 0)
                this.AddMovementInput(tRightVector, value, false)
            }
        }


        startJump() /*ActionBinding[Jump,IE_Pressed]*/ 
        {
            //execute Jump function from base Character class
            this.Jump()
            //console.log("Start Jump!!")
        } 

        stopJump() /*ActionBinding[Jump,IE_Released]*/ 
        {
            //execute StopJumping function from base Character class
            this.StopJumping()
            //console.log("Stop Jump!!")
        }        
        //---Input binding end
    }

    //compile MyThirdPerson class
    let MyThirdPerson_C = require('uclass')()(global, MyThirdPerson)

    //  1)hot reload code to run the game inside the editor
    //  2) run initial code 
    function hotReload_Init(){
            //define spawn location using vector
            let mySpawnLocation = Vector.MakeVector(0, 0, 200)

            //spawn the MyThirdPerson character.  Will fail if there is collision at spawn point
            //the MyThirdPerson character object will force possess the player controller in Event Begin Play
            let myChar = new MyThirdPerson_C(GWorld, mySpawnLocation)
    }

    //clean up function for hot reload -- I don't really understand it'
    function hotReload_CleanUp()
    {
        console.log("I am cleanup for live reload")
    }

    // 1) bootstrap to initiate live-reloading dev env. 
    // 2) load required JavaScript files for normal operation
    // 3) run initial code in hotReload_Init
    // 4) REQUIRE bootstrap.js
    try 
    {
        module.exports = () => 
        {
            let cleanup = null

            // wait for map to be loaded. then run hotReload_Init() which spawn the MyThirdPerson character
            process.nextTick(() => cleanup = hotReload_Init());

            // live-reloadable function should return its cleanup function
            return () => hotReload_CleanUp()
        }
    }
    catch (e) 
    {
        //if try code failed then load required JavaScript files
        require('bootstrap')('zThirdPerson')
    }
})(this)

```

**bootstrap.js**
```js
(function (global) {
    "use strict"

    module.exports = function (filename) {

        Context.RunFile('aliases.js')
        Context.RunFile('polyfill/unrealengine.js')
        Context.RunFile('polyfill/timers.js')

        require('devrequire')(filename)
    }
})(this)
```