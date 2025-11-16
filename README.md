local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/jensonhirst/Orion/main/source"))()
local player = game.Players.LocalPlayer.Name

local Window = OrionLib:MakeWindow({
    Name = "KAdaHUB (Editado por jogaprovitinho // RLK_KZN8)",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "what"
})

---------------------------------------------------------------------
--  ABA PRINCIPAL
---------------------------------------------------------------------
local Tab = Window:MakeTab({
	Name = "Main",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

---------------------------------------------------------------------
--  ESP BUTTON
---------------------------------------------------------------------
Tab:AddButton({
	Name = "esp",
	Callback = function()
        -- Esp script for Dead Rails enemies  
        local RunService = game:GetService("RunService")  
        local UserInputService = game:GetService("UserInputService")  
        local Workspace = game:GetService("Workspace")

        while true do  
            local rayParams = RaycastParams.new()  
            rayParams.FilterType = Enum.RaycastFilterType.IgnoreWater
            local char = game.Players.LocalPlayer.Character
            if not char then break end

            local rayResult = Workspace:Raycast(
                char.HumanoidRootPart.Position,
                char.HumanoidRootPart.CFrame.LookVector * 100,
                rayParams
            )

            if rayResult and rayResult.Instance:IsA("Model") and rayResult.Instance:FindFirstChild("Humanoid") then  
                drawing:Text(rayResult.Instance.Name, Vector2.new(50,50), Color3.new(1,1,1), true)
            end
            task.wait(0.1)
        end  
    end
})

---------------------------------------------------------------------
--  KILLAURA BUTTON
---------------------------------------------------------------------
Tab:AddButton({
	Name = "swing killaura",
	Callback = function()
        local UserInputService = game:GetService("UserInputService")  
        local Workspace = game:GetService("Workspace")
        local swinging = false
        
        UserInputService.InputBegan:Connect(function(input)
            if input.KeyCode == Enum.KeyCode.E then
                swinging = true
            end
        end)

        while true do
            if swinging then
                swinging = false

                local char = game.Players.LocalPlayer.Character
                if not char then continue end

                local rayResult = Workspace:Raycast(
                    char.HumanoidRootPart.Position,
                    char.HumanoidRootPart.CFrame.LookVector * 100
                )

                if rayResult and rayResult.Instance:FindFirstChild("Humanoid") then
                    rayResult.Instance.Humanoid.Health = 0
                end
            end
            task.wait(0.1)
        end
    end
})

---------------------------------------------------------------------
--  TELEPORT
---------------------------------------------------------------------
local TpTab = Window:MakeTab({
	Name = "tp",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

TpTab:AddButton({
	Name = "tesla",
	Callback = function()
        game.Players.LocalPlayer.Character:MoveTo(Vector3.new(-124745.677, 40875.192, 63567.292))
	end    
})

---------------------------------------------------------------------
--  SETTINGS
---------------------------------------------------------------------
local Settings = Window:MakeTab({
	Name = "settings",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

Settings:AddColorpicker({
	Name = "UI Color",
	Default = Color3.fromRGB(0, 140, 255),
	Callback = function(Value)
		print("Color:", Value)
	end
})

---------------------------------------------------------------------
--  CRÉDITOS + DISCORD
---------------------------------------------------------------------
local Credits = Window:MakeTab({
	Name = "credit",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

Credits:AddLabel("Script editado por: jogaprovitinho // RLK_KZN8")
Credits:AddLabel("Discord Oficial:")

Credits:AddButton({
	Name = "Entrar no Discord",
	Callback = function()
        setclipboard("https://discord.gg/BK58V5vRNv")
        OrionLib:MakeNotification({
            Name = "Discord copiado!",
            Content = "Link copiado! Cole no navegador.",
            Image = "rbxassetid://4483345998",
            Time = 4
        })
	end
})

---------------------------------------------------------------------
OrionLib:Init()
