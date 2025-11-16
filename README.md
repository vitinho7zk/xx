local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

local Window = Rayfield:CreateWindow({
    Name = "Unity Nexus | Dead Rails",
    LoadingTitle = "Unity Nexus | Loading...",
    LoadingSubtitle = "Please wait...",
    ConfigurationSaving = {
        Enabled = true,
        FolderName = nil,
        FileName = "UnityNexus_Config"
    }
})

local PlayerTab = Window:CreateTab("Player")  
local PlayerSection = PlayerTab:CreateSection("Player Tab")  

PlayerTab:CreateSlider({
    Name = "WalkSpeed",
    Range = {16, 300},
    Increment = 1,
    Suffix = "Speed",
    CurrentValue = 16,
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
    end
})

PlayerTab:CreateSlider({
    Name = "JumpPower",
    Range = {50, 500},
    Increment = 1,
    Suffix = "Power",
    CurrentValue = 50,
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
    end
})

PlayerTab:CreateButton({
    Name = "Infinite Yield Admin",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
    end
})

PlayerTab:CreateButton({
    Name = "CMD-X Admin",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/CMD-X/CMD-X/master/Source"))()
    end
})

PlayerTab:CreateButton({
    Name = "Nameless Admin V2",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/FilteringEnabled/NamelessAdmin/main/Source"))()
    end
})

local MainTab = Window:CreateTab("Main")  
local MainSection = MainTab:CreateSection("Item Tweening")  

local TweenSpeed = 50  

MainTab:CreateSlider({
    Name = "Tween Speed",
    Range = {10, 200},
    Increment = 5,
    Suffix = "Speed",
    CurrentValue = 50,
    Callback = function(value)
        TweenSpeed = value
    end
})

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local HumanoidRootPart = Character:FindFirstChild("HumanoidRootPart")

local InteractiveItems = {
    "Revolver", "Sawed-off Shotgun", "Shotgun", "Rifle", "Bolt-Action Rifle", "Mauser",
    "Navy Revolver", "Crucifix", "Holy Water", "Molotov", "Shotgun Shells", "Rifle Ammo",
    "Revolver Ammo", "Turret Ammo", "Cannon Ammo", "Dynamite", "Helmet", "Left Shoulder Armor",
    "Right Shoulder Armor", "Chestplate", "Banjo", "Barbed Wire", "Bond", "Camera", "Coal",
    "Gold Bar", "Gold Cup", "Gold Painting", "Gold Plate", "Gold Statue", "Gold Watch", "Lantern",
    "Money Bag", "Saddle", "Sheet Metal", "Silver Bar", "Silver Cup", "Silver Painting",
    "Silver Plate", "Silver Statue", "Stone Statue", "Silver Watch", "Wooden Painting",
    "Barrel", "Book", "Chair", "Newspaper", "Rope", "Teapot", "Vase", "Wheel", "Bandage",
    "Snake Oil"
}

local ItemDropdown = MainTab:CreateDropdown({
    Name = "Select Item",
    Options = {},
    CurrentOption = nil,
    Callback = function(selectedItem)
        SelectedItem = selectedItem
    end
})

local function RefreshItemList()
    local FoundItems = {}
    for _, item in ipairs(workspace:GetChildren()) do
        if table.find(InteractiveItems, item.Name) and (item.Position - HumanoidRootPart.Position).Magnitude <= 500 then
            table.insert(FoundItems, item.Name)
        end
    end
    ItemDropdown:Refresh(FoundItems, true)
end

MainTab:CreateButton({
    Name = "Refresh Items",
    Callback = function()
        RefreshItemList()
    end
})

local function TweenToPosition(targetPosition)
    if not HumanoidRootPart then return end
    local TweenInfo = TweenInfo.new((HumanoidRootPart.Position - targetPosition).Magnitude / TweenSpeed, Enum.EasingStyle.Linear)
    local TweenGoal = {Position = targetPosition}
    local Tween = TweenService:Create(HumanoidRootPart, TweenInfo, TweenGoal)
    Tween:Play()
end

MainTab:CreateButton({
    Name = "Tween to Item",
    Callback = function()
        for _, item in ipairs(workspace:GetChildren()) do
            if item.Name == SelectedItem then
                TweenToPosition(item.Position)
                break
            end
        end
    end
})

MainTab:CreateButton({
    Name = "Tween to All Items",
    Callback = function()
        for _, item in ipairs(workspace:GetChildren()) do
            if table.find(InteractiveItems, item.Name) then
                TweenToPosition(item.Position)
                task.wait(2)  
            end
        end
    end
})

RefreshItemList()
