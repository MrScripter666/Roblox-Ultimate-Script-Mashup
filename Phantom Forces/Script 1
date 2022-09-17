-- Settings

local Settings = {
    FOV = 0,
    SilentAim = false,
    ShowFOV = false,
    UseFOV = false,
    AutoShoot = false,
    AimForHead = false,
    FOVColour = 0,
    WalkSpeed = 12,
    JumpPower = 4,
    FlySpeed = 12,
    InfiniteJump = false,
    AntiAim = false,
    FallDamage = false,
    AutoRespawn = false,
    FlyKeybind = "Space",
    TrackerLength = 1.5,
    TrackerFrequency = 0.4,
    Tracker = false,
    NameESP = false,
    BoxESP = false,
    HealthESP = false,
	DistanceESP = false,
    Tracers = false,
    TrackerColour = 0,
    RainbowGun = false,
    RapidFire = false,
    InstantReload = false,
    InstantEquip = false,
    InstantAim = false,
    NoRecoil = false,
    NoSpread = false,
    NoSway = false,
    NoFlash = false,
    CombineMags = false,
    HeadshotChance = 0,
    Fullbright = false,
    NoBlood = false,
    NoShells = false,
    WindowsKeybind = "Z"
}

-- Variables

local Services = {
    Players = game:GetService("Players"),
    ReplicatedStorage = game:GetService("ReplicatedStorage"),
    UserInputService = game:GetService("UserInputService"),
    RunService = game:GetService("RunService"),
    Lighting = game:GetService("Lighting"),
    TweenService = game:GetService("TweenService"),
    HttpService = game:GetService("HttpService")
}

local Local = {
    Player = Services.Players.LocalPlayer,
    Mouse = Services.Players.LocalPlayer:GetMouse(),
    Cam = workspace.CurrentCamera
}

local Connections = {
    RainbowGun = nil
}

local FullbrightSettings = {
    Brightness = 1,
    ClockTime = 12,
    FogEnd = 999999,
    GlobalShadows = false,
    Ambient = Color3.fromRGB(178, 178, 178)
}

local BypassWords = Services.HttpService:JSONDecode(game:HttpGet("https://raw.githubusercontent.com/SykoticCataclysm/ScreamSploit/master/BypassWords.json"))
local Network, Effects, Gamelogic, Char, Particle, Menu, Hud
local Send, Walk, Jump, Bloodhit, Ejectshell, New
local GameGui = Local.Player.PlayerGui.MainGui.GameGui
local FogEnd, Ambient = Services.Lighting.FogEnd, Services.Lighting.Ambient
local Modules = Services.ReplicatedStorage.GunModules
local TracerStart = Vector2.new(Local.Cam.ViewportSize.X / 2, Local.Cam.ViewportSize.Y)
local SilentTarget, FOVCircle = nil, nil
local ScrMid = Vector2.new(Local.Cam.ViewportSize.X / 2, Local.Cam.ViewportSize.Y / 2)
local IsFlying = false
local TrackFolder = Instance.new("Folder", workspace)
local Parts = { "HumanoidRootPart", "Left Leg", "Right Leg" }
local Esp = { Esps = {} }
local GunData = {}

-- Setup

for a, b in next, Modules:GetChildren() do
    GunData[b.Name] = {}
    for c, d in next, require(b) do
        GunData[b.Name][c] = d
    end
end

function SetSilentTarget()
    if not Local.Player.Character then return nil end
    local Bodypart, Dist = nil, Settings.UseFOV and Settings.FOV or math.huge
    for a, b in next, workspace.Players:GetChildren() do
        if b ~= Local.Player.Character.Parent then
            for c, d in next, b:GetChildren() do
                local Pos, Vis = Local.Cam:WorldToViewportPoint(d.Torso.Position)
                if Vis and #Local.Cam:GetPartsObscuringTarget({d.Torso.Position}, {d}) == 0 then
                    local Mag = (ScrMid - Vector2.new(Pos.X, Pos.Y)).Magnitude
                    if Mag < Dist then
                        Bodypart = Settings.AimForHead and d.Head or d.Torso
                        Dist = Mag
                    end
                end
            end
        end
    end
    SilentTarget = Bodypart
end

function RegisterChar(char)
    Local.Char = char
    Local.Hum = char:WaitForChild("Humanoid")
    Local.Root = char:WaitForChild("HumanoidRootPart")
    Local.Hum.Died:Connect(function()
        Local.Char = nil
        Local.Hum = nil
        Local.Root = nil
    end)
