Listening to the log output is easy. 
```js
class MyOutputDevice extends JavascriptOutputDevice {
  OnMessage(message, verbosity, category) {
    // handle messages
  }
}
let MyOutputDevice_C = require('uclass')()(global,MyOutputDevice)
let myOutputDevice = new MyOutputDevice_C()
// myOutputDevice.Kill() ; to dispose
```

```js
let msgEvent = new require('events').EventEmitter
class MyOutputDevice extends JavascriptOutputDevice {
  OnMessage(message, verbosity, category) {
    msgEvent.emit('msg',[message,verbosity,category])
  }
}
let MyOutputDevice_C = require('uclass')()(global,MyOutputDevice)
let myOutputDevice = new MyOutputDevice_C()

let theConsole = UMG.div({$link:elem => {
  msgEvent.on('msg',array => {
    elem.add_child(UMG.span({},
      array.map(item => UMG.text({},item))
    ))
  })
}, 
  UMG(EditableText,{
    OnTextCommitted: text => {
      eval(text)
    }
  })
)

let consoleWidget = require('instantiator')(theConsole)
```