You can declare `USTRUCT` and `UCLASS` while your javascript is running.

```js
// NOTE: Struct flag is *required* for 'USTRUCT'.
class YourStructName /* Struct+StructFlag+StructFlag+... */ extends BaseStruct {
   properties() {
     property-declarations
   }
}
```

```js
class YourClassName /* ClassFlag+ClassFlag+... */ extends ParentClass {
   ctor() {
     // initialization
     // component setup
   }
   properties() {
     property-declarations
   }
   YourUFunctionName(arg/*PropertyFlag+...*/) /*FunctionFlag+...*/ {
   }
   YourPureJavascriptFunctionName(arg,...) {
   }
}
```

These classes should be transformed into corresponding `USTRUCT` and `UCLASS` by calling `require('uclass')()(global, source-class)`. 

StructFlag | Description
-----------|------------
Atomic|
Immutable|

ClassFlag | Description
----------|------------
Abstract|
DefaultConfig|
Transient|
AdvancedDisplay|
NotPlaceable|
PerObjectConfig|
EditInlineNew|
CollapseCategories|
Const|
DefaultToInstanced|
Hidden|
HideDropDown|
BlueprintType|
BlueprintSpawnableComponent|