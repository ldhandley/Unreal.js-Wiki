# Simple way to profile your javascript app

Go to [[V8 inspector]]

----

* For serious V8 profiling, add '--prof' to V8 flags in 'Editor - Project Settings - Plugins - UnrealJS - V8 Flags' and restart engine. After shutting down JavascriptIsolate, 'isolate-*-v8.log' will be dumped in 'Engine/Binaries/Win64/...' folder.
1. clone `v8` 
2. `npm i -g http-server`
3. `cd v8/tools` and `http-server` to launch simple web server
4. open `http://localhost:8080/profviz/profviz.html`

* Visit http://v8.googlecode.com/svn/trunk/tools/tick-processor.html, and feed '*-v8.log' to analyze.
 - https://v8.googlecode.com/svn/branches/bleeding_edge/tools/profviz/profviz.html

```js
const sessionName = 'SessionName'
JavascriptProfile.Start(sessionName)

<<< HEAVY WORK LOAD >>>

let profile = JavascriptProfile.Stop(sessionName)

profile.GetTopRootNode().GetFunctionName()

function traverse(node,visit) {
  visit(node)
  _.range(node.GetChildCount()).forEach(index =>
    traverse(node.GetChild(index))
  )
)

traverse(profile.GetTopRootNode(), node => console.log(node.GetFunctionName()))
```