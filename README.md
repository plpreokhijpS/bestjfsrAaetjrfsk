-------------------------------------------------------------- Save Setting
_G.Setting_table = {
    Auto_Farm = false,
    Hop_AutoFarm_Boss = false,
    Auto_Farm_Boss = false,
    FastAttack1 = true,
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
-------------------------------------------------------------- savesetting

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
if game:GetService("CoreGui"):FindFirstChild("LiverHub") then
    game:GetService("CoreGui"):FindFirstChild("LiverHub"):Destroy()
end
-------------------------------------------------------------- Code
spawn(function()
    while task.wait() do
        if  Auto_Farm == true or Katakuri or _G.Setting_table.AutoFarm_Players or Clip == true or Auto_Farm_Fruit or _G.FarmMasteryFruit == true or BuddySword == true or AutoFarm_Boss or _G.Auto_Raid or Auto_Three then 
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
        					if not string.find(x.Name,"Boss") and(x.HumanoidRootPart.Position-_G.PosMon.Position).Magnitude <= 300 then --370
        						x.HumanoidRootPart.CFrame = _G.PosMon
        						x.Humanoid.JumpPower = 0
        						x.Humanoid.WalkSpeed = 0
        						x.HumanoidRootPart.Size = Vector3.new(50,50,50)
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
                                    v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                                    if v.Humanoid:FindFirstChild("Animator") then
                                        v.Humanoid.Animator:Destroy()
                                    end
                                    sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
            						v.Humanoid:ChangeState(14)
                                            health = v.Humanoid.Health
                                            maxhealth = v.Humanoid.MaxHealth
                                            percent = (health / maxhealth) * 100 --percentage
            						StatrMagnet = true
            						    if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                            local args = {
                                                [1] = "Buso"
                                            }
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            						    end
                                        Fruit_E = game:GetService("Players").LocalPlayer.Data.DevilFruit.Value
                                        if Auto_Farm_Fruit then
                                            for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
                                                if tostring(v2.ToolTip) == "Melee" then
                                                    Melee_E = v2.Name
                                                end
                                            end
                                            local vim = game:service("VirtualInputManager")
                                            local function hold(keyCode, time)
                                                vim:SendKeyEvent(true, keyCode, false, game)
                                                task.wait(time)
                                                vim:SendKeyEvent(false, keyCode, false, game)
                                            end
                                            game.Workspace.CurrentCamera.CameraSubject = v.Humanoid
                                            repeat wait(.1)
                                                pcall(function()
                                            health = v.Humanoid.Health
                                            maxhealth = v.Humanoid.MaxHealth
                                            percent = (health / maxhealth) * 100 --percentage
                                                if percent <= MinHealth then
                                                    EquipWeapon(Fruit_E)
                                                    TP(v.HumanoidRootPart.CFrame * CFrame.new(0,-10,0))
                                                    wait(0.3)
                                                    --game.Workspace.CurrentCamera.CoordinateFrame = CFrame.new(game.Workspace.CurrentCamera.CoordinateFrame.p,v.HumanoidRootPart.CFrame)
                                                    if Auto_Skill_Z then
                                                    
                                                        hold(Enum.KeyCode.Z, 0.1)
                                                    end
                                                    if Auto_Skill_X then
                                                        
                                                        hold(Enum.KeyCode.X, 0.1)
                                                    end
                                                    if Auto_Skill_C then
                                                        
                                                        hold(Enum.KeyCode.C, 0.1)
                                                    end
                                                    if Auto_Skill_V then
                                                        
                                                        hold(Enum.KeyCode.V, 0.1)
                                                    end
                                                elseif percent > MinHealth then
                                                    if percent > MinHealth then
                                                        EquipWeapon(Melee_E)
                                                        TP(v.HumanoidRootPart.CFrame * CFrame.new(0,20,0))
                                                        game:GetService'VirtualUser':CaptureController()
                                                        game:GetService'VirtualUser':CreateButton1Down(Vector2.new(1280, 672))
                                                    end
                                                end
                                                end)
                                            until v.Humanoid.Health <= 0 or not v.Parent or Auto_Farm_Fruit == false or Auto_Farm == false or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false or game.Players.LocalPlayer.Character.Humanoid.Health <= 0
                                        else
                                            repeat game:GetService("RunService").Stepped:wait()
                                                TP(v.HumanoidRootPart.CFrame * CFrame.new(0,20,0))
                                                game:GetService'VirtualUser':CaptureController()
                                                game:GetService'VirtualUser':CreateButton1Down(Vector2.new(1280, 672))
                                            until v.Humanoid.Health <= 0 or not v.Parent or Auto_Farm == false or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false or game.Players.LocalPlayer.Character.Humanoid.Health <= 0 
                                        end
                                        game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
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
		elseif Lv >= 1900 and Lv <= 1924 or SelectMonster == "Jungle Pirate [Lv. 1900]" then -- Jungle Pirate
			Ms = "Jungle Pirate [Lv. 1900]"
			NameQuest = "DeepForestIsland2"
			QuestLv = 1
			NameMon = "Jungle Pirate"
			CFrameQ = CFrame.new(-12682.096679688, 390.88653564453, -9902.1240234375)
			CFrameMon = CFrame.new(-12267.103515625, 459.75262451172, -10277.200195313)
		elseif Lv >= 1925 and Lv <= 1974 or SelectMonster == "Musketeer Pirate [Lv. 1925]" then -- Musketeer Pirate
			Ms = "Musketeer Pirate [Lv. 1925]"
			NameQuest = "DeepForestIsland2"
			QuestLv = 2
			NameMon = "Musketeer Pirate"
			CFrameQ = CFrame.new(-12682.096679688, 390.88653564453, -9902.1240234375)
			CFrameMon = CFrame.new(-13291.5078125, 520.47338867188, -9904.638671875)
		elseif Lv >= 1975 and Lv <= 1999 or SelectMonster == "Reborn Skeleton [Lv. 1975]" then -- Reborn Skeleton
			Ms = "Musketeer Pirate [Lv. 1925]"
			NameQuest = "DeepForestIsland2"
			QuestLv = 2
			NameMon = "Musketeer Pirate"
			CFrameQ = CFrame.new(-12682.096679688, 390.88653564453, -9902.1240234375)
			CFrameMon = CFrame.new(-13291.5078125, 520.47338867188, -9904.638671875)
		elseif Lv >= 2000 and Lv <= 2024 or SelectMonster == "Living Zombie [Lv. 2000]" then -- Living Zombie
			Ms = "Living Zombie [Lv. 2000]"
			NameQuest = "HauntedQuest1"
			QuestLv = 2
			NameMon = "Living Zombie"
			CFrameQ = CFrame.new(-9480.80762, 142.130661, 5566.37305)
			CFrameMon = CFrame.new(-10103.7529, 238.565979, 6179.75977)
		elseif Lv >= 2025 and Lv <= 2049 or SelectMonster == "Demonic Soul [Lv. 2025]" then -- Demonic Soul
			Ms = "Demonic Soul [Lv. 2025]"
			NameQuest = "HauntedQuest1"
			QuestLv = 1
			NameMon = "Demonic Souls"
			CFrameQ = CFrame.new(-9515.39551, 172.266037, 6078.89746)
			CFrameMon = CFrame.new(-9709.30762, 204.695892, 6044.04688)
		elseif Lv >= 2050 and Lv <= 2074 or SelectMonster == "Posessed Mummy [Lv. 2050]" then -- Posessed Mummy
			Ms = "Posessed Mummy [Lv. 2050]"
			NameQuest = "HauntedQuest2"
			QuestLv = 2
			NameMon = "Posessed Mummys"
			CFrameQ = CFrame.new(-9515.39551, 172.266037, 6078.89746)
			CFrameMon = CFrame.new(-9554.11035, 65.6141663, 6041.73584)
		elseif Lv >= 2075 and Lv <= 2099 or SelectMonster == "Peanut Scout [Lv. 2075]" then -- Peanut Scout
			Ms = "Peanut Scout [Lv. 2075]"
			NameQuest = "PeanutQuest1"
			QuestLv = 1
			NameMon = "Peanut Scout"
			CFrameQ = CFrame.new(-2104.453125, 38.129974365234, -10194.0078125)
			CFrameMon = CFrame.new(-2068.0949707031, 76.512603759766, -10117.150390625)
		elseif Lv >= 2100 and Lv <= 2124 or SelectMonster == "Peanut President [Lv. 2100]" then -- Peanut President
			Ms = "Peanut President [Lv. 2100]"
			NameQuest = "PeanutQuest2"
			QuestLv = 2
			NameMon = "Peanut Presidents"
			CFrameQ = CFrame.new(-2104.453125, 38.129974365234, -10194.0078125)
			CFrameMon = CFrame.new(-2067.33203125, 90.557350158691, -10552.051757812)
		elseif Lv >= 2125 and Lv <= 2149 or SelectMonster == "Ice Cream Chef [Lv. 2125]" then --Ice Cream Chef
			Ms = "Ice Cream Chef [Lv. 2125]"
			NameQuest = "IceCreamQuest1"
			QuestLv = 1
			NameMon = "	Ice Cream Chefs"
			CFrameQ = CFrame.new(-821.35913085938, 65.845329284668, -10965.2578125)
			CFrameMon = CFrame.new(-796.37261962891, 110.95275878906, -10847.473632812)
		elseif Lv >= 2150 and Lv <= 2200 or SelectMonster == "Ice Cream Commander [Lv. 2150]" then -- Ice Cream Commander
			Ms = "Ice Cream Commander [Lv. 2150]"
			NameQuest = "IceCreamIslandQuest"
			QuestLv = 2
			NameMon = "Ice Cream Commanders"
			CFrameQ = CFrame.new(-821.35913085938, 65.845329284668, -10965.2578125)
			CFrameMon = CFrame.new(-697.65338134766, 174.48368835449, -11218.38671875)
		elseif Lv >= 2200 and Lv <= 2250 or SelectMonster == "Ice Cream Commander [Lv. 2150]" then -- Ice Cream Commander
			Ms = "Cookie Crafter [Lv. 2200]"
			NameQuest = "CakeQuest1"
			QuestLv = 1
			NameMon = "Cookie Crafters"
			CFrameQ = CFrame.new(-2017.4874267578125, 36.85276412963867, -12027.53515625)
			CFrameMon = CFrame.new(-2358.5791015625, 36.85615539550781, -12111.052734375)
		elseif Lv >= 2225 or SelectMonster == "Cake Guard [Lv. 2225]" then
		    Ms = "Cake Guard [Lv. 2225]"
		    NameQuest = "CakeQuest1"
		    QuestLv = 2
		    NameMon = "Cake Guards"
		    CFrameMon = CFrame.new(-1430.4925537109375, 36.85621643066406, -12322.162109375)
		    CFrameQ = CFrame.new(-2017.4874267578125, 36.85276412963867, -12027.53515625)
        end
	end
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
		game:GetService("Players").LocalPlayer.Idled:connect(function()
			VirtualUser:CreateButton2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
			wait(1)
			VirtualUser:CreateButton2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
		end)
	end)

    function EquipWeapon(ToolSe)
        if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
            local tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
            wait(.4)
            game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
        end
    end
-------------------------------------------------------------- Code
local Config = {
    WindowName = "Liver Hub - Premium",
	Color = Color3.fromRGB(0, 255, 170),
	Keybind = Enum.KeyCode.RightControl
}

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/x7Swiftz/UI-V4/main/README.md"))()
local Window = Library:CreateWindow(Config, game:GetService("CoreGui"))

local page1 = Window:CreateTab("Main")
local page2 = Window:CreateTab("PvP")
local page3 = Window:CreateTab("Raid")
local page4 = Window:CreateTab("Shop")
local page5 = Window:CreateTab("Teleport")
local page6 = Window:CreateTab("Misc")
local Tab2 = Window:CreateTab("UI Settings")
game:GetService("CoreGui").LiverHub.Main.Holder.Border.BorderColor3 = Color3.fromRGB(118, 254, 227)
game:GetService("CoreGui").LiverHub.Main.Holder.TBContainer.Holder["Main TB"].Title.TextStrokeTransparency = 0.3
game:GetService("CoreGui").LiverHub.Main.Holder.TBContainer.Holder["PvP TB"].Title.TextStrokeTransparency = 0.3
game:GetService("CoreGui").LiverHub.Main.Holder.TBContainer.Holder["Raid TB"].Title.TextStrokeTransparency = 0.3
game:GetService("CoreGui").LiverHub.Main.Holder.TBContainer.Holder["Shop TB"].Title.TextStrokeTransparency = 0.3
game:GetService("CoreGui").LiverHub.Main.Holder.TBContainer.Holder["Teleport TB"].Title.TextStrokeTransparency = 0.3
game:GetService("CoreGui").LiverHub.Main.Holder.TBContainer.Holder["Misc TB"].Title.TextStrokeTransparency = 0.3
game:GetService("CoreGui").LiverHub.Main.Holder.TBContainer.Holder["UI Settings TB"].Title.TextStrokeTransparency = 0.3
game:GetService("CoreGui").LiverHub.Main.Border.BorderColor3 = Color3.fromRGB(0, 255, 170)
game:GetService("CoreGui").LiverHub.Main.Holder.TBContainer.BorderColor3 = Color3.fromRGB(0, 255, 170)
game:GetService("CoreGui").LiverHub.Main.Holder.TBContainer.BorderSizePixel = 1
game:GetService("CoreGui").LiverHub.Main.Topbar.WindowName.TextColor3 = Color3.fromRGB(118, 254, 227)

local Section3 = Tab2:CreateSection("Menu")
local Section4 = Tab2:CreateSection("Background")


-------------
local Toggle3 = Section3:CreateToggle("UI Toggle", nil, function(State)
	Window:Toggle(State)
end)
Toggle3:CreateKeybind(tostring(Config.Keybind):gsub("Enum.KeyCode.", ""), function(Key)
	Config.Keybind = Enum.KeyCode[Key]
end)
Toggle3:SetState(true)

local Colorpicker3 = Section3:CreateColorpicker("UI Color", function(Color)
	Window:ChangeColor(Color)
end)
Colorpicker3:UpdateColor(Config.Color)

-- credits to jan for patterns
local Dropdown3 = Section4:CreateDropdown("Image", {"Default","Hearts","Abstract","Hexagon","Circles","Lace With Flowers","Floral"}, function(Name)
	if Name == "Default" then
	    Window:SetBackground("5553946656")
		--Window:SetBackground("2151741365")
	elseif Name == "Hearts" then
		Window:SetBackground("6073763717")
	elseif Name == "Abstract" then
		Window:SetBackground("6073743871")
	elseif Name == "Hexagon" then
		Window:SetBackground("6073628839")
	elseif Name == "Circles" then
		Window:SetBackground("6071579801")
	elseif Name == "Lace With Flowers" then
		Window:SetBackground("6071575925")
	elseif Name == "Floral" then
		Window:SetBackground("5553946656")
	end
end)
Dropdown3:SetOption("Default")

local Colorpicker4 = Section4:CreateColorpicker("Color",function(Color)
    --Color = Color3.fromRGB(0, 255, 170)
	Window:SetBackgroundColor(Color)
end)
Colorpicker4:UpdateColor(Color3.new(0, 255, 170))

local Slider3 = Section4:CreateSlider("Transparency",0,1,nil,false, function(Value)
	Window:SetBackgroundTransparency(Value)
end)
Slider3:SetValue(0.88)

local Slider4 = Section4:CreateSlider("Tile Scale",0,1,nil,false, function(Value)
	Window:SetTileScale(Value)
end)
Slider4:SetValue(0.37)


-------------------------------------------------- Blox Fruit
local Main = page1:CreateSection("AutoFarm Level")
Main:CreateToggle("Auto Farm",_G.Setting_table.AutoFarm,function(vu)
    _G.Setting_table.AutoFarm = vu
    SelectMonster = nil
    Auto_Farm = vu
    savesetting()
end)
Main:CreateToggle("Fast Attack",_G.Setting_table.FastAttack1,function(vu)
    FastAttack1 = vu
    _G.Setting_table.FastAttack1 = vu
    savesetting()
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

Main:CreateToggle("Effect Attack",_G.Setting_table.Effect_Attack,function(vu)
    _G.Setting_table.Effect_Attack = vu
    if _G.Setting_table.Effect_Attack then
        game:GetService("ReplicatedStorage").Assets.GUI.DamageCounter.Enabled = true
    else
        game:GetService("ReplicatedStorage").Assets.GUI.DamageCounter.Enabled = false
    end
    savesetting()
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

local SelectWeapon = Main:CreateDropdown("SelectWeapon", Waspon, function(Name)
    _G.Setting_table.SelectWeapon = Name
    if _G.Setting_table.SelectWeapon == nil then
        _G.Setting_table.EP = false
    else
        _G.Setting_table.EP = true
        EquipWeapon(_G.Setting_table.SelectWeapon)
    end
    savesetting()
    while _G.Setting_table.EP == true do wait(2)
        EquipWeapon(_G.Setting_table.SelectWeapon)
    end
end)
Main:CreateButton("Refresh Weapon",function()
    _G.Setting_table.EP = nil
    _G.Setting_table.SelectWeapon = nil
    SelectWeapon:ClearOptions()
    SelectWeapon:Up()
    savesetting()
end)

local Main3 = page1:CreateSection("Status")
Mp = 0
Elite = Main3:CreateLabel("Kill Elite Hunter  :  "..Mp)
if Three_World then
    _G.Lip = true
end
Lp = 500
Monster = Main3:CreateLabel("Kill Monster  :  "..Lp.."/".."500")
spawn(function()
    while _G.Lip do wait(1)
        OP = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CakePrinceSpawner")
        Lp = tonumber(string.match(tostring(OP), "%d+"))
        if Lp > 0 then
            Monster:UpdateText("Kill Monster  :  "..Lp.."/".."500")
        else
            Monster:UpdateText("Kill Monster  :  ".."nil".."/".."500")
        end
    end
end)
spawn(function()
    while _G.Lip do wait(3)
        Elite:UpdateText("Kill Elite Hunter  :  "..game.ReplicatedStorage.Remotes.CommF_:InvokeServer("EliteHunter", "Progress"))
    end
end)

local Main7 = page1:CreateSection("AutoStats")
Main7:CreateToggle("Melee",_G.Setting_table.Melee,function(vu)
    _G.Setting_table.Melee = vu
    savesetting()
end)
Main7:CreateToggle("Sword",_G.Setting_table.Sword,function(vu)
    _G.Setting_table.Sword = vu
    savesetting()
end)
Main7:CreateToggle("Defense",_G.Setting_table.Defense,function(vu)
    _G.Setting_table.Defense = vu
    savesetting()
end)
Main7:CreateToggle("Fruit",_G.Setting_table.Fruit,function(vu)
    _G.Setting_table.Fruit = vu
    savesetting()
end)
Main7:CreateToggle("Gun",_G.Setting_table.Gun,function(vu)
    _G.Setting_table.Gun = vu
    savesetting()
end)
local Point = Main7:CreateSlider("Point", 1,20,nil,true, function(Value)
	SelectPoint = Value
end)
Point:SetValue(3)

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

local New = page1:CreateSection("New! UPDATE")
New:CreateToggle("Auto Boss Katakuri ❌",false,function()
    
end)
New:CreateToggle("Auto Awake Phoenix ❌",false,function()
    
end)
New:CreateToggle("Auto Yoru V3 ❌",false,function()
    
end)



local Main6 = page1:CreateSection("AutoFarm Mastery")
Main6:CreateToggle("AutoFarm DevilFruit",_G.Setting_table.Auto_Farm_Fruit,function(vu)
    Auto_Farm_Fruit = vu
    Auto_Farm = vu
    _G.Setting_table.Auto_Farm_Fruit = vu
    savesetting()
end)
Main6:CreateToggle("AutoFarm Gun ❌",false,function()
    
end)
MinHealth = 25
local HPmin = Main6:CreateSlider("Health %", 1,100,nil,true, function(Value)
	MinHealth = Value
end)
HPmin:AddToolTip("Health Monser")
HPmin:SetValue(25)

Main6:CreateToggle("Auto Skill Z",true,function(vu)
    Auto_Skill_Z = vu
end)
Main6:CreateToggle("Auto Skill X",false,function(vu)
    Auto_Skill_X = vu
end)
Main6:CreateToggle("Auto Skill C",false,function(vu)
    Auto_Skill_C = vu
end)
Main6:CreateToggle("Auto Skill V",false,function(vu)
    Auto_Skill_V = vu
end)



local Main3 = page1:CreateSection("Melee")
Main3:CreateToggle("Auto Superhuman ❌",false,function()
    
end)
Main3:CreateToggle("Auto Sharkman Karate ❌",false,function()
    
end)
Main3:CreateToggle("Auto Death Step ❌",false,function()
    
end)
Main3:CreateToggle("Auto Electric Claw ❌",false,function()
    
end)
Main3:CreateToggle("Auto Dragon Talon ❌",false,function()
    
end)


local Main4 = page1:CreateSection("Sword")
Main4:CreateToggle("Auto BuddySword ",false,function()
    
end)
Main4:CreateToggle("Auto DarkDagger ❌",false,function()
    
end)
Main4:CreateToggle("Auto Tushita ❌",false,function()
    
end)
Main4:CreateToggle("Auto Yama ❌",false,function()
    
end)
Main4:CreateToggle("Auto Saber ❌",false,function()
    
end)


Mons = {}
local xx = {}
for i,v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
    if string.find(v.Name , "Lv") then
        table.insert(xx, v.Name)
    end
end
table.sort(xx)
local result = {}

for key,value in ipairs(xx) do
  if value ~=xx[key+1] then
    table.insert(result,value)
  end
end

for key,value in ipairs(result) do
    table.insert(Mons, value)
end
local End = page1:CreateSection("AutoFarm Monster")
End:CreateToggle("AutoFarm",false,function(vu)
    if SelectMonster == nil then
        
    else
        Auto_Farm = vu
    end
end)

local SelectMonster = End:CreateDropdown("Select Monster", Mons, function(Name)
    SelectMonster = Name
end)



local Main5 = page1:CreateSection("Boss")
Main5:CreateToggle("Auto Boss EliteHunter ❌",false,function()
    
end)
Main5:CreateToggle("Auto Boss Rip indra ( Admin ) ❌",false,function()
    
end)


local Main8 = page1:CreateSection("Accessory")
Main8:CreateToggle("Auto Swan Glass ❌",false,function()
    
end)
Main8:CreateToggle("Auto Dark Code ❌",false,function()
    
end)


local Main9 = page1:CreateSection("Evo Ability")
Main9:CreateToggle("Auto Evo Mink ❌",false,function()
    
end)
Main9:CreateToggle("Auto Evo Sky ❌",false,function()
    
end)
Main9:CreateToggle("Auto Evo Human ❌",false,function()
    
end)
Main9:CreateToggle("Auto Evo FishMan ❌",false,function()
    
end)
Main9:CreateToggle("Auto Evo Ghool ❌",false,function()
    
end)
Main9:CreateToggle("Auto Evo Cyborg ❌",false,function()
    
end)

local Main10 = page5:CreateSection("Teleport Map")

local Map_Misc = page5:CreateSection("Teleport Server")

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
Map_Misc:CreateButton("Hop Server",function()
    Teleport()
end)
Map_Misc:CreateButton("Hop LowerServer",function()
    HopLowerServer()
end)
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
Map_Misc:CreateToggle("Auto Hop LowerServer",_G.Setting_table.HopLowerServer,function(vu)
     _G.Setting_table.HopLowerServer = vu
    if _G.Hop then
        
    else
        if _G.Setting_table.HopLowerServer then
            PlayerDetect()
        end
    end
end)


if Old_World then
          Main10:CreateButton("Start Island",function()
             TP2(CFrame.new(1071.2832, 16.3085976, 1426.86792))
          end)
          Main10:CreateButton("Marine Start",function()
             TP2(CFrame.new(-2573.3374, 6.88881969, 2046.99817))
          end)
          Main10:CreateButton("Middle Town",function()
             TP2(CFrame.new(-655.824158, 7.88708115, 1436.67908))
          end)
          Main10:CreateButton("Jungle",function()
             TP2(CFrame.new(-1249.77222, 11.8870859, 341.356476))
          end)
          Main10:CreateButton("Pirate Village",function()
             TP2(CFrame.new(-1122.34998, 4.78708982, 3855.91992))
          end)
          Main10:CreateButton("Desert",function()
             TP2(CFrame.new(1094.14587, 6.47350502, 4192.88721))
          end)
          Main10:CreateButton("Frozen Village",function()
             TP2(CFrame.new(1198.00928, 27.0074959, -1211.73376))
          end)
          Main10:CreateButton("MarineFord",function()
             TP2(CFrame.new(-4505.375, 20.687294, 4260.55908))
          end)
          Main10:CreateButton("Colosseum",function()
             TP2(CFrame.new(-1428.35474, 7.38933945, -3014.37305))
          end)
          Main10:CreateButton("Sky 1st Floor",function()
             TP2(CFrame.new(-4970.21875, 717.707275, -2622.35449))
          end)
          Main10:CreateButton("Sky 2st Floor",function()
             TP2(CFrame.new(-4813.0249, 903.708557, -1912.69055))
          end)
          Main10:CreateButton("Sky 3st Floor",function()
             TP2(CFrame.new(-7952.31006, 5545.52832, -320.704956))
          end)
          Main10:CreateButton("Prison",function()
             TP2(CFrame.new(4854.16455, 5.68742752, 740.194641))
          end)
          Main10:CreateButton("Magma Village",function()
             TP2(CFrame.new(-5231.75879, 8.61593437, 8467.87695))
          end)
          Main10:CreateButton("UndeyWater City",function()
             TP2(CFrame.new(61163.8516, 11.7796879, 1819.78418))
          end)
          Main10:CreateButton("Fountain City",function()
             TP2(CFrame.new(5132.7124, 4.53632832, 4037.8562))
          end)
          Main10:CreateButton("House Cyborg's",function()
             TP2(CFrame.new(6262.72559, 71.3003616, 3998.23047))
          end)
          Main10:CreateButton("Shank's Room",function()
             TP2(CFrame.new(-1442.16553, 29.8788261, -28.3547478))
          end)
          Main10:CreateButton("Mob Island",function()
             TP2(CFrame.new(-2850.20068, 7.39224768, 5354.99268))
          end)
end
if New_World then
    		Main10:CreateButton("Dock",function()
			TP2(CFrame.new(82.9490662, 18.0710983, 2834.98779))
		end)
		Main10:CreateButton("Kingdom of Rose",function()
			TP2(CFrame.new(-394.983521, 118.503128, 1245.8446))
		end)
		Main10:CreateButton("Dark Arena",function()
			TP2(game.Workspace["_WorldOrigin"].Locations["Dark Arena"].CFrame)
		end)
		Main10:CreateButton("Mansion",function()
			TP2(CFrame.new(-390.096313, 331.886475, 673.464966))
		end)
		Main10:CreateButton("Flamingo Room",function()
			TP2(CFrame.new(2302.19019, 15.1778421, 663.811035))
		end)
		Main10:CreateButton("Green Zone",function()
			TP2(CFrame.new(-2372.14697, 72.9919434, -3166.51416))
		end)
		Main10:CreateButton("Cafe",function()
			TP2(CFrame.new(-385.250916, 73.0458984, 297.388397))
		end)
		Main10:CreateButton("Factroy",function()
			TP2(CFrame.new(430.42569, 210.019623, -432.504791))
		end)
		Main10:CreateButton("Colosseum",function()
			TP2(CFrame.new(-1836.58191, 44.5890656, 1360.30652))
		end)
		Main10:CreateButton("GraveIsland",function()
			TP2(CFrame.new(-5411.47607, 48.8234024, -721.272522))
		end)
		Main10:CreateButton("Snow Mountain",function()
			TP2(CFrame.new(511.825226, 401.765198, -5380.396))
		end)
		Main10:CreateButton("Cold Island",function()
			TP2(CFrame.new(-6026.96484, 14.7461271, -5071.96338))
		end)
		Main10:CreateButton("Hot Island",function()
			TP2(CFrame.new(-5478.39209, 15.9775667, -5246.9126))
		end)
		Main10:CreateButton("Cursed Ship",function()
			TP2(CFrame.new(902.059143, 124.752518, 33071.8125))
		end)
		Main10:CreateButton("IceCastle",function()
			TP2(CFrame.new(5400.40381, 28.21698, -6236.99219))
		end)
		Main10:CreateButton("Forgotten Island",function()
			TP2(CFrame.new(-3043.31543, 238.881271, -10191.5791))
		end)
		Main10:CreateButton("Usoapp Island",function()
			TP2(CFrame.new(4748.78857, 8.35370827, 2849.57959))
		end)
		Main10:CreateButton("Minisky Island",function()
			TP2(CFrame.new(-260.358917, 49325.7031, -35259.3008))
		end)
end
if Three_World then
    Main10:CreateButton("Port Towen",function()
			TP2(CFrame.new(-610.309692, 57.8323097, 6436.33594, 1, 0, 0, 0, 1, 0, 0, 0, 1))
		end)
		Main10:CreateButton("Hydra Island",function()
			TP2(CFrame.new(5229.99561, 603.916565, 345.154022, -0.137452736, 6.26227887e-08, -0.990508318, 5.81512971e-08, 1, 5.51532295e-08, 0.990508318, -5.00183823e-08, -0.137452736))
		end)
		Main10:CreateButton("Great Tree",function()
			TP2(CFrame.new(2174.94873, 28.7312393, -6728.83154, 0.864815354, 2.51030592e-08, -0.502090037, -5.24263299e-09, 1, 4.09670555e-08, 0.502090037, -3.27966632e-08, 0.864815354))
		end)
		Main10:CreateButton("Castle on the Sea",function()
			TP2(CFrame.new(-5477.62842, 313.794739, -2808.4585, 0.914748192, -2.40542199e-08, 0.404024392, -8.97737973e-09, 1, 7.98621613e-08, -0.404024392, -7.66808483e-08, 0.914748192))
		end)
		Main10:CreateButton("Floating Turtle",function()
			TP2(CFrame.new(-10919.2998, 331.788452, -8637.57227, 0.606543362, 0, -0.795050383, -0, 1, -0, 0.795050383, 0, 0.606543362))
		end)
		Main10:CreateButton("Mansion",function()
			TP2(CFrame.new(-12553.8125, 332.403961, -7621.91748, -0.999466479, 2.33264661e-08, 0.0326608531, 2.2023519e-08, 1, -4.02529707e-08, -0.0326608531, -3.95121873e-08, -0.999466479))
		end)
		Main10:CreateButton("Secret Temple",function()
			TP2(CFrame.new(5217.35693, 6.56511116, 1100.88159, 0.00408430398, 7.00437894e-08, -0.999991655, 1.42367229e-08, 1, 7.01025229e-08, 0.999991655, -1.45229242e-08, 0.00408430398))
		end)
		Main10:CreateButton("Friendly Arena",function()
			TP2(CFrame.new(5220.28955, 72.8193436, -1450.86304, 1, 0, 0, 0, 1, 0, 0, 0, 1))
		end)
		Main10:CreateButton("Beautiful Pirate Domain",function()
			TP2(CFrame.new(5310.8095703125, 21.594484329224, 129.39053344727))
		end)
end



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
                                                    wait(3)
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
                                                --if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true and game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
                                					if game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 5"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 3000 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 5"].CFrame*CFrame.new(0,80,0))
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame*CFrame.new(0,80,0))
                                					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 4"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 3000 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 4"].CFrame*CFrame.new(0,80,0))
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame*CFrame.new(0,80,0))
                                					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 3"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 3000 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 3"].CFrame*CFrame.new(0,80,0))
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame*CFrame.new(0,80,0))
                                					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 2"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 3000 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 2"].CFrame*CFrame.new(0,80,0))
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame*CFrame.new(0,80,0))
                                					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") and (game:GetService("Workspace")["_WorldOrigin"].Locations["Island 1"].Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 3000 then
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations["Island 1"].CFrame*CFrame.new(0,80,0))
                                						TP2(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame*CFrame.new(0,80,0))
                                					end
                                                --end
                                            end
                                        end
                                    end
                                end)
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


