[Slate in C++](https://docs.unrealengine.com/latest/INT/Programming/Slate/Widgets/) easily translates to UMG.js:

***C++***
```
[...]
ChildSlot
[
    SNew(SVerticalBox)
    + SVerticalBox::Slot()
    [
        SNew(STextBlock).Text(FText::FromString("A text"))
    ]
    + SVerticalBox::Slot()
    [
        SNew(SCheckBox)
        .IsChecked(this, &SPBMainWidget::HandleCheckBoxIsChecked, &SPBMainWidget::bCheckboxValue)
        .OnCheckStateChanged(this, &SPBMainWidget::OnCheckBoxChanged, &SPBMainWidget::bCheckboxValue)
        [
            SNew(STextBlock).Text(FText::FromString("A checkbox"))
        ]
    ]
    + SVerticalBox::Slot().AutoHeight()
    [
        SNew( SSpinBox<float> )
        .Delta(1)
        .MinValue(-10000.0)
        .MaxValue(10000.0)
        .MinSliderValue(-500)
        .MaxSliderValue(500)
        .Value( this, &SPBMainWidget::OnGetSpinBoxValue )
        .OnValueChanged( this, &SPBMainWidget::OnGetSpinBoxChanged )
    ]
]

```
***UMG.js***

```js
UMG.div({
        Visibility: 'Visible',
        $link: elem => this.GUIElem = elem,   // save the GUI element to change it later
        $unlink: elem => this.GUIElem = null
    },
    UMG.text({}, "A text"),
    UMG(CheckBox, { IsChecked: _ => this.HandleCheckBoxIsChecked() , OnCheckStateChanged: Value => this.OnCheckBoxChanged() }, "A checkbox"),
    UMG(SpinBox, { Delta: 1, MinValue: -10000.0, MaxValue: 10000.0, MinSliderValue: -500, MaxSliderValue: 500, Value: this.OnGetSpinBoxValue, OnValueChanged: this.OnGetSpinBoxChanged }),
)
```

As you can see, the widget parameters are given as a javascript object; then comes the child widgets.

Assuming you are already familiar with `widget.SetRootWidget(page)`,
```js
UMG.text({},"Dummy text")
UMG.div({}, UMG.text({}, "First"), UMG.text({}, "Second"))
UMG.div({}, [1,2,3].map(item => UMG.text({}, `Item: ${item}`)))
UMG.div({}, _ => Math.random() > 0.5 ? UMG.text({}, ">0.5") : UMG.text({}, "<0.5"))
UMG.text({ColorAndOpacity:{SpecifiedColor:{R:1,A:1}}},"RED!")
```