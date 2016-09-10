Here is the First Person Template rewritten in Unreal.js. The example is very close to Unreal C++ format. There are two files needed for this to work bootstrap.js and zFirstPerson.js. This code require game assets from FirstPerson Blueprint template i.e. SK_Mannequin_Arms, sounds and animations.

I'll include the code below. I have a small post on Unreal forum with pictures how to install the Third Person template, but the installation process should be very similar. https://forums.unrealengine.com/showthread.php?122377-Default-Game-Template-using-Unreal-JS

**zFirstPerson.js**

```java
/// <reference path="typings/ue.d.ts">/>

/*
 *  Author: Kiet Khong
 *  Version: UE4 style programming, 
 *  License: MIT, no warranty
 *  Description: This java file is to implement FirstPerson Character similar to the engine game template.  
 *  Implement Details: Require assets from FirstPerson Blueprint templates
 * 
 * 
 */

//  "(function (global){your codes}) (this)" implement closure for zFirstPerson.js script.  
//  It is a cross between private variable and namespace in C++/C#---I think
//  More info at https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

(function (global) 
{
    //Disable some unsafe java programming practices. 
    //More info at https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode
    "use strict"

    //first person Character
    class myFirstPerson extends Character
    {
        properties()
        {
            this.myCamera /*EditAnywhere+CameraComponent*/
            this.myFPMesh /*EditAnywhere+SkeletalMeshComponent*/
            this.myFPGunMesh /*EditAnywhere+SkeletalMeshComponent*/

            this.fireSound /*EditAnywhere+SoundBase*/
            this.fireAnimation /*EditAnywhere+AnimMontage*/

            this.gunOffset /*EditAnywhere+Vector*/
            this.weaponRange /*EditAnywhere+float*/
            this.weaponDamage /*EditAnywhere+float*/
        }

        //constructor for class (this is similar to c++ constructor). Very different from 'Blueprint Construction Script'
        ctor()
        {
            //Set size for collision capsule
            this.CapsuleComponent.CapsuleRadius = 42.0
            this.CapsuleComponent.CapsuleHalfHeight = 96.0
            //this.CapsuleComponent.bVisible = true
            //this.CapsuleComponent.bHiddenInGame = false

            // Create a CameraComponent named 'FP_Camera'
            let tempCamera = CameraComponent.CreateDefaultSubobject("FP_Camera")  
            //attach 'FP_Camera' to capsule
            tempCamera.AttachParent = this.CapsuleComponent
            //change relative location
            tempCamera.RelativeLocation = Vector.MakeVector(0, 0, 64)
            // Camera rotate the myFirstPerson character?
            tempCamera.bUsePawnControlRotation = true 
            //assign camera to properties variable 'myCamera'
            this.myCamera = tempCamera       

            //create first person mesh
            let tempFPMesh = SkeletalMeshComponent.CreateDefaultSubobject("FP_Mesh")
            //make only owner can see first person arms, turn off shadows
            tempFPMesh.bOnlyOwnerSee = true
            tempFPMesh.AttachParent = this.myCamera
            tempFPMesh.bCastDynamicShadow = false
            tempFPMesh.CastShadow = false
            //initialize first person position and rotation to look right
            tempFPMesh.RelativeLocation = Vector.MakeVector(0, -4, -156)
            tempFPMesh.RelativeRotation = Rotator.MakeRotator(5, 2, -20)
            //assign mesh to Unreal properties variable for use during runtime
            this.myFPMesh = tempFPMesh

            //create gun mesh component
            let tempFPGunMesh = SkeletalMeshComponent.CreateDefaultSubobject("FPGun_Mesh")
            //make only owner can see first person gun, turn off shadows
            //in first person shooter game there is another mesh usually called 3rd person mesh 
            //the 3rd person mesh is what is shown in game to other players 
            tempFPGunMesh.bOnlyOwnerSee = true
            tempFPGunMesh.bCastDynamicShadow = false
            tempFPGunMesh.CastShadow = false
            tempFPGunMesh.AttachParent = this.myFPMesh
            tempFPGunMesh.AttachSocketName = "GripPoint"
            //assign mesh to Unreal properties variable for use during runtime
            this.myFPGunMesh = tempFPGunMesh

            //load assets from editor.  REQUIRE assets from FirstPerson Blueprint template
            let FP_mesh = SkeletalMesh.Load('/Game/FirstPerson/Character/Mesh/SK_Mannequin_Arms.SK_Mannequin_Arms')
            let FPGun_mesh = SkeletalMesh.Load('/Game/FirstPerson/FPWeapon/Mesh/SK_FPGun.SK_FPGun')
            let ANI_AnimationBP = AnimBlueprint.Load('/Game/FirstPerson/Animations/FirstPerson_animBP.FirstPerson_AnimBP').GeneratedClass
            this.fireSound = SoundBase.Load('/Game/FirstPerson/Audio/FirstPersonTemplateWeaponFire02.FirstPersonTemplateWeaponFire02')
            this.fireAnimation = AnimMontage.Load('/Game/FirstPerson/Animations/FirstPersonFire_Montage.FirstPersonFire_Montage')

            //set loaded assets into class mesh
            this.myFPMesh.SetSkeletalMesh(FP_mesh)
            this.myFPGunMesh.SetSkeletalMesh(FPGun_mesh)

            //set loaded animation blueprint into class
            this.myFPMesh.SetAnimInstanceClass(ANI_AnimationBP) 

            //initialize weapon properties data
            this.weaponRange = 5000
            this.weaponDamage = 500000
            this.gunOffset = Vector.MakeVector(100, 30, 10)

        }

        //Event Begin Play
        ReceiveBeginPlay()
        {
            console.log("myFirstPerson Begin Play")

            //force player controller to possess myFirstPerson character
            GWorld.GetPlayerController(0).Possess(this)
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
                //move pawn forward (value > 0) or backward(value < 0)
                this.AddMovementInput(this.GetActorForwardVector(), value, false)
            }
        }
 
        MoveRight(value /*float*/) /*AxisBinding[MoveRight, -bConsumeInput]*/
        {
            if (value)
            {
                //console.log("MoveRight", value)

                //move pawn right (value > 0) or left (value < 0)
                this.AddMovementInput(this.GetActorRightVector(), value, false)
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

        onFire() /*ActionBinding[Fire, IE_Pressed]*/
        {
            console.log("shooting projectile")

            // Play a sound if there is one
            if (this.fireSound)
            {
                GWorld.PlaySoundAtLocation(this.fireSound, this.GetActorLocation(), Rotator.MakeRotator(0,0,0), 1, 1, 0)
            }

            // try and play a firing animation if specified
            if (this.fireAnimation)
            {
                let tempAnimInstance = this.myFPMesh.GetAnimInstance();
                tempAnimInstance.Montage_Play(this.fireAnimation, 1)
            }

            //simplified raytrace, trace from player camera traight forward by weaponRange (5000 cm)
            //cast this.myCamera into CameraComponent for autocomplete features in Visual Studio Code
            let tempCamera = CameraComponent.C(this.myCamera)

            //get camera world location
            let tempStartTrace = tempCamera.GetWorldLocation()

            //end location is start location + weaponrange(5000 cm) unit forward
            let tempForwardDirection = tempCamera.GetWorldRotation().GetForwardVector()
            let tempOffset = tempForwardDirection.Multiply_VectorFloat(this.weaponRange)
            let tempEndTrace = Vector.Add_VectorVector(tempStartTrace, tempOffset)

            //console.log(tempStartTrace.ToString(), " + ", tempOffset.ToString(), " = ", tempEndTrace.ToString())

            //create a HitResult to store trace result 
            let tempHitResult = HitResult.C(HitResult.MakeHitResult())

            //line trace and return result into tempHitResult
            //'TraceTypeQuery1' is the 'Visibility' channel
            //'TraceTypeQuery2' is the 'Camera' channel
            GWorld.LineTraceByChannel(tempStartTrace, tempEndTrace, 'TraceTypeQuery2', false, [this], 'ForDuration', tempHitResult, true, LinearColor.MakeColor(1, 0, 0), LinearColor.MakeColor(1, 0, 0), 3)

            //console.log("hitresult = ", tempHitResult.bBlockingHit)
            
            //store hit actor and component from HitResult
            let damageActor = tempHitResult.Actor
            let damageComponent = tempHitResult.Component

            //if actor&component is valid while simulating physic then apply physic impulse
            if (damageActor != null && damageComponent != null && damageComponent.IsSimulatingPhysics())
            {
                //console.log("Hitting a physic enabled actor = ", damageActor, ", of component = ", damageComponent.ToString(), "at location =>", tempHitResult.ImpactPoint.ToString())
                
                //calculate physic impulse from this.weaponDamage
                let tempImpulseVector = tempForwardDirection.Multiply_VectorFloat(this.weaponDamage)

                //apply physic impulse
                damageComponent.AddImpulseAtLocation(tempImpulseVector, tempHitResult.ImpactPoint)
            }
            //in a real game, a gun trace would require 2 traces, 
            //1st trace start from the camera and extend x distance forward.  The goal is to check if player can hit anything, 
            //the 2nd trace is from the muzzle of the gun to the hit location, just to make sure nothing is between the gun muzzle to hit location

        }

        //---Input binding end

    }

    //compile myFirstPerson class
    let myFirstPerson_C = require('uclass')()(global, myFirstPerson)

    //  1)hot reload code to run the game inside the editor
    //  2) run initial code 
    function hotReload_Init()
    {
            //print text to screen
            GWorld.PrintText("Loading zFirstPerson.js", true, true, LinearColor.MakeColor(1,0,0,1), 3)
            //define spawn location using vector
            let mySpawnLocation = Vector.MakeVector(0, 0, 200)

            //spawn the myFirstPerson_C character.  
            //Will fail if there is collision at spawn point
            //the myFirstPerson_C character object will force possess the player controller in Event Begin Play
            let myChar = new myFirstPerson_C(GWorld, mySpawnLocation)
    }

    //clean up function for hot reload -- I don't really understand it'
    function hotReload_CleanUp()
    {
        console.log("I am cleanup for live reload")
    }

    // 1) bootstrap to initiate live-reloading dev env. 
    // 2) load required java files for normal operation
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
        //if try code failed then load required java files
        require('bootstrap')('zFirstPerson')
    }

})(this)
```

bootstrap.js
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