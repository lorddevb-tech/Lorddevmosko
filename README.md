# Aether Library for Roblox

Aether Library is a small Roblox Luau interface library for a game's own client UI. It creates a draggable, responsive `ScreenGui` with tabs, reusable controls, a floating launcher, optional floating action buttons, and toast notifications. It has no external dependencies or executor-specific code.



## API

```lua
local AetherUI = require(script.Parent.AetherUI)

local window = AetherUI:CreateWindow({
    Title = "My game",
    Subtitle = "Player controls",
    ToggleKey = Enum.KeyCode.RightShift,
    Accent = Color3.fromRGB(143, 119, 255),
})

window:AddFloatingButton("?", function()
    window:Notify({ Title = "Help", Text = "Your quick action goes here." })
end)

local tab = window:AddTab({ Name = "Main", Icon = "M" })
local section = tab:AddSection("Actions")

section:AddLabel("A short description")
section:AddButton("Do something", "Optional supporting text", function()
    print("Clicked")
end)

local toggle = section:AddToggle("Enabled", false, function(value)
    print("Enabled:", value)
end)
toggle:SetValue(true, true) -- second argument suppresses the callback
print(toggle:GetValue())

local slider = section:AddSlider("Volume", {
    Min = 0, Max = 100, Default = 60, Step = 5,
}, function(value)
    print("Volume:", value)
end)

local dropdown = section:AddDropdown("Mode", {
    Options = { "Casual", "Ranked" },
    Default = "Casual",
}, function(value)
    print("Mode:", value)
end)

local input = section:AddTextBox("Note", {
    Placeholder = "Type here...",
}, function(value)
    print("Note:", value)
end)

window:Notify({ Title = "Saved", Text = "Your setting was updated." })
window:SetVisible(false)
window:Toggle()
window:Destroy()
```

`AddButton(title, callback)` is also supported when no supporting text is needed. `SetValue(value, true)` updates a control without firing its callback.
