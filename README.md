local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()
 
local Window = Fluent:CreateWindow({
    Title = "BANNED STORE | V1 ",
    SubTitle = "by jogaprovitinho//RLK_KZN8",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = false, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Amethyst",
    MinimizeKey = Enum.KeyCode.RightControl -- Used when theres no MinimizeKeybind
})
 
--Fluent provides Lucide Icons https://lucide.dev/icons/ for the tabs, icons are optional
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "menu" }),
    Universal = Window:AddTab({ Title = "Universal", Icon = "globe" }),
	jumpeverysec = Window:AddTab({ Title = "1 Jump Every Sec", Icon = "gamepad" }),
	v1v1pistol = Window:AddTab({ Title = "1v1 Pistol", Icon = "gamepad" }),
	c3008 = Window:AddTab({ Title = "3008", Icon = "gamepad" }),
	Abilitywars = Window:AddTab({ Title = "Ability Wars", Icon = "gamepad" }),
	Ageofheroes = Window:AddTab({ Title = "Age of Heroes", Icon = "gamepad" }),
	Aimblox = Window:AddTab({ Title = "Aimblox", Icon = "gamepad" }),
	Animefightersim = Window:AddTab({ Title = "Anime Fighter Sim", Icon = "gamepad" }),
	Animespeedrace = Window:AddTab({ Title = "Anime Speed Race", Icon = "gamepad" }),
	Antlife = Window:AddTab({ Title = "Ant Life", Icon = "gamepad" }),
	Arsenal = Window:AddTab({ Title = "Arsenal", Icon = "gamepad" }),
	Attackontitan = Window:AddTab({ Title = "Attack on Titan", Icon = "gamepad" }),
	Basketballlegends = Window:AddTab({ Title = "Basketball Legends", Icon = "gamepad" }),
	Beaduck = Window:AddTab({ Title = "Be a Duck", Icon = "gamepad" }),
	Benpcordie = Window:AddTab({ Title = "Be NPC or Die", Icon = "gamepad" }),
	Beattherobloxian = Window:AddTab({ Title = "Beat the Robloxian", Icon = "gamepad" }),
	BedWars = Window:AddTab({ Title = "Bed Wars", Icon = "gamepad" }),
	Bettermusic = Window:AddTab({ Title = "Better Music", Icon = "gamepad" }),
	BladeBall = Window:AddTab({ Title = "Blade Ball", Icon = "gamepad" }),
	Bladeslayer = Window:AddTab({ Title = "Blade Slayer", Icon = "gamepad" }),
	Bloxhunt = Window:AddTab({ Title = "Blox Hunt", Icon = "gamepad" }),
	Bloxburg = Window:AddTab({ Title = "Bloxburg", Icon = "gamepad" }),
	Bloxfruit = Window:AddTab({ Title = "Bloxfruit", Icon = "gamepad" }),
	Blockdiggingsim = Window:AddTab({ Title = "Block Digging Sim", Icon = "gamepad" }),
	Boxingleague = Window:AddTab({ Title = "Boxing League", Icon = "gamepad" }),
	Breakin2 = Window:AddTab({ Title = "Break in 2", Icon = "gamepad" }),
	Breakingpoint = Window:AddTab({ Title = "Breaking Point", Icon = "gamepad" }),
	BrimsRNG = Window:AddTab({ Title = "Brims RNG", Icon = "gamepad" }),
	Brookhaven = Window:AddTab({ Title = "Brookhaven", Icon = "gamepad" }),
	Buildaboatfortreasure = Window:AddTab({ Title = "Build a Boat for Treasure", Icon = "gamepad" }),
	Buildabunkertosurvivezombies = Window:AddTab({ Title = "Build a Bunker to Survive Zombies", Icon = "gamepad" }),
	Calishotout = Window:AddTab({ Title = "Cali Shotout", Icon = "gamepad" }),
	CardRNG = Window:AddTab({ Title = "Card RNG", Icon = "gamepad" }),
	Cardealershiptycoon = Window:AddTab({ Title = "Car Dealership Tycoon", Icon = "gamepad" }),
	Clickermadness = Window:AddTab({ Title = "Clicker Madness", Icon = "gamepad" }),
	Combatwarriors = Window:AddTab({ Title = "Combat Warriors", Icon = "gamepad" }),
	Counterblox = Window:AddTab({ Title = "Counterblox", Icon = "gamepad" }),
	Criminality = Window:AddTab({ Title = "Criminality", Icon = "gamepad" }),
	Damtycoon = Window:AddTab({ Title = "Dam Tycoon", Icon = "gamepad" }),
	DaHood = Window:AddTab({ Title = "DaHood", Icon = "gamepad" }),
	DaHoodcustom = Window:AddTab({ Title = "DaHood Custom", Icon = "gamepad" }),
	Deacyingwinter = Window:AddTab({ Title = "Decaying Winter", Icon = "gamepad" }),
	Demonfall = Window:AddTab({ Title = "Demonfall", Icon = "gamepad" }),
	Doomspirebrickbattle = Window:AddTab({ Title = "Doomspire Brickbattle", Icon = "gamepad" }),
	Doors = Window:AddTab({ Title = "Doors", Icon = "gamepad" }),
	Driveworld = Window:AddTab({ Title = "Drive World", Icon = "gamepad" }),
	Drivingempire = Window:AddTab({ Title = "Driving Empire", Icon = "gamepad" }),
	Dungeonquest = Window:AddTab({ Title = "Dungeon Quest", Icon = "gamepad" }),
	Dustytrip = Window:AddTab({ Title = "Dusty Trip", Icon = "gamepad" }),
	Eatslimestogrowhuge = Window:AddTab({ Title = "East Slimes to Grow Huge", Icon = "gamepad" }),
	Epicminigames = Window:AddTab({ Title = "Epic Minigames", Icon = "gamepad" }),
	Evade = Window:AddTab({ Title = "Evade", Icon = "gamepad" }),
	FF2 = Window:AddTab({ Title = "FF2", Icon = "gamepad" }),
	Fightinaschool = Window:AddTab({ Title = "Fight in a School", Icon = "gamepad" }),
	Findtheauras = Window:AddTab({ Title = "Find the Auras", Icon = "gamepad" }),
	Findtheflag = Window:AddTab({ Title = "Find the Flag", Icon = "gamepad" }),
	Fleethefacility = Window:AddTab({ Title = "Flee the Facility", Icon = "gamepad" }),
	Flingthingsandpeople = Window:AddTab({ Title = "Fling Things and People", Icon = "gamepad" }),
	Frontlines = Window:AddTab({ Title = "Frontlines", Icon = "gamepad" }),
	Fruitarena = Window:AddTab({ Title = "Fruit Arena", Icon = "gamepad" }),
	Fruitswarriors = Window:AddTab({ Title = "Fruits Warriors", Icon = "gamepad" }),
	FudgeRNG = Window:AddTab({ Title = "Fudge RNG", Icon = "gamepad" }),
	Ganguponpeoplesim = Window:AddTab({ Title = "Gang up on People Sim", Icon = "gamepad" }),
	Gethitbyacarsim = Window:AddTab({ Title = "Get Hit by a Car Sim", Icon = "gamepad" }),
	Godswill = Window:AddTab({ Title = "Gods Will", Icon = "gamepad" }),
	Gymleague = Window:AddTab({ Title = "Gym League", Icon = "gamepad" }),
	Gunball = Window:AddTab({ Title = "Gun Ball", Icon = "gamepad" }),
	Gunfightarena = Window:AddTab({ Title = "Gun Fight Arena", Icon = "gamepad" }),
	Hardtime = Window:AddTab({ Title = "Hard Time", Icon = "gamepad" }),
	Hellmet = Window:AddTab({ Title = "Hellmet", Icon = "gamepad" }),
	Hideandseekextreme = Window:AddTab({ Title = "Hide and Seek Extreme", Icon = "gamepad" }),
	Hoopslife = Window:AddTab({ Title = "Hoops Life", Icon = "gamepad" }),
	Hoopz = Window:AddTab({ Title = "Hoopz", Icon = "gamepad" }),
	HorrorsRNG = Window:AddTab({ Title = "Horror's RNG", Icon = "gamepad" }),
	Horrifichousing = Window:AddTab({ Title = "Horrific Housing", Icon = "gamepad" }),
	Icespiceobby = Window:AddTab({ Title = "Ice Spice Obby", Icon = "gamepad" }),
	Impossibleobby = Window:AddTab({ Title = "Impossible Obby", Icon = "gamepad" }),
	Impossiblesquidgameglass = Window:AddTab({ Title = "Impossible Squid Game Glass", Icon = "gamepad" }),
	Jailbird = Window:AddTab({ Title = "Jailbird", Icon = "gamepad" }),
	Jailbreak = Window:AddTab({ Title = "Jailbreak", Icon = "gamepad" }),
	Jujutsushenanigans = Window:AddTab({ Title = "Jujutsu Shenanigans", Icon = "gamepad" }),
	Kaijuparadise = Window:AddTab({ Title = "Kaiju Paradise", Icon = "gamepad" }),
	KAT = Window:AddTab({ Title = "KAT", Icon = "gamepad" }),
	Launchintospace = Window:AddTab({ Title = "Launch into Space Sim", Icon = "gamepad" }),
	Legendofspeed = Window:AddTab({ Title = "Legend of Speed", Icon = "gamepad" }),
	Lifeinparadise = Window:AddTab({ Title = "Life in Paradise", Icon = "gamepad" }),
	liftingsim = Window:AddTab({ Title = "Lifting Sim", Icon = "gamepad" }),
	Lumbertycoon2 = Window:AddTab({ Title = "Lumber Tycoon 2", Icon = "gamepad" }),
	MagicRNG = Window:AddTab({ Title = "Magic RNG", Icon = "gamepad" }),
	Mansiontycoon = Window:AddTab({ Title = "Mansion Tycoon", Icon = "gamepad" }),
	Megaprincesstycoon = Window:AddTab({ Title = "Mega Princess Tycoon", Icon = "gamepad" }),
	Micup = Window:AddTab({ Title = "Mic Up", Icon = "gamepad" }),
	Moneygrabsim = Window:AddTab({ Title = "Money Grab Sim", Icon = "gamepad" }),
	Moneyrollsim = Window:AddTab({ Title = "Money Roll Sim", Icon = "gamepad" }),
	MurdervsSherrif = Window:AddTab({ Title = "Murder vs Sheriff", Icon = "gamepad" }),
	Musclelegends = Window:AddTab({ Title = "Muscle Legends", Icon = "gamepad" }),
	Museumsim = Window:AddTab({ Title = "Museum Sim", Icon = "gamepad" }),
	Naturaldisaster = Window:AddTab({ Title = "Natural Disaster", Icon = "gamepad" }),
	Ninjalegends = Window:AddTab({ Title = "Ninja Legends", Icon = "gamepad" }),
	Noscopesniping = Window:AddTab({ Title = "No Scope Sniping", Icon = "gamepad" }),
	Operationsiege = Window:AddTab({ Title = "Operation Siege", Icon = "gamepad" }),
	ParadiseRP = Window:AddTab({ Title = "Paradise RP", Icon = "gamepad" }),
	Parkour = Window:AddTab({ Title = "Parkour", Icon = "gamepad" }),
	Petsim99 = Window:AddTab({ Title = "Pet Sim 99", Icon = "gamepad" }),
	Phantomforces = Window:AddTab({ Title = "Phantom Forces", Icon = "gamepad" }),
	Piggy = Window:AddTab({ Title = "Piggy", Icon = "gamepad" }),
	Pixelincremental2 = Window:AddTab({ Title = "Pixel Incremental 2", Icon = "gamepad" }),
	Plsdonate = Window:AddTab({ Title = "Pls Donate", Icon = "gamepad" }),
	Pizzaclicker = Window:AddTab({ Title = "Pizza Clicker", Icon = "gamepad" }),
	Projectdelta = Window:AddTab({ Title = "Project Delta", Icon = "gamepad" }),
	Projectslayer = Window:AddTab({ Title = "Project Slayer", Icon = "gamepad" }),
	Prisonlife = Window:AddTab({ Title = "Prison Life", Icon = "gamepad" }),
	Pullasword = Window:AddTab({ Title = "Pull a Sword", Icon = "gamepad" }),
	Ragdollengine = Window:AddTab({ Title = "Ragdoll Engine", Icon = "gamepad" }),
	Rainbowfriends = Window:AddTab({ Title = "Rainbow Friends", Icon = "gamepad" }),
	Raiseafloppa2 = Window:AddTab({ Title = "Raise a Floppa 2", Icon = "gamepad" }),
	REXL = Window:AddTab({ Title = "RE:XL", Icon = "gamepad" }),
	Rebornasaswordman = Window:AddTab({ Title = "Reborn as a Swordsman", Icon = "gamepad" }),
	Ridethetraintocactus = Window:AddTab({ Title = "Ride the Train to Cactus", Icon = "gamepad" }),
	Roach = Window:AddTab({ Title = "Roach", Icon = "gamepad" }),
	Scythesim = Window:AddTab({ Title = "Scythe Sim", Icon = "gamepad" }),
	Sharkbite2 = Window:AddTab({ Title = "Shark Bite 2", Icon = "gamepad" }),
	Shinobistorm = Window:AddTab({ Title = "Shinobi Storm", Icon = "gamepad" }),
	Simpleincremental = Window:AddTab({ Title = "Simple Incremental", Icon = "gamepad" }),
	SolsRNG = Window:AddTab({ Title = "Sol's RNG", Icon = "gamepad" }),
	Southbronx = Window:AddTab({ Title = "South Bronx", Icon = "gamepad" }),
	Sourpatchkidsgame = Window:AddTab({ Title = "Sour Patch Kids Game", Icon = "gamepad" }),
	Stateofanarchy = Window:AddTab({ Title = "State of Anarchy", Icon = "gamepad" }),
	Stealtimefromothers = Window:AddTab({ Title = "Steal Time from Others", Icon = "gamepad" }),
	Strucid = Window:AddTab({ Title = "Strucid", Icon = "gamepad" }),
	Sukunabattlegrounds = Window:AddTab({ Title = "Sukuna Battlegrounds", Icon = "gamepad" }),
	Supermusclesim = Window:AddTab({ Title = "Super Muscle Sim", Icon = "gamepad" }),
	Swordtrainingsim = Window:AddTab({ Title = "Sword Training Sim", Icon = "gamepad" }),
	Taxiboss = Window:AddTab({ Title = "Taxi Boss", Icon = "gamepad" }),
	Teddyescape = Window:AddTab({ Title = "Teddy Escape", Icon = "gamepad" }),
	Tennissim = Window:AddTab({ Title = "Tennis Sim", Icon = "gamepad" }),
	Theclassic = Window:AddTab({ Title = "The Classic", Icon = "gamepad" }),
	Therake = Window:AddTab({ Title = "The Rake", Icon = "gamepad" }),
	Therakeremastered = Window:AddTab({ Title = "The Rake Remastered", Icon = "gamepad" }),
	Therpgmines = Window:AddTab({ Title = "The RPG Mines", Icon = "gamepad" }),
	Thestrongestbattleground = Window:AddTab({ Title = "The Strongest Battleground", Icon = "gamepad" }),
	Therapy = Window:AddTab({ Title = "Therapy", Icon = "gamepad" }),
	TMNTBattletycoon = Window:AddTab({ Title = "TMNT Battle Tycoon", Icon = "gamepad" }),
	Totalrobloxdrama = Window:AddTab({ Title = "Total Roblox Drama", Icon = "gamepad" }),
	Towerofhell = Window:AddTab({ Title = "Tower of Hell", Icon = "gamepad" }),
	Trackandfieldinfinite = Window:AddTab({ Title = "Track and Field Infinite", Icon = "gamepad" }),
	Treasurehuntsim = Window:AddTab({ Title = "Treasure Hunt Sim", Icon = "gamepad" }),
	TPSstreetsoccer = Window:AddTab({ Title = "TPS Street Soccer", Icon = "gamepad" }),
	Typesoul = Window:AddTab({ Title = "Type Soul", Icon = "gamepad" }),
	TycoonRNG = Window:AddTab({ Title = "Tycoon RNG", Icon = "gamepad" }),
	Ultrathegame = Window:AddTab({ Title = "Ultra the Game", Icon = "gamepad" }),
	Undergroundwar2 = Window:AddTab({ Title = "Underground War 2", Icon = "gamepad" }),
	Untitledtaggame = Window:AddTab({ Title = "Untitled Tag Game", Icon = "gamepad" }),
	Vehiclelegends = Window:AddTab({ Title = "Vehicle Legends", Icon = "gamepad" }),
	Wackywizard = Window:AddTab({ Title = "Wacky Wizard", Icon = "gamepad" }),
	Wartycoon = Window:AddTab({ Title = "War Tycoon", Icon = "gamepad" }),
	Warriorssim = Window:AddTab({ Title = "Warriors Sim", Icon = "gamepad" }),
	Westbound = Window:AddTab({ Title = "Westbound", Icon = "gamepad" }),
	Wordle = Window:AddTab({ Title = "Wordle", Icon = "gamepad" }),
	YBA = Window:AddTab({ Title = "YBA", Icon = "gamepad" }),
	Zombieattack = Window:AddTab({ Title = "Zombie Attack", Icon = "gamepad" })
}
 
