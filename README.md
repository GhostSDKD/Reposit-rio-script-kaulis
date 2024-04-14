--Kaulis.hub
-- Script desenvolvido por Kauam
-- Versão: 1.0
-- Data de criação: 14/04/2024
repeat task.wait()until game:IsLoaded()
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local VirtualUser = game:GetService("VirtualUser")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")

local Remotes = ReplicatedStorage:WaitForChild("Remotes", 9e9)
local CommF = Remotes:WaitForChild("CommF_", 9e9)

local Enemies = workspace:WaitForChild("Enemies", 9e9)
local Boats = workspace:WaitForChild("Boats", 9e9)

local Player = Players.LocalPlayer
local PlayerLevel = Player.Data.Level 
local Quest = {CFrame.new(), CFrame.new(), "", "", 1}
local QuestTween = {}
local Sea1, Sea2, Sea3 = game.PlaceId == 2753915549, game.PlaceId == 4442272183, game.PlaceId == 7449423635

local function Get_Fruit(Fruit)
  if Fruit == "Rocket Fruit" then
    return "Rocket-Rocket"
  elseif Fruit == "Spin Fruit" then
    return "Spin-Spin"
  elseif Fruit == "Chop Fruit" then
    return "Chop-Chop"
  elseif Fruit == "Spring Fruit" then
    return "Spring-Spring"
  elseif Fruit == "Bomb Fruit" then
    return "Bomb-Bomb"
  elseif Fruit == "Smoke Fruit" then
    return "Smoke-Smoke"
  elseif Fruit == "Spike Fruit" then
    return "Spike-Spike"
  elseif Fruit == "Flame Fruit" then
    return "Flame-Flame"
  elseif Fruit == "Falcon Fruit" then
    return "Falcon-Falcon"
  elseif Fruit == "Ice Fruit" then
    return "Ice-Ice"
  elseif Fruit == "Sand Fruit" then
    return "Sand-Sand"
  elseif Fruit == "Dark Fruit" then
    return "Dark-Dark"
  elseif Fruit == "Ghost Fruit" then
    return "Ghost-Ghost"
  elseif Fruit == "Diamond Fruit" then
    return "Diamond-Diamond"
  elseif Fruit == "Light Fruit" then
    return "Light-Light"
  elseif Fruit == "Rubber Fruit" then
    return "Rubber-Rubber"
  elseif Fruit == "Barrier Fruit" then
    return "Barrier-Barrier"
  elseif Fruit == "Magma Fruit" then
    return "Magma-Magma"
  elseif Fruit == "Quake Fruit" then
    return "Quake-Quake"
  elseif Fruit == "Buddha Fruit" then
    return "Buddha-Buddha"
  elseif Fruit == "Love Fruit" then
    return "Love-Love"
  elseif Fruit == "Spider Fruit" then
    return "Spider-Spider"
  elseif Fruit == "Sound Fruit" then
    return "Sound-Sound"
  elseif Fruit == "Phoenix Fruit" then
    return "Phoenix-Phoenix"
  elseif Fruit == "Portal Fruit" then
    return "Portal-Portal"
  elseif Fruit == "Rumble Fruit" then
    return "Rumble-Rumble"
  elseif Fruit == "Pain Fruit" then
    return "Pain-Pain"
  elseif Fruit == "Blizzard Fruit" then
    return "Blizzard-Blizzard"
  elseif Fruit == "Gravity Fruit" then
    return "Gravity-Gravity"
  elseif Fruit == "Mammoth Fruit" then
    return "Mammoth-Mammoth"
  elseif Fruit == "T-Rex Fruit" then
    return "T-Rex-T-Rex"
  elseif Fruit == "Dough Fruit" then
    return "Dough-Dough"
  elseif Fruit == "Shadow Fruit" then
    return "Shadow-Shadow"
  elseif Fruit == "Venom Fruit" then
    return "Venom-Venom"
  elseif Fruit == "Control Fruit" then
    return "Control-Control"
  elseif Fruit == "Spirit Fruit" then
    return "Spirit-Spirit"
  elseif Fruit == "Dragon Fruit" then
    return "Dragon-Dragon"
  elseif Fruit == "Leopard Fruit" then
    return "Leopard-Leopard"
  elseif Fruit == "Kitsune Fruit" then
    return "Kitsune-Kitsune"
  end
