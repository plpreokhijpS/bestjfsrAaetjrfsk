-------------------------------------------------------------- Save Setting
_G.Setting_table = {
    Auto_Farm = false,
    Hop_AutoFarm_Boss = false,
    Auto_Farm_Boss = false,
    FastAttack = false,
    Effect_Attack = true,
    Auto_Raid = false,
    RandomFruit = false,
    BringFruit = false,
    BuyFruitSinper = false,
    Hallow_Scryte = false,
    Tushita = false,
    Yama = false,
    BuddySword = false,
    Sharkman_Karate = false,
    AutoFarm_Boss = false,
    Superhuman = false,
    Electric_Claw = false,
    Dragon_Talon = false,
    Death_Step = false,
    SelectWeapon = false,
    EP = false,
    SelectPoint = false,
    Fruit = false,
    Gun = false,
    Sword = false,
    Defense = false,
    Melee = false,
    SelectBoss = false,
    selectchip = false,
    SelectDevil = false,
    Hop = false,
    HopLowerServer = false,
    HopLegendarySword = false,
    KenHaki = false,
    Haki = false,
    LegendarySword = false,
    AutoCandyExp = false,
    AutoRedeem = false
}

local filename = "Bf_setting.txt"

function savesetting()
    local json
    local HttpService = game:GetService("HttpService")
    if (writefile) then
        json = HttpService:JSONEncode(_G.Setting_table)
        writefile(filename, json)
    else
        print("-- Sorry You Noob --")
    end
end

function loadsetting()
    local HttpService = game:GetService("HttpService")
    if (readfile and isfile and isfile(filename)) then
        _G.Setting_table = HttpService:JSONDecode(readfile(filename))
        -- print("-- New Value --")
        for i,v in pairs(_G.Setting_table) do
            -- print(i,v)
        end
    end
end

loadsetting()
-------------------------------------------------------------- Save Setting

local tpservice= game:GetService("TeleportService")
local plr = game.Players.LocalPlayer

if game:GetService("CoreGui"):FindFirstChild("Discord") then
    -- tpservice:Teleport(game.PlaceId, plr)
    game:GetService("CoreGui"):FindFirstChild("Discord"):Destroy()
end
game:GetService("UserInputService").InputBegan:Connect(function(input)
	pcall(function()
		if input.KeyCode == Enum.KeyCode.RightControl and _G.Pik  then
			game:GetService("CoreGui"):FindFirstChild("Discord").Enabled = true
			_G.Pik = nil
		elseif input.KeyCode == Enum.KeyCode.RightControl and _G.Pik == nil then
		    game:GetService("CoreGui"):FindFirstChild("Discord").Enabled = false
		    _G.Pik = true
		end
	end)
end)
-------------------------------------------------------------- Code
if not game:IsLoaded() then 
    repeat game.Loaded:Wait() 
    until game:IsLoaded() end
    

Old_World = false
New_World = false
Three_World = false
local placeId = game.PlaceId
if placeId == 2753915549 then
    Old_World = true
elseif placeId == 4442272183 then
    New_World = true
elseif placeId == 7449423635 then
    Three_World = true
end
wait(2)
repeat wait(1)
    if _G.Teams == "Pirates" then
        for i,v in pairs(getconnections(game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.MouseButton1Click)) do
            v.Function()
        end
    elseif _G.Teams == "Marines" then
        for i,v in pairs(getconnections(game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Marines.Frame.ViewportFrame.TextButton.MouseButton1Click)) do
            v.Function()
        end
    else
        for i,v in pairs(getconnections(game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.MouseButton1Click)) do
            v.Function()
        end
    end
until game.Players.localPlayer.Neutral == false
-----------------------------Code
spawn(function()
    while task.wait() do
        if  Auto_Farm == true or _G.Setting_table.AutoFarm_Players or Clip == true or _G.FarmMasteryFruit == true or _G.BuddySword == true or AutoFarm_Boss or _G.Auto_Raid or _G.Setting_table.Auto_Three then 
            if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyVelocity") then 
                local L_1 = Instance.new("BodyVelocity") 
                L_1.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart 
                L_1.MaxForce=Vector3.new(100000,100000,100000)
                L_1.Velocity=Vector3.new(0,0,0) 
            end
        else
            if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyVelocity") then
                game.Players.LocalPlayer.Character.HumanoidRootPart.BodyVelocity:Destroy()
            end
        end 
    end
end)

