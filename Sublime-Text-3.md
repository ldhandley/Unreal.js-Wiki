You can also use Sublime Text 3 as your code editor , Just make sure to install the following Packages : 
* [Babel](https://packagecontrol.io/packages/Babel): For Javascript usage in Sublime Text 3 
* [Microsoft Typescript](https://packagecontrol.io/packages/TypeScript) : Used for autocompletion

After installing the packages mentioned above , You can start coding : 
1. Open the scripts folder in Sublime Text 3 (either via toolbar , or dragging it)
2. Place your [bootstrap.js](https://github.com/ncsoft/Unreal.js/blob/master/Examples/Content/Scripts/bootstrap.js) file in your scripts folder if you haven't done that before (you can just copy the contents and create a new script)
3. Create a script with the extension ".js"
4. Open your Command Pallet (Ctrl + Shift + P) , and while your script is open , Type in in the command pallet : Set Syntax Typescript (This would enable Autocompletion for that specific file)
5. Paste in the top of that file , the following : `/// <reference path="typings/ue.d.ts">/>`

Now you can code in Sublime Text 3 and use Autocompletion ! 
NOTE : Autocompletion here is Context Insensitive , But you can go through those typescript typings to learn more.
TODO : Video explaining steps