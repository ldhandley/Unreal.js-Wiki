You can declare `USTRUCT` and `UCLASS` while your javascript is running.

```js
class YourStructName /* StructFlag+StructFlag+... */ extends BaseStruct {
   properties() {
     property-declarations
   }
}
```

```js
class YourClassName /* ClassFlag+ClassFlag+... */ extends ParentClass {
   properties() {
     property-declarations
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