spawn(function()
    game:GetService("RunService").Heartbeat:Connect(function()
		pcall(function()
            local MyLevel = game.Players.LocalPlayer.Data.Level.Value
			if StatrMagnet then
			    if (CFrameMon.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1000 then
    				for y,x in pairs(game.Workspace.Enemies:GetChildren()) do
        					if not string.find(x.Name,"Boss") and(x.HumanoidRootPart.Position-_G.PosMon.Position).magnitude <= 300 then --370
        						x.HumanoidRootPart.CFrame = _G.PosMon
        						x.Humanoid.JumpPower = 0
        						x.Humanoid.WalkSpeed = 0
                                x.HumanoidRootPart.CanCollide = false
                                if x.Humanoid:FindFirstChild("Animator") then
                                    x.Humanoid.Animator:Destroy()
                                end
                                sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
        						x.Humanoid:ChangeState(14)
        					end
    				end
				end
            end
        end)
    end)
end)

spawn(function()
        while wait() do
            pcall(function()
                if Auto_Farm == true then
                    if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false then
        				CheckLevel()
        				StatrMagnet = false
                        if (CFrameQ.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 100 then 
            				TP(CFrameQ)
            			else
            			    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameQ
                        end
        				if (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 4 then
        					wait(1.1)
        					CheckLevel()
        					if (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 20 then
        						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuest, QuestLv)
        					    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
        					else
        						TP(CFrameQ)
        					end
        				end
                    elseif game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                        pcall(function()
                        CheckLevel()
                        if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v.Name == Ms and v.Humanoid.Health > 0 then
    								if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                        _G.PosMon = v.HumanoidRootPart.CFrame
            						v.Humanoid.JumpPower = 0 
            						v.Humanoid.WalkSpeed = 0
                                    v.HumanoidRootPart.CanCollide = false
                                    if v.Humanoid:FindFirstChild("Animator") then
                                        v.Humanoid.Animator:Destroy()
                                    end
                                    sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
            						v.Humanoid:ChangeState(14)
            						StatrMagnet = true
            						if _G.Setting_table.SelectWeapon == nil then
            						    for i2,v2 in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
                                            if tostring(v2.ToolTip) == "Melee" then
                                                EquipWeapon(v2.Name)
                                            end
                                        end
            						end
                                        repeat game:GetService("RunService").Stepped:wait()
                                            TP(v.HumanoidRootPart.CFrame * CFrame.new(0,20,0))
                                            game:GetService'VirtualUser':CaptureController()
                                            game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                        until v.Humanoid.Health <= 0 or not v.Parent or Auto_Farm == false or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false or game.Players.LocalPlayer.Character.Humanoid.Health <= 0
                                        CheckLevel()
                                    else
    									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
    								end
                                end
                            end
                        else
                            TP(CFrameMon)
                            wait(0.5)
                        end
                    end)
                end
                end
            end)
        end
end)

spawn(function()
        while wait() do
            pcall(function()
                if AutoFarm_Boss then
                    pcall(function()
                        CheckQuestBoss()
                        if game:GetService("Workspace").Enemies:FindFirstChild(MsBoss) then
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v.Name == MsBoss then
    								-- if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameBoss) then
                                        _G.PosMon = v.HumanoidRootPart.CFrame
                                        v.HumanoidRootPart.Size = Vector3.new(5,5,5)
                                        v.HumanoidRootPart.Transparency = 0.5
                                        if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                            local args = {
                                                [1] = "Buso"
                                            }
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                        end
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                                        repeat game:GetService("RunService").Heartbeat:wait(0.2)
                                                TP(v.HumanoidRootPart.CFrame * CFrame.new(0,25,0))
                                                game:GetService'VirtualUser':CaptureController()
                                                game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                        until v.Humanoid.Health <= 0 or AutoFarm_Boss == false or game.Players.LocalPlayer.Character.Humanoid.Health <= 0
                                        if v.Humanoid.Health <= 0 and _G.Hop then
                                            Teleport()
                                        end
    								-- end
                                end
                            end
                        elseif (CFrameBoss.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10 then
                            TP(CFrameBoss)
                            wait(0.5)
                        elseif (CFrameBoss.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 10 and _G.Hop then
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                            wait(3)
                            if not game:GetService("Workspace").Enemies:FindFirstChild(MsBoss) then
                                Teleport()
                            end
                        end
                    end)
                end
            end)
        end
end)


spawn(function()
	game:GetService("RunService").Stepped:Connect(function()
		pcall(function()
			local yedkuy112 = require(game.Players.LocalPlayer.PlayerScripts.CombatFramework.CameraShaker)
			local VirtualUser = game:GetService('VirtualUser')
			local yedhee = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework)
            yedkuy112.CameraShakeInstance.CameraShakeState.Inactive = 0
            yedhee.activeController.hitboxMagnitude = 55
			if FastAttack1 then
                    if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") then
                        yedhee.activeController.timeToNextAttack = 3
                    else
                        yedhee.activeController.timeToNextAttack = -(math.huge^math.huge)
                    end
                    yedhee.activeController.attacking = false
                    yedhee.activeController.increment = 3
                    --if yedhee.activeController:attack() then
                    --    yedhee.activeController:attack()
                    --end
                    yedhee.activeController.blocking = false
                    yedhee.activeController.timeToNextBlock = 0
                    game.Players.LocalPlayer.Character.Stun.Value = 0
                    game.Players.LocalPlayer.Character.Humanoid.Sit = false
                    --[[yedhee.activeController.timeToNextAttack = 0
                    yedhee.activeController.attacking = false
                    yedhee.activeController.blocking = false
                    yedhee.activeController.timeToNextAttack = 0
                    yedhee.activeController.timeToNextBlock = 0
                    yedhee.activeController.increment = 3
                    yedhee.activeController.hitboxMagnitude = 55
                    yedhee.activeController.focusStart = 0
                    if yedhee.activeController:attack() then
                        yedhee.activeController:attack()
                    end
                    ]]
			end
		end)
	end)
end)

local RigC = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework)
spawn(function()
game:GetService("RunService").Stepped:Connect(function()
        if _G.FastAttack2 then
            if game.Players.LocalPlayer.Character:FindFirstChild("Electric Claw") or not game.Players.LocalPlayer.Character then
		RigC.activeController.timeToNextAttack = -(math.huge * math.huge)
		RigC.activeController.increment = 3
	        RigC.activeController:attack()
	elseif not game.Players.LocalPlayer.Character then
	        RigC.activeController.timeToNextAttack = 1
	        RigC.activeController.increment = 3
	        RigC.activeController:attack()
	else
		RigC.activeController.timeToNextAttack = 0
		RigC.activeController:attack()
	end
		RigC.activeController.attacking = false
		RigC.activeController.blocking = false
		RigC.activeController.timeToNextBlock = 0
		RigC.activeController.hitboxMagnitude = 100
	   end
    end)
end)

	spawn(function()
		game:GetService("Players").LocalPlayer.Idled:connect(function()
			if _G.AntiAFK then
				VirtualUser:Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
				wait(1)
				VirtualUser:Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
			end
		end)
	end)

    function EquipWeapon(ToolSe)
        if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
            local tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
            wait(.4)
            game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
        end
    end
	
function CheckQuestBoss()
    -- Old World
    if _G.SelectBoss == "Saber Expert [Lv. 200] [Boss]" then
        MsBoss = "Saber Expert [Lv. 200] [Boss]"
        NameBoss = "Saber Expert"
        CFrameBoss = CFrame.new(-1458.89502, 29.8870335, -50.633564, 0.858821094, 1.13848939e-08, 0.512275636, -4.85649254e-09, 1, -1.40823326e-08, -0.512275636, 9.6063415e-09, 0.858821094)
    elseif _G.SelectBoss == "The Saw [Lv. 100] [Boss]" then
        MsBoss = "The Saw [Lv. 100] [Boss]"
        NameBoss = "The Saw"
        CFrameBoss = CFrame.new(-683.519897, 13.8534927, 1610.87854, -0.290192783, 6.88365773e-08, 0.956968188, 6.98413629e-08, 1, -5.07531119e-08, -0.956968188, 5.21077759e-08, -0.290192783)
    elseif _G.SelectBoss == "Greybeard [Lv. 750] [Raid Boss]" then
        MsBoss = "Greybeard [Lv. 750] [Raid Boss]"
        NameBoss = "Greybeard"
        CFrameBoss = CFrame.new(-4955.72949, 80.8163834, 4305.82666, -0.433646321, -1.03394289e-08, 0.901083171, -3.0443168e-08, 1, -3.17633075e-09, -0.901083171, -2.88092288e-08, -0.433646321)
    elseif _G.SelectBoss == "The Gorilla King [Lv. 25] [Boss]" then
        MsBoss = "The Gorilla King [Lv. 25] [Boss]"
        NameBoss = "The Gorilla King"
        NameQuestBoss = "JungleQuest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-1604.12012, 36.8521118, 154.23732, 0.0648873374, -4.70858913e-06, -0.997892559, 1.41431883e-07, 1, -4.70933674e-06, 0.997892559, 1.64442184e-07, 0.0648873374)
        CFrameBoss = CFrame.new(-1223.52808, 6.27936459, -502.292664, 0.310949147, -5.66602516e-08, 0.950426519, -3.37275488e-08, 1, 7.06501808e-08, -0.950426519, -5.40241736e-08, 0.310949147)
    elseif _G.SelectBoss == "Bobby [Lv. 55] [Boss]" then
        MsBoss = "Bobby [Lv. 55] [Boss]"
        NameBoss = "Bobby"
        NameQuestBoss = "BuggyQuest1"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-1139.59717, 4.75205183, 3825.16211, -0.959730506, -7.5857054e-09, 0.280922383, -4.06310328e-08, 1, -1.11807175e-07, -0.280922383, -1.18718916e-07, -0.959730506)
        CFrameBoss = CFrame.new(-1147.65173, 32.5966301, 4156.02588, 0.956680477, -1.77109952e-10, -0.29113996, 5.16530874e-10, 1, 1.08897802e-09, 0.29113996, -1.19218679e-09, 0.956680477)
    elseif _G.SelectBoss == "Yeti [Lv. 110] [Boss]" then
        MsBoss = "Yeti [Lv. 110] [Boss]"
        NameBoss = "Yeti"
        NameQuestBoss = "SnowQuest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(1384.90247, 87.3078308, -1296.6825, 0.280209213, 2.72035177e-08, -0.959938943, -6.75690828e-08, 1, 8.6151708e-09, 0.959938943, 6.24481444e-08, 0.280209213)
        CFrameBoss = CFrame.new(1221.7356, 138.046906, -1488.84082, 0.349343032, -9.49245944e-08, 0.936994851, 6.29478194e-08, 1, 7.7838429e-08, -0.936994851, 3.17894653e-08, 0.349343032)
    elseif _G.SelectBoss == "Mob Leader [Lv. 120] [Boss]" then
        MsBoss = "Mob Leader [Lv. 120] [Boss]"
        NameBoss = "Mob Leader"
        CFrameBoss = CFrame.new(-2848.59399, 7.4272871, 5342.44043, -0.928248107, -8.7248246e-08, 0.371961564, -7.61816636e-08, 1, 4.44474857e-08, -0.371961564, 1.29216433e-08, -0.92824)
    elseif _G.SelectBoss == "Vice Admiral [Lv. 130] [Boss]" then
        MsBoss = "Vice Admiral [Lv. 130] [Boss]"
        NameBoss = "Vice Admiral"
        NameQuestBoss = "MarineQuest2"
        LevelQuestBoss = 2
        CFrameQuestBoss = CFrame.new(-5035.42285, 28.6520386, 4324.50293, -0.0611100644, -8.08395768e-08, 0.998130739, -1.57416586e-08, 1, 8.00271849e-08, -0.998130739, -1.08217701e-08, -0.0611100644)
        CFrameBoss = CFrame.new(-5078.45898, 99.6520691, 4402.1665, -0.555574954, -9.88630566e-11, 0.831466436, -6.35508286e-08, 1, -4.23449258e-08, -0.831466436, -7.63661632e-08, -0.555574954)
    elseif _G.SelectBoss == "Warden [Lv. 175] [Boss]" then
        MsBoss = "Warden [Lv. 175] [Boss]"
        NameBoss = "Warden"
        NameQuestBoss = "ImpelQuest"
        LevelQuestBoss = 1
        CFrameQuestBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
        CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
    elseif _G.SelectBoss == "Chief Warden [Lv. 200] [Boss]" then
        MsBoss = "Chief Warden [Lv. 200] [Boss]"
        NameBoss = "Chief Warden"
        NameQuestBoss = "ImpelQuest"
        LevelQuestBoss = 2
        CFrameQuestBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
        CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
    elseif _G.SelectBoss == "Swan [Lv. 225] [Boss]" then
        MsBoss = "Swan [Lv. 225] [Boss]"
        NameBoss = "Swan"
        NameQuestBoss = "ImpelQuest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
        CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
    elseif _G.SelectBoss == "Magma Admiral [Lv. 350] [Boss]" then
        MsBoss = "Magma Admiral [Lv. 350] [Boss]"
        NameBoss = "Magma Admiral"
        NameQuestBoss = "MagmaQuest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-5317.07666, 12.2721891, 8517.41699, 0.51175487, -2.65508806e-08, -0.859131515, -3.91131572e-08, 1, -5.42026761e-08, 0.859131515, 6.13418294e-08, 0.51175487)
        CFrameBoss = CFrame.new(-5530.12646, 22.8769703, 8859.91309, 0.857838571, 2.23414389e-08, 0.513919294, 1.53689133e-08, 1, -6.91265853e-08, -0.513919294, 6.71978384e-08, 0.857838571)
    elseif _G.SelectBoss == "Fishman Lord [Lv. 425] [Boss]" then
        MsBoss = "Fishman Lord [Lv. 425] [Boss]"
        NameBoss = "Fishman Lord"
        NameQuestBoss = "FishmanQuest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(61123.0859, 18.5066795, 1570.18018, 0.927145958, 1.0624845e-07, 0.374700129, -6.98219367e-08, 1, -1.10790765e-07, -0.374700129, 7.65569368e-08, 0.927145958)
        CFrameBoss = CFrame.new(61351.7773, 31.0306778, 1113.31409, 0.999974668, 0, -0.00714713801, 0, 1.00000012, 0, 0.00714714266, 0, 0.999974549)
    elseif _G.SelectBoss == "Wysper [Lv. 500] [Boss]" then
        MsBoss = "Wysper [Lv. 500] [Boss]"
        NameBoss = "Wysper"
        NameQuestBoss = "SkyExp1Quest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-7862.94629, 5545.52832, -379.833954, 0.462944925, 1.45838088e-08, -0.886386991, 1.0534996e-08, 1, 2.19553424e-08, 0.886386991, -1.95022007e-08, 0.462944925)
        CFrameBoss = CFrame.new(-7925.48389, 5550.76074, -636.178345, 0.716468513, -1.22915289e-09, 0.697619379, 3.37381434e-09, 1, -1.70304748e-09, -0.697619379, 3.57381835e-09, 0.716468513)
    elseif _G.SelectBoss == "Thunder God [Lv. 575] [Boss]" then
        MsBoss = "Thunder God [Lv. 575] [Boss]"
        NameBoss = "Thunder God"
        NameQuestBoss = "SkyExp2Quest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-7902.78613, 5635.99902, -1411.98706, -0.0361216255, -1.16895912e-07, 0.999347389, 1.44533963e-09, 1, 1.17024491e-07, -0.999347389, 5.6715117e-09, -0.0361216255)
        CFrameBoss = CFrame.new(-7917.53613, 5616.61377, -2277.78564, 0.965189934, 4.80563429e-08, -0.261550069, -6.73089886e-08, 1, -6.46515304e-08, 0.261550069, 8.00056768e-08, 0.965189934)
    elseif _G.SelectBoss == "Cyborg [Lv. 675] [Boss]" then
        MsBoss = "Cyborg [Lv. 675] [Boss]"
        NameBoss = "Cyborg"
        NameQuestBoss = "FountainQuest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(5253.54834, 38.5361786, 4050.45166, -0.0112687312, -9.93677887e-08, -0.999936521, 2.55291371e-10, 1, -9.93769547e-08, 0.999936521, -1.37512213e-09, -0.0112687312)
        CFrameBoss = CFrame.new(6041.82813, 52.7112198, 3907.45142, -0.563162148, 1.73805248e-09, -0.826346457, -5.94632716e-08, 1, 4.26280238e-08, 0.826346457, 7.31437524e-08, -0.563162148)
    -- New World
    elseif _G.SelectBoss == "Diamond [Lv. 750] [Boss]" then
        MsBoss = "Diamond [Lv. 750] [Boss]"
        NameBoss = "Diamond"
        NameQuestBoss = "Area1Quest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601, -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
        CFrameBoss = CFrame.new(-1736.26587, 198.627731, -236.412857, -0.997808516, 0, -0.0661673471, 0, 1, 0, 0.0661673471, 0, -0.997808516)
    elseif _G.SelectBoss == "Jeremy [Lv. 850] [Boss]" then
        MsBoss = "Jeremy [Lv. 850] [Boss]"
        NameBoss = "Jeremy"
        NameQuestBoss = "Area2Quest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(632.698608, 73.1055908, 918.666321, -0.0319722369, 8.96074881e-10, -0.999488771, 1.36326533e-10, 1, 8.92172336e-10, 0.999488771, -1.07732087e-10, -0.0319722369)
        CFrameBoss = CFrame.new(2203.76953, 448.966034, 752.731079, -0.0217453763, 0, -0.999763548, 0, 1, 0, 0.999763548, 0, -0.0217453763)
    elseif _G.SelectBoss == "Fajita [Lv. 925] [Boss]" then
        MsBoss = "Fajita [Lv. 925] [Boss]"
        NameBoss = "Fajita"
        NameQuestBoss = "MarineQuest3"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-2442.65015, 73.0511475, -3219.11523, -0.873540044, 4.2329841e-08, -0.486752301, 5.64383384e-08, 1, -1.43220786e-08, 0.486752301, -3.99823996e-08, -0.873540044)
        CFrameBoss = CFrame.new(-2297.40332, 115.449463, -3946.53833, 0.961227536, -1.46645796e-09, -0.275756449, -2.3212845e-09, 1, -1.34094433e-08, 0.275756449, 1.35296352e-08, 0.961227536)
    elseif _G.SelectBoss == "Don Swan [Lv. 1000] [Boss]" then
        MsBoss = "Don Swan [Lv. 1000] [Boss]"
        NameBoss = "Don Swan"
        CFrameBoss = CFrame.new(2288.802, 15.1870775, 863.034607, 0.99974072, -8.41247214e-08, -0.0227668174, 8.4774733e-08, 1, 2.75850098e-08, 0.0227668174, -2.95079072e-08, 0.99974072)
    elseif _G.SelectBoss == "Smoke Admiral [Lv. 1150] [Boss]" then
        MsBoss = "Smoke Admiral [Lv. 1150] [Boss]"
        NameBoss = "Smoke Admiral"
        NameQuestBoss = "IceSideQuest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-6059.96191, 15.9868021, -4904.7373, -0.444992423, -3.0874483e-09, 0.895534337, -3.64098796e-08, 1, -1.4644522e-08, -0.895534337, -3.91229982e-08, -0.444992423)
        CFrameBoss = CFrame.new(-5115.72754, 23.7664986, -5338.2207, 0.251453817, 1.48345061e-08, -0.967869282, 4.02796978e-08, 1, 2.57916977e-08, 0.967869282, -4.54708946e-08, 0.251453817)
    elseif _G.SelectBoss == "Cursed Captain [Lv. 1325] [Raid Boss]" then
        MsBoss = "Cursed Captain [Lv. 1325] [Raid Boss]"
        NameBoss = "Cursed Captain"
        CFrameBoss = CFrame.new(916.928589, 181.092773, 33422, -0.999505103, 9.26310495e-09, 0.0314563364, 8.42916226e-09, 1, -2.6643713e-08, -0.0314563364, -2.63653774e-08, -0.999505103)
    elseif _G.SelectBoss == "Darkbeard [Lv. 1000] [Raid Boss]" then
        MsBoss = "Darkbeard [Lv. 1000] [Raid Boss]"
        NameBoss = "Darkbeard"
        CFrameBoss = CFrame.new(3876.00366, 24.6882591, -3820.21777, -0.976951957, 4.97356325e-08, 0.213458836, 4.57335361e-08, 1, -2.36868622e-08, -0.213458836, -1.33787044e-08, -0.976951957)
    elseif _G.SelectBoss == "Order [Lv. 1250] [Raid Boss]" then
        MsBoss = "Order [Lv. 1250] [Raid Boss]"
        NameBoss = "Order"
        CFrameBoss = CFrame.new(-6221.15039, 16.2351036, -5045.23584, -0.380726993, 7.41463495e-08, 0.924687505, 5.85604774e-08, 1, -5.60738549e-08, -0.924687505, 3.28013137e-08, -0.380726993)
    elseif _G.SelectBoss == "Awakened Ice Admiral [Lv. 1400] [Boss]" then
        MsBoss = "Awakened Ice Admiral [Lv. 1400] [Boss]"
        NameBoss = "Awakened Ice Admiral"
        NameQuestBoss = "FrostQuest"
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(5669.33203, 28.2118053, -6481.55908, 0.921275556, -1.25320829e-08, 0.388910472, 4.72230788e-08, 1, -7.96414241e-08, -0.388910472, 9.17372489e-08, 0.921275556)
        CFrameBoss = CFrame.new(6407.33936, 340.223785, -6892.521, 0.49051559, -5.25310213e-08, -0.871432424, -2.76146022e-08, 1, -7.58250565e-08, 0.871432424, 6.12576301e-08, 0.49051559)
    elseif _G.SelectBoss == "Tide Keeper [Lv. 1475] [Boss]" then
        MsBoss = "Tide Keeper [Lv. 1475] [Boss]"
         NameBoss = "Tide Keeper"
        NameQuestBoss = "ForgottenQuest"             
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-3053.89648, 236.881363, -10148.2324, -0.985987961, -3.58504737e-09, 0.16681771, -3.07832915e-09, 1, 3.29612559e-09, -0.16681771, 2.73641976e-09, -0.985987961)
        CFrameBoss = CFrame.new(-3570.18652, 123.328949, -11555.9072, 0.465199202, -1.3857326e-08, 0.885206044, 4.0332897e-09, 1, 1.35347511e-08, -0.885206044, -2.72606271e-09, 0.465199202)
    -- Thire World
    elseif _G.SelectBoss == "Stone [Lv. 1550] [Boss]" then
        MsBoss = "Stone [Lv. 1550] [Boss]"
        NameBoss = "Stone"
        NameQuestBoss = "PiratePortQuest"             
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-290, 44, 5577)
        CFrameBoss = CFrame.new(-1085, 40, 6779)
    elseif _G.SelectBoss == "Island Empress [Lv. 1675] [Boss]" then
        MsBoss = "Island Empress [Lv. 1675] [Boss]"
         NameBoss = "Island Empress"
        NameQuestBoss = "AmazonQuest2"             
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(5443, 602, 752)
        CFrameBoss = CFrame.new(5659, 602, 244)
    elseif _G.SelectBoss == "Kilo Admiral [Lv. 1750] [Boss]" then
        MsBoss = "Kilo Admiral [Lv. 1750] [Boss]"
        NameBoss = "Kilo Admiral"
        NameQuestBoss = "MarineTreeIsland"             
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(2178, 29, -6737)
        CFrameBoss =CFrame.new(2846, 433, -7100)
    elseif _G.SelectBoss == "Captain Elephant [Lv. 1875] [Boss]" then
        MsBoss = "Captain Elephant [Lv. 1875] [Boss]"
        NameBoss = "Captain Elephant"
        NameQuestBoss = "DeepForestIsland"             
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-13232, 333, -7631)
        CFrameBoss = CFrame.new(-13221, 325, -8405)
    elseif _G.SelectBoss == "Beautiful Pirate [Lv. 1950] [Boss]" then
        MsBoss = "Beautiful Pirate [Lv. 1950] [Boss]"
        NameBoss = "Beautiful Pirate"
        NameQuestBoss = "DeepForestIsland2"             
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-12686, 391, -9902)
        CFrameBoss = CFrame.new(5182, 23, -20)
    elseif SelectBoss == "Cake Queen [Lv. 2175] [Boss]" then
        MsBoss = "Cake Queen [Lv. 2175] [Boss]"
        NameQuestBoss = "IceCreamIslandQuest"             
        LevelQuestBoss = 3
        CFrameQuestBoss = CFrame.new(-716, 382, -11010)
        CFrameBoss = CFrame.new(-821, 66, -10965)
    elseif _G.SelectBoss == "rip_indra True Form [Lv. 5000] [Raid Boss]" then
        MsBoss = "rip_indra True Form [Lv. 5000] [Raid Boss]"
        NameBoss = "rip_indra True Form"
        CFrameBoss = CFrame.new(-5359, 424, -2735)
    elseif _G.SelectBoss == "Longma [Lv. 2000] [Boss]" then
        MsBoss = "Longma [Lv. 2000] [Boss]"
        NameBoss = "Longma"
        CFrameBoss = CFrame.new(-10248.3936, 353.79129, -9306.34473)
    elseif _G.SelectBoss == "Soul Reaper [Lv. 2100] [Raid Boss]" then
        MsBoss = "Soul Reaper [Lv. 2100] [Raid Boss]"
        NameBoss = "Soul Reaper"
        CFrameBoss = CFrame.new(-9515.62109, 315.925537, 6691.12012)
    end
end
	
