Unreal.js doesn't require any meta data to expose into Javascript because UnrealEngine has already enough information of `UCLASS`, `UPROPERTY` and `UFUNCTION`. So if you want some functions to be used within `*.js`, you may declare a `UBlueprintFunctionLibrary`. This doesn't require the whole engine to be rebuilt.

```c++
class UMyBlueprintFunctionLibrary : public UBlueprintFunctionLibrary
{
  GENERATED_BODY()
public:
  static void ReallyNiceFunction(ASomeSneakyActor* Actor, int Parameter);
];
```

```js
let actor = new ASomeSneakyActor(GWorld)
UMyBlueprintFunctionLibrary.ReallyNiceFunction(actor, 1)
actor.ReallyNiceFunction(1)
```