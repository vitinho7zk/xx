--========================================================--
--            DEV TOOL HUB • MOBILE DARK EDITION
--             Feito especialmente para Vitinho M
--        IA + Itens + Inimigos + HUD Gamer Mobile
--========================================================--

local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Workspace = game:GetService("Workspace")

--========================================================--
--                 IA DEV — INIMIGOS & ITENS
--========================================================--

local DEV = {
    Enemies = {},
    Items = {},
}

-- INIMIGOS DO TIPO 2:
-- Model com PrimaryPart + Health: NumberValue
local function IsEnemy(model)
    if not model:IsA("Model") then return false end
    
    if model.PrimaryPart ~= nil and model:FindFirstChild("Health") then
        return true
    end

    return false
end

-- Itens podem ser Tools ou Models
local function IsItem(obj)
    if obj:IsA("Tool") then return true end
    if obj:IsA("Model") and obj.PrimaryPart then return true end
    return false
end

-- Scanner IA
task.spawn(function()
    while true do
        table.clear(DEV.Enemies)
        table.clear(DEV.Items)

        for _, obj in ipairs(Workspace:GetChildren()) do
            if IsEnemy(obj) then
                table.insert(DEV.Enemies, obj)
            elseif IsItem(obj) then
                table.insert(DEV.Items, obj)
            end
        end
        
        task.wait(0.5)
    end
end)

--========================================================--
--     FUNÇÕES DEV (puxar item, teleportar, dano, etc.)
--========================================================--

-- puxar item até o jogador
local function PullItem(item)
    if item.PrimaryPart then
        item:SetPrimaryPartCFrame(LocalPlayer.Character.HumanoidRootPart.CFrame)
    end
end

-- ir até item
local function TeleportToItem(item)
    if item.PrimaryPart then
        LocalPlayer.Character:MoveTo(item.PrimaryPart.Position)
    end
end

--DEV: matar inimigo modelo (tipo 2)
local function KillEnemy(enemy)
    if enemy:FindFirstChild("Health") then
        enemy.Health.Value = 0
    end
end

--Aimbot DEV mirando no PrimaryPart
local AimbotEnabled = false
RunService.RenderStepped:Connect(function()
    if not AimbotEnabled then return end

    local closest, dist = nil, 9999

    for _, enemy in ipairs(DEV.Enemies) do
        if enemy.PrimaryPart then
            local d = (enemy.PrimaryPart.Position - LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
            if d < dist then
                dist = d
                closest = enemy
            end
        end
    end

    if closest then
        LocalPlayer.Character.HumanoidRootPart.CFrame =
            CFrame.new(LocalPlayer.Character.HumanoidRootPart.Position, closest.PrimaryPart.Position)
    end
end)

--========================================================--
--                   HUD GAMER MOBILE DARK
--========================================================--

local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.ResetOnSpawn = false
ScreenGui.Name = "Vitinho_DEV_HUB"

-- Botão principal circular
local MainButton = Instance.new("ImageButton", ScreenGui)
MainButton.Size = UDim2.new(0, 70, 0, 70)
MainButton.Position = UDim2.new(0.04, 0, 0.45, 0)
MainButton.Image = "rbxassetid://3926305904"
MainButton.ImageRectOffset = Vector2.new(4, 4)
MainButton.ImageRectSize = Vector2.new(36, 36)
MainButton.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainButton.BorderSizePixel = 0

local Corner = Instance.new("UICorner", MainButton)
Corner.CornerRadius = UDim.new(1, 0)

-- Painel lateral
local Panel = Instance.new("Frame", ScreenGui)
Panel.Size = UDim2.new(0, 260, 1, 0)
Panel.Position = UDim2.new(-0.5, 0, 0, 0)
Panel.BackgroundColor3 = Color3.fromRGB(15, 15, 15)

local CornerPanel = Instance.new("UICorner", Panel)
CornerPanel.CornerRadius = UDim.new(0, 12)

local Stroke = Instance.new("UIStroke", Panel)
Stroke.Color = Color3.fromRGB(40, 40, 40)
Stroke.Thickness = 1

local Open = false
MainButton.MouseButton1Click:Connect(function()
    Open = not Open
    Panel:TweenPosition(
        UDim2.new(Open and 0 or -0.5, 0, 0, 0),
        Enum.EasingDirection.Out,
        Enum.EasingStyle.Quad,
        0.25
    )
end)

-- Lista rolável
local Scroll = Instance.new("ScrollingFrame", Panel)
Scroll.Size = UDim2.new(1, 0, 1, -20)
Scroll.Position = UDim2.new(0, 0, 0, 20)
Scroll.CanvasSize = UDim2.new(0, 0, 0, 800)
Scroll.BackgroundTransparency = 1
Scroll.ScrollBarThickness = 6

local List = Instance.new("UIListLayout", Scroll)
List.Padding = UDim.new(0, 12)
List.SortOrder = Enum.SortOrder.LayoutOrder

-- Criador de botões
local function CreateButton(text, callback)
    local Btn = Instance.new("TextButton", Scroll)
    Btn.Size = UDim2.new(1, -20, 0, 50)
    Btn.Position = UDim2.new(0, 10, 0, 0)
    Btn.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    Btn.TextColor3 = Color3.fromRGB(255,255,255)
    Btn.TextScaled = true
    Btn.Text = text
    Btn.BorderSizePixel = 0

    local C = Instance.new("UICorner", Btn)
    C.CornerRadius = UDim.new(0, 10)

    Btn.MouseButton1Click:Connect(callback)
end

--========================================================--
--                 BOTÕES + FUNÇÕES DEV
--========================================================--

CreateButton("Aimbot DEV", function()
    AimbotEnabled = not AimbotEnabled
    print("Aimbot DEV:", AimbotEnabled)
end)

CreateButton("Auto Kill Inimigos", function()
    for _, enemy in ipairs(DEV.Enemies) do
        KillEnemy(enemy)
    end
end)

CreateButton("Puxar TODOS Itens", function()
    for _, item in ipairs(DEV.Items) do
        PullItem(item)
    end
end)

CreateButton("Teleport até ITEM MAIS PRÓXIMO", function()
    local closest, dist = nil, 9999
    for _, item in ipairs(DEV.Items) do
        if item.PrimaryPart then
            local d = (item.PrimaryPart.Position - LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
            if d < dist then
                dist = d
                closest = item
            end
        end
    end
    if closest then
        TeleportToItem(closest)
    end
end)

CreateButton("Listar Itens no Console", function()
    print("===== ITENS DETECTADOS =====")
    for _, item in ipairs(DEV.Items) do
        print(item.Name)
    end
end)

CreateButton("Listar Inimigos no Console", function()
    print("===== INIMIGOS DETECTADOS =====")
    for _, enemy in ipairs(DEV.Enemies) do
        print(enemy.Name, "HP:", enemy.Health.Value)
    end
end)

-- Créditos
local Credits = Instance.new("TextLabel", Panel)
Credits.Text = "DEV HUB • Vitinho M"
Credits.TextColor3 = Color3.fromRGB(120,120,120)
Credits.TextScaled = true
Credits.BackgroundTransparency = 1
Credits.Size = UDim2.new(1, 0, 0, 40)
Credits.Position = UDim2.new(0, 0, 1, -40)

print("DEV HUB carregado com sucesso para Vitinho M!")
