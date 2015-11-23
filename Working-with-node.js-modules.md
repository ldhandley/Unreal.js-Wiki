Unreal.js provides `require` function which is a crucial element to live along node.js modules. But Unreal.js is not a node.js, so there are no `net`, `fs`, `process`, `http`, ...

Only small amount of functions are provided including timer functions(`setTimeout`, `clearTimeout`, ...), `process.nextTick` and `fs.readFileSync`(which reads UTF8 only).

But modules in node.js are designed to be shallow, so most of modules are just usable! :+1: 