end

local function GetBossQuest(BossName)
  -- Bosses Sea 1
  if BossName == "The Gorilla King" then
    return true, CFrame.new(-1128, 6, -451), "JungleQuest"
  elseif BossName == "Bobby" then
    return true, CFrame.new(-1131, 14, 4080), "BuggyQuest1"
  elseif BossName == "Yeti" then
    return true, CFrame.new(1185, 106, -1518), "SnowQuest"
  elseif BossName == "Vice Admiral" then
    return true, CFrame.new(-4807, 21, 4360), "MarineQuest2", 2
  elseif BossName == "Swan" then
    return true, CFrame.new(5230, 4, 749), "ImpelQuest"
  elseif BossName == "Chief Warden" then
    return true, CFrame.new(5230, 4, 749), "ImpelQuest", 2
  elseif BossName == "Warden" then
    return true, CFrame.new(5230, 4, 749), "ImpelQuest", 1
  elseif BossName == "Magma Admiral" then
    return true, CFrame.new(-5694, 18, 8735), "MagmaQuest"
  elseif BossName == "Fishman Lord" then
    return true, CFrame.new(61350, 31, 1095), "FishmanQuest"
  elseif BossName == "Wysper" then
    return true, CFrame.new(-7927, 5551, -637), "SkyExp1Quest"
  elseif BossName == "Thunder God" then
    return true, CFrame.new(-7751, 5607, -2315), "SkyExp2Quest"
  elseif BossName == "Cyborg" then
    return true, CFrame.new(6138, 10, 3939), "FountainQuest"
  elseif BossName == "Saber Expert" then
    return false, CFrame.new(-1461, 30, -51)
  elseif BossName == "The Saw" then
    return false, CFrame.new(-690, 15, 1583)
  elseif BossName == "Greybeard" then
    return false, CFrame.new(-4807, 21, 4360)
  -- Bosses Sea 2
  elseif BossName == "Diamond" then
    return true, CFrame.new(-1569, 199, -31), "Area1Quest"
  elseif BossName == "Jeremy" then
    return true, CFrame.new(2316, 449, 787), "Area2Quest"
  elseif BossName == "Fajita" then
    return true, CFrame.new(-2086, 73, -4208), "MarineQuest3"
  elseif BossName == "Smoke Admiral" then
    return true, CFrame.new(-5078, 24, -5352), "IceSideQuest"
  elseif BossName == "Awakened Ice Admiral" then
    return true, CFrame.new(6473, 297, -6944), "FrostQuest"
  elseif BossName == "Tide Keeper" then
    return true, CFrame.new(-3711, 77, -11469), "ForgottenQuest"
  elseif BossName == "Don Swan" then
    return false, CFrame.new(2289, 15, 808)
  elseif BossName == "Cursed Captain" then
    return false, CFrame.new(912, 186, 33591)
  elseif BossName == "Darkbeard" then
    return false, CFrame.new(3695, 13, -3599)
  -- Bosses Sea 3
  elseif BossName == "Longma" then
    return false, CFrame.new(-10218, 333, -9444)
  elseif BossName == "Stone" then
    return true, CFrame.new(-1049, 40, 6791), "PiratePortQuest"
  elseif BossName == "Beautiful Pirate" then
    return true, CFrame.new(5241, 23, 129), "DeepForestIsland2"
  elseif BossName == "Island Empress" then
    return true, CFrame.new(5730, 602, 199), "AmazonQuest2"
  elseif BossName == "Kilo Admiral" then
    return true, CFrame.new(2889, 424, -7233), "MarineTreeIsland"
  elseif BossName == "Captain Elephant" then
    return true, CFrame.new(-13393, 319, -8423), "DeepForestIsland"
  elseif BossName == "Cake Queen" then
    return true, CFrame.new(-710, 382, -11150), "IceCreamIslandQuest"
  elseif BossName == "Dough King" or BossName == "Cake Prince" then
    return false, CFrame.new(-2103, 70, -12165)
  elseif BossName == "rip_indra True Form" then
    return false, CFrame.new(-5333, 424, -2673)
  end
