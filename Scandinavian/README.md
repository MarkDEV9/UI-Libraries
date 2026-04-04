# Scandinavian UI Library

<img width="400" alt="image" src="https://github.com/user-attachments/assets/5ec14c78-3981-47f2-94d2-a39429e6a6a7" />
<img width="400" alt="image" src="https://github.com/user-attachments/assets/ed014ba9-3ffd-4a79-bd1e-24c24de2f3c0" />
<img width="400" alt="image" src="https://github.com/user-attachments/assets/410bd4aa-c325-4da7-ba6c-7b81c9a6b548" />

## Loading the Library

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/MarkDEV9/UI-Libraries/refs/heads/main/Scandinavian/main.lua"))()
```

## Creating a Window
Both the Window Icon and Toggle Key are optional parameters.

```lua
-- Creating the window (Title, Icon ID, Toggle Key)
local Window = Library.CreateLib("Scandinavian UI", "rbxassetid://12345678", Enum.KeyCode.RightControl)

-- Skipping the Icon
local Window = Library.CreateLib("Scandinavian UI", Enum.KeyCode.RightControl)

-- Minimum setup
local Window = Library.CreateLib("Scandinavian UI")
```

To control the window state later:
```lua
Window:Toggle()  -- Hides or shows the UI
Window:Destroy() -- Removes the UI entirely
```

## Creating Tabs and Sections
The layout is completely automatic. If you create exactly one section, it will fill the entire screen width. The moment you create a second section, the UI will automatically split them side-by-side and continue alternating (Left, Right, Left, Right) for all future sections.

```lua
-- Creating a Tab
local MainTab = Window:NewTab("Main Features")

-- Creating Sections
local Section1 = MainTab:NewSection("Player Setup")
local Section2 = MainTab:NewSection("Combat Options")
```

## Components (Creating and Updating)
Every component you create returns an object. You can save this object to a variable to update its values later.

### Labels
**Creating a Label:**
```lua
local MyLabel = Section1:NewLabel("Current Status: Idle")
```
**Updating a Label:**
```lua
MyLabel:SetText("Current Status: Active")
local currentText = MyLabel:GetText()
```

### Buttons
**Creating a Button:**
```lua
local MyButton = Section1:NewButton("Execute Script", function()
    print("Button Clicked!")
end)
```
**Updating a Button:**
```lua
MyButton:SetText("Script Executed")
```

### Toggles
**Creating a Toggle:**
(Text, Default State, Callback)
```lua
local MyToggle = Section1:NewToggle("Auto Heal", false, function(state)
    print("Toggle is now:", state)
end)
```
**Updating a Toggle:**
```lua
MyToggle:Set(true) -- Changes state and fires callback
local currentState = MyToggle:Get() -- Returns true or false
```

### Sliders
**Creating a Slider:**
(Text, Min, Max, Default, HideValue, Callback)
```lua
local MySlider = Section1:NewSlider("Walk Speed", 16, 100, 16, false, function(value)
    print("Speed:", value)
end)
```
**Updating a Slider:**
```lua
MySlider:Set(50) -- Moves slider to 50 and fires callback
local currentValue = MySlider:Get()
```

### Dropdowns
**Creating a Dropdown:**
(Text, Items Table, Default Item, Callback)
```lua
local MyDropdown = Section1:NewDropdown("Hitbox", {"Head", "Torso", "Legs"}, "Head", function(selected)
    print("Selected:", selected)
end)
```
**Updating a Dropdown:**
```lua
-- Change the currently selected item
MyDropdown:Set("Torso")

-- Completely replace the list of items
MyDropdown:Refresh({"Arms", "Feet", "Hands"})

local currentSelection = MyDropdown:Get()
```

### Textboxes
**Creating a Textbox:**
(Text, Placeholder, Callback)
```lua
local MyTextbox = Section1:NewTextbox("Target", "Enter name...", function(text)
    print("Target set to:", text)
end)
```
**Updating a Textbox:**
```lua
MyTextbox:Set("NewTargetName")
local currentText = MyTextbox:Get()
```

### Color Pickers
**Creating a Color Picker:**
(Text, Default Color, Callback)
```lua
local MyColorPicker = Section1:NewColorPicker("ESP Color", Color3.fromRGB(255, 95, 95), function(color)
    print("New Color:", color)
end)
```
**Updating a Color Picker:**
```lua
MyColorPicker:Set(Color3.fromRGB(0, 255, 0))
local currentColor = MyColorPicker:Get()
```

### Keybinds
**Creating a Keybind:**
(Text, Default Key, Callback)
```lua
local MyKeybind = Section1:NewKeybind("Aimbot Key", Enum.KeyCode.E, function()
    print("Key pressed!")
end)
```
**Updating a Keybind:**
```lua
MyKeybind:Set(Enum.KeyCode.Q)
local currentKey = MyKeybind:Get()
```

## Full Example Script

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/MarkDEV9/UI-Libraries/refs/heads/main/Scandinavian/main.lua"))()

local Window = Library.CreateLib("Scandinavian UI", Enum.KeyCode.RightControl)

local MainTab = Window:NewTab("Main Features")

local PlayerSection = MainTab:NewSection("Player Setup")
PlayerSection:NewLabel("Modifications")

local WalkSlider = PlayerSection:NewSlider("Walk Speed", 16, 100, 16, false, function(value)
	game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
end)

PlayerSection:NewButton("Reset Speed", function()
	WalkSlider:Set(16)
end)

local CombatSection = MainTab:NewSection("Combat Options")
local WeaponDropdown = CombatSection:NewDropdown("Weapon", {"Sword", "Bow", "Magic"}, "Sword", function(selected)
	print("Equipped:", selected)
end)

CombatSection:NewButton("Update Weapons", function()
	WeaponDropdown:Refresh({"Rifle", "Shotgun", "Pistol"})
	WeaponDropdown:Set("Rifle")
end)

CombatSection:NewColorPicker("ESP Outline", Color3.fromRGB(255, 255, 255), function(color)
	print("Color updated")
end)
```
