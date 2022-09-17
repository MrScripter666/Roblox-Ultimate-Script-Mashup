-- This code is a mess, but it works. I might add better comments down the line.
-- jbsparrow#5747 Black Hawk Rescue Mission 5 Teleportation GUI Full overhaul.
-- Fully overhauled the GUI and changed some teleport coordinates.
-- I'll add a translucent GUI later because in BRM5 your cursor gets hidden under the GUI, making it a pain in the ass to click things.


-- Instances:

local BlackHawkTeleportGUI = Instance.new("ScreenGui")
local TopFrame = Instance.new("Frame")
local BaseFrame = Instance.new("Frame")
local ToggleHelp = Instance.new("TextLabel")
local FeatureRequests = Instance.new("TextLabel")
local ImageLabel = Instance.new("ImageLabel")
local CargoWarpsButton = Instance.new("TextButton")
local MiscWarpsButton = Instance.new("TextButton")
local CargoWarpsFrame = Instance.new("Frame")
local DesertCargo = Instance.new("TextButton")
local ForestCargo = Instance.new("TextButton")
local OutskirtsCargo = Instance.new("TextButton")
local BaseWarp = Instance.new("TextButton")
local MiscWarpsFrame = Instance.new("Frame")
local Mountain = Instance.new("TextButton")
local Ronograd = Instance.new("TextButton")
local Arctic = Instance.new("TextButton")
local Desert = Instance.new("TextButton")
local Naval = Instance.new("TextButton")
local Quarry = Instance.new("TextButton")
local Skydive = Instance.new("TextButton")
local ExploitName = Instance.new("TextLabel")
local DiscordUsername = Instance.new("TextLabel")

-- Other Stuff:

function onKeyPress(inputObject, gameProcessedEvent)
	if inputObject.KeyCode == Enum.KeyCode.M then
		if TopFrame.Visible == false then
			TopFrame.Visible = true
		else
			TopFrame.Visible = false
		end
	end
end

game:GetService("UserInputService").InputBegan:connect(onKeyPress)

-- Properties:

BlackHawkTeleportGUI.Name = "BlackHawkTeleportGUI"
BlackHawkTeleportGUI.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
BlackHawkTeleportGUI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
BlackHawkTeleportGUI.ResetOnSpawn = false

TopFrame.Name = "TopFrame"
TopFrame.Parent = BlackHawkTeleportGUI
TopFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
TopFrame.BorderSizePixel = 2
TopFrame.Position = UDim2.new(0.0634372011, 0, 0.514084518, 0)
TopFrame.Size = UDim2.new(0, 302, 0, 206)
TopFrame.Active = true
TopFrame.Draggable = true

BaseFrame.Name = "BaseFrame"
BaseFrame.Parent = TopFrame
BaseFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
BaseFrame.BorderColor3 = Color3.fromRGB(50, 50, 50)
BaseFrame.BorderSizePixel = 3
BaseFrame.Position = UDim2.new(0.0198675506, 0, 0.281553388, 0)
BaseFrame.Size = UDim2.new(0, 289, 0, 142)

ToggleHelp.Name = "ToggleHelp"
ToggleHelp.Parent = BaseFrame
ToggleHelp.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ToggleHelp.BackgroundTransparency = 1.000
ToggleHelp.BorderSizePixel = 0
ToggleHelp.Position = UDim2.new(0.0276816618, 0, 0.830985904, 0)
ToggleHelp.Size = UDim2.new(0, 149, 0, 24)
ToggleHelp.Font = Enum.Font.SourceSans
ToggleHelp.Text = "Press M to toggle the GUI"
ToggleHelp.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleHelp.TextSize = 17.000
ToggleHelp.TextXAlignment = Enum.TextXAlignment.Left