end

local BossListT = {
  -- Sea 1 --
  -- Raid Boss
  "Greybeard",
  "The Saw",
  "Saber Expert",
  
  -- Normal Boss
  "The Gorilla King",
  "Bobby",
  "Yeti",
  "Vice Admiral",
  "Warden",
  "Chief Warden",
  "Swan",
  "Magma Admiral",
  "Fishman Lord",
  "Wysper",
  "Thunder God",
  "Cyborg",
  
  -- Sea 2 --
  -- Raid Boss
  "Darkbeard",
  "Cursed Captain",
  "Order",
  "Don Swan",
  
  -- Normal Blss
  "Diamond",
  "Jeremy",
  "Fajita",
  "Smoke Admiral",
  "Awakened Ice Admiral",
  "Tide Keeper",
  
  -- Sea 3 --
  -- Raid Boss
  "Dough King",
  "Cake Prince",
  "rip_indra True Form",
  "Soul Reaper",
  
  -- Normal Boss
  "Stone",
  "Island Empress",
  "Kilo Admiral",
  "Captain Elephant",
  "Beautiful Pirate",
  "Cake Queen",
  "Longma"
}

local function FireRemote(...)
  return CommF:InvokeServer(...)
end

local block = Instance.new("Part", workspace)
block.Size = Vector3.new(1, 1, 1)
block.Name = "player platform ............."
block.Anchored = true
block.CanCollide = false
block.CanTouch = false
block.Transparency = 1

local blockfind = workspace:FindFirstChild(block.Name)
if blockfind and blockfind ~= block then
  blockfind:Destroy()
end

task.spawn(function()
  while task.wait() do
    if block and block.Parent == workspace then
      if getgenv().AutoFarmNearest
      or getgenv().TeleportToIsland
      or getgenv().AutoFinishTrial
      or getgenv().AutoWoodPlanks
      or getgenv().AutoFarm_Level
      -- or getgenv().AutoGift
      -- or getgenv().AutoCandy
      or getgenv().AutoFarmSea
      or getgenv().AutoEliteHunter
      or getgenv().AutoPiratesSea
      or getgenv().AutoFarmBossSelected
      or getgenv().AutoRengoku
      or getgenv().TeleportToFruit
      or getgenv().AutoFactory
      or getgenv().AutoBartiloQuest
      or getgenv().AutoFarmRaid
      or getgenv().AutoRaceV2
      or getgenv().AutoCakePrince
      or getgenv().AutoDoughKing
      or getgenv().RipIndraLegendaryHaki
      or getgenv().AutoRipIndra
      or getgenv().AutoUnlockSaber
      or getgenv().AutoSawBoss
      or getgenv().AutoEnelBossPole
      or getgenv().AutoMusketeerHat
      or getgenv().AutoKenV2
      or getgenv().AutoFarmKen
      or getgenv().AutoFarmBone
      or getgenv().AutoCursedCaptain
      or getgenv().AutoFarmEctoplasm
      or getgenv().AutoKitsuneIsland
      or getgenv().AutoSoulReaper
      or getgenv().AutoSoulGuitar
      or getgenv().TeleportToMirage
      or getgenv().AutoSecondSea
      or getgenv().AutoThirdSea
      or getgenv().AutoDarkbeard
      or getgenv().AutoKillLawBoss
      or getgenv().AutoChestTween
      or getgenv().AutoRainbowHaki
      or getgenv().AutoFarmMaterial
      or getgenv().AutoSharkmanKarate
      or getgenv().AutoKillDonSwan
      or getgenv().AutoSoulGuitar
      or getgenv().AutoCursedDualKatana
      or getgenv().AutoDeathStep
      or getgenv().AutoDragonTalon
      or getgenv().AutoElectricClaw
      or getgenv().AutoSuperhuman
      or getgenv().AutoMasteryFightingStyle
      or getgenv().AutoGodHuman
      or getgenv().AutoTushita
      or getgenv().AutoFarmMastery
      or getgenv().NPCtween
      or getgenv().KillAllBosses then
        getgenv().OnFarm = true
      else
        getgenv().OnFarm = false
      end
    else
      getgenv().OnFarm = false
    end
  end
end)

