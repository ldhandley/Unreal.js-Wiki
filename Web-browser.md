If you should embed 'web' page, you would go with UE4 UWebBrowser plugin. But if you just need to talk with internet, I recommend using REST api by JavascriptHTTP and JavascriptUMG for UI.
Bridge between JS engine in UWebBrowser and Unreal.js seems doable.

You can communicate browser with BP.

UWebBrowser doesn't surface sufficient methods including ExecuteJavascript and Bind/Unbind UObjects.
So I recommend to implement a new UMG widget in C++ like JavascriptTreeView so that you can get full access to those functions.
To access JS functions in CEF(chromium), just call ExecuteJavascript.
To get notified by JS functions in CEF, first bind your UObject to this CEF context.
This UObject doesn't need to be a blue print class. You can use your own Unreal.js UObject! ☺