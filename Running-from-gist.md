This snippet demonstrates 'downloadable program'.

```js
const url = "https://gist.githubusercontent.com/nakosung/815d203d8f44e7f4a9ca/raw/"

let req = new JavascriptHttpRequest()
req.SetVerb("GET")
req.SetURL(url)
req.OnComplete.Add((success) => {
  if (success) {
    eval(req.GetContentAsString())
  } else {
    console.error(req.GetResponseCode())
  }
})
req.ProcessRequest()
```

To invalidate cache everytime,
```js
const url = `https://gist.githubusercontent.com/nakosung/815d203d8f44e7f4a9ca/raw?random=${Math.random}`
```