You can download an image from web and use it as a `UTexture2D`. UnrealEngine has a helper object doing this job, `AsyncTaskDownloadImage`.

```js
const url = "http://www.blogcdn.com/massively.joystiq.com/media/2013/03/ncsoft.jpg"
let job = AsyncTaskDownloadImage.DownloadImage(url)
let texture = null
job.OnSuccess = (_texture) => texture = _texture

class MyHUD extends HUD {
  ReceiveDrawHUD() {
    super.ReceiveDrawHUD()

    this.Canvas.DrawTexture(
      texture,
      {X:0,Y:0},{X:200,Y:200}, // screen
      {X:0,Y:0},{X:1,Y:1}, // texture
      {R:1,G:1,B:1,A:1},'BLEND_Opaque'
    )
  }
}
```

## Using promises
```
function webimageCache() {
    let cached = {}
    let pending = {}
    function webimage(url) {
        if (cached[url]) {
            return Promise.resolve(cached[url])
        } else if (pending[url]) {
            return pending[url]
        } else {
            let Resolve, Reject                    
            let p = new Promise((resolve,reject) => {
                Resolve = resolve
                Reject = reject
            })
            pending[url] = p
            let job = AsyncTaskDownloadImage.DownloadImage(url)
            let texture = null                
            job.OnSuccess = (texture) => {
                cached[url] = texture
                delete pending[url]
                Resolve(texture)            
            }
            job.OnFail = (reason) => {                    
                delete pending[url]
                Reject(texture)
            }
            return p
        }
    }
    return webimage
}
```