function CheckLevel()
    local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
    if Old_World then
        if Lv == 1 or Lv <= 9 or SelectMonster == "Bandit [Lv. 5]" then -- Bandit
            Ms = "Bandit [Lv. 5]"
            NameQuest = "BanditQuest1"
            QuestLv = 1
            NameMon = "Bandit"
            CFrameQ = CFrame.new(1060.9383544922, 16.455066680908, 1547.7841796875)
            CFrameMon = CFrame.new(1038.5533447266, 41.296249389648, 1576.5098876953)
        elseif Lv == 10 or Lv <= 14 or SelectMonster == "Monkey [Lv. 14]" then -- Monkey
            Ms = "Monkey [Lv. 14]"
            NameQuest = "JungleQuest"
            QuestLv = 1
            NameMon = "Monkey"
            CFrameQ = CFrame.new(-1601.6553955078, 36.85213470459, 153.38809204102)
            CFrameMon = CFrame.new(-1448.1446533203, 50.851993560791, 63.60718536377)
        elseif Lv == 15 or Lv <= 29 or SelectMonster == "Gorilla [Lv. 20]" then -- Gorilla
            Ms = "Gorilla [Lv. 20]"
            NameQuest = "JungleQuest"
            QuestLv = 2
            NameMon = "Gorilla"
            CFrameQ = CFrame.new(-1601.6553955078, 36.85213470459, 153.38809204102)
            CFrameMon = CFrame.new(-1142.6488037109, 40.462348937988, -515.39227294922)
        elseif Lv == 30 or Lv <= 39 or SelectMonster == "Pirate [Lv. 35]" then -- Pirate
            Ms = "Pirate [Lv. 35]"
            NameQuest = "BuggyQuest1"
            QuestLv = 1
            NameMon = "Pirate"
            CFrameQ = CFrame.new(-1140.1761474609, 4.752049446106, 3827.4057617188)
            CFrameMon = CFrame.new(-1201.0881347656, 40.628940582275, 3857.5966796875)
        elseif Lv == 40 or Lv <= 59 or SelectMonster == "Brute [Lv. 45]" then -- Brute
            Ms = "Brute [Lv. 45]"
            NameQuest = "BuggyQuest1"
            QuestLv = 2
            NameMon = "Brute"
            CFrameQ = CFrame.new(-1140.1761474609, 4.752049446106, 3827.4057617188)
            CFrameMon = CFrame.new(-1387.5324707031, 24.592035293579, 4100.9575195313)
        elseif Lv == 60 or Lv <= 74 or SelectMonster == "Desert Bandit [Lv. 60]" then -- Desert Bandit
            Ms = "Desert Bandit [Lv. 60]"
            NameQuest = "DesertQuest"
            QuestLv = 1
            NameMon = "Desert Bandit"
            CFrameQ = CFrame.new(896.51721191406, 6.4384617805481, 4390.1494140625)
            CFrameMon = CFrame.new(984.99896240234, 16.109552383423, 4417.91015625)
        elseif Lv == 75 or Lv <= 89 or SelectMonster == "Desert Officer [Lv. 70]" then -- Desert Officer
            Ms = "Desert Officer [Lv. 70]"
            NameQuest = "DesertQuest"
            QuestLv = 2
            NameMon = "Desert Officer"
            CFrameQ = CFrame.new(896.51721191406, 6.4384617805481, 4390.1494140625)
            CFrameMon = CFrame.new(1547.1510009766, 14.452038764954, 4381.8002929688)
        elseif Lv == 90 or Lv <= 99 or SelectMonster == "Snow Bandit [Lv. 90]" then -- Snow Bandit
            Ms = "Snow Bandit [Lv. 90]"
            NameQuest = "SnowQuest"
            QuestLv = 1
            NameMon = "Snow Bandit"
            CFrameQ = CFrame.new(1386.8073730469, 87.272789001465, -1298.3576660156)
            CFrameMon = CFrame.new(1356.3028564453, 105.76865386963, -1328.2418212891)
        elseif Lv == 100 or Lv <= 119 or SelectMonster == "Snowman [Lv. 100]" then -- Snowman
            Ms = "Snowman [Lv. 100]"
            NameQuest = "SnowQuest"
            QuestLv = 2
            NameMon = "Snowman"
            CFrameQ = CFrame.new(1386.8073730469, 87.272789001465, -1298.3576660156)
            CFrameMon = CFrame.new(1218.7956542969, 138.01184082031, -1488.0262451172)
        elseif Lv == 120 or Lv <= 149 or SelectMonster == "Chief Petty Officer [Lv. 120]" then -- Chief Petty Officer
            Ms = "Chief Petty Officer [Lv. 120]"
            NameQuest = "MarineQuest2"
            QuestLv = 1
            NameMon = "Chief Petty Officer"
            CFrameQ = CFrame.new(-5035.49609375, 28.677835464478, 4324.1840820313)
            CFrameMon = CFrame.new(-4931.1552734375, 65.793113708496, 4121.8393554688)
        elseif Lv == 150 or Lv <= 174 or SelectMonster == "Sky Bandit [Lv. 150]" then -- Sky Bandit
            Ms = "Sky Bandit [Lv. 150]"
            NameQuest = "SkyQuest"
            QuestLv = 1
            NameMon = "Sky Bandit"
            CFrameQ = CFrame.new(-4842.1372070313, 717.69543457031, -2623.0483398438)
            CFrameMon = CFrame.new(-4955.6411132813, 365.46365356445, -2908.1865234375)
        elseif Lv == 175 or Lv <= 224 or SelectMonster == "Dark Master [Lv. 175]" then -- Dark Master
            Ms = "Dark Master [Lv. 175]"
            NameQuest = "SkyQuest"
            QuestLv = 2
            NameMon = "Dark Master"
            CFrameQ = CFrame.new(-4842.1372070313, 717.69543457031, -2623.0483398438)
            CFrameMon = CFrame.new(-5148.1650390625, 439.04571533203, -2332.9611816406)
        elseif Lv == 225 or Lv <= 274 or SelectMonster == "Toga Warrior [Lv. 225]" then -- Toga Warrior
            Ms = "Toga Warrior [Lv. 225]"
            NameQuest = "ColosseumQuest"
            QuestLv = 1
            NameMon = "Toga Warrior"
            CFrameQ = CFrame.new(-1577.7890625, 7.4151420593262, -2984.4838867188)
            CFrameMon = CFrame.new(-1872.5166015625, 49.080215454102, -2913.810546875)
        elseif Lv == 275 or Lv <= 299 or SelectMonster == "Gladiator [Lv. 275]" then -- Gladiator
            Ms = "Gladiator [Lv. 275]"
            NameQuest = "ColosseumQuest"
            QuestLv = 2
            NameMon = "Gladiator"
            CFrameQ = CFrame.new(-1577.7890625, 7.4151420593262, -2984.4838867188)
            CFrameMon = CFrame.new(-1521.3740234375, 81.203170776367, -3066.3139648438)
        elseif Lv == 300 or Lv <= 329 or SelectMonster == "Military Soldier [Lv. 300]" then -- Military Soldier
            Ms = "Military Soldier [Lv. 300]"
            NameQuest = "MagmaQuest"
            QuestLv = 1
            NameMon = "Military Soldier"
            CFrameQ = CFrame.new(-5316.1157226563, 12.262831687927, 8517.00390625)
            CFrameMon = CFrame.new(-5369.0004882813, 61.24352645874, 8556.4921875)
        elseif Lv == 330 or Lv <= 374 or SelectMonster == "Military Spy [Lv. 330]" then -- Military Spy
            Ms = "Military Spy [Lv. 330]"
            NameQuest = "MagmaQuest"
            QuestLv = 2
            NameMon = "Military Spy"
            CFrameQ = CFrame.new(-5316.1157226563, 12.262831687927, 8517.00390625)
            CFrameMon = CFrame.new(-5984.0532226563, 82.14656829834, 8753.326171875)
        elseif Lv == 375 or Lv <= 399 or SelectMonster == "Fishman Warrior [Lv. 375]" then -- Fishman Warrior 
            _G.FM = true
            Ms = "Fishman Warrior [Lv. 375]"
            NameQuest = "FishmanQuest"
            QuestLv = 1
            NameMon = "Fishman Warrior"
            CFrameQ = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734)
            CFrameMon = CFrame.new(60844.10546875, 98.462875366211, 1298.3985595703)
			if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
			end
        elseif Lv == 400 or Lv <= 449 or SelectMonster == "Fishman Commando [Lv. 400]" then -- Fishman Commando
            _G.FM = true
            Ms = "Fishman Commando [Lv. 400]"
            NameQuest = "FishmanQuest"
            QuestLv = 2
            NameMon = "Fishman Commando"
            CFrameQ = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734)
            CFrameMon = CFrame.new(61738.3984375, 64.207321166992, 1433.8375244141)
			if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
			end
        elseif Lv == 450 or Lv <= 474 or SelectMonster == "God's Guard [Lv. 450]" then -- God's Guard
            _G.FM = false
            Ms = "God's Guard [Lv. 450]"
            NameQuest = "SkyExp1Quest"
            QuestLv = 1
            NameMon = "God's Guard"
            CFrameQ = CFrame.new(-4721.8603515625, 845.30297851563, -1953.8489990234)
            CFrameMon = CFrame.new(-4628.0498046875, 866.92877197266, -1931.2352294922)
			if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
			end
        elseif Lv == 475 or Lv <= 524 or SelectMonster == "Shanda [Lv. 475]" then -- Shanda
            _G.FM = false
            Ms = "Shanda [Lv. 475]"
            NameQuest = "SkyExp1Quest"
            QuestLv = 2
            NameMon = "Shanda"
            CFrameQ = CFrame.new(-7863.1596679688, 5545.5190429688, -378.42266845703)
            CFrameMon = CFrame.new(-7685.1474609375, 5601.0751953125, -441.38876342773)
			if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
			end
        elseif Lv == 525 or Lv <= 549 or SelectMonster == "Royal Squad [Lv. 525]" then -- Royal Squad
            Ms = "Royal Squad [Lv. 525]"
            NameQuest = "SkyExp2Quest"
            QuestLv = 1
            NameMon = "Royal Squad"
            CFrameQ = CFrame.new(-7903.3828125, 5635.9897460938, -1410.923828125)
            CFrameMon = CFrame.new(-7654.2514648438, 5637.1079101563, -1407.7550048828)
        elseif Lv == 550 or Lv <= 624 or SelectMonster == "Royal Soldier [Lv. 550]" then -- Royal Soldier
            Ms = "Royal Soldier [Lv. 550]"
            NameQuest = "SkyExp2Quest"
            QuestLv = 2
            NameMon = "Royal Soldier"
            CFrameQ = CFrame.new(-7903.3828125, 5635.9897460938, -1410.923828125)
            CFrameMon = CFrame.new(-7760.4106445313, 5679.9077148438, -1884.8112792969)
        elseif Lv == 625 or Lv <= 649 or SelectMonster == "Galley Pirate [Lv. 625]" then -- Galley Pirate
            Ms = "Galley Pirate [Lv. 625]"
            NameQuest = "FountainQuest"
            QuestLv = 1
            NameMon = "Galley Pirate"
            CFrameQ = CFrame.new(5258.2788085938, 38.526931762695, 4050.044921875)
            CFrameMon = CFrame.new(5557.1684570313, 152.32717895508, 3998.7758789063)
        elseif Lv >= 650 or SelectMonster == "Galley Captain [Lv. 650]" then -- Galley Captain
            Ms = "Galley Captain [Lv. 650]"
            NameQuest = "FountainQuest"
            QuestLv = 2
            NameMon = "Galley Captain"
            CFrameQ = CFrame.new(5258.2788085938, 38.526931762695, 4050.044921875)
            CFrameMon = CFrame.new(5677.6772460938, 92.786109924316, 4966.6323242188)
        end
    end
    if New_World then
        if Lv == 700 or Lv <= 724 or SelectMonster == "Raider [Lv. 700]" then -- Raider
            Ms = "Raider [Lv. 700]"
            NameQuest = "Area1Quest"
            QuestLv = 1
            NameMon = "Raider"
            CFrameQ = CFrame.new(-427.72567749023, 72.99634552002, 1835.9426269531)
            CFrameMon = CFrame.new(68.874565124512, 93.635643005371, 2429.6752929688)
        elseif Lv == 725 or Lv <= 774 or SelectMonster == "Mercenary [Lv. 725]" then -- Mercenary
            Ms = "Mercenary [Lv. 725]"
            NameQuest = "Area1Quest"
            QuestLv = 2
            NameMon = "Mercenary"
            CFrameQ = CFrame.new(-427.72567749023, 72.99634552002, 1835.9426269531)
            CFrameMon = CFrame.new(-864.85009765625, 122.47104644775, 1453.1505126953)
        elseif Lv == 775 or Lv <= 799 or SelectMonster == "Swan Pirate [Lv. 775]" then -- Swan Pirate
            Ms = "Swan Pirate [Lv. 775]"
            NameQuest = "Area2Quest"
            QuestLv = 1
            NameMon = "Swan Pirate"
            CFrameQ = CFrame.new(635.61151123047, 73.096351623535, 917.81298828125)
            CFrameMon = CFrame.new(1065.3669433594, 137.64012145996, 1324.3798828125)
        elseif Lv == 800 or Lv <= 874 or SelectMonster == "Factory Staff [Lv. 800]" then -- Factory Staff
            Ms = "Factory Staff [Lv. 800]"
            NameQuest = "Area2Quest"
            QuestLv = 2
            NameMon = "Factory Staff"
            CFrameQ = CFrame.new(635.61151123047, 73.096351623535, 917.81298828125)
            CFrameMon = CFrame.new(533.22045898438, 128.46876525879, 355.62615966797)
        elseif Lv == 875 or Lv <= 899 or SelectMonster == "Marine Lieutenant [Lv. 875]" then -- Marine Lieutenant
            Ms = "Marine Lieutenant [Lv. 875]"
            NameQuest = "MarineQuest3"
            QuestLv = 1
            NameMon = "Marine Lieutenant"
            CFrameQ = CFrame.new(-2440.9934082031, 73.04190826416, -3217.7082519531)
            CFrameMon = CFrame.new(-2489.2622070313, 84.613594055176, -3151.8830566406)
        elseif Lv == 900 or Lv <= 949 or SelectMonster == "Marine Captain [Lv. 900]" then -- Marine Captain
            Ms = "Marine Captain [Lv. 900]"
            NameQuest = "MarineQuest3"
            QuestLv = 2
            NameMon = "Marine Captain"
            CFrameQ = CFrame.new(-2440.9934082031, 73.04190826416, -3217.7082519531)
            CFrameMon = CFrame.new(-2335.2026367188, 79.786659240723, -3245.8674316406)
        elseif Lv == 950 or Lv <= 974 or SelectMonster == "Zombie [Lv. 950]" then -- Zombie
            Ms = "Zombie [Lv. 950]"
            NameQuest = "ZombieQuest"
            QuestLv = 1
            NameMon = "Zombie"
            CFrameQ = CFrame.new(-5494.3413085938, 48.505931854248, -794.59094238281)
            CFrameMon = CFrame.new(-5536.4970703125, 101.08577728271, -835.59075927734)
        elseif Lv == 975 or Lv <= 999 or SelectMonster == "Vampire [Lv. 975]" then -- Vampire
            Ms = "Vampire [Lv. 975]"
            NameQuest = "ZombieQuest"
            QuestLv = 2
            NameMon = "Vampire"
            CFrameQ = CFrame.new(-5494.3413085938, 48.505931854248, -794.59094238281)
            CFrameMon = CFrame.new(-5806.1098632813, 16.722528457642, -1164.4384765625)
        elseif Lv == 1000 or Lv <= 1049 or SelectMonster == "Snow Trooper [Lv. 1000]" then -- Snow Trooper
            Ms = "Snow Trooper [Lv. 1000]"
            NameQuest = "SnowMountainQuest"
            QuestLv = 1
            NameMon = "Snow Trooper"
            CFrameQ = CFrame.new(607.05963134766, 401.44781494141, -5370.5546875)
            CFrameMon = CFrame.new(535.21051025391, 432.74209594727, -5484.9165039063)
        elseif Lv == 1050 or Lv <= 1099 or SelectMonster == "Winter Warrior [Lv. 1050]" then -- Winter Warrior
            Ms = "Winter Warrior [Lv. 1050]"
            NameQuest = "SnowMountainQuest"
            QuestLv = 2
            NameMon = "Winter Warrior"
            CFrameQ = CFrame.new(607.05963134766, 401.44781494141, -5370.5546875)
            CFrameMon = CFrame.new(1234.4449462891, 456.95419311523, -5174.130859375)
        elseif Lv == 1100 or Lv <= 1124 or SelectMonster == "Lab Subordinate [Lv. 1100]" then -- Lab Subordinate
            Ms = "Lab Subordinate [Lv. 1100]"
            NameQuest = "IceSideQuest"
            QuestLv = 1
            NameMon = "Lab Subordinate"
            CFrameQ = CFrame.new(-6061.841796875, 15.926671981812, -4902.0385742188)
            CFrameMon = CFrame.new(-5720.5576171875, 63.309471130371, -4784.6103515625)
        elseif Lv == 1125 or Lv <= 1174 or SelectMonster == "Horned Warrior [Lv. 1125]" then -- Horned Warrior
            Ms = "Horned Warrior [Lv. 1125]"
            NameQuest = "IceSideQuest"
            QuestLv = 2
            NameMon = "Horned Warrior"
            CFrameQ = CFrame.new(-6061.841796875, 15.926671981812, -4902.0385742188)
            CFrameMon = CFrame.new(-6292.751953125, 91.181983947754, -5502.6499023438)
        elseif Lv == 1175 or Lv <= 1199 or SelectMonster == "Magma Ninja [Lv. 1175]" then -- Magma Ninja
            Ms = "Magma Ninja [Lv. 1175]"
            NameQuest = "FireSideQuest"
            QuestLv = 1
            NameMon = "Magma Ninja"
            CFrameQ = CFrame.new(-5429.0473632813, 15.977565765381, -5297.9614257813)
            CFrameMon = CFrame.new(-5461.8388671875, 130.36347961426, -5836.4702148438)
        elseif Lv == 1200 or Lv <= 1249 or SelectMonster == "Lava Pirate [Lv. 1200]" then -- Lava Pirate
            Ms = "Lava Pirate [Lv. 1200]"
            NameQuest = "FireSideQuest"
            QuestLv = 2
            NameMon = "Lava Pirate"
            CFrameQ = CFrame.new(-5429.0473632813, 15.977565765381, -5297.9614257813)
            CFrameMon = CFrame.new(-5251.1889648438, 55.164535522461, -4774.4096679688)
        elseif Lv == 1250 or Lv <= 1274 or SelectMonster == "Ship Deckhand [Lv. 1250]" then -- Ship Deckhand
            Ms = "Ship Deckhand [Lv. 1250]"
            NameQuest = "ShipQuest1"
            QuestLv = 1
            NameMon = "Ship Deckhand"
            CFrameQ = CFrame.new(1040.2927246094, 125.08293151855, 32911.0390625)
            CFrameMon = CFrame.new(921.12365722656, 125.9839553833, 33088.328125)
			if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
			end
        elseif Lv == 1275 or Lv <= 1299 or SelectMonster == "Ship Engineer [Lv. 1275]" then -- Ship Engineer
            Ms = "Ship Engineer [Lv. 1275]"
            NameQuest = "ShipQuest1"
            QuestLv = 2
            NameMon = "Ship Engineer"
            CFrameQ = CFrame.new(1040.2927246094, 125.08293151855, 32911.0390625)
            CFrameMon = CFrame.new(886.28179931641, 40.47790145874, 32800.83203125)
			if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
			end
        elseif Lv == 1300 or Lv <= 1324 or SelectMonster == "Ship Steward [Lv. 1300]" then -- Ship Steward
            Ms = "Ship Steward [Lv. 1300]"
            NameQuest = "ShipQuest2"
            QuestLv = 1
            NameMon = "Ship Steward"
            CFrameQ = CFrame.new(971.42065429688, 125.08293151855, 33245.54296875)
            CFrameMon = CFrame.new(943.85504150391, 129.58183288574, 33444.3671875)
			if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
			end
        elseif Lv == 1325 or Lv <= 1349 or SelectMonster == "Ship Officer [Lv. 1325]" then -- Ship Officer
            Ms = "Ship Officer [Lv. 1325]"
            NameQuest = "ShipQuest2"
            QuestLv = 2
            NameMon = "Ship Officer"
            CFrameQ = CFrame.new(971.42065429688, 125.08293151855, 33245.54296875)
            CFrameMon = CFrame.new(955.38458251953, 181.08335876465, 33331.890625)
			if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
			end
        elseif Lv == 1350 or Lv <= 1374 or SelectMonster == "Arctic Warrior [Lv. 1350]" then -- Arctic Warrior
            Ms = "Arctic Warrior [Lv. 1350]"
            NameQuest = "FrostQuest"
            QuestLv = 1
            NameMon = "Arctic Warrior"
            CFrameQ = CFrame.new(5668.1372070313, 28.202531814575, -6484.6005859375)
            CFrameMon = CFrame.new(5935.4541015625, 77.26016998291, -6472.7568359375)
			if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
			end
        elseif Lv == 1375 or Lv <= 1424 or SelectMonster == "Snow Lurker [Lv. 1375]" then -- Snow Lurker
            Ms = "Snow Lurker [Lv. 1375]"
            NameQuest = "FrostQuest"
            QuestLv = 2
            NameMon = "Snow Lurker"
            CFrameQ = CFrame.new(5668.1372070313, 28.202531814575, -6484.6005859375)
            CFrameMon = CFrame.new(5628.482421875, 57.574996948242, -6618.3481445313)
        elseif Lv == 1425 or Lv <= 1449 or SelectMonster == "Sea Soldier [Lv. 1425]" then -- Sea Soldier
            Ms = "Sea Soldier [Lv. 1425]"
            NameQuest = "ForgottenQuest"
            QuestLv = 1
            NameMon = "Sea Soldier"
            CFrameQ = CFrame.new(-3054.5827636719, 236.87213134766, -10147.790039063)
            CFrameMon = CFrame.new(-3185.0153808594, 58.789089202881, -9663.6064453125)
        elseif Lv >= 1450 or SelectMonster == "Water Fighter [Lv. 1450]" then -- Water Fighter
            Ms = "Water Fighter [Lv. 1450]"
            NameQuest = "ForgottenQuest"
            QuestLv = 2
            NameMon = "Water Fighter"
            CFrameQ = CFrame.new(-3054.5827636719, 236.87213134766, -10147.790039063)
            CFrameMon = CFrame.new(-3262.9301757813, 298.69036865234, -10552.529296875)
		end
	end
	if Three_World then
		if Lv == 1500 or Lv <= 1524 or SelectMonster == "Pirate Millionaire [Lv. 1500]" then -- Pirate Millionaire
			Ms = "Pirate Millionaire [Lv. 1500]"
			NameQuest = "PiratePortQuest"
			QuestLv = 1
			NameMon = "Pirate Millionaire"
			CFrameQ = CFrame.new(-289.61752319336, 43.819011688232, 5580.0903320313)
			CFrameMon = CFrame.new(-435.68109130859, 189.69866943359, 5551.0756835938)
		elseif Lv == 1525 or Lv <= 1574 or SelectMonster == "Pistol Billionaire [Lv. 1525]" then -- Pistol Billoonaire
			Ms = "Pistol Billionaire [Lv. 1525]"
			NameQuest = "PiratePortQuest"
			QuestLv = 2
			NameMon = "Pistol Billionaire"
			CFrameQ = CFrame.new(-289.61752319336, 43.819011688232, 5580.0903320313)
			CFrameMon = CFrame.new(-236.53652954102, 217.46676635742, 6006.0883789063)
		elseif Lv == 1575 or Lv <= 1599 or SelectMonster == "Dragon Crew Warrior [Lv. 1575]" then -- Dragon Crew Warrior
			Ms = "Dragon Crew Warrior [Lv. 1575]"
			NameQuest = "AmazonQuest"
			QuestLv = 1
			NameMon = "Dragon Crew Warrior"
			CFrameQ = CFrame.new(5833.1147460938, 51.60498046875, -1103.0693359375)
			CFrameMon = CFrame.new(6301.9975585938, 104.77153015137, -1082.6075439453)
		elseif Lv == 1600 or Lv <= 1624 or SelectMonster == "Dragon Crew Archer [Lv. 1600]" then -- Dragon Crew Archer
			Ms = "Dragon Crew Archer [Lv. 1600]"
			NameQuest = "AmazonQuest"
			QuestLv = 2
			NameMon = "Dragon Crew Archer"
			CFrameQ = CFrame.new(5833.1147460938, 51.60498046875, -1103.0693359375)
			CFrameMon = CFrame.new(6831.1171875, 441.76708984375, 446.58615112305)
		elseif Lv == 1625 or Lv <= 1649 or SelectMonster == "Female Islander [Lv. 1625]" then -- Female Islander
			Ms = "Female Islander [Lv. 1625]"
			NameQuest = "AmazonQuest2"
			QuestLv = 1
			NameMon = "Female Islander"
			CFrameQ = CFrame.new(5446.8793945313, 601.62945556641, 749.45672607422)
			CFrameMon = CFrame.new(5792.5166015625, 848.14392089844, 1084.1818847656)
		elseif Lv == 1650 or Lv <= 1699 or SelectMonster == "Giant Islander [Lv. 1650]" then -- Giant Islander
			Ms = "Giant Islander [Lv. 1650]"
			NameQuest = "AmazonQuest2"
			QuestLv = 2
			NameMon = "Giant Islander"
			CFrameQ = CFrame.new(5446.8793945313, 601.62945556641, 749.45672607422)
			CFrameMon = CFrame.new(5009.5068359375, 664.11071777344, -40.960144042969)
		elseif Lv == 1700 or Lv <= 1724 or SelectMonster == "Marine Commodore [Lv. 1700]" then -- Marine Commodore
			Ms = "Marine Commodore [Lv. 1700]"
			NameQuest = "MarineTreeIsland"
			QuestLv = 1
			NameMon = "Marine Commodore"
			CFrameQ = CFrame.new(2179.98828125, 28.731239318848, -6740.0551757813)
			CFrameMon = CFrame.new(2198.0063476563, 128.71075439453, -7109.5043945313)
		elseif Lv == 1725 or Lv <= 1774 or SelectMonster == "Marine Rear Admiral [Lv. 1725]" then -- Marine Rear Admiral
			Ms = "Marine Rear Admiral [Lv. 1725]"
			NameQuest = "MarineTreeIsland"
			QuestLv = 2
			NameMon = "Marine Rear Admiral"
			CFrameQ = CFrame.new(2179.98828125, 28.731239318848, -6740.0551757813)
			CFrameMon = CFrame.new(3294.3142089844, 385.41125488281, -7048.6342773438)
		elseif Lv == 1775 or Lv <= 1799 or SelectMonster == "Fishman Raider [Lv. 1775]" then -- Fishman Raide
			Ms = "Fishman Raider [Lv. 1775]"
			NameQuest = "DeepForestIsland3"
			QuestLv = 1
			NameMon = "Fishman Raider"
			CFrameQ = CFrame.new(-10582.759765625, 331.78845214844, -8757.666015625)
			CFrameMon = CFrame.new(-10553.268554688, 521.38439941406, -8176.9458007813)
		elseif Lv == 1800 or Lv <= 1824 or SelectMonster == "Fishman Captain [Lv. 1800]" then -- Fishman Captain
			Ms = "Fishman Captain [Lv. 1800]"
			NameQuest = "DeepForestIsland3"
			QuestLv = 2
			NameMon = "Fishman Captain"
			CFrameQ = CFrame.new(-10583.099609375, 331.78845214844, -8759.4638671875)
			CFrameMon = CFrame.new(-10789.401367188, 427.18637084961, -9131.4423828125)
		elseif Lv == 1825 or Lv <= 1849 or SelectMonster == "Forest Pirate [Lv. 1825]" then -- Forest Pirate
			Ms = "Forest Pirate [Lv. 1825]"
			NameQuest = "DeepForestIsland"
			QuestLv = 1
			NameMon = "Forest Pirate"
			CFrameQ = CFrame.new(-13232.662109375, 332.40396118164, -7626.4819335938)
			CFrameMon = CFrame.new(-13489.397460938, 400.30349731445, -7770.251953125)
		elseif Lv == 1850 or Lv <= 1899 or SelectMonster == "Mythological Pirate [Lv. 1850]" then -- Mythological Pirate
			Ms = "Mythological Pirate [Lv. 1850]"
			NameQuest = "DeepForestIsland"
			QuestLv = 2
			NameMon = "Mythological Pirate"
			CFrameQ = CFrame.new(-13232.662109375, 332.40396118164, -7626.4819335938)
			CFrameMon = CFrame.new(-13508.616210938, 582.46228027344, -6985.3037109375)
		elseif Lv == 1900 or Lv <= 1924 or SelectMonster == "Jungle Pirate [Lv. 1900]" then -- Jungle Pirate
			Ms = "Jungle Pirate [Lv. 1900]"
			NameQuest = "DeepForestIsland2"
			QuestLv = 1
			NameMon = "Jungle Pirate"
			CFrameQ = CFrame.new(-12682.096679688, 390.88653564453, -9902.1240234375)
			CFrameMon = CFrame.new(-12267.103515625, 459.75262451172, -10277.200195313)
		elseif Lv == 1925 or Lv <= 1974 or SelectMonster == "Musketeer Pirate [Lv. 1925]" then -- Musketeer Pirate
			Ms = "Musketeer Pirate [Lv. 1925]"
			NameQuest = "DeepForestIsland2"
			QuestLv = 2
			NameMon = "Musketeer Pirate"
			CFrameQ = CFrame.new(-12682.096679688, 390.88653564453, -9902.1240234375)
			CFrameMon = CFrame.new(-13291.5078125, 520.47338867188, -9904.638671875)
		elseif Lv == 1975 or Lv <= 1999 or SelectMonster == "Reborn Skeleton [Lv. 1975]" then -- Reborn Skeleton
			Ms = "Reborn Skeleton [Lv. 1975]"
			NameQuest = "HauntedQuest1"
			QuestLv = 1
			NameMon = "Reborn Skeleton"
			CFrameQ = CFrame.new(-9480.80762, 142.130661, 5566.37305, -0.00655503059, 4.52954225e-08, -0.999978542, 2.04920472e-08, 1, 4.51620679e-08, 0.999978542, -2.01955679e-08, -0.00655503059)
			CFrameMon = CFrame.new(-8761.77148, 183.431747, 6168.33301, 0.978073597, -1.3950732e-05, -0.208259016, -1.08073925e-06, 1, -7.20630269e-05, 0.208259016, 7.07080399e-05, 0.978073597)
		elseif Lv == 2000 or Lv <= 2024 or SelectMonster == "Living Zombie [Lv. 2000]" then -- Living Zombie
			Ms = "Living Zombie [Lv. 2000]"
			NameQuest = "HauntedQuest1"
			QuestLv = 2
			NameMon = "Living Zombie"
			CFrameQ = CFrame.new(-9480.80762, 142.130661, 5566.37305, -0.00655503059, 4.52954225e-08, -0.999978542, 2.04920472e-08, 1, 4.51620679e-08, 0.999978542, -2.01955679e-08, -0.00655503059)
			CFrameMon = CFrame.new(-10103.7529, 238.565979, 6179.75977, 0.999474227, 2.77547141e-08, 0.0324240364, -2.58006327e-08, 1, -6.06848474e-08, -0.0324240364, 5.98163865e-08, 0.999474227)
		elseif Lv == 2025 or Lv <= 2049 or SelectMonster == "Demonic Soul [Lv. 2025]" then -- Demonic Soul
			Ms = "Demonic Soul [Lv. 2025]"
			NameQuest = "HauntedQuest1"
			QuestLv = 1
			NameMon = "Demonic Soul"
			CFrameQ = CFrame.new(-9515.39551, 172.266037, 6078.89746, 0.0121199936, -9.78649624e-08, 0.999926567, 2.30358754e-08, 1, 9.75929382e-08, -0.999926567, 2.18513581e-08, 0.0121199936)
			CFrameMon = CFrame.new(-9709.30762, 204.695892, 6044.04688, -0.845798075, -3.4587876e-07, -0.533503294, -4.46235369e-08, 1, -5.77571257e-07, 0.533503294, -4.64701827e-07, -0.845798075)
		elseif Lv >= 2050 or Lv <= 2074 or SelectMonster == "Posessed Mummy [Lv. 2050]" then -- Posessed Mummy
			Ms = "Posessed Mummy [Lv. 2050]"
			NameQuest = "HauntedQuest2"
			QuestLv = 2
			NameMon = "Posessed Mummy"
			CFrameQ = CFrame.new(-9515.39551, 172.266037, 6078.89746, 0.0121199936, -9.78649624e-08, 0.999926567, 2.30358754e-08, 1, 9.75929382e-08, -0.999926567, 2.18513581e-08, 0.0121199936)
			CFrameMon = CFrame.new(-9554.11035, 65.6141663, 6041.73584, -0.877069294, 5.33355795e-08, -0.480364174, 2.06420765e-08, 1, 7.33423562e-08, 0.480364174, 5.44105987e-08, -0.877069294)
		elseif Lv >= 2075 or Lv <= 2099 or SelectMonster == "Peanut Scout [Lv. 2075]" then -- Peanut Scout
			Ms = "Peanut Scout [Lv. 2075]"
			NameQuest = "PeanutQuest1"
			QuestLv = 1
			NameMon = "Peanut Scout"
			CFrameQ = CFrame.new(-2104.453125, 38.129974365234, -10194.0078125)
			CFrameMon = CFrame.new(-2068.0949707031, 76.512603759766, -10117.150390625)
		elseif Lv >= 2100 or Lv <= 2124 or SelectMonster == "Peanut President [Lv. 2100]" then -- Peanut President
			Ms = "Peanut President [Lv. 2100]"
			NameQuest = "PeanutQuest2"
			QuestLv = 2
			NameMon = "Peanut President"
			CFrameQ = CFrame.new(-2104.453125, 38.129974365234, -10194.0078125)
			CFrameMon = CFrame.new(-2067.33203125, 90.557350158691, -10552.051757812)
		elseif Lv >= 2125 or Lv <= 2149 or SelectMonster == "Ice Cream Chef [Lv. 2125]" then --Ice Cream Chef
			Ms = "Ice Cream Chef [Lv. 2125]"
			NameQuest = "IceCreamQuest1"
			QuestLv = 1
			NameMon = "	Ice Cream Chef"
			CFrameQ = CFrame.new(-821.35913085938, 65.845329284668, -10965.2578125)
			CFrameMon = CFrame.new(-796.37261962891, 110.95275878906, -10847.473632812)
		elseif Lv >= 2150 or SelectMonster == "Ice Cream Commander [Lv. 2150]" then -- Ice Cream Commander
			Ms = "Ice Cream Commander [Lv. 2150]"
			NameQuest = "IceCreamQuest2"
			QuestLv = 2
			NameMon = "Ice Cream Commander"
			CFrameQ = CFrame.new(-821.35913085938, 65.845329284668, -10965.2578125)
			CFrameMon = CFrame.new(-697.65338134766, 174.48368835449, -11218.38671875)
        end
	end
