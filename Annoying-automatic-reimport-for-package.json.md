UPDATE: Current version of Unreal.js automatically patches reimport-rule to prevent this symptom.

With `npm` there is no need to reinvent the wheels. You can `npm install some nice package` in your `Content/Scripts` folder and have nice modules in `Content/Scripts/node_modules/nice_package`. But UnrealEditor is so kind to reimport automatically json files as data tables that it opens 'reimport dialog' automagically.

You can disable this unexpected kindness by adding a rule to Automatic content monitoring section in your editor settings.