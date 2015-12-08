Shared memory

```js
let shm = JavascriptSharedMemoryRegion.Create(
  "TestSharedMemory",
  true/*create*/,true/*read*/,true/*write*/,4096/*bytes*/)
let ab = memory.access(shm)
let fa = new Float32Array(ab)
```

Semaphore

```js
let semaphore = JavascriptSemaphore.Create("TestSemaphore",true/*creatE*/,4/*max-locks*/)
if (semaphore.TryLock(10/*nano seconds*/)) {
  semaphore.Unlock()
}
semaphore.Lock()
semaphore.Unlock()
```