end



function TP2(P1)
	Distance = (P1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
	if Distance < 1000 then
		Speed = 500
	elseif Distance >= 1000 then
		Speed = 350
	end
    game:GetService("TweenService"):Create(
        game.Players.LocalPlayer.Character.HumanoidRootPart,
        TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
        {CFrame = P1}
    ):Play()
    Clip = true
    wait(Distance/Speed)
    Clip = false
end

function TP3(P1)
    Distance = (P1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if Distance < 150 then
        Speed = 2000
    elseif Distance < 300 then
        Speed = 1500
    elseif Distance < 1000 then
        Speed = 300
    elseif Distance >= 1000 then
        Speed = 200
    end
    game:GetService("TweenService"):Create(
        game.Players.LocalPlayer.Character.HumanoidRootPart,
        TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
        {CFrame = P1}
    ):Play()
end

function TP(P1)
    Distance = (P1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if Distance < 150 then
        Speed = 1500
    elseif Distance < 300 then
        Speed = 300
    elseif Distance < 1000 then
        Speed = 300
    elseif Distance >= 1000 then
        Speed = 200
    end
    game:GetService("TweenService"):Create(
        game.Players.LocalPlayer.Character.HumanoidRootPart,
        TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
        {CFrame = P1}
    ):Play()
end

spawn(function()
        while game:GetService("RunService").Stepped:wait(5) do
            character = game.Players.LocalPlayer.Character 
            if _G.NoClip or Clip or Auto_Farm or _G.Setting_table.AutoFarm_Players then
                pcall(function()
                    for _, v in pairs(character:GetChildren()) do
                        pcall(function()
                            if v:IsA("BasePart") then
                                pcall(function()
                                v.CanCollide = false
                                end)
                            end
                        end)
                    end
                end)
            end
        end
end)

spawn(function()
	while wait(.1) do
		if _G.Setting_table.Melee then
		    if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
			    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Melee", SelectPoint)
			end
		end
	end
end)

spawn(function()
	while wait(.1) do
		if _G.Setting_table.Defense then
		    if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
			    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Defense", SelectPoint)
		    end
		end
	end
end)

spawn(function()
	while wait(.1) do
		if _G.Setting_table.Sword then
		    if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
			    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Sword", SelectPoint)
		    end
		end
	end
end)

spawn(function()
	while wait(.1) do
		if _G.Setting_table.Gun then
		    if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
			    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Gun", SelectPoint)
		    end
		end
	end
end)

spawn(function()
	while wait(.1) do
		if _G.Setting_table.Fruit then
		    if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
			    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Demon Fruit", SelectPoint)
		    end
		end
	end
end)
local PlaceID = game.PlaceId
local AllIDs = {}
local foundAnything = ""
local actualHour = os.date("!*t").hour
local Deleted = false
local File = pcall(function()
	AllIDs = game:GetService('HttpService'):JSONDecode(readfile("NotSameServers.json"))
end)
if not File then
	table.insert(AllIDs, actualHour)
	writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
end
function TPReturner()
	local Site;
	if foundAnything == "" then
		Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
	else
		Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
	end
	local ID = ""
	if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
		foundAnything = Site.nextPageCursor
	end
	local num = 0;
	for i,v in pairs(Site.data) do
		local Possible = true
		ID = tostring(v.id)
		if tonumber(v.maxPlayers) > tonumber(v.playing) then
		    game.StarterGui:SetCore("SendNotification", {
                Title = "Hop Server", 
                Text = "Players : " ..tonumber(v.playing),
                Icon = "http://www.roblox.com/asset/?id=8987392618",
                Duration = 1.5
            })
			for _,Existing in pairs(AllIDs) do
				if num ~= 0 then
					if ID == tostring(Existing) then
						Possible = false
					end
				else
				if tonumber(actualHour) ~= tonumber(Existing) then
					local delFile = pcall(function()
						--delfile("NotSameServers.json")
						AllIDs = {}
						table.insert(AllIDs, actualHour)
					end)
				end
			end
			num = num + 1
		end
		if Possible == true then
			table.insert(AllIDs, ID)
			wait(0.2)
			pcall(function()
				--writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
				wait(0.2)
				game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
			end)
			end
		end
	end
end

function Teleport()
	while wait(0.2) do
		pcall(function()
			TPReturner()
			if foundAnything ~= "" then
				TPReturner()
			end
		end)
	end
end

function HopLowerServer()
	local maxplayers, gamelink, goodserver, data_table = math.huge, "https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/Public?sortOrder=Asc&limit=100"
	if not _G.FailedServerID then _G.FailedServerID = {} end
	local function serversearch()
		data_table = game:GetService"HttpService":JSONDecode(game:HttpGetAsync(gamelink))
		for _, v in pairs(data_table.data) do
			pcall(function()
				if type(v) == "table" and v.id and v.playing and tonumber(maxplayers) > tonumber(v.playing) and not table.find(_G.FailedServerID, v.id) then
				    game.StarterGui:SetCore("SendNotification", {
                             Title = "Hop LowerServer", 
                             Text = "Players : " ..tonumber(v.playing),
                             Icon = "http://www.roblox.com/asset/?id=8987392618",
                             Duration = 1.5
                       })
                   _G.Teleport = true
					maxplayers = v.playing
					goodserver = v.id
				end
			end)
		end
	end
	function getservers()
		pcall(serversearch)
		for i, v in pairs(data_table) do
			if i == "nextPageCursor" then
				if gamelink:find"&cursor=" then
					local a = gamelink:find"&cursor="
					local b = gamelink:sub(a)
					gamelink = gamelink:gsub(b, "")
				end
				gamelink = gamelink .. "&cursor=" .. v
				pcall(getservers)
			end
		end
	end
	pcall(getservers)
	if goodserver == game.JobId or maxplayers == #game:GetService"Players":GetChildren() - 1 then
	end
	table.insert(_G.FailedServerID, goodserver)
	game:GetService"TeleportService":TeleportToPlaceInstance(game.PlaceId, goodserver)
end

spawn(function()
    while wait(2) do
        if _G.Superhuman and game.Players.LocalPlayer:FindFirstChild("WeaponAssetCache") then
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") or game.Players.LocalPlayer.Character:FindFirstChild("Combat") then
                local args = {
                    [1] = "BuyBlackLeg"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end   
            if game.Players.LocalPlayer.Character:FindFirstChild("Superhuman") or game.Players.LocalPlayer.Backpack:FindFirstChild("Superhuman") and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                _G.Setting_table.SelectWeapon = "Superhuman"
            end  
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 299 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                _G.Setting_table.SelectWeapon = "Black Leg"
            end
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 299 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                _G.Setting_table.SelectWeapon = "Electro"
            end
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value <= 299 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                _G.Setting_table.SelectWeapon = "Fishman Karate"
            end
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 299 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                _G.Setting_table.SelectWeapon = "Dragon Claw"
            end
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                local args = {
                    [1] = "BuyElectro"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end
            if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                local args = {
                    [1] = "BuyElectro"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end
            
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                local args = {
                    [1] = "BuyFishmanKarate"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end
            if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                local args = {
                    [1] = "BuyFishmanKarate"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
                if FG < 1500 then
                    if Auto_Farm then
                        Auto_Farm = false
                    end
                    _G.Auto_Raid = true
                else
                    if _G.Setting_table.Auto_Farm then
                        Auto_Farm = true
                    end
                    local args = {
                        [1] = "BlackbeardReward",
                        [2] = "DragonClaw",
                        [3] = "2"
                    }
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                end
            end
            if game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
                if FG < 1500 then
                    if Auto_Farm then
                        Auto_Farm = false
                    end
                    _G.Auto_Raid = true
                else
                    _G.Auto_Raid = false
                    if _G.Setting_table.Auto_Farm then
                        Auto_Farm = true
                    end
                    local args = {
                        [1] = "BlackbeardReward",
                        [2] = "DragonClaw",
                        [3] = "2"
                    }
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                end
            end
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                local args = {
                    [1] = "BuySuperhuman"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end
            if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                local args = {
                    [1] = "BuySuperhuman"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end 
        end
        if _G.Death_Step and game.Players.LocalPlayer:FindFirstChild("WeaponAssetCache") then
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 400 then
                local args = {
                    [1] = "BuyDeathStep"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                _G.Setting_table.SelectWeapon = "Death Step"
            end  
            if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 400 then
                local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
                if FG < 5000 and _G.Hop then
                    if Auto_Farm then
                        Auto_Farm = false
                    end
                    _G.Setting_table.Auto_Raid = true
                    _G.Auto_Raid = true
                    _G.Hop = true
                    savesetting()
                elseif FG >= 5000 then
                    _G.Setting_table.Auto_Raid = false
                    _G.Auto_Raid = false
                    _G.Hop = false
                    savesetting()
                    if _G.Setting_table.Auto_Farm then
                        Auto_Farm = true
                    end
                end
                local args = {
                    [1] = "BuyDeathStep"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                
                _G.Setting_table.SelectWeapon = "Death Step"
            end  
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value < 400 then
                _G.Setting_table.SelectWeapon = "Black Leg"
            end 
        end
        if _G.Dragon_Talon and game.Players.LocalPlayer:FindFirstChild("WeaponAssetCache") then
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 399 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                _G.Setting_table.SelectWeapon = "Dragon Claw"
            end
            if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value <= 399 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                _G.Setting_table.SelectWeapon = "Dragon Claw"
            end

            if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 400 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                _G.Setting_table.SelectWeapon = "Dragon Claw"
                local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
                if FG < 5000 and _G.Hop then
                    if Auto_Farm then
                        Auto_Farm = false
                    end
                    _G.Setting_table.Auto_Raid = true
                    _G.Auto_Raid = true
                    _G.Hop = true
                    savesetting()
                elseif FG >= 5000 then
                    _G.Setting_table.Auto_Raid = false
                    _G.Auto_Raid = false
                    _G.Hop = false
                    savesetting()
                    if _G.Setting_table.Auto_Farm then
                        Auto_Farm = true
                    end
                end
                    if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon", true) == 3 then
                        local string_1 = "Bones";
                        local string_2 = "Buy";
                        local number_1 = 1;
                        local number_2 = 1;
                        local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                        Target:InvokeServer(string_1, string_2, number_1, number_2);
    
                        local string_1 = "BuyDragonTalon";
                        local bool_1 = true;
                        local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                        Target:InvokeServer(string_1, bool_1);
                    elseif game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon", true) == 1 then
                        game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon")
                    else
                        local string_1 = "BuyDragonTalon";
                        local bool_1 = true;
                        local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                        Target:InvokeServer(string_1, bool_1);
                        local string_1 = "BuyDragonTalon";
                        local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                        Target:InvokeServer(string_1);
                    end
            end
        end
        if _G.Electric_Claw and game.Players.LocalPlayer:FindFirstChild("WeaponAssetCache") then
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value < 400 then
                _G.Setting_table.SelectWeapon = "Electro"
            end  
            if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value < 400 then
                _G.Setting_table.SelectWeapon = "Electro"
            end  
            if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 400 then
                local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
                if FG < 5000 and _G.Hop then
                    if Auto_Farm then
                        Auto_Farm = false
                    end
                    _G.Setting_table.Auto_Raid = true
                    _G.Auto_Raid = true
                    _G.Hop = true
                    savesetting()
                elseif FG >= 5000 then
                    _G.Setting_table.Auto_Raid = false
                    _G.Auto_Raid = false
                    _G.Hop = false
                    savesetting()
                    if _G.Setting_table.Auto_Farm then
                        Auto_Farm = true
                    end
                end
                local v175 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", true);
                if v175 == 4 then
                    local v176 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", "Start");
                    if v176 == nil then
                        TP2(CFrame.new(-12548, 337, -7481))
                    end
                else
                    local string_1 = "BuyElectricClaw";
                    local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                    Target:InvokeServer(string_1);
                end
            end
            if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 400 then
                local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
                if FG < 5000 and _G.Hop then
                    if Auto_Farm then
                        Auto_Farm = false
                    end
                    _G.Setting_table.Auto_Raid = true
                    _G.Auto_Raid = true
                    _G.Hop = true
                    savesetting()
                elseif FG >= 5000 then
                    _G.Setting_table.Auto_Raid = false
                    _G.Auto_Raid = false
                    _G.Hop = false
                    savesetting()
                    if _G.Setting_table.Auto_Farm then
                        Auto_Farm = true
                    end
                end
                local v175 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", true);
                if v175 == 4 then
                    local v176 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", "Start");
                    if v176 == nil then
                        TP2(CFrame.new(-12548, 337, -7481))
                    end
                else
                    local string_1 = "BuyElectricClaw";
                    local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                    Target:InvokeServer(string_1);
                end
            end
        end
    end
end)

	spawn(function()
	    while wait() do
            if _G.Setting_table.EP then
                if _G.Setting_table.SelectWeapon == nil then
                else
                    EquipWeapon(_G.Setting_table.SelectWeapon)
                end
            end
	    end
	end)
	
spawn(function()
    while wait() do
        if Killaura or _G.AutoRaid or RaidSuperhuman or _G.Auto_Raid then
            for i,v in pairs(game.Workspace.Enemies:GetDescendants()) do
                if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                    pcall(function()
                        repeat wait(.1)
                            sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                            v.Humanoid.Health = 0
                            v.HumanoidRootPart.CanCollide = false
                            v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                            v.HumanoidRootPart.Transparency = 0.5
                        until not Killaura or not _G.Auto_Raid or not RaidSuperhuman or not v.Parent or v.Humanoid.Health <= 0
                    end)
                end
            end
        end
    end
end)
spawn(function()
                                    while wait() do
                                        if _G.Auto_Raid then
                                            wait(3)
                                            if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Special Microchip") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Special Microchip") then
                                                if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false then
                                                    if New_World then
                            							fireclickdetector(game:GetService("Workspace").Map.CircleIsland.RaidSummon2.Button.Main.ClickDetector)
                            							wait(15)
                            						elseif Three_World then
                            							fireclickdetector(game:GetService("Workspace").Map["Boat Castle"].RaidSummon2.Button.Main.ClickDetector)
                            							wait(15)
                            						end
                                                end
                        					elseif _G.Hop and not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Special Microchip") and not game:GetService("Players").LocalPlayer.Character:FindFirstChild("Special Microchip") then
                                                wait(15)
                                                if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false then
                                                    Teleport()
                                                end
                                            end
                                        end
                                    end
end)
                            
spawn(function()
    while wait(.2) do
        if _G.Auto_Raid then
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("RaidsNpc", "Select", _G.Setting_table.selectchip)
        end
    end
end)

                            
                                spawn(function()
                                    while wait(.1) do
                                        if NextIsland or _G.Auto_Raid then
                                            game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(11)
                                            if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true then
                                                if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true and game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
                                					if game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 5"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2500 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 5"].CFrame*CFrame.new(0,80,0))
                                					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 4"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2500 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 4"].CFrame*CFrame.new(0,80,0))
                                					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 3"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2500 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 3"].CFrame*CFrame.new(0,80,0))
                                					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 2"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2500 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 2"].CFrame*CFrame.new(0,80,0))
                                					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 1"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2500 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 1"].CFrame*CFrame.new(0,80,0))
                                					end
                                                end
                                            end
                                        end
                                    end
                                end)

spawn(function()
	pcall(function()
		while wait(2) do
			if _G.AutoAwakener then
				local args = {
					[1] = "Awakener",
					[2] = "Check"
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				local args = {
					[1] = "Awakener",
					[2] = "Awaken"
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end
		end
	end)
end)

spawn(function()
    while wait() do
        if _G.BringFruit then
            for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
                if v:IsA ("Tool") then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame
                    wait(1)
                end
            end
        end
    end
end)
-------------------------------------------------------------- Code

local DiscordLib = loadstring(game:HttpGet"https://raw.githubusercontent.com/x7Swiftz/UI-V3/main/README.md")()

local win = DiscordLib:Window("Liver Hub - Premium")

local serv = win:Server("Blox Fruit - Premium", "http://www.roblox.com/asset/?id=8987392618")

wait(1)
game:GetService("CoreGui").Discord.MainFrame.ServersHoldFrame.ServersHold["Blox Fruit - PremiumServer"].BackgroundTransparency = 1
local Main = serv:Channel("Main")
local AutoStats = serv:Channel("AutoStats")
local MeleeP = serv:Channel("Melee")
local SwordP = serv:Channel("Sword")
local FruitP = serv:Channel("Fruit")
local Accesory = serv:Channel("Accesory")
local Ability = serv:Channel("Ability")
local PVP = serv:Channel("PVP")
local Raid = serv:Channel("Raid")
local Shop = serv:Channel("Shop")
local Teleport = serv:Channel("Teleport")
local Credit = serv:Channel("Credit")


-------------------------------------------------------------- Main

Main:Label("Level")
Main:Toggle("AutoFarm Level",_G.Setting_table.Auto_Farm,function(vu)
    Auto_Farm = vu
    _G.Setting_table.Auto_Farm = vu
    savesetting()
end)
Main:Toggle("Auto New World",_G.Setting_table.Auto_New,function(vu)
    _G.Setting_table.Auto_New = vu
end)

spawn(function()
    while wait(.2) do
        if _G.Setting_table.Auto_New then
            print("1")
            local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
            if Lv >= 700 and Old_World then
                if Auto_Farm then
                    Auto_Farm = false
                end
                wait(1)
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("DressrosaQuestProgress","Detective")
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("DressrosaQuestProgress")
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Key") then
                    EquipWeapon("Key")
                end
                wait(1)
                print("2")
                repeat wait(.2)
                    TP2(CFrame.new(1348.32861328125, 37.547386169433594, -1327.2293701171875))
                until (Vector3.new(1348.32861328125, 37.547386169433594, -1327.2293701171875)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1348.35522, 37.5473976, -1327.21301, 0.535414219, -4.35537473e-08, 0.844589591, 8.66955574e-08, 1, -3.39133788e-09, -0.844589591, 7.50379385e-08, 0.535414219)
                print("3")
                if game.Workspace.Enemies:FindFirstChild("Ice Admiral [Lv. 700] [Boss]") then
                    print("Have")
                    Clip = true
                    local v = game.Workspace.Enemies:FindFirstChild("Ice Admiral [Lv. 700] [Boss]")
                    for i,v2 in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
                        if tostring(v2.ToolTip) == "Melee" then
                            EquipWeapon(v2.Name)
                        end
                    end
                    repeat wait(.1)
                        TP(v.HumanoidRootPart.CFrame*CFrame.new(0,25,0))
                        game:GetService'VirtualUser':CaptureController()
                        game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                    until v.Humanoid.Health <= 0 or not v.Parent
                    Clip = false
                    wait(1)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
                end
            elseif New_World or Three_World then
                _G.Setting_table.Auto_Farm = true
                _G.Setting_table.Auto_New = false
                savesetting()
            end
        end
    end
end)

Main:Toggle("Auto Three World",_G.Setting_table.Auto_Three,function(vu)
    _G.Setting_table.Auto_Three = vu
    savesetting()
end)
    spawn(function()
        pcall(function()
            while wait() do
                if _G.Setting_table.Auto_Three then
                    if game:GetService("Players").LocalPlayer.Data.Level.Value >= 1500 and New_World then
                        _G.Setting_table.Auto_Farm = false
                        if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ZQuestProgress").KilledIndraBoss == false then
                            if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 3 then
                                if game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value == "Bar" then
                                    if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0 then
                                        if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ZQuestProgress","Check") == 0 then
                                            if (CFrame.new(-1926.3221435547, 12.819851875305, 1738.3092041016).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10 then
                                                wait(1.1)
                                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ZQuestProgress","Begin")
                                            else
                                                TP2(CFrame.new(-1926.3221435547, 12.819851875305, 1738.3092041016))
                                            end
                                            if game:GetService("Workspace").Enemies:FindFirstChild("rip_indra [Lv. 1500] [Boss]") then
                                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                                    if v.Name == "rip_indra [Lv. 1500] [Boss]" then
                                                        for i,v2 in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
                                                            if tostring(v2.ToolTip) == "Melee" then
                                                                EquipWeapon(v2.Name)
                                                            end
                                                        end
                                                        repeat game:GetService("RunService").Heartbeat:wait()
                                                            pcall(function()
                                                                
                                                                TP2(v.HumanoidRootPart.CFrame * CFrame.new(0,25,0))
                                                                require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework).activeController.hitboxMagnitude = 1000
                                                                game:GetService'VirtualUser':CaptureController()
                                                                game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelZou")
                                                                sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                                                            end)
                                                        until _G.Setting_table.Auto_Three == false or v.Humanoid.Health <= 0 or not v.Parent
                                                    end
                                                end
                                            elseif not game:GetService("Workspace").Enemies:FindFirstChild("rip_indra [Lv. 1500] [Boss]") and (CFrame.new(-26880.93359375, 22.848554611206, 473.18951416016).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1000 then
                                                TP2(CFrame.new(-26880.93359375, 22.848554611206, 473.18951416016))
                                            end
                                        elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ZQuestProgress","Check") ~= 0 then
                                            if game:GetService("Workspace").Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") or game:GetService("ReplicatedStorage"):FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
                                                if game:GetService("Workspace").Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
                                                    for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                                        if v.Name == "Don Swan [Lv. 1000] [Boss]" then
                                                            for i,v2 in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
                                                                if tostring(v2.ToolTip) == "Melee" then
                                                                    EquipWeapon(v2.Name)
                                                                end
                                                            end
                                                            repeat game:GetService("RunService").Heartbeat:wait()
                                                                pcall(function()
                                                                    
                                                                    TP2(v.HumanoidRootPart.CFrame * CFrame.new(0,25,0))
                                                                    require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework).activeController.hitboxMagnitude = 1000
                                                                    game:GetService'VirtualUser':CaptureController()
                                                                    game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                                                    sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                                                                end)
                                                            until _G.Setting_table.Auto_Three == false or v.Humanoid.Health <= 0 or not v.Parent
                                                        end
                                                    end
                                                else
                                                    if (CFrame.new(2284.912109375, 15.537666320801, 905.48291015625).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 1000 then
                                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(2284.912109375, 15.537666320801, 905.48291015625))
                                                        wait()
                                                    end
                                                    TP2(CFrame.new(2284.912109375, 15.537666320801, 905.48291015625))
                                                end
                                            elseif _G.Setting_table.Auto_Three and not game:GetService("Workspace").Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") and not game:GetService("ReplicatedStorage"):FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
                                                Teleport()
                                            elseif not _G.Setting_table.Auto_Three and not game:GetService("Workspace").Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") and not game:GetService("ReplicatedStorage"):FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
                                                if (CFrame.new(2284.912109375, 15.537666320801, 905.48291015625).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 1000 then
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(2284.912109375, 15.537666320801, 905.48291015625))
                                                    wait()
                                                end
                                                TP2(CFrame.new(2284.912109375, 15.537666320801, 905.48291015625))
                                            end
                                        end
                                    elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") ~= 0 then
                                        for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
                                            if string.find(v.Name, "Fruit") then
                                                if v:IsA("Tool") then
                                                    if (v.Handle.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 20000 then
                                                        v.Handle.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                                                    end
                                                end
                                            end
                                        end
                                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Quake Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Human: Buddha Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("String Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Bird: Phoenix Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Rumble Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Paw Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Gravity Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Dough Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Shadow Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Venom Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Control Fruit") or game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Quake Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Human: Buddha Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("String Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Bird: Phoenix Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Rumble Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Paw Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Gravity Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Dough Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Shadow Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Venom Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Control Fruit") or game.Players.LocalPlayer.Character:FindFirstChild("Dragon Fruit") then
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1")
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","2")
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","3")
                                        end
                                    end
                                else
                                    TP2(CFrame.new(-379.70889282227, 73.0458984375, 304.84692382813))
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                                end
                            else
                                if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 0 then
                                    if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Swan Pirates") and string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "50") and game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                                        if game.Workspace.Enemies:FindFirstChild("Swan Pirate [Lv. 775]") then
                                            for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                                if v.Name == "Swan Pirate [Lv. 775]" then
                                                    PosMonBarto =  v.HumanoidRootPart.CFrame
                                                    pcall(function()
                                                        for i,v2 in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
                                                            if tostring(v2.ToolTip) == "Melee" then
                                                                EquipWeapon(v2.Name)
                                                            end
                                                        end
                                                        repeat wait()
                                                            for k,x in pairs(game.Workspace.Enemies:GetChildren()) do
                                                                if x.Name ==  "Swan Pirate [Lv. 775]"  then
                                                                        x.Humanoid:ChangeState(11)
                                                                        sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                                                                        x.HumanoidRootPart.CanCollide = false
                                                                        sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                                                                        x.HumanoidRootPart.Size = Vector3.new(30, 30, 30)
                                                                        sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                                                                        x.HumanoidRootPart.CFrame = PosMonBarto
                                                                        sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                                                                end
                                                            end
                                                            
                                                        v.HumanoidRootPart.CanCollide = false
                                                        v.HumanoidRootPart.Size = Vector3.new(10,10,10)
                                                        TP2( v.HumanoidRootPart.CFrame * CFrame.new(0,25,0))
                                                        game:GetService'VirtualUser':CaptureController()
                                                        game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))                           
                                                        until not v.Parent or v.Humanoid.Health <= 0 or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
                                                    end)
                                                end
                                            end
                                        else
                                            TP2(CFrame.new(1057.92761, 137.614319, 1242.08069))
                                        end
                                    else
                                        TP2(CFrame.new(-456.28952, 73.0200958, 299.895966))
                                        wait(1.1)
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest","BartiloQuest",1)
                                    end
                                elseif game.Players.LocalPlayer.Data.Level.Value >= 800 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 1 then
                                    if game.Workspace.Enemies:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
                                        Ms = "Jeremy [Lv. 850] [Boss]"
                                        for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                            if v.Name == Ms then
                                                for i,v2 in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
                                                    if tostring(v2.ToolTip) == "Melee" then
                                                        EquipWeapon(v2.Name)
                                                    end
                                                end
                                                repeat wait()
                                                    
                                                    v.HumanoidRootPart.CanCollide = false
                                                    v.HumanoidRootPart.Size = Vector3.new(10,10,10)
                                                    TP2(v.HumanoidRootPart.CFrame * CFrame.new(0,25,0))
                                                    game:GetService'VirtualUser':CaptureController()
                                                    game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                                until not v.Parent or v.Humanoid.Health <= 0
                                            end
                                        end
                                    elseif game.ReplicatedStorage:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
                                        TP2(CFrame.new(-456.28952, 73.0200958, 299.895966))
                                        wait(1.1)
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo")
                                        wait(1)
                                        TP2(CFrame.new(2099.88159, 448.931, 648.997375))
                                        wait(2)
                                    else
                                        TP2(CFrame.new(2099.88159, 448.931, 648.997375))
                                    end
                                    wait(15)
                                    if not game.Workspace.Enemies:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
                                        Teleport()
                                    end
                                elseif game.Players.LocalPlayer.Data.Level.Value >= 800 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 2 then
                                    TP2(CFrame.new(-1850.49329, 13.1789551, 1750.89685))
                                    wait(1.5)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.87305, 19.3777466, 1712.01807)
                                    wait(1.5)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1803.94324, 16.5789185, 1750.89685)
                                    wait(1.5)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.55835, 16.8604317, 1724.79541)
                                    wait(1.5)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1869.54224, 15.987854, 1681.00659)
                                    wait(1.5)                                                                  
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1800.0979, 16.4978027, 1684.52368) 
                                    wait(1.5)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1819.26343, 15.795166, 1717.90625)
                                    wait(1.5)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1813.51843, 15.8604736, 1724.79541)
                                    wait(1.5)
                                end
                            end
                        else
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelZou")
                        end
                    elseif Old_World or Three_World then
                        _G.Setting_table.AutoFarm = true
                        _G.Setting_table.Three = false
                    end
                end
            end
        end)
    end)

    Waspon = {}
	for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
		if v:IsA("Tool") then
			table.insert(Waspon ,v.Name)
		end
	end
	for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do  
		if v:IsA("Tool") then
			table.insert(Waspon ,v.Name)
		end
	end