FeatureRequests.Name = "FeatureRequests"
FeatureRequests.Parent = BaseFrame
FeatureRequests.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
FeatureRequests.BorderSizePixel = 2
FeatureRequests.Position = UDim2.new(0.0276816618, 0, 0.0563380271, 0)
FeatureRequests.Size = UDim2.new(0, 94, 0, 110)
FeatureRequests.Font = Enum.Font.SourceSans
FeatureRequests.Text = "For Feature  Requests please   contact me on  Discord."
FeatureRequests.TextColor3 = Color3.fromRGB(0, 0, 0)
FeatureRequests.TextSize = 22.000
FeatureRequests.TextWrapped = true

ImageLabel.Parent = BaseFrame
ImageLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ImageLabel.BorderSizePixel = 2
ImageLabel.Position = UDim2.new(0.591695487, 0, 0.0563380271, 0)
ImageLabel.Size = UDim2.new(0, 110, 0, 110)
ImageLabel.Image = "rbxassetid://6562791820"

CargoWarpsButton.Name = "CargoWarpsButton"
CargoWarpsButton.Parent = BaseFrame
CargoWarpsButton.BackgroundColor3 = Color3.fromRGB(108, 108, 108)
CargoWarpsButton.BorderSizePixel = 2
CargoWarpsButton.Position = UDim2.new(0.0276816618, 0, -0.239436626, 0)
CargoWarpsButton.Size = UDim2.new(0, 82, 0, 26)
CargoWarpsButton.Font = Enum.Font.SourceSans
CargoWarpsButton.Text = "Cargo Warps"
CargoWarpsButton.TextColor3 = Color3.fromRGB(0, 0, 0)
CargoWarpsButton.TextSize = 15.000
CargoWarpsButton.MouseButton1Click:Connect(function()
	MiscWarpsFrame.Visible = false
	if CargoWarpsFrame.Visible == true then
		CargoWarpsFrame.Visible = false
	else
		CargoWarpsFrame.Visible = true
	end
end)

MiscWarpsButton.Name = "MiscWarpsButton"
MiscWarpsButton.Parent = BaseFrame
MiscWarpsButton.BackgroundColor3 = Color3.fromRGB(108, 108, 108)
MiscWarpsButton.BorderSizePixel = 2
MiscWarpsButton.Position = UDim2.new(0.688581288, 0, -0.239436626, 0)
MiscWarpsButton.Size = UDim2.new(0, 82, 0, 26)
MiscWarpsButton.Font = Enum.Font.SourceSans
MiscWarpsButton.Text = "Misc Warps"
MiscWarpsButton.TextColor3 = Color3.fromRGB(0, 0, 0)
MiscWarpsButton.TextSize = 15.000
MiscWarpsButton.MouseButton1Click:Connect(function()
	CargoWarpsFrame.Visible = false
	if MiscWarpsFrame.Visible == true then
		MiscWarpsFrame.Visible = false
	else
		MiscWarpsFrame.Visible = true
	end
end)

CargoWarpsFrame.Name = "CargoWarpsFrame"
CargoWarpsFrame.Parent = BaseFrame
CargoWarpsFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
CargoWarpsFrame.BorderColor3 = Color3.fromRGB(50, 50, 50)
CargoWarpsFrame.BorderSizePixel = 3
CargoWarpsFrame.Size = UDim2.new(0, 289, 0, 142)
CargoWarpsFrame.Visible = false

DesertCargo.Name = "DesertCargo"
DesertCargo.Parent = CargoWarpsFrame
DesertCargo.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
DesertCargo.BorderSizePixel = 2
DesertCargo.Position = UDim2.new(0.0276816618, 0, 0.0563380271, 0)
DesertCargo.Size = UDim2.new(0, 82, 0, 36)
DesertCargo.Font = Enum.Font.SourceSans
DesertCargo.Text = "Desert Cargo"
DesertCargo.TextColor3 = Color3.fromRGB(255, 255, 255)
DesertCargo.TextSize = 17.000
DesertCargo.MouseButton1Click:connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(-4526.27, 101, 4175.46))
end)

