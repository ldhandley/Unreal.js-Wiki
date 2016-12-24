Current version of UnrealEngine doesn't handle plugins with `Content` correctly. For a workaround you may copy `Plugins/UnrealJS/Content` into cooked target manually.

While cooking a shipping version, UnrealEngine strips all assets which are not referenced by `root asset`s. Cooker doesn't know anything about `*.js`, so `Resource.Load`ed assets will not be included in the final shipping version. As a remedy for this problem, `JavascriptComponent` has `Assets` and `ClassAssets` which are key-value store containing `FStringAssetReference` and `TSubclassOf<UObject>`. Those assets can be accessed via `Root.ResolveAsset(asset-name,true/*true for load*/)` and `Root.ResolveClass(asset-name)`.

Before
```js
class MyChildActor extends Blueprint.Load('/SomeNice').GeneratedClass {}
``` 

After
```js
class MyChildActor extends Root.ResolveClass('blueprint') {}
```

Non native project which doesn't have a single c++ class cannot be baked with game plugins. So if you have installed Unreal.js as a game plugin, you should switch your project into c++ project by adding a dummy native class.

## Packaging

Not to lose your Content/Scripts folder, please add your Content/Scripts to Package Settings - Additional Non-Asset Directories to Cook