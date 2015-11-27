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

You cannot modify an existing element in a array.

```js
Something.ArrayOfStruct = [{X:1},{Y:1},{Z:1}]
assert(Something.ArrayOfStruct[0].X == 1) // pass
Something.ArrayOfStruct[0].X = 2
assert(Something.ArrayOfStruct[0].X == 2) // fail
```
