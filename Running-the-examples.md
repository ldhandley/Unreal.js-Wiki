- Clone or Download the [Examples](https://github.com/ncsoft/Unreal.js/tree/master/Examples) directory of the Unreal.js repository
- Create the `Examples\Plugins\` directory
- Copy the [[already built plugin content|Building the plugin]] to the `Examples\Plugins\UnrealJS` directory
- Open the `Examples\JavascriptPlayground.uproject` file in the UE Editor
- Load one of the example levels from the editor's Content Browser
- Run the level in the editor to see Unreal.js in action
- If something goes wrong while running the level you can probably get useful information in the Javascript Console (`Window > Developer Tools > Javascript Console`)


***


### Install additional Node.js dependencies
- For the `helloSpringy.js` example you will need to install some external [Node.js](https://nodejs.org/en/) dependency packages
- This is done by using the [npm](https://www.npmjs.com/) command line utility
- Open the OS command prompt / shell and `cd` to the `Examples\Content\Scripts\` directory
- Install the required dependencies by using the `npm install` command
- The `node_modules` directory with the downloaded dependencies should have been created
- You can then try out and run the helloSpringy.js example