local Library = loadstring(game:HttpGet("(link unavailable)"))()
local BazukaHub = Library:CreateWindow("Bazuka Hub")

local autoFarm = true
local farmMode = "Normal"
local customFruit = ""
local levelGoal = 2550

local player = game.Players.LocalPlayer
local character = player.Character
local humanoid = character.Humanoid
local experience = 0

local function farmExperience()
    for _, enemy in pairs(game.Workspace.Enemies:GetChildren()) do
        player.Character.HumanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame
        wait(0.5)
        player.Character:FindFirstChild("Humanoid").EquipTool(enemy)
        break
    end
end

local function levelUp()
    if player.Level.Value >= levelGoal then
        autoFarm = false
        BazukaHub:Notify("Parabéns!", "Você alcançou o level " .. levelGoal)
    end
end

while wait(1) do
    if autoFarm then
        farmExperience()
        experience = experience + 10
        player.Level.Value = player.Level.Value + 1
        levelUp()
    end
end

BazukaHub:AddButton("Iniciar Farm", function()
    autoFarm = true
end)

BazukaHub:AddButton("Parar Farm", function()
    autoFarm = false
end)

BazukaHub:AddDropdown("Modo Farm", {"Normal", "AFK", "Custom"}, function(selected)
    farmMode = selected
end)

BazukaHub:AddInput("Fruta Custom", function(input)
    customFruit = input
end)

BazukaHub:AddLabel("Level: " .. player.Level.Value)
BazukaHub:AddLabel("Experiência: " .. experience)