local Weapon = Main:Dropdown("SelectWeapon",Waspon, function(bool)
    _G.Setting_table.SelectWeapon = bool
    if _G.Setting_table.SelectWeapon == nil then
    else
        _G.Setting_table.EP = true
    end
    _G.Setting_table.SelectWeapon = bool
    savesetting()
end)

Main:Button("Refresh Weapon",function()
    Weapon:Clear()
    _G.Setting_table.SelectWeapon = nil
    _G.Setting_table.EP = nil
    
    for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
		if v:IsA("Tool") then
			Weapon:Add(v.Name)
		end
	end
	for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do  
		if v:IsA("Tool") then
			Weapon:Add(v.Name)
		end
	end
	savesetting()
end)

Main:Toggle("Fast Attack",_G.Setting_table.FastAttack,function(vu)
    FastAttack1 = vu
    _G.Setting_table.FastAttack = vu
    game:GetService("ReplicatedStorage").Assets.SlashHit:Destroy()
    savesetting()
end)
Main:Toggle("Effect Attack",_G.Setting_table.Effect_Attack,function(vu)
    _G.Setting_table.Effect_Attack = vu
    if _G.Setting_table.Effect_Attack then
        game:GetService("ReplicatedStorage").Assets.GUI.DamageCounter.Enabled = true
    else
        game:GetService("ReplicatedStorage").Assets.GUI.DamageCounter.Enabled = false
    end
    savesetting()
end)

