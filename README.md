--========================================================--
--   KAdaHUB REWRITED BY: jogaprovitinho // RLK_KZN8       --
--   V1 - Aimbot, ESP Players, ESP Itens, Auto Pickup      --
--========================================================--

local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/jensonhirst/Orion/main/source"))()

local Window = OrionLib:MakeWindow({
    Name = "VITINHO PAU DE DERRUBAR AVIÃO | jogaprovitinho // RLK_KZN8",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "VITINHO COME XOXOTA"
})

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")

--========================================================--
--                   VARIÁVEIS GLOBAIS
--========================================================--

getgenv().AimbotEnabled = false
getgenv().ESPPlayersEnabled = false
getgenv().ESPItemsEnabled = false
getgenv().AutoPickupEnabled = false

local ESPObjects = {}

--========================================================--
--                      FUNÇÃO AIMBOT
--========================================================--

function Aimbot()
    RunService.RenderStepped:Connect(function()
        if not getgenv().AimbotEnabled then return end

        local closest = nil
        local distance = 999999

        for _, plr in pairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild("Head") then
                local head = plr.Character.Head
                local dist = (head.Position - LocalPlayer.Character.Head.Position).Magnitude

                if dist < distance then
                    distance = dist
                    closest = head
                end
            end
        end

        if closest then
            LocalPlayer.Character.HumanoidRootPart.CFrame =
                CFrame.new(LocalPlayer.Character.HumanoidRootPart.Position, closest.Position)
        end
    end)
end

--========================================================--
--                 SISTEMA DE ESP (PLAYERS)
--========================================================--

function CreateESP(obj, color)
    local Billboard = Instance.new("BillboardGui")
    Billboard.Size = UDim2.new(0, 100, 0, 20)
    Billboard.AlwaysOnTop = true
    Billboard.Adornee = obj
    Billboard.Name = "ESP_TAG"

    local Text = Instance.new("TextLabel", Billboard)
    Text.Size = UDim2.new(1, 0, 1, 0)
    Text.BackgroundTransparency = 1
    Text.TextColor3 = color
    Text.TextScaled = true
    Text.Text = obj.Parent.Name

    Billboard.Parent = obj
end

function RemoveESP()
    for _, v in pairs(Workspace:GetDescendants()) do
        if v.Name == "ESP_TAG" then v:Destroy() end
    end
end

function ESPPlayers()
    RunService.RenderStepped:Connect(function()
        if not getgenv().ESPPlayersEnabled then
            RemoveESP()
            return
        end

        for _, plr in ipairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild("Head") then
                local head = plr.Character.Head
                if not head:FindFirstChild("ESP_TAG") then
                    CreateESP(head, Color3.new(1,0,0))
                end
            end
        end
    end)
end

--========================================================--
--                   ESP DE ITENS / ARMAS
--========================================================--

function ESPItems()
    RunService.RenderStepped:Connect(function()
        if not getgenv().ESPItemsEnabled then
            RemoveESP()
            return
        end

        for _, item in ipairs(Workspace:GetDescendants()) do
            if item:IsA("Tool") or item.Name:lower():match("gun") or item.Name:lower():match("item") then
                if not item:FindFirstChild("ESP_TAG") then
                    CreateESP(item, Color3.new(0, 1, 0))
                end
            end
        end
    end)
end

--========================================================--
--                 AUTO PICKUP (Puxar Itens)
--========================================================--

function AutoPickup()
    RunService.RenderStepped:Connect(function()
        if not getgenv().AutoPickupEnabled then return end

        for _, item in ipairs(Workspace:GetDescendants()) do
            if item:IsA("Tool") then
                item.Handle.CFrame = LocalPlayer.Character.HumanoidRootPart.CFrame
            end
        end
    end)
end

--========================================================--
--                    UI (OrionLib Tabs)
--========================================================--

local Main = Window:MakeTab({
    Name = "Combat",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

Main:AddToggle({
    Name = "Aimbot",
    Default = false,
    Callback = function(Value)
        getgenv().AimbotEnabled = Value
        if Value then Aimbot() end
    end
})

local EspTab = Window:MakeTab({
    Name = "ESP",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

EspTab:AddToggle({
    Name = "ESP Players",
    Default = false,
    Callback = function(Value)
        getgenv().ESPPlayersEnabled = Value
        if Value then ESPPlayers() end
    end
})

EspTab:AddToggle({
    Name = "ESP Itens / Armas",
    Default = false,
    Callback = function(Value)
        getgenv().ESPItemsEnabled = Value
        if Value then ESPItems() end
    end
})

local Loot = Window:MakeTab({
    Name = "Loot / Itens",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

Loot:AddToggle({
    Name = "Auto Pickup (Puxar Itens/Armas)",
    Default = false,
    Callback = function(Value)
        getgenv().AutoPickupEnabled = Value
        if Value then AutoPickup() end
    end
})

local Credits = Window:MakeTab({
    Name = "Créditos",
    Icon = "rbxassetid://4483345998",
})

Credits:AddLabel("Editado por: jogaprovitinho // RLK_KZN8")

Credits:AddButton({
    Name = "Discord (Clique Aqui)",
    Callback = function()
        setclipboard("https://discord.gg/BK58V5vRNv")
        OrionLib:MakeNotification({
            Name = "Discord Copiado!",
            Content = "Link copiado pro CTRL+V.",
            Time = 4
        })
    end
})

OrionLib:Init()
