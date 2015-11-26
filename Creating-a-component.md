You can add components just like you can do with native c++ constructor using `ComponentClassName.CreateDefaultSubject`. Note that your root component should be hold within `UPROPERTY`.

```js
class MyActor extends Actor {
  ctor() {
    let someComp = WidgetComponent.CreateDefaultSubobject("WidgetComponent0")
    this.SetRootComponent(someComp)
    this.Comp = someComp
  }

  properties() {
    this.Comp/*WidgetComponent*/;
  }
}
```