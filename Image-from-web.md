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