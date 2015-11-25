Javascript is not a strict-typed language, so type-info is passed using javascript comment block. `property-name/*PropertyFlag+PropertyFlag+type*/`

```js
class MyTestActor extends Actor {
  properties() {
    this.replicated_int_var/*Replicated+int*/;
    this.health/*EditAnywhere+ReplicatedUsing:OnRepHealth+int*/;
    this.series/*EditAnywhere+int[]*/;
  }

  MyNiceSum(a/*int*/,b/*float*/,$/*Return+float*/) { 
    return a+b 
  }
  
  MyComplexReturn(a/*out+int*/,$/*ret+int*/) {
    return {
      $:1,
      a:2
    }
  }
}
```
PropertyFlag|Description
------------|-----------
Const|
Return|
Out|
Replicated|
NotReplicated|
ReplicatedUsing|`ReplicatedUsing:rep-notify-function-name`
Transient|
DuplicateTransient|
EditFixedSize|
EditAnywhere|
EditDefaultsOnly|
Instanced|
SimpleDisplay|
AdvancedDisplay|
SaveGame|
AssetRegistrySearchable|
Interp|
NoClear|
VisibleAnywhere|
VisibleInstanceOnly|
VisibleDefaultsOnly|
Category|`Category:your-category`
DisplayName|`DisplayName:your-nice-name`