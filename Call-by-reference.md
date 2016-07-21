## Call by reference ##

```js
let isolate = Root.GetOuter().GetOuter()
let stats = isolate.GetHeapStatistics().Statistics    
let stats2 = isolate.GetHeapStatistics(stats).Statistics

console.log(stats, stats2, stats == stats2) 
// [object JavascriptHeapStatistics] [object JavascriptHeapStatistics] true

let x = new Vector(), y = new Vector(), z = new Vector()
x.X = 1
y.X = 2
z.X = 4

let w = x.Add_VectorVector(y, z) // NOTE: z is a ghost argument which is passed by ref to catch return value.
console.log(JSON.stringify(z),'pre')
console.log(JSON.stringify(w),'result',w==z)
console.log(JSON.stringify(z))
// {"X":4,"Y":0,"Z":0} pre
// {"X":3,"Y":0,"Z":0} result
// {"X":3,"Y":0,"Z":0}
```