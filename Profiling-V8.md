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