# Mango! [U]
<img src="https://raw.githubusercontent.com/alarxic/Mango-U-/refs/heads/main/mangou.png" width="128">
A heavily modified version of the Mango! cutscene service module.

## Setting Up
- To import the module, insert the `.rbxm` file into `Roblox Studio`.
- From there, you can require the module using a `LocalScript`.
  
  ```lua
  local CutsceneService = require(game.ReplicatedStorage.CutsceneService)
  ```
  You can provide your own path.
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
  - CameraFrames is a Moon Animator camera information export folder. Moon Animator is a separate plugin that you may have to **buy.**
```lua
local CSData = {
	['cutsceneID'] = {
		functions = {
			['example1'] = function()
				print("Foo!")
			end,
			['example2'] = function()
				print("Bar!")
			end,
		},
		
		targets = {
			{
				target = character,
				animationID = "rbxassetid://id"
			},
		},

		Close = function()
			print("Byebye!")
		end,
		
		CameraFrames = folder
	}
}
return CSData
```
> [!NOTE]
> The 'targets' table will be where you include all of the Humanoids/AnimationControllers that you want in the cutscene. Provide an object path to the target, and an animation ID.

> [!TIP]
> While you do not have to use the Close function, it is vital that it exists to ensure the cutscene properly plays without error.
### Setting Targets Dynamically
- Your cutscenes may include characters that may or may not be included when a cutscene plays(e.g. players moving in and out of a queue or victims in a fight being different each time). To solve this, we can change targets with one function.
```lua
CutsceneService:setTargets(cutscene, id, {
	{
		target = character1,
		animationID = "rbxassetid://id"
	},
	{
		target = character2,
		animationID = "rbxassetid://id"
	},
})
```
- Numerous targets can be defined.
> [!NOTE]
> Each time you use :setTargets(), the table in which targets are stored resets. Make sure to include all targets when you use the function!
### Playing the Cutscene
- After everything is prepared, you can now play the cutscene.
  - Include the cutscene ID that you named in CSData.
```lua
CutsceneService:Play(cutscene, "cutsceneID")
```
All functions within CSData will be fired at the appropriate times, based on where you defined animation events.
## Origins
The Mango! module is a project by [jun-ro](https://github.com/jun-ro). While the original can be used to make acceptable sequences, there are some issues and confusing syntaxes that have to be addressed and fixed. Mango! [U] serves as a simpler, cleaner version of the original that will be continuously developed as time goes on.

### Thank you ^^
