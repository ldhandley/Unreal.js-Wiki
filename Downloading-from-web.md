```js
let req = new JavascriptRequest()
req.SetVerb("GET")
req.SetURL("http://.....zip")
req.OnComplete = (successful) => {
  if (successful) {
    let len = req.GetContentLength()
    let ab = new ArrayBuffer(len)
    memory.bind(ab)
    req.GetContentToMemory()
    req.WriteFile(req.GetDir('GameContent') + 'test.zip')
    memory.unbind(ab)
  }
}
req.OnProgress = (sent,recv) => {
  console.log(`sent ${sent} recv ${recv}`)
}
req.ProcessRequest()
```