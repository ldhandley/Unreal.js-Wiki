*CAUTION*

Dynamic array is not a javascript `Array`. It has only three operations; read, write, `.length`. This should be replaced by full `Array`-compatible implementation.


```js
Something.ArrayProperty = [ 1,2,3 ]; // ok
Something.ArrayProperty.length; // ok
Something.ArrayProperty.push(1); // fail; because Somethign.ArrayProperty just return a new instance of `Array`, so any operations against this array isn't reflected to the *real* array.
Something.ArrayProperty.pop(); // fail; same as above
```