--click to tp
local Imput = game:GetService("UserInputService")
local Plr = game:service'Players'.LocalPlayer
local Mouse = Plr:GetMouse()

function To(position)
    local Chr = Plr.Character
    if Chr ~= nil then
        Chr:MoveTo(position)
    end
end

Imput.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 and Imput:IsKeyDown(Enum.KeyCode.LeftControl) then
        To(Mouse.Hit.p)
    end
end)
