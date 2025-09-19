# Mango! [U]
A heavily modified version of the Mango! cutscene service module.

## Setting Up
- To import the module, insert the `.rbxm` file into `Roblox Studio`.
- From there, you can require the module using a `LocalScript`.
  
  ```lua
  local CutsceneService = require(game.ReplicatedStorage.CutsceneService)
  ```
- You can provide your own path.
> [!CAUTION]
> Do NOT use a regular `Script`. This module is not designed to be used by the server. **If you would like several players to view the same cutscene at once, try using RemoteEvents that fire on all clients.**
## Usage
  - There are a variety of different functions within the module that we can use.
### Creating a new Cutscene
```lua
local cutscene = CutsceneService.new()
```
- This creates a new Cutscene instance that we can use.
  - We can provide a table as a parameter that includes the current camera and data for the cutscene.
```lua
	{
		CameraObject = camera, 
		CSData = require(data)
	}
```
> [!IMPORTANT]
> The CSData module is not included in this module. To acquire CSData, you'll have to make your own table. To see CSData, look below...

### Creating CSData
- CSData is a separate module that contains a table with functions that act accordingly to animation events.
  - At the end of the table, we must include an Close function. This function will fire at the end of the cutscene.
```lua
local CSData = {
	['rbxassetid://animationID'] = {
		['example1'] = function()
			print("Foo!")
		end,
		['example2'] = function()
			print("Bar!")
		end,

		Close = function()
			print("Byebye!")
		end,
	}
}

return CSData
```
> [!TIP]
> While you do not have to use the Close function, it is vital that it exists to ensure the cutscene properly plays without error.
### Playing the Cutscene
- After everything is prepared, you can now play the cutscene.
```lua
CutsceneService:Play(cutscene)
```
All functions within CSData will be fired at the appropriate times, based on where you defined animation events.
## Origins
The Mango! module is a project by [jun-ro](https://github.com/jun-ro). While the original can be used to make acceptable sequences, there are some issues and confusing syntaxes that have to be addressed and fixed. Mango! [U] serves as a simpler, cleaner version of the original that will be continuously developed as time goes on.

### Thank you ^^
