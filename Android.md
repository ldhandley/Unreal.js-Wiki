```js
class MyTextRenderActor extends TextRenderActor {
  ctor() {
    let comp = ApplicationLifecycleComponent.CreateDefaultSubobject("Lifecycle")
    comp.ApplicationHasEnteredForegroundDelegate.Add(() => {
      this.TextRender.SetText("App foreground")
    })
  }
}
```