end

if Local.Player.Character then
    RegisterChar(Local.Player.Character)
end

Local.Player.CharacterAdded:Connect(function(char)
    RegisterChar(char)
end)

for a, b in next, getgc(true) do
    if type(b) == "table" then
        if rawget(b, "send") then
            Network, Send = b, b.send
        elseif rawget(b, "breakwindow") then
            Effects, Bloodhit, Ejectshell = b, b.bloodhit, b.ejectshell
        elseif rawget(b, "gammo") then
            Gamelogic = b
        elseif rawget(b, "jump") then
            Char, Walk, Jump = b, b.setbasewalkspeed, b.jump
        elseif rawget(b, "new") and islclosure(b.new) and table.find(debug.getconstants(b.new), "ontouch") then
            Particle, New = b, b.new
        elseif rawget(b, "deploy") then
            Menu = b
        elseif rawget(b, "getplayervisible") then
            Hud = b
        end
    end
end

function Track(char)
    coroutine.wrap(function()
    	local isleft = true
    	repeat wait(Settings.TrackerFrequency)
    	    for i, v in next, Parts do
    	        if not char:FindFirstChild(v) then
    	            break
    	        end
            end
    		local Step = Instance.new("Part", TrackFolder)
    		local Part = isleft and char["Left Leg"] or char["Right Leg"]
    		local Root = char.HumanoidRootPart
    		Step.Anchored = true
    		Step.CanCollide = false
    		Step.BottomSurface = Enum.SurfaceType.Smooth
    		Step.Color = Color3.fromHSV(Settings.TrackerColour, 1, 1)
    		Step.Position = Vector3.new(Part.Position.X - 0.25, Root.Position.Y - 3, Part.Position.Z - 0.25)
    		Step.Rotation = Vector3.new(0, Part.Rotation.Y, 0)
    		Step.Size = Vector3.new(Part.Size.X + 0.4, 0.4, Part.Size.Z + 0.2)
    		Step.TopSurface = Enum.SurfaceType.Smooth
    		isleft = not isleft
    		coroutine.wrap(function()
    			wait(Settings.TrackerLength)
    			local T = Services.TweenService:Create(Step, TweenInfo.new(0.5), {Transparency = 1})
    			T.Completed:Connect(function()
    				Step:Destroy()
    			end)
    			T:Play()
    		end)()
    	until not char or char.Parent == nil or Settings.Tracker == false
    end)()
end

Network.send = newcclosure(function(self, ...)
    local Args = {...}
    if Args[1] == "bullethit" and math.random(0, 100) <= Settings.HeadshotChance then
        Args[6] = Args[6].Parent.Head
    elseif Args[1] == "newbullets" and Settings.SilentAim then
        if SilentTarget then
            for i, v in next, Args[2]["bullets"] do
                v[1] = (SilentTarget.Position - Gamelogic.currentgun.barrel.Position).Unit
            end
        end
    elseif Args[1] == "stance" and Settings.AntiAim then
        Args[2] = "prone"
    elseif Args[1] == "changehealthx" and Args[3] == "Falling" and Settings.FallDamage then
        return
    elseif Args[1] == "closeconnection" or Args[1] == "logmessage" then
        return
    end
    return Send(self, unpack(Args))
end)

Char.jump = newcclosure(function(self, ...)
    local Args = {...}
    Args[1] = Settings.JumpPower
    return Jump(self, unpack(Args))
end)

Char.setbasewalkspeed = newcclosure(function(self, ...)
    local Args = {...}
    Args[1] = Settings.WalkSpeed
    return Walk(self, unpack(Args))
end)

Effects.bloodhit = newcclosure(function(self, ...)
    if Settings.NoBlood then
        return
    end
    Bloodhit(self, ...)
end)

Effects.ejectshell = newcclosure(function(self, ...)
    if Settings.NoShells then
        return
    end
    Ejectshell(self, ...)
end)

Particle.new = newcclosure(function(tab)
    if Settings.SilentAim then
        if SilentTarget and Gamelogic.currentgun then
            tab.velocity = (SilentTarget.Position - tab.position).Unit * Gamelogic.currentgun.data.bulletspeed
        end
    end
    New(tab)
end)