task.spawn(function()
  repeat task.wait()
  until Player.Character and Player.Character.PrimaryPart
  block.CFrame = Player.Character.PrimaryPart.CFrame
  
  while task.wait() do
    pcall(function()
      if getgenv().OnFarm then
        if block and block.Parent == workspace then
          local plrPP = Player.Character and Player.Character.PrimaryPart
          
          if plrPP and (plrPP.Position - block.Position).Magnitude <= 200 then
            plrPP.CFrame = block.CFrame
          else
            block.CFrame = plrPP.CFrame
          end
        end
        local plrChar = Player.Character
        if plrChar then
          for _,part in pairs(plrChar:GetChildren()) do
            if part:IsA("BasePart") then
              part.CanCollide = false
            end
          end
          if plrChar:FindFirstChild("Stun") and plrChar.Stun.Value ~= 0 then
            plrChar.Stun.Value = 0
          end
          if plrChar:FindFirstChild("Busy") and plrChar.Busy.Value then
            plrChar.Busy.Value = false
          end
        end
      else
        local plrChar = Player.Character
        if plrChar then
          for _,part in pairs(plrChar:GetChildren()) do
            if part:IsA("BasePart") then
              part.CanCollide = true
            end
          end
        end
      end
    end)
  end
end)

task.spawn(function()
  local PortalPos = {}
  
  if Sea1 then
    PortalPos = {
      Vector3.new(-4652, 873, -1754), -- Sky Island 1
      Vector3.new(-7895, 5547, -380), -- Sky Island 2
      Vector3.new(61164, 5, 1820), -- Under Water Island
      Vector3.new(3865, 5, -1926) -- Under Water Island Entrace
    }
  elseif Sea2 then
    PortalPos = {
      Vector3.new(-317, 331, 597), -- Flamingo Mansion
      Vector3.new(2283, 15, 867), -- Flamingo Room
      Vector3.new(923, 125, 32853), -- Cursed Ship
      Vector3.new(-6509, 83, -133) -- Zombie Island0
    }
  elseif Sea3 then
    PortalPos = {
      Vector3.new(-12471, 374, -7551), -- Mansion
      Vector3.new(5756, 610, -282), -- Hydra Island
      Vector3.new(-5092, 315, -3130), -- Castle on the Sea
      Vector3.new(-12001, 332, -8861), -- Floating Turtle
      Vector3.new(5319, 23, -93), -- Beautiful Pirate
      Vector3.new(28286, 14897, 103) -- Temple of Time
    }
  end
  
  function GetTPPos(position)
    local NearPos = math.huge
    local TpPos = Vector3.new()
    
    table.foreach(PortalPos, function(___, pos)
      if (pos - position).Magnitude <= NearPos then
        NearPos = (pos - position).Magnitude
        TpPos = pos
      end
    end)
    return TpPos
  end
end)

local TeleportPos
local function PlayerTP(Tween_Pos)
  TeleportPos = Tween_Pos.p
  local plrPP = Player.Character and Player.Character.PrimaryPart
  if not plrPP then return end
  local Distance = (plrPP.Position - Tween_Pos.p).Magnitude
  local PortalPos = GetTPPos(Tween_Pos.p)
  if (plrPP.Position - Tween_Pos.p).Magnitude > (Tween_Pos.p - PortalPos).Magnitude + 250 then
    plrPP.CFrame = CFrame.new(PortalPos)
    block.CFrame = CFrame.new(PortalPos)
  elseif block then
    if Distance <= 450 then
      local tween = game:GetService("TweenService"):Create(block,
      TweenInfo.new(Distance / tonumber(getgenv().TweenSpeed * 1.8), Enum.EasingStyle.Linear),
      {CFrame = Tween_Pos}):Play()
    else
      local tween = game:GetService("TweenService"):Create(block,
      TweenInfo.new(Distance / getgenv().TweenSpeed, Enum.EasingStyle.Linear),
      {CFrame = Tween_Pos}):Play()
    end
  end