local Main15 = page4:CreateSection("Main")
Main15:CreateButton("Buy SkyJump",function()
    local args = {
        [1] = "BuyHaki",
        [2] = "Geppo"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Main15:CreateButton("Buy Soru",function()
    local args = {
        [1] = "BuyHaki",
        [2] = "Soru"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Main15:CreateButton("Buy Haki",function()
    local args = {
        [1] = "BuyHaki",
        [2] = "Buso"
    }

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))    
end)
Main15:CreateButton("Buy KenHaki",function()
    local args = {
        [1] = "KenTalk",
        [2] = "Buy"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

local Main14 = page4:CreateSection("Fruit")
Main14:CreateToggle("Devil Fruit Sniper",_G.Setting_table.BuyFruitSinper,function(vu)
	BuyFruitSinper = vu
	_G.Setting_table.BuyFruitSinper = vu
	savesetting()
end)
local l__Remotes__11 = game.ReplicatedStorage:WaitForChild("Remotes");
u45 = l__Remotes__11.CommF_:InvokeServer("GetFruits");
Table_DevilFruitSniper = {}
for i,v in next,u45 do
    table.insert(Table_DevilFruitSniper,v.Name)
end
local Sniper_Fruit = Main14:CreateDropdown("Select Devil Fruit",Table_DevilFruitSniper,function(ply)
	_G.Setting_table.SelectDevil = ply
	savesetting()
end)

spawn(function()
	while wait(2) do
		if BuyFruitSinper then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetFruits")
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("PurchaseRawFruit",_G.Setting_table.SelectBoss)
		end 
	end
end)
Main14:CreateToggle("Bring Fruit",_G.Setting_table.BringFruit,function(vu)
    _G.BringFruit = vu
    _G.Setting_table.BringFruit = vu
    savesetting()
end)

Main14:CreateToggle("Auto Buy Random Fruit",_G.Setting_table.RandomFruit, function(vu)
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
Main14:CreateToggle("Fruit Inventory",_G.Setting_table.Fruit_Inventory,function(vu)
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

local Main16 = page4:CreateSection("Melee")
Main16:CreateButton("Buy Electro",function()
    local args = {
        [1] = "BuyElectro"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Main16:CreateButton("Buy Black Leg",function()
    local args = {
        [1] = "BuyBlackLeg"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Main16:CreateButton("Buy Fishman Karate",function()
    local args = {
        [1] = "BuyFishmanKarate"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Main16:CreateButton("Buy Dragon Claw",function()
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
Main16:CreateLabel(" ")
Main16:CreateButton("Buy Superhuman",function()
    local args = {
        [1] = "BuySuperhuman"
    }

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Main16:CreateButton("Buy Death Step",function()
    local args = {
        [1] = "BuyDeathStep"
    }

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Main16:CreateButton("Buy Shakman Karate",function()
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
Main16:CreateButton("Buy ElectricClaw",function()
    local args = {
        [1] = "BuyElectricClaw"
        }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Main16:CreateButton("Buy Dragon Talon",function()
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

local Main17 = page4:CreateSection("Sword")
Main17:CreateButton("Buy Katana",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Katana")
end)
Main17:CreateButton("Buy Cutlass",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cutlass")
end)
Main17:CreateButton("Buy Duel Katana",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Duel Katana")
end)
Main17:CreateButton("Buy Iron Mace",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Iron Mace")
end)
Main17:CreateButton("Buy Pipe",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Pipe")
end)
Main17:CreateButton("Triple Katana",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Triple Katana")
end)
Main17:CreateButton("Dual-Headed Blade",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Dual-Headed Blade")
end)
Main17:CreateButton("Bisento",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Bisento")
end)
Main17:CreateButton("Soul Cane",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Soul Cane")
end)

local Main18 = page4:CreateSection("Gun")
Main18:CreateButton("Buy Slingshot",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Slingshot")
end)
Main18:CreateButton("Buy Musket",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Musket")
end)
Main18:CreateButton("Buy Fintlock",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Flintlock")
end)
Main18:CreateButton("Buy Refined Flintlock",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Refined Flintlock")
end)
Main18:CreateButton("Buy Cannon",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cannon")
end)
Main18:CreateButton("Buy Kabucha",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","1")
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","2")
end)

local Main19 = page4:CreateSection("Candy")
Main19:CreateButton("Buy Fragments 300",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 2,
        [4] = 1
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Main19:CreateButton("Buy Fragments 700",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 2,
        [4] = 2
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Main19:CreateToggle("AutoBuy Exp x2",_G.Setting_table.AutoCandyExp,function(vu)
    _G.Setting_table.AutoCandyExp = vu
end)
Main19:CreateButton("Buy Exp x2",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 1,
        [4] = 1
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Main19:CreateButton("Buy Refund Stat",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 1,
        [4] = 2
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Main19:CreateButton("Buy Random Ability",function()
    local args = {
        [1] = "Candies",
        [2] = "Buy",
        [3] = 1,
        [4] = 3
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)


local Main20 = page4:CreateSection("Fragments")
Main20:CreateButton("Buy Refund Stat",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","1")
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","2")
end)
Main20:CreateButton("Buy Random Ability",function()
    local args = {
        [1] = "BlackbeardReward",
        [2] = "Reroll",
        [3] = "2"
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)


local Main21 = page4:CreateSection("Bone")
Main21:CreateButton("Buy Random Surprise",function()
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

Main21:CreateToggle("AutoBuy Random Surprise",_G.Setting_table.Auto_Random,function(vu)
    _G.Auto_Random = vu
    _G.Setting_table.Auto_Random = vu
    savesetting()
end)

spawn(function()
    while wait(0.3) do
        if _G.Auto_Random then
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
        end
    end
end)



local Main11 = page3:CreateSection("Main")
local Main13 = page3:CreateSection("Misc")
Main13:CreateToggle("Bring Fruit",_G.Setting_table.BringFruit_Raid,function(vu)
    _G.Setting_table.BringFruit_Raid = vu
    _G.BringFruit = vu
    savesetting()
end)

Main11:CreateToggle("AutoRaid",_G.Setting_table.Auto_Raid, function(vu)
    _G.Auto_Raid = vu
    _G.Setting_table.Auto_Raid = vu
    savesetting()
end)
Main11:CreateToggle("AutoRaid Hop",_G.Setting_table.Auto_Raid_Hop, function(vu)
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
        if v:IsA ("Tool") then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame*CFrame.new(0,1,0)
            wait(1)
        end
	end
	if _G.Auto_Raid then
	    
	else
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
    end
	    _G.Auto_Raid = vu
	    _G.Hop = vu
	    _G.Setting_table.Auto_Raid_Hop = vu
	    savesetting()
end)
Main11:CreateToggle("Auto Awakener",_G.Setting_table.Auto_Awaken, function(vu)
    _G.Setting_table.Auto_Awaken = vu
    _G.AutoAwakener = vu
    savesetting()
end)


local Chip_Raid = Main11:CreateDropdown("Select Chip",{"Flame","Ice","Quake","Light","Dark","String","Rumble","Magma","Human: Buddha"},function(t)
	_G.Setting_table.selectchip = t
	savesetting()
end)
Chip_Raid:SetOption(_G.Setting_table.selectchip)

Main11:CreateButton("Buy Chip", function(vu)
	game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer( "RaidsNpc", "Select", _G.Setting_table.selectchip)
end)



spawn(function()
    while wait() do
        if _G.BringFruit then
            for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
                if v:IsA ("Tool") and (v.Handle.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 20000 then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame
                    wait(0.5)
                end
            end
        end
    end
end)

-------------------------------------------------- Blox Fruit