function Esp:Create(plr)
    local Box = Drawing.new("Square")
    Box.Filled = false
    Box.Thickness = 2
    local Tracer = Drawing.new("Line")
    Tracer.From = TracerStart
    Tracer.Thickness = 2
    local Label = Drawing.new("Text")
    Label.Text = plr.Name
    Label.Center = true
    Label.Outline = false
    local Health = Drawing.new("Text")
    Health.Text = "[0/100]"
    Health.Center = true
    Health.Outline = false
	local Distance = Drawing.new("Text")
    Distance.Text = "0 Studs Away"
    Distance.Center = true
    Distance.Outline = false
    Esp.Esps[plr] = {
        Box = Box,
        Tracer = Tracer,
        Label = Label,
        Health = Health,
		Distance = Distance
    }
    return Esp.Esps[plr]
end

function Esp:Remove(plr)
	local PlrEsp = Esp.Esps[plr]
    if PlrEsp then
        for i, v in next, PlrEsp do
			v:Remove()
		end
        Esp.Esps[plr] = nil
    end
end

function Esp:Update(plr)
    local v = Esp.Esps[plr] or Esp:Create(plr)
    local Pos = Hud:getplayerpos(plr)
    if Pos then
        local RootPos, Vis = Local.Cam:WorldToViewportPoint(Pos)
        if Vis then
            v.Box.Visible = Settings.BoxESP
            v.Tracer.Visible = Settings.Tracers
            v.Label.Visible = Settings.NameESP
            v.Health.Visible = Settings.HealthESP
			v.Distance.Visible = Settings.DistanceESP
            local HeadPos = Local.Cam:WorldToViewportPoint(Pos + Vector3.new(0, 3, 0))
            local LegPos = Local.Cam:WorldToViewportPoint(Pos - Vector3.new(0, 3, 0))
            if Settings.BoxESP then
                local Y = HeadPos.Y - LegPos.Y
                v.Box.Size = Vector2.new(Y / 1.5, Y)
                v.Box.Position = Vector2.new(RootPos.X - v.Box.Size.X / 2, RootPos.Y - v.Box.Size.Y / 2)
                v.Box.Color = plr.Team == Local.Player.Team and Color3.fromRGB(0, 200, 0) or Color3.fromRGB(200, 0, 0)
            end
            if Settings.Tracers then
                v.Tracer.To = Vector2.new(RootPos.X, RootPos.Y - v.Box.Size.Y / 2)
                v.Tracer.Color = plr.Team == Local.Player.Team and Color3.fromRGB(0, 200, 0) or Color3.fromRGB(200, 0, 0)
            end
            if Settings.NameESP then
                v.Label.Position = Vector2.new(RootPos.X, RootPos.Y + v.Box.Size.Y / 2 - (Settings.HealthESP and v.Label.Size * 2 or v.Label.Size))
                v.Label.Color = plr.Team == Local.Player.Team and Color3.fromRGB(0, 200, 0) or Color3.fromRGB(200, 0, 0)
            end
            if Settings.HealthESP then
                v.Health.Text = "[" .. math.floor(Hud:getplayerhealth(plr)) .. "/100]"
                v.Health.Position = Vector2.new(RootPos.X, RootPos.Y + v.Box.Size.Y / 2 - v.Label.Size)
                v.Health.Color = plr.Team == Local.Player.Team and Color3.fromRGB(0, 200, 0) or Color3.fromRGB(200, 0, 0)
            end
			if Settings.DistanceESP then
				v.Distance.Text = math.floor((Local.Cam.CFrame.Position - Pos).Magnitude) .. " Studs Away"
                v.Distance.Position = Vector2.new(RootPos.X, RootPos.Y - v.Box.Size.Y / 2)
                v.Distance.Color = plr.Team == Local.Player.Team and Color3.fromRGB(0, 200, 0) or Color3.fromRGB(200, 0, 0)
			end
        else
            v.Box.Visible = false
            v.Tracer.Visible = false
            v.Label.Visible = false
            v.Health.Visible = false
			v.Distance.Visible = false
        end
    else
        v.Box.Visible = false
        v.Tracer.Visible = false
        v.Label.Visible = false
        v.Health.Visible = false
		v.Distance.Visible = false
    end
end

Services.RunService.Stepped:Connect(function()
    for i, v in next, game:GetService("Players"):GetPlayers() do
        if v ~= Local.Player then
            if not Esp.Esps[v] then
                Esp:Create(v)
            else
                Esp:Update(v)
            end
        end
    end
    SetSilentTarget()
    if SilentTarget and Settings.SilentAim and Settings.AutoShoot then
        mouse1press()
        wait()
        mouse1release()
    end
end)

Services.Players.PlayerRemoving:Connect(function(plr)
    Esp:Remove(plr)
end)

