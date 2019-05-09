If you want to define a class which inheritance from JS class, you can download it:
[uclass.js updated](https://github.com/ncsoft/Unreal.js/files/3159837/uclass.zip)

Example:

        class A extends JavascriptWidget{

            OnInitialized(){
                let btn = new Border(this);
                let txt = new TextBlock(this);
                txt.SetText('uclass btn');
                btn.AddChild(txt);
                this.SetRootWidget(btn);
            }

            OnMouseButtonDown(MyGeometry: Geometry,MouseEvent: UPointerEvent){
                console.log('A.OnMouseButtonDown');
                return super.OnMouseButtonDown(MyGeometry, MouseEvent);
            }

            OnMouseEnter(MyGeometry: Geometry,MouseEvent: UPointerEvent){
                console.log('A.OnMouseEnter');
                return super.OnMouseEnter(MyGeometry, MouseEvent);
            }

            /*this function cannot been find from B_C befor replace uclass.js */
            OnMouseLeave(MouseEvent: UPointerEvent){
                console.log('A.OnMouseLeave');
                return super.OnMouseLeave(MouseEvent)
            }
            
        }

        class B extends A {

            OnMouseButtonDown(MyGeometry: Geometry,MouseEvent: UPointerEvent){
                console.log('B.OnMouseButtonDown');
                return super.OnMouseButtonDown(MyGeometry, MouseEvent);
            }

            OnMouseEnter(MyGeometry: Geometry,MouseEvent: UPointerEvent){
                console.log('B.OnMouseEnter');
                // return super.OnMouseButtonUp(MyGeometry, MouseEvent);
            }
        }

        let B_C = require('uclass')()(global, B, true, null, true);
        let b = new B_C(this);

>b.OnMouseButtonDown:
B.OnMouseButtonDown
A.OnMouseButtonDown

>b.OnMouseEnter:
B.OnMouseEnter

now, OnMouseLeave can been execute from b

>b.OnMouseLeave:
A.OnMouseLeave