ForestCargo.Name = "ForestCargo"
ForestCargo.Parent = CargoWarpsFrame
ForestCargo.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
ForestCargo.BorderSizePixel = 2
ForestCargo.Position = UDim2.new(0.359861583, 0, 0.0563380271, 0)
ForestCargo.Size = UDim2.new(0, 82, 0, 36)
ForestCargo.Font = Enum.Font.SourceSans
ForestCargo.Text = "Forest Cargo"
ForestCargo.TextColor3 = Color3.fromRGB(255, 255, 255)
ForestCargo.TextSize = 17.000
ForestCargo.MouseButton1Click:connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(166.59, 64, 3064.55))
end)

OutskirtsCargo.Name = "OutskirtsCargo"
OutskirtsCargo.Parent = CargoWarpsFrame
OutskirtsCargo.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
OutskirtsCargo.BorderSizePixel = 2
OutskirtsCargo.Position = UDim2.new(0.688581347, 0, 0.0563380271, 0)
OutskirtsCargo.Size = UDim2.new(0, 82, 0, 36)
OutskirtsCargo.Font = Enum.Font.SourceSans
OutskirtsCargo.Text = "OS Cargo"
OutskirtsCargo.TextColor3 = Color3.fromRGB(255, 255, 255)
OutskirtsCargo.TextSize = 17.000
OutskirtsCargo.MouseButton1Click:connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(1803.77, 232, 3101.72))
end)

BaseWarp.Name = "BaseWarp"
BaseWarp.Parent = BaseFrame
BaseWarp.BackgroundColor3 = Color3.fromRGB(108, 108, 108)
BaseWarp.BorderSizePixel = 2
BaseWarp.Position = UDim2.new(0.359861583, 0, -0.239436626, 0)
BaseWarp.Size = UDim2.new(0, 82, 0, 26)
BaseWarp.Font = Enum.Font.SourceSans
BaseWarp.Text = "Base Warp"
BaseWarp.TextColor3 = Color3.fromRGB(0, 0, 0)
BaseWarp.TextSize = 15.000
BaseWarp.MouseButton1Click:connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(-3467.55, 61.5745, 1147.81))
end)

MiscWarpsFrame.Name = "MiscWarpsFrame"
MiscWarpsFrame.Parent = BaseFrame
MiscWarpsFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
MiscWarpsFrame.BorderColor3 = Color3.fromRGB(50, 50, 50)
MiscWarpsFrame.BorderSizePixel = 3
MiscWarpsFrame.Size = UDim2.new(0, 289, 0, 142)
MiscWarpsFrame.Visible = false

Mountain.Name = "Mountain"
Mountain.Parent = MiscWarpsFrame
Mountain.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
Mountain.BorderSizePixel = 2
Mountain.Position = UDim2.new(0.359861583, 0, 0.0563380718, 0)
Mountain.Size = UDim2.new(0, 82, 0, 36)
Mountain.Font = Enum.Font.SourceSans
Mountain.Text = "Mountain"
Mountain.TextColor3 = Color3.fromRGB(255, 255, 255)
Mountain.TextSize = 17.000
Mountain.MouseButton1Click:connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(-1799.10657, 823.465637, -4301.93408))
end)

Ronograd.Name = "Ronograd"
Ronograd.Parent = MiscWarpsFrame
Ronograd.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
Ronograd.BorderSizePixel = 2
Ronograd.Position = UDim2.new(0.688581288, 0, 0.0563380718, 0)
Ronograd.Size = UDim2.new(0, 82, 0, 36)
Ronograd.Font = Enum.Font.SourceSans
Ronograd.Text = "Ronograd"
Ronograd.TextColor3 = Color3.fromRGB(255, 255, 255)
Ronograd.TextSize = 17.000
Ronograd.MouseButton1Click:connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(3356.396, 176.642868, 479.418335))
end)

Arctic.Name = "Arctic"
Arctic.Parent = MiscWarpsFrame
Arctic.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
Arctic.BorderSizePixel = 2
Arctic.Position = UDim2.new(0.359861612, 0, 0.690140784, 0)
Arctic.Size = UDim2.new(0, 82, 0, 36)
Arctic.Font = Enum.Font.SourceSans
Arctic.Text = "Arctic Base"
Arctic.TextColor3 = Color3.fromRGB(255, 255, 255)
Arctic.TextSize = 17.000
Arctic.MouseButton1Click:connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(6839.26, 290, -1994.75))
end)