FOVCircle = Drawing.new("Circle")
FOVCircle.Color = Color3.fromHSV(Settings.FOVColour, 1, 1)
FOVCircle.Filled = false
FOVCircle.Position = Services.UserInputService:GetMouseLocation()
FOVCircle.Radius = Settings.FOV
FOVCircle.Thickness = 2

Services.UserInputService.InputBegan:Connect(function(input, istyping)
    if not istyping and input.KeyCode == Enum.KeyCode.Space and Settings.InfiniteJump then
        if Local.Root and Local.Hum and Local.Hum.FloorMaterial == Enum.Material.Air then
            Local.Root.Velocity = Vector3.new(Local.Root.Velocity.X, Settings.JumpPower * 12, Local.Root.Velocity.Z)
        end
    end
end)

Services.UserInputService.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        FOVCircle.Position = Services.UserInputService:GetMouseLocation()
    end
end)

Services.UserInputService.InputEnded:Connect(function(input, istyping)
    if not istyping and (input.KeyCode.Name == Settings.FlyKeybind or input.UserInputType.Name == Settings.FlyKeybind) then
        IsFlying = false
    end
end)

for i, v in next, FullbrightSettings do
    Services.Lighting:GetPropertyChangedSignal(i):Connect(function()
        if Settings.Fullbright then
            Services.Lighting[i] = v
        end
    end)
end

GameGui:GetPropertyChangedSignal("Visible"):Connect(function()
    if GameGui.Visible == false and Settings.AutoRespawn then
        repeat wait(1)
            Menu:deploy()
        until Menu:isdeployed()
    end
end)

for a, b in next, workspace.Players:GetChildren() do
    b.ChildAdded:Connect(function(child)
        if Settings.Tracker then
            Track(child)
        end
    end)
end

-- Gui

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/SykoticCataclysm/ScreamSploit/master/GuiLibrary.lua", true))()

local SilentTab = Library:Window("Silent Aim")

SilentTab:Slider("FOV", 0, 600, Settings.FOV, function(val)
    Settings.FOV = val
    FOVCircle.Radius = Settings.FOV
end)

SilentTab:Toggle("Silent Aim", Settings.SilentAim, function(toggle)
    Settings.SilentAim = toggle
end)

SilentTab:Toggle("Show FOV", Settings.ShowFOV, function(toggle)
    Settings.ShowFOV = toggle
    FOVCircle.Visible = Settings.ShowFOV
end)

SilentTab:Toggle("Use FOV", Settings.UseFOV, function(toggle)
    Settings.UseFOV = toggle
end)

SilentTab:Toggle("Auto Shoot", Settings.AutoShoot, function(toggle)
    Settings.AutoShoot = toggle
end)

SilentTab:Toggle("Aim For Head", Settings.AimForHead, function(toggle)
    Settings.AimForHead = toggle
end)

SilentTab:ColourSlider("FOV Colour", Settings.FOVColour, function(hue)
    Settings.FOVColour = hue
    FOVCircle.Color = Color3.fromHSV(hue, 1, 1)
end)

local PlayerTab = Library:Window("Player")

PlayerTab:Slider("WalkSpeed", 12, 30, Settings.WalkSpeed, function(val)
    Settings.WalkSpeed = val
    Char:setbasewalkspeed(val)
end)

PlayerTab:Slider("JumpPower", 4, 40, Settings.JumpPower, function(val)
    Settings.JumpPower = val
end)

PlayerTab:Slider("Fly Speed", 12, 40, Settings.FlySpeed, function(val)
    Settings.FlySpeed = val
end)

PlayerTab:Toggle("Infinite Jump", Settings.InfiniteJump, function(toggle)
    Settings.InfiniteJump = toggle
end)

PlayerTab:Toggle("Anti Aim", Settings.AntiAim, function(toggle)
    Settings.AntiAim = toggle
	if toggle then
		Network:send("stance", "prone")
	end
end)

PlayerTab:Toggle("Anti Fall Damage", Settings.FallDamage, function(toggle)
    Settings.FallDamage = toggle
end)

PlayerTab:Toggle("Auto Respawn", Settings.AutoRespawn, function(toggle)
    Settings.AutoRespawn = toggle
end)

