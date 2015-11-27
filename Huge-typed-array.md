If you have to pass 32k uint8 as input, `TArray` may be too slow. With `ArrayBuffer` and `memory.bind`, data transfer will be blazingly fast.

```js
let ab = new ArrayBuffer(32*1024); // 32K bytes buffer
let u8 = new Uint8Array(ab); // typed array
memory.bind(ab);
GWorld.MySuperMemoryFunction();
memory.unbind(ab);
```

Bound array buffer can be accessed with `FArrayBufferAccessor`. After handshaking with javascript, native handles huge amount of memory safely.

```c++
void UMyBlueprintFunctionLibrary::MySuperMemoryFunction(UWorld* World)
{
    auto size = FArrayBufferAccessor::GetSize();
    auto buffer = FArrayBufferAccessor::GetData();
}
```