local Options = Fluent.Options
 
do
    Fluent:Notify({
        Title = "Welcome!",
        Content = "Welcome to the Hub",
        SubContent = "D6 made this", -- Optional
        Duration = 5 -- Set to nil to make the notification not disappear
    })
 
 
 
    Tabs.Main:AddParagraph({
        Title = "EC Hub",
        Content = "Welcome to the Exploit Central Hub.\nJoin our Discord for more!"
    })
 
    Tabs.Main:AddButton({
        Title = "Server invite",
        Description = "Copy our Discord server invite",
        Callback = function()
            setclipboard("https://discord.gg/hAmMkNSyTV")
        end
    })
 
    Tabs.Universal:AddButton({
        Title = "Universal Aimbot",
        Description = "",
        Callback = function()
            local Camera = workspace.CurrentCamera
            local Players = game:GetService("Players")
            local RunService = game:GetService("RunService")
            local UserInputService = game:GetService("UserInputService")
            local TweenService = game:GetService("TweenService")
            local LocalPlayer = Players.LocalPlayer
            local Holding = false
 
            _G.AimbotEnabled = true
            _G.TeamCheck = false -- If set to true then the script would only lock your aim at enemy team members.
            _G.AimPart = "Head" -- Where the aimbot script would lock at.
            _G.Sensitivity = 0 -- How many seconds it takes for the aimbot script to officially lock onto the target's aimpart.
 
            _G.CircleSides = 64 -- How many sides the FOV circle would have.
            _G.CircleColor = Color3.fromRGB(255, 255, 255) -- (RGB) Color that the FOV circle would appear as.
            _G.CircleTransparency = 0.7 -- Transparency of the circle.
            _G.CircleRadius = 80 -- The radius of the circle / FOV.
            _G.CircleFilled = false -- Determines whether or not the circle is filled.
            _G.CircleVisible = true -- Determines whether or not the circle is visible.
            _G.CircleThickness = 0 -- The thickness of the circle.
 
            local FOVCircle = Drawing.new("Circle")
            FOVCircle.Position = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)
            FOVCircle.Radius = _G.CircleRadius
            FOVCircle.Filled = _G.CircleFilled
            FOVCircle.Color = _G.CircleColor
            FOVCircle.Visible = _G.CircleVisible
            FOVCircle.Radius = _G.CircleRadius
            FOVCircle.Transparency = _G.CircleTransparency
            FOVCircle.NumSides = _G.CircleSides
            FOVCircle.Thickness = _G.CircleThickness
 
            local function GetClosestPlayer()
                local MaximumDistance = _G.CircleRadius
                local Target = nil
 
                for _, v in next, Players:GetPlayers() do
                    if v.Name ~= LocalPlayer.Name then
                        if _G.TeamCheck == true then
                            if v.Team ~= LocalPlayer.Team then
                                if v.Character ~= nil then
                                    if v.Character:FindFirstChild("HumanoidRootPart") ~= nil then
                                        if v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("Humanoid").Health ~= 0 then
                                            local ScreenPoint = Camera:WorldToScreenPoint(v.Character:WaitForChild("HumanoidRootPart", math.huge).Position)
                                            local VectorDistance = (Vector2.new(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y) - Vector2.new(ScreenPoint.X, ScreenPoint.Y)).Magnitude
 
                                            if VectorDistance < MaximumDistance then
                                                Target = v
                                            end
                                        end
                                    end
                                end
                            end
                        else
                            if v.Character ~= nil then
                                if v.Character:FindFirstChild("HumanoidRootPart") ~= nil then
                                    if v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("Humanoid").Health ~= 0 then
                                        local ScreenPoint = Camera:WorldToScreenPoint(v.Character:WaitForChild("HumanoidRootPart", math.huge).Position)
                                        local VectorDistance = (Vector2.new(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y) - Vector2.new(ScreenPoint.X, ScreenPoint.Y)).Magnitude
 
                                        if VectorDistance < MaximumDistance then
                                            Target = v
                                        end
                                    end
                                end
                            end
                        end
                    end
                end
 
                return Target
            end
 
            UserInputService.InputBegan:Connect(function(Input)
                if Input.UserInputType == Enum.UserInputType.MouseButton2 then
                    Holding = true
                end
            end)
 
            UserInputService.InputEnded:Connect(function(Input)
                if Input.UserInputType == Enum.UserInputType.MouseButton2 then
                    Holding = false
                end
            end)
 
            RunService.RenderStepped:Connect(function()
                FOVCircle.Position = Vector2.new(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y)
                FOVCircle.Radius = _G.CircleRadius
                FOVCircle.Filled = _G.CircleFilled
                FOVCircle.Color = _G.CircleColor
                FOVCircle.Visible = _G.CircleVisible
                FOVCircle.Radius = _G.CircleRadius
                FOVCircle.Transparency = _G.CircleTransparency
                FOVCircle.NumSides = _G.CircleSides
                FOVCircle.Thickness = _G.CircleThickness
 
                if Holding == true and _G.AimbotEnabled == true then
                    TweenService:Create(Camera, TweenInfo.new(_G.Sensitivity, Enum.EasingStyle.Sine, Enum.EasingDirection.Out), {CFrame = CFrame.new(Camera.CFrame.Position, GetClosestPlayer().Character[_G.AimPart].Position)}):Play()
                end
            end)
        end
 