Main:Label(" ")
Main:Label("Boss")
Main:Toggle("AutoFarm Boss",_G.Setting_table.AutoFarm_Boss,function(vu)
    AutoFarm_Boss = vu
    _G.Setting_table.AutoFarm_Boss = vu
    savesetting()
end)

Main:Toggle("Hop AutoFarm Boss",_G.Setting_table.Hop_AutoFarm_Boss,function(vu)
    if _G.Setting_table.SelectWeapon == nil and _G.Setting_table.SelectBoss == nil then
        DiscordLib:Notification("Notification", "SelectWeapon! - SelectBoss!", "Okay!")
    elseif _G.Setting_table.SelectWeapon == nil then
        DiscordLib:Notification("Notification", "SelectWeapon!", "Okay!")
    elseif _G.Setting_table.SelectBoss == nil then
        DiscordLib:Notification("Notification", "SelectBoss!", "Okay!")
    else
        AutoFarm_Boss = vu
        _G.Hop = vu
        _G.Setting_table.Hop_AutoFarm_Boss = vu
        savesetting()
    end
end)

local Bosslist = {}
for i, v in pairs(game.ReplicatedStorage:GetChildren()) do
    if string.find(v.Name, "Boss") then
        if v.Name ~= "Ice Admiral [Lv. 700] [Boss]" then
            table.insert(Bosslist, v.Name)
        end
    end
