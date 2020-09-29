### Easy installation
Unreal.js is now on the Unreal Engine MarketPlace. If you have installed Unreal Engine from Epic Games Launcher, you can grab Unreal.js from the MarketPlace.

### Build process
- Make sure you have installed the [UnrealEngine 4.13.? canonical build](https://www.unrealengine.com/dashboard).
- Create a UE4 C++ project and close the editor after the project creation is finished
- Clone the content of [Unreal.js-core](https://github.com/ncsoft/Unreal.js-core) into the `{ProjectRoot}\Plugins\UnrealJS` directory of the UE4 project directory
```
cd {ProjectRoot}
git clone https://github.com/ncsoft/Unreal.js-core Plugins/UnrealJS
cd Plugins/UnrealJS
```
- For Windows,
  * Run `install-v8-libs.bat` in Git CMD
  * Or run `install-v8-libs.sh` in Git bash
- For other platforms,
  * Run `install-v8-libs.sh`
- Now open the C++ `.uproject` again in the UE editor
- Once the UE Editor opens the project it should ask if you want to rebuild the plugin modules, click `Yes` to start the C++ build
- The compilation of the Unreal.js plugin should go through and you end up with a compiled version of the plugin in the `{ProjectRoot}\Plugins\UnrealJS` directory
- To verify that the C++ binaries of the plugin have been built check that the DLLs for the plugin have been created in `{ProjectRoot}\Plugins\UnrealJS\Binaries\Win64`
- In the UE Editor you can check that the plugin was successfully loaded in `Edit > Plugins > Project > Programming > Unreal.js - Javascript Runtime`
- You can then start using the plugin in the project or copy the built plugin folder to a different UE project (Blueprint or C++) and use it there