PlayerTab:Keybind("Fly", Settings.FlyKeybind, function(key)
    Settings.FlyKeybind = key
    IsFlying = true
    if Local.Root and Local.Hum then
		Local.Hum.PlatformStand = true
        repeat Services.RunService.Stepped:Wait()
            Local.Root.Velocity = Local.Cam.CFrame.LookVector * (math.random(Settings.FlySpeed - 2.5, Settings.FlySpeed + 2.5))
        until not IsFlying
        Local.Hum.PlatformStand = false
	end
end)

local ESPTab = Library:Window("ESP")

ESPTab:Slider("Tracker Length", 0, 10, Settings.TrackerLength, function(val)
    Settings.TrackerLength = val
end)

ESPTab:Slider("Tracker Frequency", 0, 1, Settings.TrackerFrequency, function(val)
    Settings.TrackerFrequency = val
end)

ESPTab:Toggle("Footstep Tracker", Settings.Tracker, function(toggle)
    Settings.Tracker = toggle
    if toggle then
        for a, b in next, workspace.Players:GetChildren() do
            for c, d in next, b:GetChildren() do
                Track(d)
            end
        end
    end
end)

ESPTab:Toggle("Show Names", Settings.NameESP, function(toggle)
    Settings.NameESP = toggle
end)

ESPTab:Toggle("Show Boxes", Settings.BoxESP, function(toggle)
    Settings.BoxESP = toggle
end)

ESPTab:Toggle("Show Health", Settings.HealthESP, function(toggle)
    Settings.HealthESP = toggle
end)

ESPTab:Toggle("Show Distance", Settings.DistanceESP, function(toggle)
	Settings.DistanceESP = toggle
end)

ESPTab:Toggle("Tracers", Settings.Tracers, function(toggle)
    Settings.Tracers = toggle
end)

ESPTab:ColourSlider("Tracker Colour", Settings.TrackerColour, function(hue)
    Settings.TrackerColour = hue
end)

local GunTab = Library:Window("Guns")

GunTab:Toggle("Rainbow Guns", Settings.RainbowGun, function(toggle)
    Settings.RainbowGun = toggle
    if Connections.RainbowGun then
        Connections.RainbowGun:Disconnect()
    end
    if Settings.RainbowGun then
        Connections.RainbowGun = Services.RunService.Heartbeat:Connect(function()
            if rawget(Gamelogic, "currentgun") then
                for i, v in next, workspace.CurrentCamera[Gamelogic.currentgun.name]:GetDescendants() do
                    if v:IsA("BasePart") then
                        v.Color = Color3.fromHSV(tick() % 10 / 10, 1, 1)
                    end
                end
            end
        end)
    end
end)

GunTab:Toggle("Rapid Fire", Settings.RapidFire, function(toggle)
    Settings.RapidFire = toggle
    for i, v in next, Modules:GetChildren() do
        local req = require(v)
        if type(req.firerate) == "table" then
            req.firerate = toggle and { 1000 } or GunData[v.name].firerate
        else
            req.firerate = toggle and 1000 or GunData[v.name].firerate
        end
		req.variablefirerate = toggle and false or GunData[v.name].variablefirerate
        req.requirechamber = toggle and false or GunData[v.name].requirechamber
        req.firemodes = toggle and { true } or GunData[v.name].firemodes
    end
end)

GunTab:Toggle("Instant Reload", Settings.InstantReload, function(toggle)
    Settings.InstantReload = toggle
    for i, v in next, Modules:GetChildren() do
        local req = require(v)
        if rawget(req, "animations") then
            if rawget(req.animations, "reload") then
                req.animations.reload.timescale = toggle and  0.1 or GunData[v.name].animations.reload.timescale
                req.animations.reload.stdtimescale = toggle and  0.1 or GunData[v.name].animations.reload.stdtimescale
            end
            if rawget(req.animations, "tacticalreload") then    
                req.animations.tacticalreload.timescale = toggle and  0.1 or GunData[v.name].animations.tacticalreload.timescale
                req.animations.tacticalreload.stdtimescale = toggle and  0.1 or GunData[v.name].animations.tacticalreload.stdtimescale
            end
        end
    end
end)

GunTab:Toggle("Instant Equip", Settings.InstantEquip, function(toggle)
    Settings.InstantEquip = toggle
    for i, v in next, Modules:GetChildren() do
        local req = require(v)
        req.equipspeed = toggle and 9999 or GunData[v.name].equipspeed
    end
end)