end
for i, v in pairs(game.workspace.Enemies:GetChildren()) do
    if string.find(v.Name, "Boss") then
        if v.Name ~= "Ice Admiral [Lv. 700] [Boss]" then
            table.insert(Bosslist, v.Name)
        end
    end
end

local BossP = Main:Dropdown("SelectBoss",Bosslist, function(bool)
    _G.Setting_table.SelectBoss = bool
end)

Main:Button("Refresh Boss",function()
    BossP:Clear()
    _G.Setting_table.SelectBoss = nil
    --local Boss = {}
    for i, v in pairs(game.ReplicatedStorage:GetChildren()) do
        if string.find(v.Name, "Boss") then
            if v.Name == "Ice Admiral [Lv. 700] [Boss]" then
            else
                -- table.insert(Boss, v.Name)
                BossP:Add(v.Name)
            end
        end
    end
    for i, v in pairs(game.workspace.Enemies:GetChildren()) do
        if string.find(v.Name, "Boss") then
            if v.Name ~= "Ice Admiral [Lv. 700] [Boss]" then
                BossP:Add(v.Name)
            end
        end
    end
end)

Main:Label(" ")
Main:Label("Misc Main")
Main:Button("Redeem All Code",function()
    Redeem()
end)
function Redeem()
    local args = {
        [1] = "Sub2OfficialNoobie"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "FUDD10"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "BIGNEWS"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "THEGREATACE"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "SUB2NOOBMASTER123"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "SUB2GAMERROBOT_EXP1"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "Sub2Daigrock"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "Axiore"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "TantaiGaming"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "STRAWHATMAINE"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "UPD15"
        }
        
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "2BILLION"
        }

        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "UPD16"
        }

        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        wait()
        local args = {
        [1] = "3BVISITS"
        }
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(unpack(args))
        _G.Redeem = true
end
spawn(function()
    pcall(function()
        while wait(3) do
            if _G.Setting_table.AutoCandyExp then
                if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Level.Exp.Text, "2x ends in") then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Candies","Buy",1,1)
                end
            end
        end
    end)
end)
Main:Toggle("AutoBuy LegendarySword",_G.Setting_table.LegendarySword,function(vu)
    _G.Setting_table.LegendarySword = vu
    LegendarySword = vu
end)


Main:Toggle("Auto Haki",_G.Setting_table.Haki,function(vu)
    _G.Setting_table.Haki = vu
end)
spawn(function()
    while wait(3) do
        if _G.Setting_table.Haki then
            if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
            end
        end
    end
end)

Main:Toggle("Auto KenHaki",_G.Setting_table.KenHaki,function(vu)
    _G.Setting_table.KenHaki = vu
end)

spawn(function()
    while wait(3) do
        if _G.Setting_table.KenHaki then
            game:GetService("ReplicatedStorage").Remotes.CommE:FireServer("Ken",true)
        end
    end
end)

Main:Label(" ")
Main:Label("Misc Hop")
Main:Toggle("AutoHop Buy LegendarySword",_G.Setting_table.HopLegendarySword,function(vu)
    _G.Setting_table.HopLegendarySword = vu
    LegendarySword = vu
end)
spawn(function()
	while wait(.1) do
	    local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
		if LegendarySword and New_World and Beli >= 2000000 then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LegendarySwordDealer","1")
			_G.Pik = true
		end
	end
end)
spawn(function()
    while wait(1) do
        if _G.Setting_table.HopLegendarySword then
            wait(10)
            Teleport()
        end
    end
end)

 
Main:Toggle("AutoHop LowerServer",_G.Setting_table.HopLowerServer,function(vu)
    _G.Setting_table.HopLowerServer = vu
    if _G.Hop then
    else
        PlayerDetect()
    end
end)
-------------------------------------------------------------- Main

-------------------------------------------------------------- AutoStats

AutoStats:Label("MarineFord")
AutoStats:Toggle("Melee",_G.Setting_table.Melee,function(vu)
    Melee = vu
    _G.Setting_table.Melee = vu
    savesetting()
end)
AutoStats:Toggle("Defense",_G.Setting_table.Defense,function(vu)
    Defense = vu
    _G.Setting_table.Defense = vu
    savesetting()
end)
AutoStats:Toggle("Sword",_G.Setting_table.Sword,function(vu)
    Sword = vu
    _G.Setting_table.Sword = vu
    savesetting()
end)
AutoStats:Toggle("Gun",_G.Setting_table.Gun,function(vu)
    Gun = vu
    _G.Setting_table.Gun = vu
    savesetting()
end)
AutoStats:Toggle("Devil Fruit",_G.Setting_table.Fruit,function(vu)
    Fruit = vu
    _G.Setting_table.Fruit = vu
    savesetting()
end)
local Point = AutoStats:Slider("SelectPoint", 1, 20, 1, function(t)
    SelectPoint = t
end)
-------------------------------------------------------------- AutoStats

-------------------------------------------------------------- Melee
MeleeP:Label("Main")
MeleeP:Toggle("Auto Superhuman",_G.Setting_table.Superhuman,function(vu)
    _G.Superhuman = vu
    _G.Setting_table.Superhuman = vu
    _G.Setting_table.EP = vu
    savesetting()
end)
MeleeP:Toggle("Auto Electric Claw",_G.Setting_table.Electric_Claw,function(vu)
    _G.Electric_Claw = vu
    _G.Setting_table.Electric_Claw = vu
    _G.Setting_table.EP = vu
    local args = {
        [1] = "BuyElectro"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    savesetting()
end)
MeleeP:Toggle("Auto Dragon Talon",_G.Setting_table.Dragon_Talon,function(vu)
    local args = {
                        [1] = "BlackbeardReward",
                        [2] = "DragonClaw",
                        [3] = "1"
                    }
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                    local args = {
                        [1] = "BlackbeardReward",
                        [2] = "DragonClaw",
                        [3] = "2"
                    }
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                    _G.Setting_table.EP = vu
    _G.Dragon_Talon = vu
    _G.Setting_table.Dragon_Talon = vu
    savesetting()
end)
MeleeP:Toggle("Auto Death Step",_G.Setting_table.Death_Step,function(vu)
    _G.Death_Step = vu
    _G.Setting_table.Death_Step = vu
    _G.Setting_table.EP = vu
    local args = {
        [1] = "BuyBlackLeg"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    savesetting()
end)
MeleeP:Toggle("Auto Sharkman Karate",_G.Setting_table.Sharkman_Karate,function(vu)
    _G.Sharkman_Karate = vu
    _G.Setting_table.Sharkman_Karate = vu
    _G.Setting_table.EP = vu
    local args = {
        [1] = "BuyFishmanKarate"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    savesetting()
end)
-------------------------------------------------------------- Melee

-------------------------------------------------------------- Sword

SwordP:Label("Main")
SwordP:Toggle("Auto BuddySword",_G.Setting_table.BuddySword,function(vu)
    _G.BuddySword = vu
    _G.Setting_table.BuddySword = vu
    savesetting()
end)
SwordP:Toggle("Auto Yama",_G.Setting_table.Yama,function(vu)
    _G.Yama = vu
    _G.Setting_table.Yama = vu
    savesetting()
end)
SwordP:Toggle("Auto Tushita",_G.Setting_table.Tushita,function(vu)
    _G.Tushita = vu
    _G.Setting_table.Tushita = vu
    savesetting()
end)
SwordP:Toggle("Auto HallowScryte",_G.Setting_table.Hallow_Scryte,function(vu)
    _G.Hallow_Scryte = vu
    _G.Setting_table.Hallow_Scryte = vu
    savesetting()
end)

SwordP:Label(" ")
SwordP:Label("Hop")
SwordP:Toggle("AutoHop BuddySword",_G.Setting_table.BuddySword_Hop,function(vu)
    _G.BuddySword = vu
    _G.Hop = vu
    _G.Setting_table.BuddySword_Hop = vu
    savesetting()
end)
---------------- Sword

---------------- Fruit
FruitP:Label("Main")
FruitP:Toggle("Devil Fruit Sniper",_G.Setting_table.BuyFruitSinper,function(vu)
	BuyFruitSinper = vu
	_G.Setting_table.BuyFruitSinper = vu
end)
local l__Remotes__11 = game.ReplicatedStorage:WaitForChild("Remotes");
u45 = l__Remotes__11.CommF_:InvokeServer("GetFruits");
Table_DevilFruitSniper = {}
for i,v in next,u45 do
    table.insert(Table_DevilFruitSniper,v.Name)
end
FruitP:Dropdown("Select Devil Fruit",Table_DevilFruitSniper,function(ply)
	_G.Setting_table.SelectDevil = ply
end)
spawn(function()
	while wait(2) do
		if BuyFruitSinper then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetFruits")
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("PurchaseRawFruit",_G.Setting_table.SelectBoss)
		end 
	end
end)
FruitP:Toggle("Bring Fruit",_G.Setting_table.BringFruit,function(vu)
    _G.BringFruit = vu
    _G.Setting_table.BringFruit = vu
    savesetting()
end)

FruitP:Toggle("Auto Buy Random Fruit",_G.Setting_table.RandomFruit, function(vu)
	_G.RandomFruit = vu
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
	_G.Setting_table.RandomFruit = vu
	savesetting()
end)
spawn(function()
    while wait(5) do
        if _G.RandomFruit then
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
        end
    end
end)
FruitP:Toggle("Fruit Inventory",_G.Setting_table.Fruit_Inventory,function(vu)
    _G.Setting_table.Fruit_Inventory = vu
    savesetting()
end)
spawn(function()
	pcall(function()
		while wait(.1) do
			if _G.Setting_table.Fruit_Inventory then
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bomb Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bomb Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bomb-Bomb")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spike Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spike Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spike-Spike")
                end
                if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Chop Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Chop Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Chop-Chop")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spring Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spring Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spring-Spring")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Kilo Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Kilo Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Kilo-Kilo")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Smoke Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Smoke Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Smoke-Smoke")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spin Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spin Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spin-Spin")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flame Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flame Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Flame-Flame")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Falcon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Falcon Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bird-Bird: Falcon")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Ice Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Ice Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Ice-Ice")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Sand Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Sand Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Sand-Sand")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dark Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dark Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dark-Dark")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Revive Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Revive Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Revive-Dark")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Diamond Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Diamond Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Diamond-Diamond")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Light Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Light Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Light-Light")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Love Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Love Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Love-Love")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rubber Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rubber Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Rubber-Rubber")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Barrier Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Barrier Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Barrier-Barrier")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Magma Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Magma Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Magma-Magma")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Door Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Door Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Door-Door")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Quake Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Quake Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Quake-Quake")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Human-Human: Buddha Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Human-Human: Buddha")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("String Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("String Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","String-String")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Phoenix Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Phoenix Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bird-Bird: Phoenix")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rumble Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rumble Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Rumble-Rumble")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Paw Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Paw Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Paw-Paw")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Gravity Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Gravity Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Gravity-Gravity")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dough Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dough Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dough-Dough")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Shadow Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Shadow Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Shadow-Shadow")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Venom Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Venom Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Venom-Venom")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Control Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Control Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Control-Control")
                end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dragon-Dragon")
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Soul Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Soul Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Soul-Sou")
				end
			end
		end
	end)
end)

---------------- Fruit

---------------- PVP
PVP:Label("Main")

---------------- PVP


---------------- Raid
Raid:Label("Main")
Raid:Toggle("AutoRaid",_G.Setting_table.Auto_Raid, function(vu)
    if _G.Setting_table.selectchip == nil then
	    DiscordLib:Notification("Notification", "Select Chip!", "Okay!")
	else
	    _G.Auto_Raid = vu
	    _G.Setting_table.Auto_Raid = vu
	    savesetting()
	end
end)
Raid:Toggle("AutoRaid Hop",_G.Setting_table.Auto_Raid_Hop, function(vu)
    if _G.Setting_table.selectchip == nil then
	    DiscordLib:Notification("Notification", "Select Chip!", "Okay!")
	else
	    for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
            if v:IsA ("Tool") then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame*CFrame.new(0,1,0)
                wait(1)
            end
	    end
    for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren()) do
                                                    if v.Name == "Island 5" then
                                                        v:Destroy()
                                                    elseif v.Name == "Island 4" then
                                                        v:Destroy()
                                                    elseif v.Name == "Island 3" then
                                                        v:Destroy()
                                                    elseif v.Name == "Island 2" then
                                                        v:Destroy()
                                                    elseif v.Name == "Island 1" then
                                                        v:Destroy()
                                                    end
                                                end
	    _G.Auto_Raid = vu
	    _G.Hop = vu
	    _G.Setting_table.Auto_Raid_Hop = vu
	    savesetting()
	end
end)
Raid:Toggle("Auto Awakener",_G.Setting_table.Auto_Awaken, function(vu)
    _G.Setting_table.Auto_Awaken = vu
    _G.AutoAwakener = vu
    savesetting()
end)


Raid:Dropdown("Select Chip",{"Flame","Ice","Quake","Light","Dark","String","Rumble","Magma","Human: Buddha"},function(t)
	_G.Setting_table.selectchip = t
	savesetting()
end)

Raid:Button("Buy Chip", function(vu)
	game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer( "RaidsNpc", "Select", _G.Setting_table.selectchip)
end)

---------------- Raid

