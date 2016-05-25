Unlike BP, with Unreal.js you can access all delegates which are reflected as `UPROPERTY`. In blueprint you cannot access single delegate which returns a value, but Unreal.js lets you do.

```js
SomeNiceInstance.SomeNiceMulticastDelegates.Add(delegate-fn)
SomeNiceInstance.SomeNiceMulticastDelegates.Remove(delegate-fn) 
SomeNiceInstance.SomeNiceMulticastDelegates = [delegate-fn]
```

```js
SomeNiceInstance.SomeNiceSinglecastDelegates = delegate-fn
```

There is an another code path for delegate. `FJavascriptFunction` holds reference to javascript function. You can invoke JS function call within your C++ function.

```cpp
void UYourClass::YourMethod(FJavascriptFunction Function)
{
  YourMember.Delegate = Function;
}

void UYourClass::YourEventHandler()
{
  YourMember.Delegate.Execute(); // call JS function
}
```