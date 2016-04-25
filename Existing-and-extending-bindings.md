# Existing bindings

Bindings are mostly rooted from BlueprintFunctionLibrary. Those functions are accessible as context-aware functions within blueprint editor.

# Extending bindings
To extend bindings, I recommend creating a new [BlueprintFunctionLibrary class](https://docs.unrealengine.com/latest/INT/Programming/BlueprintFunctionLibraries/) ([wiki article](https://wiki.unrealengine.com/Blueprint_Function_Library,_Create_Your_Own_to_Share_With_Others)). For most of cases it just works.

There are plenty of math functions exposed into BP world by UKismetMathLibraryFunction. There are some edge cases where you cannot access some functions because they are overloaded functions (which have same name but different type of arguments).