```js
   class MyTextRenderActor extends TextRenderActor {
        ctor() {
            this.AppComponent = ApplicationLifecycleComponent.CreateDefaultSubobject("Lifecycle")
            this.AppComponent.ApplicationHasEnteredForegroundDelegate.Add(() => {
                this.TextRender.SetText("App foreground")
            })
        }
    }
```