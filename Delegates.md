Unlike BP, with Unreal.js you can access all delegates which are reflected as `UPROPERTY`. In blueprint you cannot access single delegate which returns a value, but Unreal.js lets you do.

```js
SomeNiceInstance.SomeNiceMulticastDelegates.Add(delegate-fn)
SomeNiceInstance.SomeNiceMulticastDelegates.Remove(delegate-fn) 
SomeNiceInstance.SomeNiceMulticastDelegates = [delegate-fn]
```

```js
SomeNiceInstance.SomeNiceSinglecastDelegates = delegate-fn
```