---------------- Shop
Shop:Label("Main")
Shop:Button("Buy SkyJump",function()
    local args = {
        [1] = "BuyHaki",
        [2] = "Geppo"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Buy Soru",function()
    local args = {
        [1] = "BuyHaki",
        [2] = "Soru"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Buy Haki",function()
    local args = {
        [1] = "BuyHaki",
        [2] = "Buso"
    }

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))    
end)
Shop:Button("Buy KenHaki",function()
    local args = {
        [1] = "KenTalk",
        [2] = "Buy"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)


Shop:Label(" ")
Shop:Label("Melee")
Shop:Button("Buy Electro",function()
    local args = {
        [1] = "BuyElectro"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Buy Black Leg",function()
    local args = {
        [1] = "BuyBlackLeg"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Buy Fishman Karate",function()
    local args = {
        [1] = "BuyFishmanKarate"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Shop:Button("Buy Dragon Claw",function()
    local args = {
        [1] = "BlackbeardReward",
        [2] = "DragonClaw",
        [3] = "1"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    local args = {
        [1] = "BlackbeardReward",
        [2] = "DragonClaw",
        [3] = "2"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Label(" ")
Shop:Button("Buy Superhuman",function()
    local args = {
        [1] = "BuySuperhuman"
    }

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Shop:Button("Buy Death Step",function()
    local args = {
        [1] = "BuyDeathStep"
    }

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Shop:Button("Buy Shakman Karate",function()
    local args = {
        [1] = "BuySharkmanKarate",
        [2] = true
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    local args = {
        [1] = "BuySharkmanKarate"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Buy ElectricClaw",function()
    local args = {
        [1] = "BuyElectricClaw"
        }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Buy Dragon Talon",function()
    local args = {
        [1] = "BuyDragonTalon",
        [2] = true
        }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    local args = {
        [1] = "BuyDragonTalon"
        }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Shop:Label(" ")
Shop:Label("Sword")
Shop:Button("Buy Katana",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Katana")
end)
Shop:Button("Buy Cutlass",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cutlass")
end)
Shop:Button("Buy Duel Katana",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Duel Katana")
end)
Shop:Button("Buy Iron Mace",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Iron Mace")
end)
Shop:Button("Buy Pipe",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Pipe")
end)
Shop:Button("Triple Katana",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Triple Katana")
end)
Shop:Button("Dual-Headed Blade",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Dual-Headed Blade")
end)
Shop:Button("Bisento",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Bisento")
end)
Shop:Button("Soul Cane",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Soul Cane")
end)

Shop:Label(" ")
Shop:Label("Gun")
Shop:Button("Buy Slingshot",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Slingshot")
end)
Shop:Button("Buy Musket",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Musket")
end)
Shop:Button("Buy Fintlock",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Flintlock")
end)
Shop:Button("Buy Refined Flintlock",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Refined Flintlock")
end)
Shop:Button("Buy Cannon",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cannon")
end)
Shop:Button("Buy Kabucha",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","1")
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","2")
end)
Shop:Label(" ")
Shop:Label("Candy")
Shop:Button("Buy Fragments 300",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 2,
        [4] = 1
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Buy Fragments 700",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 2,
        [4] = 2
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Toggle("AutoBuy Exp x2",_G.Setting_table.AutoCandyExp,function(vu)
    _G.Setting_table.AutoCandyExp = vu
end)
Shop:Button("Buy Exp x2",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 1,
        [4] = 1
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Buy Refund Stat",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 1,
        [4] = 2
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Buy Random Ability",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 1,
        [4] = 3
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Shop:Label(" ")
Shop:Label("Fragments")
Shop:Button("Buy Refund Stat",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","1")
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","2")
end)
Shop:Button("Buy Random Ability",function()
    local args = {
        [1] = "BlackbeardReward",
        [2] = "Reroll",
        [3] = "2"
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Shop:Label(" ")
Shop:Label("Bone")
Shop:Button("Buy Random Surprise",function()
-- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Bones",
    [2] = "Check"
}

game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
-- Script generated by SimpleSpy - credits to exx#9394

local args = {
    [1] = "Bones",
    [2] = "Buy",
    [3] = 1,
    [4] = 1
}

game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))

end)

---------------- Shop

---------------- Teleport
Teleport:Label("Teleport Main")
Teleport:Button("Hop Server",function()
    Teleport()
end)
Teleport:Button("Hop LowerServer",function()
    HopLowerServer()
end)

Teleport:Label(" ")
Teleport:Label("Teleport World")
Teleport:Button("Old World",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelMain")
end)
Teleport:Button("New World",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
end)
Teleport:Button("Three World",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelZou")
end)
Teleport:Label(" ")
Teleport:Label("Teleport Map")
if Old_World then
          Teleport:Button("Start Island",function()
             TP2(CFrame.new(1071.2832, 16.3085976, 1426.86792))
          end)
          Teleport:Button("Marine Start",function()
             TP2(CFrame.new(-2573.3374, 6.88881969, 2046.99817))
          end)
          Teleport:Button("Middle Town",function()
             TP2(CFrame.new(-655.824158, 7.88708115, 1436.67908))
          end)
          Teleport:Button("Jungle",function()
             TP2(CFrame.new(-1249.77222, 11.8870859, 341.356476))
          end)
          Teleport:Button("Pirate Village",function()
             TP2(CFrame.new(-1122.34998, 4.78708982, 3855.91992))
          end)
          Teleport:Button("Desert",function()
             TP2(CFrame.new(1094.14587, 6.47350502, 4192.88721))
          end)
          Teleport:Button("Frozen Village",function()
             TP2(CFrame.new(1198.00928, 27.0074959, -1211.73376))
          end)
          Teleport:Button("MarineFord",function()
             TP2(CFrame.new(-4505.375, 20.687294, 4260.55908))
          end)
          Teleport:Button("Colosseum",function()
             TP2(CFrame.new(-1428.35474, 7.38933945, -3014.37305))
          end)
          Teleport:Button("Sky 1st Floor",function()
             TP2(CFrame.new(-4970.21875, 717.707275, -2622.35449))
          end)
          Teleport:Button("Sky 2st Floor",function()
             TP2(CFrame.new(-4813.0249, 903.708557, -1912.69055))
          end)
          Teleport:Button("Sky 3st Floor",function()
             TP2(CFrame.new(-7952.31006, 5545.52832, -320.704956))
          end)
          Teleport:Button("Prison",function()
             TP2(CFrame.new(4854.16455, 5.68742752, 740.194641))
          end)
          Teleport:Button("Magma Village",function()
             TP2(CFrame.new(-5231.75879, 8.61593437, 8467.87695))
          end)
          Teleport:Button("UndeyWater City",function()
             TP2(CFrame.new(61163.8516, 11.7796879, 1819.78418))
          end)
          Teleport:Button("Fountain City",function()
             TP2(CFrame.new(5132.7124, 4.53632832, 4037.8562))
          end)
          Teleport:Button("House Cyborg's",function()
             TP2(CFrame.new(6262.72559, 71.3003616, 3998.23047))
          end)
          Teleport:Button("Shank's Room",function()
             TP2(CFrame.new(-1442.16553, 29.8788261, -28.3547478))
          end)
          Teleport:Button("Mob Island",function()
             TP2(CFrame.new(-2850.20068, 7.39224768, 5354.99268))
          end)
end
if New_World then
    	Teleport:Button("Dock",function()
			TP2(CFrame.new(82.9490662, 18.0710983, 2834.98779))
		end)
		Teleport:Button("Kingdom of Rose",function()
			TP2(CFrame.new(-394.983521, 118.503128, 1245.8446))
		end)
		Teleport:Button("Dark Arena",function()
			TP2(game.Workspace["_WorldOrigin"].Locations["Dark Arena"].CFrame)
		end)
		Teleport:Button("Mansion",function()
			TP2(CFrame.new(-390.096313, 331.886475, 673.464966))
		end)
		Teleport:Button("Flamingo Room",function()
			TP2(CFrame.new(2302.19019, 15.1778421, 663.811035))
		end)
		Teleport:Button("Green Zone",function()
			TP2(CFrame.new(-2372.14697, 72.9919434, -3166.51416))
		end)
		Teleport:Button("Cafe",function()
			TP2(CFrame.new(-385.250916, 73.0458984, 297.388397))
		end)
		Teleport:Button("Factroy",function()
			TP2(CFrame.new(430.42569, 210.019623, -432.504791))
		end)
		Teleport:Button("Colosseum",function()
			TP2(CFrame.new(-1836.58191, 44.5890656, 1360.30652))
		end)
		Teleport:Button("GraveIsland",function()
			TP2(CFrame.new(-5411.47607, 48.8234024, -721.272522))
		end)
		Teleport:Button("Snow Mountain",function()
			TP2(CFrame.new(511.825226, 401.765198, -5380.396))
		end)
		Teleport:Button("Cold Island",function()
			TP2(CFrame.new(-6026.96484, 14.7461271, -5071.96338))
		end)
		Teleport:Button("Hot Island",function()
			TP2(CFrame.new(-5478.39209, 15.9775667, -5246.9126))
		end)
		Teleport:Button("Cursed Ship",function()
			TP2(CFrame.new(902.059143, 124.752518, 33071.8125))
		end)
		Teleport:Button("IceCastle",function()
			TP2(CFrame.new(5400.40381, 28.21698, -6236.99219))
		end)
		Teleport:Button("Forgotten Island",function()
			TP2(CFrame.new(-3043.31543, 238.881271, -10191.5791))
		end)
		Teleport:Button("Usoapp Island",function()
			TP2(CFrame.new(4748.78857, 8.35370827, 2849.57959))
		end)
		Teleport:Button("Minisky Island",function()
			TP2(CFrame.new(-260.358917, 49325.7031, -35259.3008))
		end)
end
if Three_World then
        Teleport:Button("Port Towen",function()
			TP2(CFrame.new(-610.309692, 57.8323097, 6436.33594, 1, 0, 0, 0, 1, 0, 0, 0, 1))
		end)
		Teleport:Button("Hydra Island",function()
			TP2(CFrame.new(5229.99561, 603.916565, 345.154022, -0.137452736, 6.26227887e-08, -0.990508318, 5.81512971e-08, 1, 5.51532295e-08, 0.990508318, -5.00183823e-08, -0.137452736))
		end)
		Teleport:Button("Great Tree",function()
			TP2(CFrame.new(2174.94873, 28.7312393, -6728.83154, 0.864815354, 2.51030592e-08, -0.502090037, -5.24263299e-09, 1, 4.09670555e-08, 0.502090037, -3.27966632e-08, 0.864815354))
		end)
		Teleport:Button("Castle on the Sea",function()
			TP2(CFrame.new(-5477.62842, 313.794739, -2808.4585, 0.914748192, -2.40542199e-08, 0.404024392, -8.97737973e-09, 1, 7.98621613e-08, -0.404024392, -7.66808483e-08, 0.914748192))
		end)
		Teleport:Button("Floating Turtle",function()
			TP2(CFrame.new(-10919.2998, 331.788452, -8637.57227, 0.606543362, 0, -0.795050383, -0, 1, -0, 0.795050383, 0, 0.606543362))
		end)
		Teleport:Button("Mansion",function()
			TP2(CFrame.new(-12553.8125, 332.403961, -7621.91748, -0.999466479, 2.33264661e-08, 0.0326608531, 2.2023519e-08, 1, -4.02529707e-08, -0.0326608531, -3.95121873e-08, -0.999466479))
		end)
		Teleport:Button("Secret Temple",function()
			TP2(CFrame.new(5217.35693, 6.56511116, 1100.88159, 0.00408430398, 7.00437894e-08, -0.999991655, 1.42367229e-08, 1, 7.01025229e-08, 0.999991655, -1.45229242e-08, 0.00408430398))
		end)
		Teleport:Button("Friendly Arena",function()
			TP2(CFrame.new(5220.28955, 72.8193436, -1450.86304, 1, 0, 0, 0, 1, 0, 0, 0, 1))
		end)
		Teleport:Button("Beautiful Pirate Domain",function()
			TP2(CFrame.new(5310.8095703125, 21.594484329224, 129.39053344727))
		end)
end
---------------- Teleport
local PlaceID = game.PlaceId
local AllIDs = {}
local foundAnything = ""
local actualHour = os.date("!*t").hour
local Deleted = false
local File = pcall(function()
	AllIDs = game:GetService('HttpService'):JSONDecode(readfile("NotSameServers.json"))
end)
if not File then
	table.insert(AllIDs, actualHour)
	writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
end
function TPReturner()
	local Site;
	if foundAnything == "" then
		Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
	else
		Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
	end
	local ID = ""
	if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
		foundAnything = Site.nextPageCursor
	end
	local num = 0;
	for i,v in pairs(Site.data) do
		local Possible = true
		ID = tostring(v.id)
		if tonumber(v.maxPlayers) > tonumber(v.playing) then
		    game.StarterGui:SetCore("SendNotification", {
                Title = "Hop Server", 
                Text = "Players : " ..tonumber(v.playing),
                Icon = "http://www.roblox.com/asset/?id=8987392618",
                Duration = 1.5
            })
			for _,Existing in pairs(AllIDs) do
				if num ~= 0 then
					if ID == tostring(Existing) then
						Possible = false
					end
				else
				if tonumber(actualHour) ~= tonumber(Existing) then
					local delFile = pcall(function()
						--delfile("NotSameServers.json")
						AllIDs = {}
						table.insert(AllIDs, actualHour)
					end)
				end
			end
			num = num + 1
		end
		if Possible == true then
			table.insert(AllIDs, ID)
			wait(0.2)
			pcall(function()
				--writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
				wait(0.2)
				game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
			end)
			end
		end
	end
end

function Teleport()
	while wait(0.2) do
		pcall(function()
			TPReturner()
			if foundAnything ~= "" then
				TPReturner()
			end
		end)
	end
end
---------------- Sword
spawn(function()
    while wait() do
        if _G.BuddySword then
            if game:GetService("Workspace").Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") or game.ReplicatedStorage:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
                repeat game:GetService("RunService").Stepped:wait()
                    TP(game:GetService("Workspace").Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]").CFrame*CFrame.new(0,25,0))
                    game:GetService'VirtualUser':CaptureController()
                    game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                until game:GetService("Workspace").Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]").Humanoid.Health <= 0 or not game:GetService("Workspace").Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") or _G.BuddySword == false
            else
                if (Vector3.new(-821, 66, -10965)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10 then
                    repeat wait(1)
                        TP2(CFrame.new(-821, 66, -10965))
                    until (Vector3.new(-821, 66, -10965)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 10
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                end
                wait(5)
                if not game:GetService("Workspace").Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") and _G.Hop == true and not game.ReplicatedStorage:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
                    game.StarterGui:SetCore("SendNotification", {
                        Title = "Liver Hub", 
                        Text = "ไม่เจอบอส",
                        Icon = "http://www.roblox.com/asset/?id=8987392618",
                        Duration = 3
                    })
                    wait(1)
                    Teleport()
                end
            end
        end
    end
end)

---------------- Sword
local games = game:HttpGet("https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/Public") -- send request to API
local json = game:GetService("HttpService"):JSONDecode(games)
local maxplayerCount = 4

function PlayerDetect()
               local Players = game.Players:GetPlayers()
               if #Players  > maxplayerCount then
                   _G.Teleport = true
                   HopLowerServer()
                   for i = 1,#json.data do
                       if json.data[i].id ~= game.JobId then
                           --HopLowerServer()
                           if json.data[i].maxPlayers ~= json.data[i].playing then
                               --HopLowerServer()
                               if json.data[i].playing < 3 or json.data[i].playing < maxplayerCount then
                               end
                           end
                       end
                   end
               end
            end

spawn(function()
    while wait(2) do
        if _G.Setting_table.HopLowerServer then
            game.Players.PlayerAdded:Connect(function()
                if _G.Teleport == nil then
                    PlayerDetect()
                    wait(10)
                end
            end)
        end
    end
end)