GunTab:Toggle("No Recoil", Settings.NoRecoil, function(toggle)
    Settings.NoRecoil = toggle
    for i, v in next, Modules:GetChildren() do
        local req = require(v)
        req.camkickmin = toggle and Vector3.new() or GunData[v.name].camkickmin
		req.camkickmax = toggle and Vector3.new() or GunData[v.name].camkickmax
		req.aimcamkickmin = toggle and Vector3.new() or GunData[v.name].aimcamkickmin
		req.aimcamkickmax = toggle and Vector3.new() or GunData[v.name].aimcamkickmax
		req.aimtranskickmin = toggle and Vector3.new() or GunData[v.name].aimtranskickmin
		req.aimtranskickmax = toggle and Vector3.new() or GunData[v.name].aimtranskickmax
		req.transkickmin = toggle and Vector3.new() or GunData[v.name].transkickmin
		req.transkickmax = toggle and Vector3.new() or GunData[v.name].transkickmax
		req.rotkickmin = toggle and Vector3.new() or GunData[v.name].rotkickmin
		req.rotkickmax = toggle and Vector3.new() or GunData[v.name].rotkickmax
		req.aimrotkickmin = toggle and Vector3.new() or GunData[v.name].aimrotkickmin
		req.aimrotkickmax = toggle and Vector3.new() or GunData[v.name].aimrotkickmax
    end
end)

GunTab:Toggle("No Spread", Settings.NoSpread, function(toggle)
    Settings.NoSpread = toggle
    for i, v in next, Modules:GetChildren() do
        local req = require(v)
		req.hipfirespreadrecover = toggle and 100 or GunData[v.name].hipfirespreadrecover
		req.hipfirespread = toggle and 0 or GunData[v.name].hipfirespread
		req.hipfirestability = toggle and 0 or GunData[v.name].hipfirestability
		req.crosssize = toggle and 2 or GunData[v.name].crosssize
		req.crossexpansion = toggle and 0 or GunData[v.name].crossexpansion
    end
end)

GunTab:Toggle("No Sway", Settings.NoSway, function(toggle)
    Settings.NoSway = toggle
    for i, v in next, Modules:GetChildren() do
        local req = require(v)
        req.swayamp = toggle and 0 or GunData[v.name].swayamp
		req.swayspeed = toggle and 0 or GunData[v.name].swayspeed
		req.steadyspeed = toggle and 0 or GunData[v.name].steadyspeed
        req.breathspeed = toggle and 0 or GunData[v.name].breathspeed
    end
end)

GunTab:Toggle("No Flash", Settings.NoFlash, function(toggle)
    Settings.NoFlash = toggle
    for i, v in next, Modules:GetChildren() do
        local req = require(v)
        req.hideflash = toggle and true or GunData[v.name].hideflash
		req.hideminimap = toggle and true or GunData[v.name].hideminimap
    end
end)

GunTab:Toggle("Combine Mags", Settings.CombineMags, function(toggle)
	Settings.CombineMags = toggle
    for i, v in next, Modules:GetChildren() do
        local req = require(v)
        if rawget(req, "magsize") and rawget(req, "sparerounds") then
            req.magsize = toggle and GunData[v.Name].magsize + GunData[v.Name].sparerounds or GunData[v.Name].magsize
            req.sparerounds = toggle and 0 or GunData[v.Name].sparerounds
        end
    end
end)

local MiscTab = Library:Window("Misc")

MiscTab:Slider("Headshot Chance", 0, 100, Settings.HeadshotChance, function(val)
    Settings.HeadshotChance = val
end)

MiscTab:Toggle("Fullbright", Settings.Fullbright, function(toggle)
    Settings.Fullbright = toggle
    if toggle then
        for i, v in next, FullbrightSettings do
            Services.Lighting[i] = v
        end
    else
        Services.Lighting.FogEnd = FogEnd
        Services.Lighting.Ambient = Ambient
        Services.Lighting.GlobalShadows = true
    end
end)

MiscTab:Toggle("Disable Blood", Settings.NoBlood, function(toggle)
    Settings.NoBlood = toggle
    if toggle then
        for i, v in next, workspace.Ignore.Blood:GetChildren() do
            v:Destroy()
        end
    end
end)

MiscTab:Toggle("Disable Shells", Settings.NoShells, function(toggle)
    Settings.NoShells = toggle
    if toggle then
        for i, v in next, workspace.Ignore.Bullets:GetChildren() do
            v:Destroy()
        end
    end
end)

MiscTab:Keybind("Break Windows", Settings.WindowsKeybind, function(key)
    Settings.WindowsKeybind = key
    for i, v in next, workspace:GetDescendants() do
        if v.Name == "Window" then
            Effects:breakwindow(v)
        end
    end
end)
