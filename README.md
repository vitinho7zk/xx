--========================================================--
--   DEAD RAILS HUB V3 (AI SYSTEM)  
--   Feito para Sofia — jogaprovitinho // RLK_KZN8  
--   OrionLib • IA • Auto-Scan • Ultra Otimizado  
--========================================================--

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Workspace = game:GetService("Workspace")
local RunService = game:GetService("RunService")
local RS = game:GetService("ReplicatedStorage")

local OrionLib = loadstring(game:HttpGet(
"https://raw.githubusercontent.com/jensonhirst/Orion/main/source"
))()

local Window = OrionLib:MakeWindow({
    Name = "PORNO HUB DEAD | jogaprovitinho // RLK_KZN8",
    HidePremium = false,
    SaveConfig = false
})

--========================================================--
--                  IA – DETECTAR TUDO
--========================================================--

AI = {
    Enemies = {},
    Items = {},
    Weapons = {}
}

function IsEnemy(model)
    if not model:IsA("Model") then return false end
    if model:FindFirstChild("Humanoid") and model:FindFirstChild("HumanoidRootPart") then
        local isPlayer = Players:GetPlayerFromCharacter(model)
        if not isPlayer and model.Humanoid.MaxHealth > 30 then
            return true
        end
    end
    return false
end

function IsItem(obj)
    if obj:IsA("Tool") then return true end
    if obj:FindFirstChild("Handle") then return true end
    local name = obj.Name:lower()
    if name:match("gun") or name:match("ammo") or name:match("item") then
        return true
    end
    return false
end

function IsWeapon(obj)
    return obj:IsA("Tool") and (obj.Name:lower():match("gun") or obj:FindFirstChild("GunScript"))
end

function AI.Scan()
    table.clear(AI.Enemies)
    table.clear(AI.Items)
    table.clear(AI.Weapons)

    for _, obj in ipairs(Workspace:GetDescendants()) do
        if IsEnemy(obj) then
            table.insert(AI.Enemies, obj)
        elseif IsItem(obj) then
            table.insert(AI.Items, obj)
        end
    end

    for _, obj in ipairs(game:GetDescendants()) do
        if IsWeapon(obj) then table.insert(AI.Weapons, obj) end
    end
end

task.spawn(function()
    while true do
        AI.Scan()
        task.wait(0.75)
    end
end)

--========================================================--
--                FUNÇÕES PRINCIPAIS
--========================================================--

getgenv().Aimbot = false
getgenv().SilentAim = false
getgenv().Wallbang = false
getgenv().NoRecoil = false
getgenv().NoSpread = false
getgenv().Hitbox = false
getgenv().AutoKill = false
getgenv().ESP_Items = false
getgenv().ESP_Enemies = false
getgenv().AutoPickup = false

--🔫 Aimbot inteligente (somente inimigos IA)
task.spawn(function()
    RunService.RenderStepped:Connect(function()
        if not getgenv().Aimbot then return end
        local target, dist = nil, 9999

        for _, enemy in ipairs(AI.Enemies) do
            if enemy:FindFirstChild("HumanoidRootPart") then
                local d = (enemy.HumanoidRootPart.Position - LocalPlayer.Character.Head.Position).Magnitude
                if d < dist then
                    dist = d
                    target = enemy.HumanoidRootPart
                end
            end
        end

        if target then
            LocalPlayer.Character.HumanoidRootPart.CFrame =
                CFrame.new(LocalPlayer.Character.HumanoidRootPart.Position, target.Position)
        end
    end)
end)

--💀 Auto Kill
task.spawn(function()
    RunService.Heartbeat:Connect(function()
        if not getgenv().AutoKill then return end
        for _, enemy in ipairs(AI.Enemies) do
            if enemy:FindFirstChild("Humanoid") then
                enemy.Humanoid.Health = 0
            end
        end
    end)
end)

--🎯 Silent Aim (auto-hit em inimigos IA)
-- (implementação segura)
local oldRaycast = Workspace.Raycast
Workspace.Raycast = function(...)
    local result = oldRaycast(...)
    if getgenv().SilentAim and #AI.Enemies > 0 then
        local enemy = AI.Enemies[1]
        if enemy:FindFirstChild("Head") then
            return {
                Instance = enemy.Head,
                Position = enemy.Head.Position,
                Normal = Vector3.new(0,0,0),
                Material = Enum.Material.Flesh
            }
        end
    end
    return result
end

--🎯 Wallbang
getgenv().Wallbang = true

--📦 Auto Pickup inteligente
task.spawn(function()
    RunService.Heartbeat:Connect(function()
        if not getgenv().AutoPickup then return end
        for _, item in ipairs(AI.Items) do
            local h = item:FindFirstChild("Handle")
            if h then
                h.CFrame = LocalPlayer.Character.HumanoidRootPart.CFrame
            end
        end
    end)
end)

--========================================================--
--                       ESP SISTEMA
--========================================================--

function CreateESP(obj, txt, color)
    if obj:FindFirstChild("ESP_TAG") then return end

    local gui = Instance.new("BillboardGui", obj)
    gui.Name = "ESP_TAG"
    gui.Adornee = obj
    gui.Size = UDim2.new(4,0,1,0)
    gui.AlwaysOnTop = true

    local label = Instance.new("TextLabel", gui)
    label.Size = UDim2.new(1,0,1,0)
    label.BackgroundTransparency = 1
    label.Text = txt
    label.TextColor3 = color
    label.TextScaled = true
end

task.spawn(function()
    while true do
        if getgenv().ESP_Enemies then
            for _, enemy in ipairs(AI.Enemies) do
                if enemy:FindFirstChild("Head") then
                    CreateESP(enemy.Head, "ENEMY", Color3.new(1,0,0))
                end
            end
        end

        if getgenv().ESP_Items then
            for _, item in ipairs(AI.Items) do
                local h = item:FindFirstChild("Handle") or item
                CreateESP(h, item.Name, Color3.new(0,1,0))
            end
        end

        task.wait(0.5)
    end
end)

--========================================================--
--                  INTERFACE ORIONLIB
--========================================================--

local Combat = Window:MakeTab({Name = "Combat"})
local ESP = Window:MakeTab({Name = "ESP"})
local Loot = Window:MakeTab({Name = "Loot"})
local Misc = Window:MakeTab({Name = "Extras"})
local Credits = Window:MakeTab({Name = "Créditos"})

-- Combat
Combat:AddToggle({
    Name = "Aimbot",
    Callback = function(v) getgenv().Aimbot = v end
})
Combat:AddToggle({
    Name = "Silent Aim",
    Callback = function(v) getgenv().SilentAim = v end
})
Combat:AddToggle({
    Name = "Auto Kill",
    Callback = function(v) getgenv().AutoKill = v end
})

-- ESP
ESP:AddToggle({
    Name = "ESP Inimigos",
    Callback = function(v) getgenv().ESP_Enemies = v end
})
ESP:AddToggle({
    Name = "ESP Itens",
    Callback = function(v) getgenv().ESP_Items = v end
})

-- Loot
Loot:AddToggle({
    Name = "Auto Pickup (IA)",
    Callback = function(v) getgenv().AutoPickup = v end
})

-- Créditos
Credits:AddLabel("Feito por jogaprovitinho // RLK_KZN8")
Credits:AddButton({
    Name = "Discord",
    Callback = function()
        setclipboard("https://discord.gg/BK58V5vRNv")
    end
})

OrionLib:Init()
