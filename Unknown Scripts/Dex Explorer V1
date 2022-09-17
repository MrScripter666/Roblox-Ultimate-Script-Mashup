--credits to infinite yield fe creators
--it may take a while to load plz be patient if the game isn't small
-- btw the comment "sirhurt is retarded" isn't made by me, check the source here ok https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source

function randomString()
	local length = math.random(10,20)
	local array = {}
	for i = 1, length do
		array[i] = string.char(math.random(32, 126))
	end
	return table.concat(array)
end

PARENT = nil
if (not is_sirhurt_closure) and (syn and syn.protect_gui) then --sirhurt is retarded
	local Main = Instance.new("ScreenGui")
	Main.Name = randomString()
	syn.protect_gui(Main)
	Main.Parent = game:GetService("CoreGui")
	PARENT = Main
elseif PROTOSMASHER_LOADED and get_hidden_gui then
	local Main = Instance.new("ScreenGui")
	Main.Name = randomString()
	Main.Parent = get_hidden_gui()
	PARENT = Main
--elseif elysianexecute and gethui then
--	local Main = Instance.new("ScreenGui")
--	Main.Name = randomString()
--	Main.Parent = gethui()
--	PARENT = Main
elseif game:GetService("CoreGui"):FindFirstChild('RobloxGui') then
	PARENT = game:GetService("CoreGui").RobloxGui
else
	local Main = Instance.new("ScreenGui")
	Main.Name = randomString()
	Main.Parent = game:GetService("CoreGui")
	PARENT = Main
end

if PARENT:FindFirstChild'Dex' then
	PARENT.Dex:Destroy();
end

local Dex = game:GetObjects("rbxassetid://3567096419")[1]
Dex.Name = 'Dex'
Dex.Parent = PARENT
	
local function Load(Obj)
	local function GiveOwnGlobals(Func, Script)
		local Fenv = {}
		local RealFenv = {script = Script}
		local FenvMt = {}
		FenvMt.__index = function(a,b)
			if RealFenv[b] == nil then
				return getfenv()[b]
			else
				return RealFenv[b]
			end
		end
		FenvMt.__newindex = function(a, b, c)
			if RealFenv[b] == nil then
				getfenv()[b] = c
			else
				RealFenv[b] = c
			end
		end
		setmetatable(Fenv, FenvMt)
		setfenv(Func, Fenv)
		return Func
	end
	local function LoadScripts(Script)
		if Script.ClassName == "Script" or Script.ClassName == "LocalScript" then
			spawn(function()
				GiveOwnGlobals(loadstring(Script.Source, "=" .. Script:GetFullName()), Script)()
			end)
		end
	    for i,v in pairs(Script:GetChildren()) do
			LoadScripts(v)
		end
	end
	LoadScripts(Obj)
end
	
Load(Dex)