end

local function BoatTP(Boat, pos)
  if Boat then
    local Distance = (Boat.PrimaryPart.Position - pos.p).Magnitude
    game:GetService("TweenService"):Create(Boat.PrimaryPart,
    TweenInfo.new(Distance / getgenv().SeaBoatSpeed, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
    {CFrame = pos}):Play()
  end
end

local function KillAura()
  local function Kill(_,Enemie)
    local EnemieH = Enemie:FindFirstChild("Humanoid")
    
    if EnemieH and EnemieH.Health > 0 then
      local PlayerPP = Player.Character and Player.Character.PrimaryPart
      local EnemiePP = Enemie.PrimaryPart
      
      if PlayerPP and EnemiePP and (EnemiePP.Position - PlayerPP.Position).Magnitude < 1500 then
        EnemieH.Health = 0
        EnemiePP.Size = Vector3.new(75, 75, 75)
        EnemiePP.CanCollide = false
        sethiddenproperty(Player, "SimulationRadius", math.huge)
      end
    else
      local EnemieHead = Enemie:FindFirstChild("Head")
      
      if EnemieHead then
        EnemieHead:Destroy()
      end
    end
  end
  
  table.foreach(Enemies:GetChildren(), Kill)
  table.foreach(ReplicatedStorage:GetChildren(), Kill)
end

local function AutoKillAura()
  while getgenv().AutoKillAura do task.wait()
    KillAura()
  end
end

local function VerifyTableNPCs(npcs)
  if typeof(npcs) == "table" then
    for _,npc in pairs(Enemies:GetChildren()) do
      if table.find(npcs, npc.Name) then
        return true
      end
    end
  end
end

local function TweenNPCSpawn(pos, NPC)
  if pos then
    repeat task.wait()
      for _,v in pairs(pos) do
        if VerifyTableNPCs(NPC) or Enemies:FindFirstChild(NPC or Quest[3]) then
          break
        end
        if block then
          local tween = game:GetService("TweenService"):Create(block,
          TweenInfo.new((block.Position - v.p).Magnitude / getgenv().TweenSpeed, Enum.EasingStyle.Linear),
          {CFrame = v})tween:Play()tween.Completed:Wait()
        end
      end
    until not getgenv().AutoFarm_Level or Enemies:FindFirstChild(NPC or Quest[3])
    -- or getgenv().TimeToGift < 90
    return
  end
end

local function AddESP(Part, ESPColor)
  if Part and Part:FindFirstChild("ESP_REDzHUB") then
    return
  end
  
  local Folder = Instance.new("Folder", Part)
  Folder.Name = "ESP_REDzHUB"
  
  local BHA = Instance.new("BoxHandleAdornment", Folder)
  BHA.Size = Vector3.new(1, 0, 1, 0)
  BHA.Name = "ESP_REDzHUB"
  BHA.AlwaysOnTop = true
  BHA.ZIndex = 10
  BHA.Transparency = 0
  
  local BBG = Instance.new("BillboardGui", BHA)
  BBG.Adornee = Part
  BBG.Size = UDim2.new(0, 100, 0, 150)
  BBG.StudsOffset = Vector3.new(0, 1, 0)
  BBG.AlwaysOnTop = true
  
  local TL = Instance.new("TextLabel", BBG)
  TL.BackgroundTransparency = 1
  TL.Position = UDim2.new(0, 0, 0, -50)
  TL.Size = UDim2.new(0, 100, 0, 100)
  TL.TextSize = 10
  TL.TextColor3 = Color3.new(1, 1, 1)
  TL.TextStrokeTransparency = 0
  TL.TextYAlignment = Enum.TextYAlignment.Bottom
  TL.Text = "..."
  TL.ZIndex = 15
  TL.TextColor3 = ESPColor or Color3.fromRGB(255, 255, 0)
  
  task.spawn(function()
    while task.wait() do
      pcall(function()
        local plrRP = Player.Character:FindFirstChild("HumanoidRootPart")
        if plrRP and Part and Part.Name == "HumanoidRootPart" and Part.Parent:FindFirstChild("Humanoid") then
          local distance = math.floor((plrRP.Position - Part.Position).Magnitude / 3)
          local Health = math.floor(Part.Parent.Humanoid.Health)
          TL.Text = "Name : " .. Part.Parent.Name .. " | HP : " .. tostring(Health).. " | MAG : " .. tostring(distance)
        elseif plrRP and Part and Part.Name == "Handle" then
          local distance = math.floor((plrRP.Position - Part.Position).Magnitude / 3)
          TL.Text = Part.Parent.Name .. " <" .. tostring(distance) .. ">"
        elseif plrRP and Part then
          local distance = math.floor((plrRP.Position - Part.Position).Magnitude / 3)
          TL.Text = Part.Name .. " <" .. tostring(distance) .. ">"
        end
      end)
    end
  end)
end

local function RemoveESP(Part)
  if Part and Part:FindFirstChild("ESP_REDzHUB") then
    Part.ESP_REDzHUB:Destroy()
  end
end

local function EspPlayer()
  while getgenv().EspPlayer do task.wait()
    for _,player in pairs(game:GetService("Players"):GetPlayers()) do
      if player.Name ~= Player.Name and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        AddESP(player.Character.HumanoidRootPart, Color3.fromRGB(0, 255, 0))
      end
    end
  end
  for _,player in pairs(game:GetService("Players"):GetPlayers()) do
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
      RemoveESP(player.Character.HumanoidRootPart)
    end
  end
end

local function EspFlowers()
  while getgenv().EspFlowers do task.wait()
    for _,Flower in pairs(workspace:GetChildren()) do
      if Flower and Flower:IsA("BasePart") then
        if Flower.Name == "Flower1" then
          AddESP(Flower, Flower.Color)
        end
      end
    end
  end
  for _,Flower in pairs(workspace:GetChildren()) do
    if Flower and Flower:IsA("BasePart") then
      if Flower.Name == "Flower1" or Flower.Name == "Flower2" then
        RemoveESP(Flower)
      end
    end
  end
end

local function EspFruits()
  while getgenv().EspFruits do task.wait()
    for _,Fruit in pairs(workspace:GetChildren()) do
      if Fruit and Fruit:IsA("Tool") and Fruit:FindFirstChild("Handle") or
      Fruit and string.find(Fruit.Name, "Fruit") and Fruit:FindFirstChild("Handle") then
        AddESP(Fruit.Handle, Color3.fromRGB(255, 0, 0))
      end
    end
  end
  for _,Fruit in pairs(workspace:GetChildren()) do
    if Fruit and Fruit:FindFirstChild("Handle") then
      RemoveESP(Fruit.Handle)
    end
  end
end

local function EspIslands()
  while getgenv().EspIslands do task.wait()
    local Locations = workspace:WaitForChild("_WorldOrigin", 9e9):WaitForChild("Locations", 9e9)
    for _,Island in pairs(Locations:GetChildren()) do
      if Island then
        AddESP(Island, Color3.fromRGB(0, 255, 255))
      end
    end
  end
  local Locations = workspace:WaitForChild("_WorldOrigin", 9e9):WaitForChild("Locations", 9e9)
  for _,Island in pairs(Locations:GetChildren()) do
    if Island then
      RemoveESP(Island)
    end
  end
end

local function EspChests()
  while getgenv().EspChests do task.wait()
    for _,Chest in pairs(workspace:GetChildren()) do
      if Chest then
        if Chest.Name == "Chest3" then
          AddESP(Chest, Color3.fromRGB(0, 255, 255))
        elseif Ches