Desert.Name = "Desert"
Desert.Parent = MiscWarpsFrame
Desert.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
Desert.BorderSizePixel = 2
Desert.Position = UDim2.new(0.0276816618, 0, 0.0563380122, 0)
Desert.Size = UDim2.new(0, 82, 0, 36)
Desert.Font = Enum.Font.SourceSans
Desert.Text = "Desert Town"
Desert.TextColor3 = Color3.fromRGB(255, 255, 255)
Desert.TextSize = 17.000
Desert.MouseButton1Click:connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(-4972.27979, 107.465622, 5641.16016))
end)

Naval.Name = "Naval"
Naval.Parent = MiscWarpsFrame
Naval.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
Naval.BorderSizePixel = 2
Naval.Position = UDim2.new(0.0276816599, 0, 0.690140784, 0)
Naval.Size = UDim2.new(0, 82, 0, 36)
Naval.Font = Enum.Font.SourceSans
Naval.Text = "Naval Base"
Naval.TextColor3 = Color3.fromRGB(255, 255, 255)
Naval.TextSize = 17.000
Naval.MouseButton1Click:connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(6408.08, 195, 2156.84))
end)

Quarry.Name = "Quarry"
Quarry.Parent = MiscWarpsFrame
Quarry.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
Quarry.BorderSizePixel = 2
Quarry.Position = UDim2.new(0.685121119, 0, 0.690140784, 0)
Quarry.Size = UDim2.new(0, 82, 0, 36)
Quarry.Font = Enum.Font.SourceSans
Quarry.Text = "Quarry"
Quarry.TextColor3 = Color3.fromRGB(255, 255, 255)
Quarry.TextSize = 17.000
Quarry.MouseButton1Click:Connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(167.03, 284, 2097.12))
end)

Skydive.Name = "Skydive"
Skydive.Parent = MiscWarpsFrame
Skydive.BackgroundColor3 = Color3.fromRGB(74, 74, 74)
Skydive.BorderSizePixel = 2
Skydive.Position = UDim2.new(0.360000014, 0, 0.372999996, 0)
Skydive.Size = UDim2.new(0, 82, 0, 36)
Skydive.Font = Enum.Font.SourceSans
Skydive.Text = "Skydive"
Skydive.TextColor3 = Color3.fromRGB(255, 255, 255)
Skydive.TextSize = 17.000
Skydive.MouseButton1Click:Connect(function()
	game.Players.LocalPlayer.Character:MoveTo(Vector3.new(167.03, 35000, 2097.12))
end)

ExploitName.Name = "ExploitName"
ExploitName.Parent = TopFrame
ExploitName.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
ExploitName.BorderSizePixel = 0
ExploitName.Size = UDim2.new(0, 88, 0, 24)
ExploitName.Font = Enum.Font.SourceSans
ExploitName.Text = "  BRM5 TP GUI"
ExploitName.TextColor3 = Color3.fromRGB(255, 255, 255)
ExploitName.TextSize = 18.000
ExploitName.TextXAlignment = Enum.TextXAlignment.Left

DiscordUsername.Name = "DiscordUsername"
DiscordUsername.Parent = TopFrame
DiscordUsername.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
DiscordUsername.BorderSizePixel = 0
DiscordUsername.Position = UDim2.new(0.655629158, 0, 0, 0)
DiscordUsername.Size = UDim2.new(0, 104, 0, 24)
DiscordUsername.Font = Enum.Font.SourceSans
DiscordUsername.Text = " jbsparrow#5747  "
DiscordUsername.TextColor3 = Color3.fromRGB(255, 255, 255)
DiscordUsername.TextSize = 18.000
DiscordUsername.TextXAlignment = Enum.TextXAlignment.Right
