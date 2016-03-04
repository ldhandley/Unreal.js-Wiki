* For serious V8 profiling, add '--prof' to V8 flags in 'Editor - Project Settings - Plugins - UnrealJS - V8 Flags' and restart engine. After shutting down JavascriptIsolate, 'isolate-*-v8.log' will be dumped in 'Engine/Binaries/Win64/...' folder.
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