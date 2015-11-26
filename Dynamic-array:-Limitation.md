*CAUTION*

Dynamic array is not a javascript `Array`. It has only three operations; read, write, `.length`. This should be replaced by full `Array`-compatible implementation.


```js
Something.ArrayProperty = [ 1,2,3 ]; // ok
Something.ArrayProperty.length; // ok
Something.ArrayProperty.push(1); // fail; 
// because Somethign.ArrayProperty just returns
// a new instance of `Array`, so any operations
// against this array isn't reflected to 
// the *real* array.
Something.ArrayProperty.pop(); // fail; same as above
```

*CAUTION* Current implementation may crash in case of dealing with an array of `USTRUCT`. As a work-around you may serialize and deserialize your array into/from string by using `JSON.stringify`, `JSON.parse`.

eg)
```js
let prev = SomeObject.ArrayOfStruct
prev.push({x:1,y:4})
SomeObject.ArrayOfStruct = prev // May crash
SomeObject.ArrayOfStruct = JSON.parse(JSON.stringify(prev)) // This will be fine
// unless your struct hold references on UObject.
```
