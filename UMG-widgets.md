Assuming you are already familiar with `widget.SetRootWidget(page)`,
```js
UMG.text({},"Dummy text")
UMG.div({}, UMG.text({}, "First"), UMG.text({}, "Second"))
UMG.div({}, [1,2,3].map(item => UMG.text({}, `Item: ${item}`)))
UMG.div({}, _ => Math.random() > 0.5 ? UMG.text({}, ">0.5") : UMG.text({}, "<0.5"))
UMG.text({ColorAndOpacity:{SpecifiedColor:{R:1,A:1}}},"RED!")
```