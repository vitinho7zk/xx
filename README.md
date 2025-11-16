--========================================================--
--           DEAD RAILS HUB V5 – DARK UI + IA  
--    Feito para Sofia — jogaprovitinho // RLK_KZN8  
--========================================================--

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Workspace = game:GetService("Workspace")
local RunService = game:GetService("RunService")

--========================================================--
--                 IA – DETECTOR AUTOMÁTICO
--========================================================--

AI = {
    Enemies = {},
    Items = {},
}

function IsEnemy(model)
    if not model:IsA("Model") then return false end
    if model:FindFirstChild("Humanoid") and model:FindFirstChild("HumanoidRootPart") then
        local isPlayer = Players:GetPlayerFromCharacter(model)
        if not isPlayer and model.Humanoid.MaxHealth > 40 then
            return true
        end
    end
    return false
end

function IsItem(obj)
    if obj:IsA("Tool") then return true end
    if obj:FindFirstChild("Handle") then return true end
    local name = obj.Name:lower()
    return name:match("gun") or name:match("ammo") or name:match("item")
end

function AI.Scan()
    table.clear(AI.Enemies)
    table.clear(AI.Items)

    for _, obj in ipairs(Workspace:GetDescendants()) do
        
        if IsEnemy(obj) then
            table.insert(AI.Enemies, obj)
        
        elseif IsItem(obj) then
            table.insert(AI.Items, obj)
        
        end
    end
end

task.spawn(function()
    while true do
        AI.Scan()
        task.wait(0.5)
    end
end)

--========================================================--
--                       SISTEMAS
--========================================================--

getgenv().Aimbot = false
getgenv().SilentAim = false
getgenv().AutoKill = false
getgenv().ESP_Enemies = false
getgenv().ESP_Items = false
getgenv().AutoPickup = false

-- AIMBOT
task.spawn(function()
    RunService.RenderStepped:Connect(function()
        if not getgenv().Aimbot then return end
        
        local closest, dist = nil, 9999
        
        for _, enemy in ipairs(AI.Enemies) do
            local hrp = enemy:FindFirstChild("HumanoidRootPart")
            if hrp then
                local d = (hrp.Position - LocalPlayer.Character.Head.Position).Magnitude
                if d < dist then
                    dist = d
                    closest = hrp
                end
            end
        end
        
        if closest then
            LocalPlayer.Character.HumanoidRootPart.CFrame =
                CFrame.new(LocalPlayer.Character.HumanoidRootPart.Position, closest.Position)
        end
    end)
end)

-- AUTO KILL
task.spawn(function()
    while true do
        if getgenv().AutoKill then
            for _, enemy in ipairs(AI.Enemies) do
                if enemy:FindFirstChild("Humanoid") then
                    enemy.Humanoid.Health = 0
                end
            end
        end
        task.wait(0.1)
    end
end)

-- AUTO PICKUP
task.spawn(function()
    while true do
        if getgenv().AutoPickup then
            for _, item in ipairs(AI.Items) do
                local h = item:FindFirstChild("Handle")
                if h then
                    h.CFrame = LocalPlayer.Character.HumanoidRootPart.CFrame
                end
            end
        end
        task.wait(0.1)
    end
end)

--========================================================--
--                       ESP
--========================================================--

function CreateESP(obj, text, color)
    if obj:FindFirstChild("DRH_ESP") then return end

    local tag = Instance.new("BillboardGui", obj)
    tag.Name = "DRH_ESP"
    tag.Adornee = obj
    tag.Size = UDim2.new(4, 0, 1, 0)
    tag.AlwaysOnTop = true

    local label = Instance.new("TextLabel", tag)
    label.Size = UDim2.new(1,0,1,0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = color
    label.TextScaled = true
end

task.spawn(function()
    while true do
        if getgenv().ESP_Enemies then
            for _, enemy in ipairs(AI.Enemies) do
                if enemy:FindFirstChild("Head") then
                    CreateESP(enemy.Head, "Enemy", Color3.new(1,0,0))
                end
            end
        end
        
        if getgenv().ESP_Items then
            for _, item in ipairs(AI.Items) do
                local h = item:FindFirstChild("Handle") or item
                CreateESP(h, item.Name, Color3.new(0,1,0))
            end
        end
        
        task.wait(0.4)
    end
end)

--========================================================--
--                     UI DARK MINIMAL
--========================================================--

local Screen = Instance.new("ScreenGui", game.CoreGui)
local Frame = Instance.new("Frame", Screen)
Frame.Size = UDim2.new(0, 260, 0, 350)
Frame.Position = UDim2.new(0.1, 0, 0.2, 0)
Frame.BackgroundColor3 = Color3.fromRGB(20,20,20)
Frame.BorderSizePixel = 0

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1,0,0,40)
Title.BackgroundTransparency = 1
Title.Text = "Dead Rails Hub V5"
Title.TextColor3 = Color3.fromRGB(255,255,255)
Title.TextScaled = true

function AddToggle(name, callback)
    local btn = Instance.new("TextButton", Frame)
    btn.Size = UDim2.new(1,-20,0,35)
    btn.Position = UDim2.new(0,10,0, 45 + (#Frame:GetChildren()-1)*40)
    btn.BackgroundColor3 = Color3.fromRGB(30,30,30)
    btn.TextColor3 = Color3.new(1,1,1)
    btn.TextScaled = true
    btn.Text = name .. ": OFF"

    local state = false

    btn.MouseButton1Click:Connect(function()
        state = not state
        btn.Text = name .. ": " .. (state and "ON" or "OFF")
        callback(state)
    end)
end

-- Toggles
AddToggle("Aimbot", function(v) getgenv().Aimbot = v end)
AddToggle("Auto Kill", function(v) getgenv().AutoKill = v end)
AddToggle("ESP Inimigos", function(v) getgenv().ESP_Enemies = v end)
AddToggle("ESP Itens", function(v) getgenv().ESP_Items = v end)
AddToggle("Auto Pickup", function(v) getgenv().AutoPickup = v end)

