```js
let req = new JavascriptHttpRequest()
req.SetVerb("GET")
req.SetURL("http://.....zip")
req.OnComplete.Add( (successful) => {
  if (successful) {
    let len = req.GetContentLength()
    let ab = new ArrayBuffer(len)
    // pass array buffer to Unreal.js native
    memory.bind(ab)
    // copy content into the array buffer
    req.GetContentToMemory()
    // request to write down buffer into file
    req.WriteFile(req.GetDir('GameContent') + 'test.zip')
    // we're done
    memory.unbind(ab)
  }
})
req.OnProgress.Add( (sent,recv) => {
  console.log(`sent ${sent} recv ${recv}`)
})
req.ProcessRequest()
```