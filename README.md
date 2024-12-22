--Start

local function dupeItem(itemPath, maxTeleports)
    if itemPath then
        local teleportCount = 0
        while teleportCount < maxTeleports do
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = itemPath.CFrame
            clickNormally(itemPath)
            teleportCount = teleportCount + 1
            wait(0.01) -- Tempo de espera para evitar travamento
        end
    end
end

local function lagarServer()
--Spam
    local ghostMeterPath = workspace:FindFirstChild("WorkspaceCom"):FindFirstChild("001_GiveTools"):FindFirstChild("ElectricGuitar")
    if ghostMeterPath then
        local teleportCount = 0
        local maxTeleports = 99999999999999999999999999

        while teleportCount < maxTeleports do
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = ghostMeterPath.CFrame
            clickNormally(ElectricGuitar)
            teleportCount = teleportCount + 1
            wait(0.1) -- Executa rapidamente
        end
    else
        warn("Item ElectricGuitar não encontrado.")
    end
end

--Test v1
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/Hads9/UiLibMod/main/Orion.lua')))()
OrionLib:MakeNotification({
	Name = "inf",
	Content = "Bem - Vindo Ao Salazar hub,Pode conter bugs e falhas!",
	Image = "rbxassetid://4483345998",
	Time = 10
})
local Window = OrionLib:MakeWindow({Name = "Salazar hub", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest",IntroEnabled = false})
local flingActive = false
local loopFlingActive = false
local selectedPlayer = nil
local bodyVelocity, bodyAngularVelocity

local function startFling()
    if flingActive or not selectedPlayer then return end
    flingActive = true

    local character = game.Players.LocalPlayer.Character
    local targetCharacter = selectedPlayer.Character
    if not character or not targetCharacter then return end
    local hrp = character:WaitForChild("HumanoidRootPart")
    local targetHrp = targetCharacter:WaitForChild("HumanoidRootPart")

    -- Change character size down
    local args = {
        [1] = "CharacterSizeDown",
        [2] = 5
    }
    game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
  
  -- Equipa o item 'Couch'
  local args = {
[1] = "PickingTools",
[2] = "Couch"
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
  
  -- Equipa o item 'Couch' no inventário se ainda não estiver equipado
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end
  
    bodyVelocity = Instance.new("BodyVelocity")
    bodyVelocity.Velocity = Vector3.new(100, 999, 100)
    bodyVelocity.MaxForce = Vector3.new(9999, 9999, 9999)
    bodyVelocity.Parent = hrp

    bodyAngularVelocity = Instance.new("BodyAngularVelocity")
    bodyAngularVelocity.AngularVelocity = Vector3.new(9999, 9999, 9999)
    bodyAngularVelocity.MaxTorque = Vector3.new(999999, 999999, 999999)
    bodyAngularVelocity.Parent = hrp

    game:GetService("RunService").Stepped:Connect(function()
        if flingActive then
            hrp.CFrame = targetHrp.CFrame
            hrp.CFrame = hrp.CFrame * CFrame.Angles(0, math.rad(10), 0)
        end
    end)
end

local function stopFling()
    if not flingActive then return end
    flingActive = false

    -- Change character size up
    local args = {
        [1] = "CharacterSizeUp",
        [2] = 1
    }
    game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

    if bodyVelocity then bodyVelocity:Destroy() end
    if bodyAngularVelocity then bodyAngularVelocity:Destroy() end
end

local function loopFling()
    while loopFlingActive do
        if selectedPlayer and selectedPlayer.Character then
            startFling()
            wait(0.1)
            stopFling()
        end
        wait(0.1)
    end
end

local function updatePlayerList()
local players = game.Players:GetPlayers()
local playerNames = {}
for _, player in ipairs(players) do
table.insert(playerNames, player.Name)
end
return playerNames
end

local Tab = Window:MakeTab({
Name = "Main",
Icon = "rbxassetid://4483345998",
PremiumOnly = false
})
local Section = Tab:AddSection({
	Name = "KILL TYPES"
})

local function couch()
local args = {
[1] = "PickingTools",
[2] = "Couch"
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
end

local function shoppingCart()
local args = {
[1] = "PickingTools",
[2] = "ShoppingCart"
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
end

local function stretcher()
local args = {
[1] = "PickingTools",
[2] = "Stretcher"
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
end

Tab:AddDropdown({
Name = "Kill Types",
Default = "",
Options = {"Couch", "Shopping Cart", "Stretcher"},
Callback = function(value)
if value == "Couch" then
couch()
elseif value == "Shopping Cart" then
shoppingCart()
elseif value == "Stretcher" then
stretcher()
end
end
})
local Section = Tab:AddSection({
	Name = "Damage Player"
})

local function WatherAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-72.37123107910156, -10.816083908081055, 112.93341827392578) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

-- Lista de Players para Bring Avançado
local killAdvancedPlayerList = {}
for _, player in ipairs(game.Players:GetPlayers()) do
table.insert(killAdvancedPlayerList, player.Name)
end

local function updatePlayerList()
local players = game.Players:GetPlayers()
local playerNames = {}
for _, player in ipairs(players) do
table.insert(playerNames, player.Name)
end
return playerNames
end

Tab:AddDropdown({
Name = "Selecionar Jogador",
Description = "Selecione o jogador alvo para o Bring Avançado",
Options = killAdvancedPlayerList,
Callback = function(playerName)
selectedKillAdvancedPlayer = playerName
end
})

Tab:AddButton({
Name = "Tornado Player",
Description = "Equipa o item 'Couch' e teleporta o jogador selecionado",
Callback = function()
WatherAdvancedPlayer()
end
})
local Section = Tab:AddSection({
	Name = "Kills"
})
local selectedKillAdvancedPlayer = nil
local couchEquipped = false

local function killAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-8.657157897949219, -222.3133087158203, -23.58349609375) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function FlyAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-107.91380310058594, -10.128937721252441, 261.37420654296875) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function SafeVoidAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(462.886474609375, -75.30844116210938, 123.47378540039062) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function BowAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-588.5294189453125, 8.251455307006836, -182.5675506591797) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function PlaneAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(665.856201171875, 3.6353466510772705, 89.86775970458984) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function LagAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(104.80880737304688, 34.60691833496094, 632.2498168945312) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function BringAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-570.4937133789062, 37.714874267578125, 963.8348999023438) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function SafeVoifAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(104.80880737304688, 34.60691833496094, 632.2498168945312) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function SkyAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(104.80880737304688, 34.60691833496094, 632.2498168945312) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function PriAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-783.1765747070312, -517.522216796875, 1115.422119140625) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function PrisionAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-783.1765747070312, -517.522216796875, 1115.422119140625) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

local function BugAdvancedPlayer()
if selectedKillAdvancedPlayer then
local player = game.Players:FindFirstChild(selectedKillAdvancedPlayer)
if player then
-- Equipa o item 'Couch' no inventário se ainda não estiver equipado
--big
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
local backpack = game.Players.LocalPlayer.Backpack
if backpack and not couchEquipped then
local couch = backpack:FindFirstChild("Couch")
if couch then
game.Players.LocalPlayer.Character.Humanoid:EquipTool(couch)
couchEquipped = true
else
print("O item 'Couch' não foi encontrado no seu inventário.")
end
end

-- Looping de teleportes no jogador selecionado da lista
while true do
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
wait(0.0) -- Intervalo entre cada teleporte, ajuste conforme necessário

-- Verifica se o jogador sentou no 'Couch' e realiza o teleporte para o céu
if player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.SeatPart then
player.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 0) -- Teleporta para cima novamente
wait(0.0) -- Espera um pouco antes de teleportar de volta para evitar bugs
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(176.63543701171875, 594.9183959960938, 393.3529052734375) -- Teleporta de volta para a posição original
break -- Sai do loop após teleportar de volta
end
end

--Small
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))

-- Remove o item 'Couch' da mão do jogador após o teleporte para o céu
if couchEquipped then
local backpack = game.Players.LocalPlayer.Backpack
if backpack then
local couch = backpack:FindFirstChild("Couch")
if couch then
couch.Parent = nil -- Remove o 'Couch' do inventário
couchEquipped = false
end
end
end
else
print("Jogador não encontrado.")
end
else
print("Nenhum jogador selecionado para o Bring Avançado.")
end
end

-- Lista de Players para Bring Avançado
local killAdvancedPlayerList = {}
for _, player in ipairs(game.Players:GetPlayers()) do
table.insert(killAdvancedPlayerList, player.Name)
end

local function updatePlayerList()
local players = game.Players:GetPlayers()
local playerNames = {}
for _, player in ipairs(players) do
table.insert(playerNames, player.Name)
end
return playerNames
end

Tab:AddDropdown({
Name = "Selecionar Jogador",
Description = "Selecione o jogador alvo para o Bring Avançado",
Options = killAdvancedPlayerList,
Callback = function(playerName)
selectedKillAdvancedPlayer = playerName
end
})

Tab:AddButton({
Name = "Kill",
Description = "Equipa o item 'Couch' e teleporta o jogador selecionado",
Callback = function()
killAdvancedPlayer()
end
})
Tab:AddButton({
Name = "Sky",
Description = "Equipa o item 'Couch' e teleporta o jogador selecionado",
Callback = function()
BugAdvancedPlayer()
end
})
Tab:AddButton({
Name = "Bow Prision [NEW]",
Description = "Equipa o item 'Couch' e teleporta o jogador selecionado",
Callback = function()
BowAdvancedPlayer()
end
})
Tab:AddButton({
Name = "Bug Kill",
Description = "Equipa o item 'Couch' e teleporta o jogador selecionado",
Callback = function()
SkyAdvancedPlayer()
end
})

Tab:AddButton({
Name = "Freeze kill",
Description = "Equipa o item 'Couch' e teleporta o jogador selecionado",
Callback = function()
LagAdvancedPlayer()
end
})

Tab:AddButton({
Name = "Kidnapping",
Description = "Equipa o item 'Couch' e teleporta o jogador selecionado",
Callback = function()
FlyAdvancedPlayer()
end
})
local Section = Tab:AddSection({
	Name = "Fling area"
})
local playerDropdown = Tab:AddDropdown({
Name = "Select Player",
Default = "",
Options = updatePlayerList(),
Callback = function(value)
selectedPlayer = game.Players:FindFirstChild(value)
end
})

Tab:AddButton({
Name = "Update Player List",
Callback = function()
playerDropdown:Refresh(updatePlayerList(), true)
end
})

Tab:AddButton({
Name = "Start Fling",
Callback = function()
startFling()
end
})

Tab:AddButton({
Name = "Stop Fling",
Callback = function()
stopFling()
end
})
local Section = Tab:AddSection({
    Name = "all"
})
Tab:AddButton({
	Name = "Fling all",
	Callback = function()
      	loadstring(game:HttpGet("https://pastebin.com/raw/zqyDSUWX"))()
  	end    
})
-- Variável para controlar o toggle
local teleportToggle = false

-- Função de teletransporte
local function teleportToPlayers()
    local localPlayer = game.Players.LocalPlayer
    local players = game.Players:GetPlayers()
    
    for _, player in pairs(players) do
        if not teleportToggle then break end -- Para se o toggle for desativado
        if player ~= localPlayer then
        --Ficar pequeno antes
        local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
            -- Teleporta para o jogador
            local character = player.Character
            if character and character:FindFirstChild("HumanoidRootPart") then
                local hrp = character.HumanoidRootPart
                localPlayer.Character.HumanoidRootPart.CFrame = hrp.CFrame
                wait(1) -- Aguarda 1 segundo para evitar problemas de sincronia
            end
        end
        -- Teleporta para (-8.657157897949219, -222.3133087158203, -23.58349609375)
        localPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-8.657157897949219, -222.3133087158203, -23.58349609375)
        wait(1) -- Aguarda antes de passar para o próximo jogador
    end
end

Tab:AddToggle({
    Name = "Kill All",
    Default = false,
    Callback = function(value)
        teleportToggle = value
        if teleportToggle then
            teleportToPlayers()
        end
    end
})

-- Variável para controlar o toggle
local teleportToggle = false

-- Função de teletransporte
local function teleportToSky()


--xaet

local args = {
[1] = "PickingTools",
[2] = "ShoppingCart"
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))

--xaetttttt

local args = {
[1] = "PickingTools",
[2] = "Stretcher"
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))

--Couch

local args = {
[1] = "PickingTools",
[2] = "Couch"
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))

--Equip itens

local function equiparItem(itemName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    
    if backpack then
        -- Verifica se o item já está no inventário
        local item = backpack:FindFirstChild(itemName)
        if item then
            -- Move o item para a mão do jogador, caso não esteja equipado
            local character = player.Character
            if character and not character:FindFirstChild(itemName) then
                item.Parent = character
                print(itemName .. " equipado!")
            else
                print(itemName .. " já está equipado.")
            end
        else
            print(itemName .. " não está no inventário.")
        end
    else
        print("Backpack não encontrado.")
    end
end

-- Checar e equipar Sniper e FireX
equiparItem("Couch")
equiparItem("ShoppingCart")
equiparItem("Stretcher")

    local localPlayer = game.Players.LocalPlayer
    local players = game.Players:GetPlayers()
    
    for _, player in pairs(players) do
        if not teleportToggle then break end -- Para se o toggle for desativado
        if player ~= localPlayer then
        --Ficar pequeno antes
        local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
            -- Teleporta para o jogador
            local character = player.Character
            if character and character:FindFirstChild("HumanoidRootPart") then
                local hrp = character.HumanoidRootPart
                localPlayer.Character.HumanoidRootPart.CFrame = hrp.CFrame
                wait(1) -- Aguarda 1 segundo para evitar problemas de sincronia
            end
        end
        -- Teleporta para (9999999827968, 9999999827968, 9999999827968)
        localPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(9999999827968, 9999999827968, 9999999827968)
        wait(1) -- Aguarda antes de passar para o próximo jogador
    end
end

Tab:AddToggle({
    Name = "Bug All",
    Default = false,
    Callback = function(value)
        teleportToggle = value
        if teleportToggle then
            teleportToSky()
        end
    end
})

-- Variáveis e serviços
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local TeleportToggle = false
local OriginalPosition

-- Função para teletransportar e voltar à posição original
local function TeleportToPlayers()
    while TeleportToggle do
        -- Salva a posição original do jogador
        if not OriginalPosition then
            OriginalPosition = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart").CFrame
        end
        
        for _, player in ipairs(Players:GetPlayers()) do
            -- Ignora o jogador local
            if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                -- Teleporta para o jogador
                LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
                wait(1) -- Espera 1 segundo antes de ir para o próximo jogador
                
                -- Retorna para a posição original
                if OriginalPosition then
                    LocalPlayer.Character.HumanoidRootPart.CFrame = OriginalPosition
                end
                wait(1) -- Espera 1 segundo antes de continuar
            end
        end
        
        -- Reseta a posição original se todos foram visitados
        OriginalPosition = nil
    end
end


Tab:AddToggle({
    Name = "Bring all",
    Default = false,
    Callback = function(Value)
        TeleportToggle = Value
        if TeleportToggle then
            TeleportToPlayers()
        end
    end
})
local Tab = Window:MakeTab({
Name = "Misc",
Icon = "rbxassetid://4483345998",
PremiumOnly = false
})

local Section = Tab:AddSection({
    Name = "Kick"
})

local Players = game:GetService("Players")
local playerNames = {}

local function updatePlayerList()
    playerNames = {}
    for _, player in pairs(Players:GetPlayers()) do
        table.insert(playerNames, player.Name)
    end
end

updatePlayerList()


local selectedPlayer = ""
local selectedReason = ""

Tab:AddDropdown({
    Name = "Select Player",
    Default = "",
    Options = playerNames,
    Callback = function(value)
        selectedPlayer = value
        print("Selected player: " .. value)
    end
})

Tab:AddButton({
    Name = "Update Player List",
    Callback = function()
        updatePlayerList()
        OrionLib:MakeNotification({
            Name = "Player List Updated",
            Content = "The player list has been updated.",
            Image = "rbxassetid://4483345998",
            Time = 5
        })
    end
})

Tab:AddDropdown({
    Name = "Select Reason",
    Default = "",
    Options = {"Web Namoro", "Exploits"},
    Callback = function(value)
        selectedReason = value
        print("Selected reason: " .. value)
    end
})

Tab:AddToggle({
    Name = "Loop Report",
    Default = false,
    Callback = function(value)
        while value do
            if selectedPlayer ~= "" and selectedReason ~= "" then
                print("Reporting " .. selectedPlayer .. " for " .. selectedReason)
                -- Aqui você pode adicionar o código para enviar a denúncia
            end
            wait(0.1)
        end
    end
})
local Section = Tab:AddSection({
    Name = "Notifications"
})
local Players = game:GetService("Players")
local notificationsEnabled = false

local function onPlayerAdded(player)
if notificationsEnabled then
game.StarterGui:SetCore("SendNotification", {
Title = "Player entered";
Text = player.Name .. " entrou no jogo";
Duration = 5;
})
end
end

local function onPlayerRemoving(player)
if notificationsEnabled then
game.StarterGui:SetCore("SendNotification", {
Title = "Player Left";
Text = player.Name .. " left the game";
Duration = 5;
})
end
end

local function toggleNotifications(toggleState)
notificationsEnabled = toggleState
if notificationsEnabled then
print("Notificações Ativadas")
else
print("Notificações Desativadas")
end
end

Tab:AddToggle({
Name = "Notify when player leaves/joins",
Default = false,
Callback = function(Value)
toggleNotifications(Value)
end
})

Players.PlayerAdded:Connect(onPlayerAdded)
Players.PlayerRemoving:Connect(onPlayerRemoving)

local Section = Tab:AddSection({
    Name = "Anti Functions"
})

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")
local TeleportService = game:GetService("TeleportService")

local function disableLaggyFeatures()
for _, v in pairs(workspace:GetDescendants()) do
if v:IsA("ParticleEmitter") or v:IsA("Trail") or v:IsA("Smoke") or v:IsA("Fire") then
v.Enabled = false
end
end
end

Tab:AddToggle({
Name = "Anti Sit",
Default = false,
Callback = function(value)
if value then
RunService.Stepped:Connect(function()
if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
if LocalPlayer.Character.Humanoid.Sit then
LocalPlayer.Character.Humanoid.Sit = false
end
end
end)
end
end
})

Tab:AddToggle({
Name = "Anti Void",
Default = false,
Callback = function(value)
if value then
RunService.Stepped:Connect(function()
if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
if LocalPlayer.Character.HumanoidRootPart.Position.Y < -50 then
LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-118.54170227050781, 3.8526408672332764, -1.622152805328369)
end
end
end)
end
end
})

Tab:AddToggle({
Name = "Anti Kick",
Default = false,
Callback = function(value)
if value then
game:GetService("CoreGui").RobloxPromptGui.promptOverlay.ChildAdded:Connect(function(child)
if child.Name == "ErrorPrompt" then
TeleportService:Teleport(game.PlaceId, LocalPlayer)
end
end)
end
end
})

Tab:AddToggle({
Name = "Anti Lag",
Default = false,
Callback = function(value)
if value then
disableLaggyFeatures()
workspace.DescendantAdded:Connect(function(descendant)
if descendant:IsA("ParticleEmitter") or descendant:IsA("Trail") or descendant:IsA("Smoke") or descendant:IsA("Fire") then
descendant.Enabled = false
end
end)
end
end
})
local Section = Tab:AddSection({
    Name = "Others Functions"
})

local function backToSize()
local args = {
[1] = "CharacterSizeUp",
[2] = 1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args)) 
end

local function small()
local args = {
[1] = "CharacterSizeDown",
[2] = 5
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
end

Tab:AddDropdown({
Name = "Select Function - Stay small",
Default = "None",
Options = {"Back to size", "Small"},
Callback = function(option)
if option == "Back to size" then
backToSize()
elseif option == "Small" then
small()
end
end
})

local function danger()
local args = {
    [1] = "RolePlayName",
    [2] = "D\205\156\205\137\205\150\204\175A\204\162\204\169\204\150N\205\156\205\153\204\174\204\166\204\173G\204\167\204\150\205\154\205\150\205\149\204\175E\204\167\204\170\205\141\204\153\204\179R\205\162\205\149\204\150\204\171"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eTex1t"):FireServer(unpack(args))
end

local function hacker()
local args = {
    [1] = "RolePlayName",
    [2] = "H\204\167\204\159\205\150\205\149\204\172\205\148A\204\161\204\172\205\153\205\133\204\174\205\153C\204\168\205\141\204\164\204\150K\204\168\204\174\204\169\204\170E\204\168\204\179\204\169\204\164R\204\161\205\149\205\147\204\163"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eTex1t"):FireServer(unpack(args))
end

local function invasion()
local args = {
    [1] = "RolePlayName",
    [2] = "I\205\157\204\132\204\128\204\131\204\143n\204\155\205\155\204\132\204\142\204\137v\205\158\204\139\204\137\204\190\205\132a\204\155\204\132\205\131s\205\158\205\140\204\154\204\139\204\133i\204\155\204\130\204\136\204\138\204\136\204\129o\205\161\204\129\204\136n\205\160\205\128\204\129\205\129\204\146\205\132"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eTex1t"):FireServer(unpack(args))
end

Tab:AddDropdown({
Name = "Select Name - Zalgo",
Default = "None",
Options = {"Danger", "Hacker", "Invasion"},
Callback = function(option)
if option == "Danger" then
danger()
elseif option == "Hacker" then
hacker()
elseif option == "Invasion" then
invasion()
end
end
})
local Section = Tab:AddSection({
	Name = "Pull player information"
})
local selectedPlayer = nil

local function getPlayerId(player)
    return player.UserId
end

local function getJoinDate(player)
    return player.AccountAge
end

local function copyName(player)
    setclipboard(player.Name)
end

local function createESP(player)
    local esp = Instance.new("Highlight")
    esp.Parent = player.Character
    esp.Adornee = player.Character
    esp.FillColor = Color3.new(1, 0, 0)
    esp.FillTransparency = 0.5
    esp.OutlineColor = Color3.new(1, 1, 1)
    esp.OutlineTransparency = 0
end

local function updateDropdown()
    local players = game:GetService("Players"):GetPlayers()
    local playerNames = {}
    for _, player in ipairs(players) do
        table.insert(playerNames, player.Name)
    end
    return playerNames
end

Tab:AddDropdown({
    Name = "Players",
    Default = "",
    Options = updateDropdown(),
    Callback = function(value)
        selectedPlayer = game:GetService("Players"):FindFirstChild(value)
    end
})

Tab:AddButton({
    Name = "Player id",
    Callback = function()
        if selectedPlayer then
            OrionLib:MakeNotification({
                Name = "Player ID",
                Content = "ID: " .. getPlayerId(selectedPlayer),
                Image = "rbxassetid://4483345998",
                Time = 5
            })
        end
    end
})

Tab:AddButton({
    Name = "JoinDate (see when the player entered the game)",
    Callback = function()
        if selectedPlayer then
            OrionLib:MakeNotification({
                Name = "Join Date",
                Content = "Account Age: " .. getJoinDate(selectedPlayer) .. " days",
                Image = "rbxassetid://4483345998",
                Time = 5
            })
        end
    end
})

Tab:AddButton({
    Name = "Copyname",
    Callback = function()
        if selectedPlayer then
            copyName(selectedPlayer)
            OrionLib:MakeNotification({
                Name = "Copy Name",
                Content = "Name copied to clipboard",
                Image = "rbxassetid://4483345998",
                Time = 5
            })
        end
    end
})
local Section = Tab:AddSection({
    Name = "Horror Song (GamePass - Only Skateboards, Overboards between others...)"
})

local songs = {
["Song 1"] = "933230732",
["Song 2"] = "300533476",
["Song 3"] = "472763153",
["Song 4"] = "300533288",
["Song 5"] = "1840020395",
["Song 6"] = "1840020758",
["Song 7"] = "567545087",
["Song 8"] = "5546573724",
["Song 9"] = "8584754036",
["Song 10"] = "8604878451",
}

local selectedSong = "Song 1"

local function executeSong(songId)
local args = {
[1] = "PickingScooterMusicText",
[2] = songId
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1NoMoto1rVehicle1s"):FireServer(unpack(args))
end

Tab:AddDropdown({
Name = "Select Horror Song",
Default = "Song 1",
Options = {"Song 1", "Song 2", "Song 3", "Song 4", "Song 5", "Song 6", "Song 7", "Song 8", "Song 9", "Song 10"},
Callback = function(value)
selectedSong = value
end
})


Tab:AddButton({
Name = "Execute Song",
Callback = function()
executeSong(songs[selectedSong])
end
})

local songs = {
["Song 1"] = "16662829817",
["Song 2"] = "14145618923",
["Song 3"] = "6841685130",
["Song 4"] = "13530439502",
["Song 5"] = "6676732301",
["Song 6"] = "15689448519"
}

local selectedSong = "Song 1"

local function executeSong(songId)
local args = {
[1] = "PickingScooterMusicText",
[2] = songId
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1NoMoto1rVehicle1s"):FireServer(unpack(args))
end

Tab:AddDropdown({
Name = "Select Phonk Song",
Default = "Song 1",
Options = {"Song 1", "Song 2", "Song 3", "Song 4", "Song 5", "Song 6"},
Callback = function(value)
selectedSong = value
end
})

Tab:AddButton({
Name = "Execute Song",
Callback = function()
executeSong(songs[selectedSong])
end
})
local Section = Tab:AddSection({
    Name = "Fire Function"
})
Tab:AddButton({
Name = "Hand Fire",
Callback = function()
OrionLib:MakeNotification({
	Name = "You only have 6 seconds!",
	Content = "Click the button under the table to get the fire hand!",
	Image = "rbxassetid://4483345998",
	Time = 6
})
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-350.8634338378906, 3.6591341495513916, 100.41527557373047)
wait(6)
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-24.741954803466797, 3.0249993801116943, -66.39078521728516)
    end
})
local Tab = Window:MakeTab({
Name = "House",
Icon = "rbxassetid://4483345998",
PremiumOnly = false
})

-- Variáveis globais
local Enabled = false
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- Função para alternar noclip
local function toggleNoclip()
    noclipEnabled = not noclipEnabled

    if noclipEnabled then
        OrionLib:MakeNotification({
            Name = "UnBan Enabled",
            Content = "Você agora pode atravessar objetos.",
            Image = "rbxassetid://4483345998", -- Ícone opcional
            Time = 5
        })
    else
        OrionLib:MakeNotification({
            Name = "UnBan Disable",
            Content = "Modo normal ativado.",
            Image = "rbxassetid://4483345998", -- Ícone opcional
            Time = 5
        })
    end
end

-- Função para manipular colisões
local function noclipLoop()
    while wait() do
        if noclipEnabled then
            for _, part in pairs(character:GetDescendants()) do
                if part:IsA("BasePart") and part.CanCollide then
                    part.CanCollide = false
                end
            end
        else
            for _, part in pairs(character:GetDescendants()) do
                if part:IsA("BasePart") and not part.CanCollide then
                    part.CanCollide = true
                end
            end
        end
    end
end


Tab:AddButton({
    Name = "Ativar/Desativar UnBan",
    Callback = toggleNoclip
})

-- Inicia o loop de noclip em uma thread separada
spawn(noclipLoop)

local Section = Tab:AddSection({
    Name = "Ban tool"
})

-- Lista de Jogadores
local selectedPlayer = nil
local playerNames = {}

-- Atualizar lista de jogadores
local function updatePlayerList()
    playerNames = {}
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= Players.LocalPlayer then
            table.insert(playerNames, player.Name)
        end
    end
end

-- Banir jogador
local function banPlayer(playerName)
    local targetPlayer = Players:FindFirstChild(playerName)
    if targetPlayer and targetPlayer.Character then
        local args = {
            [1] = "BanPlayerFromHouse",
            [2] = targetPlayer,
            [3] = targetPlayer.Character
        }
        local remoteEvent = ReplicatedStorage.RE:FindFirstChild("1Playe1rTrigge1rEven1t")
        if remoteEvent then
            remoteEvent:FireServer(unpack(args))
        end
    end
end

local function updatePlayerList()
local players = game.Players:GetPlayers()
local playerNames = {}
for _, player in ipairs(players) do
table.insert(playerNames, player.Name)
end
return playerNames
end

Tab:AddDropdown({
    Name = "Selecione um Jogador",
    Options = playerNames,
    Callback = function(value)
        selectedKillAdvancedPlayer = playerName
    end
})

Tab:AddButton({
    Name = "Atualizar Lista de Jogadores",
    Callback = function()
        updatePlayerList()
        OrionLib:MakeNotification({
            Name = "Atualizado",
            Content = "Lista de jogadores foi atualizada.",
            Image = "rbxassetid://4483345998",
            Time = 5
        })
    end
})

Tab:AddToggle({
    Name = "Ativar Loop de Ban",
    Default = false,
    Callback = function(value)
        if value and selectedPlayer then
            while value do
                banPlayer(selectedPlayer)
                task.wait(1) -- Delay para evitar spam excessivo
            end
        end
    end
})
local Section = Tab:AddSection({
    Name = "Loops "
})
local toggleState = false
local function toggleCurtains()
while toggleState do
local args = {
[1] = "Curtains"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sHous1e"):FireServer(unpack(args))
wait(1) -- ajusta o tempo de espera conforme necessário
end
end

Tab:AddToggle({
Name = "Toggle Curtains",
Default = false,
Callback = function(value)
toggleState = value
if toggleState then
toggleCurtains()
end
end
})

local toggleState = false
local function togglePool()
while toggleState do
local args = {
[1] = "PoolOnOff"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sHous1e"):FireServer(unpack(args))
wait(1) -- ajusta o tempo de espera conforme necessário
end
end

Tab:AddToggle({
Name = "Toggle Pool",
Default = false,
Callback = function(value)
toggleState = value
if toggleState then
togglePool()
end
end
})

local toggleState = false
local function toggleGarageDoor()
while toggleState do
local args = {
[1] = "GarageDoor"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sHous1e"):FireServer(unpack(args))
wait(1) -- ajusta o tempo de espera conforme necessário
end
end

Tab:AddToggle({
Name = "Toggle Garage Door",
Default = false,
Callback = function(value)
toggleState = value
if toggleState then
toggleGarageDoor()
end
end
})
local Section = Tab:AddSection({
    Name = "Fire Function"
})
Tab:AddButton({
	Name = "Fire On",
	Callback = function()
      	local args = {
    [1] = "PlayerWantsFireOnFirePassNotShowingAnyone"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sHous1e"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Fire Off",
	Callback = function()
      	local args = {
    [1] = "PlayerWantsFireOffFirePassNotShowingAnyone"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sHous1e"):FireServer(unpack(args))
  	end    
})

local toggleActive = false
local function repeatRemote()
while toggleActive do
local args = {
[1] = "PlayerWantsFireOnFirePassNotShowingAnyone"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sHous1e"):FireServer(unpack(args))
wait(0.1) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop Fire ",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
repeatRemote()
end
end
})

local toggleActive = false
local function repeatRemote()
while toggleActive do
--This is a simple roblox game crasher made by casanova
--Github cfreemepq
--fixed script*

while wait(0.6) do --// don't change it's the best
game:GetService("NetworkClient"):SetOutgoingKBPSLimit(math.huge)
local function getmaxvalue(val)
   local mainvalueifonetable = 499999
   if type(val) ~= "number" then
       return nil
   end
   local calculateperfectval = (mainvalueifonetable/(val+2))
   return calculateperfectval
end

local function bomb(tableincrease, tries)
local maintable = {}
local spammedtable = {}

table.insert(spammedtable, {})
z = spammedtable[1]

for i = 1, tableincrease do
    local tableins = {}
    table.insert(z, tableins)
    z = tableins
end

local calculatemax = getmaxvalue(tableincrease)
local maximum

if calculatemax then
     maximum = calculatemax
     else
     maximum = 999999
end

for i = 1, maximum do
     table.insert(maintable, spammedtable)
end

for i = 1, tries do
     game.RobloxReplicatedStorage.SetPlayerBlockList:FireServer(maintable)
end
end

bomb(250, 2) --// change values if client crashes.
end
wait(0.0) -- intervalo de 1 segundo entre cada repetição
end
end
local Section = Tab:AddSection({
	Name = "Doors"
})
Tab:AddButton({
Name = "DESTROY DOORS",
Callback = function()
local UserInputService = game:GetService("UserInputService")
local Mouse = game:GetService("Players").LocalPlayer:GetMouse()
local Folder = Instance.new("Folder", game:GetService("Workspace"))
local Part = Instance.new("Part", Folder)
local Attachment1 = Instance.new("Attachment", Part)
Part.Anchored = true
Part.CanCollide = false
Part.Transparency = 1
local Updated = Mouse.Hit + Vector3.new(0, 5, 0)
local NetworkAccess = coroutine.create(function()
    settings().Physics.AllowSleep = false
    while game:GetService("RunService").RenderStepped:Wait() do
        for _, Players in next, game:GetService("Players"):GetPlayers() do
            if Players ~= game:GetService("Players").LocalPlayer then
                Players.MaximumSimulationRadius = 0 
                sethiddenproperty(Players, "SimulationRadius", 0) 
            end 
        end
        game:GetService("Players").LocalPlayer.MaximumSimulationRadius = math.pow(math.huge,math.huge)
        setsimulationradius(math.huge) 
    end 
end) 
coroutine.resume(NetworkAccess)
local function ForcePart(v)
    if v:IsA("Part") and v.Anchored == false and v.Parent:FindFirstChild("Humanoid") == nil and v.Parent:FindFirstChild("Head") == nil and v.Name ~= "Handle" then
        Mouse.TargetFilter = v
        for _, x in next, v:GetChildren() do
            if x:IsA("BodyAngularVelocity") or x:IsA("BodyForce") or x:IsA("BodyGyro") or x:IsA("BodyPosition") or x:IsA("BodyThrust") or x:IsA("BodyVelocity") or x:IsA("RocketPropulsion") then
                x:Destroy()
            end
        end
        if v:FindFirstChild("Attachment") then
            v:FindFirstChild("Attachment"):Destroy()
        end
        if v:FindFirstChild("AlignPosition") then
            v:FindFirstChild("AlignPosition"):Destroy()
        end
        if v:FindFirstChild("Torque") then
            v:FindFirstChild("Torque"):Destroy()
        end
        v.CanCollide = false
        local Torque = Instance.new("Torque", v)
        Torque.Torque = Vector3.new(999999, 999999, 999999)
        local AlignPosition = Instance.new("AlignPosition", v)
        local Attachment2 = Instance.new("Attachment", v)
        Torque.Attachment0 = Attachment2
        AlignPosition.MaxForce = 99999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999
        AlignPosition.MaxVelocity = math.huge
        AlignPosition.Responsiveness = 200
        AlignPosition.Attachment0 = Attachment2 
        AlignPosition.Attachment1 = Attachment1
    end
end
for _, v in next, game:GetService("Workspace"):GetDescendants() do
    ForcePart(v)
end
game:GetService("Workspace").DescendantAdded:Connect(function(v)
    ForcePart(v)
end)
UserInputService.InputBegan:Connect(function(Key, Chat)
    if Key.KeyCode == Enum.KeyCode.E and not Chat then
       Updated = Mouse.Hit + Vector3.new(0, 5, 0)
    end
end)
spawn(function()
    while game:GetService("RunService").RenderStepped:Wait() do
        Attachment1.WorldCFrame = Updated
    end
end)
end
})
Tab:AddParagraph("How to use","You need to have permission from the person's house and get close to the house.The function will not work if the house is locked, but if you have permission you can unlock it, this function works like the Ice Hub's fling Doors")
Tab:AddParagraph("Como usar","Você precisa ter permissão da casa da pessoa e chegar perto da casa. A função não funcionará se a casa estiver trancada, mas se você tiver permissão, poderá desbloqueá-la.esta função funciona como as portas de lançamento do Ice Hub")
local Section = Tab:AddSection({
	Name = "Get Permission Houses"
})
Tab:AddButton({
	Name = "House 1",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 1
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 2",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 2
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 3",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 3
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 4",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 4
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 5",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 5
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 6",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 6
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 7",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 7
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 8",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 8
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 9",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 9
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 10",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 10
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 11",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 11
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 12",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 12
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 13",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 13
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 14",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 14
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 15",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 15
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 16",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 16
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 17",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 17
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 18",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 18
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 19",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 19
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 20",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 20
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 21",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 21
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 22",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 22
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 23",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 23
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
Tab:AddButton({
	Name = "House 24",
	Callback = function()
      	local args = {
    [1] = "GivePermissionLoopToServer",
    [2] = game:GetService("Players").LocalPlayer,
    [3] = 24
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))	
  	end    
})
local Tab = Window:MakeTab({
Name = "Avatar",
Icon = "rbxassetid://4483345998",
PremiumOnly = false
})

-- Variables
local name1 = ""
local name2 = ""
local name3 = ""
local repeatNames = false

-- Textbox for Name 1
Tab:AddTextbox({
Name = "Name 1",
Default = "",
TextDisappear = true,
Callback = function(value)
name1 = value
end
})

-- Textbox for Name 2
Tab:AddTextbox({
Name = "Name 2",
Default = "",
TextDisappear = true,
Callback = function(value)
name2 = value
end
})

-- Textbox for Name 3
Tab:AddTextbox({
Name = "Name 3",
Default = "",
TextDisappear = true,
Callback = function(value)
name3 = value
end
})

-- Toggle for Repeating Names
Tab:AddToggle({
Name = "Repeat Names",
Default = false,
Callback = function(value)
repeatNames = value
while repeatNames do
local args1 = {
[1] = "RolePlayName",
[2] = name1
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eTex1t"):FireServer(unpack(args1))

local args2 = {
[1] = "RolePlayName",
[2] = name2
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eTex1t"):FireServer(unpack(args2))

wait(1) -- Adjust the wait time as needed


local args3 = {
[1] = "RolePlayName",
[2] = name3
}
game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eTex1t"):FireServer(unpack(args3))
end
end
})
local Section = Tab:AddSection({
    Name = "Limiteds"
})
local valks = {
["Valk timeless"] = 17517206952,
["Valk esmerald"] = 2830437685,
["Valk Shine Time"] = 1180433861
}

Tab:AddDropdown({
Name = "Select Valks",
Default = "",
Options = {"Valk timeless", "Valk esmerald", "Valk Shine Time"},
Callback = function(selected)
local args = {
[1] = "wear",
[2] = valks[selected]
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})

local dominus = {
["Dominus Frigidus"] = 48545806,
["Dominus Empyreus"] = 64444871,
["Dominus Astra"] = 162067148,
["Dominus Infernus"] = 31101391
}

Tab:AddDropdown({
Name = "Select Dominus",
Default = "",
Options = {"Dominus Frigidus", "Dominus Empyreus", "Dominus Astra", "Dominus Infernus"},
Callback = function(selected)
local args = {
[1] = "wear",
[2] = dominus[selected]
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
local Section = Tab:AddSection({
    Name = "Characters"
})
local characters = {
["Chef Tordet"] = {
[1] = 3657481497,
[2] = 3657478273,
[3] = 3657474549,
[4] = 3657479706,
[5] = 3745126840,
[6] = 1
},
["Chicken"] = {
[1] = 128157408,
[2] = 128157262,
[3] = 128157213,
[4] = 128157361,
[5] = 128157317,
[6] = 1
},
["Gang potato"] = {
[1] = 5392155773,
[2] = 5392150804,
[3] = 5392146467,
[4] = 5392152751,
[5] = 5392148570,
[6] = 1
},
["The overser"] = {
[1] = 81725326,
[2] = 81725366,
[3] = 81725392,
[4] = 1,
[5] = 1,
[6] = 1
},
["All korblox"] = {
[1] = 139607770,
[2] = 139607625,
[3] = 139607570,
[4] = 139607718,
[5] = 139607673,
[6] = 1
}
}

Tab:AddDropdown({
Name = "Characters",
Default = "",
Options = {"Chef Tordet", "Chicken", "Gang potato", "The overser", "All korblox"},
Callback = function(selected)
local args = {
[1] = "CharacterChange",
[2] = characters[selected],
[3] = "by:REDz"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l"):FireServer(unpack(args))
end
})


local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local function copyAvatar(targetPlayer)
if targetPlayer and targetPlayer.Character and LocalPlayer.Character then
for _, v in pairs(LocalPlayer.Character:GetChildren()) do
if v:IsA("Accessory") or v:IsA("Clothing") or v:IsA("BodyColors") or v:IsA("CharacterMesh") or v:IsA("ShirtGraphic") then
v:Destroy()
end
end

for _, v in pairs(targetPlayer.Character:GetChildren()) do
if v:IsA("Accessory") or v:IsA("Clothing") or v:IsA("BodyColors") or v:IsA("CharacterMesh") or v:IsA("ShirtGraphic") then
v:Clone().Parent = LocalPlayer.Character
end
end

LocalPlayer.Character.Humanoid:ApplyDescription(targetPlayer.Character.Humanoid:GetAppliedDescription())
end
end

Tab:AddTextbox({
Name = "Player Name {Copy Avatar}",
Default = "",
TextDisappear = true,
Callback = function(value)
local targetPlayer = Players:FindFirstChild(value)
if targetPlayer then
copyAvatar(targetPlayer)
else
print("Player not found")
end
end
})
local Section = Tab:AddSection({
    Name = "Bold animatiom"
})
Tab:AddButton({
	Name = "Idle",
	Callback = function()
      		local args = {
    [1] = "wearWalkStyle",
    [2] = 16744209868
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "Run",
	Callback = function()
      		local args = {
    [1] = "wearWalkStyle",
    [2] = 16744214662
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "Walk",
	Callback = function()
      		local args = {
    [1] = "wearWalkStyle",
    [2] = 16744219182
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "Jump",
	Callback = function()
      		local args = {
    [1] = "wearWalkStyle",
    [2] = 16744212581
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "Fall",
	Callback = function()
      		local args = {
    [1] = "wearWalkStyle",
    [2] = 16744207822
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "Climb",
	Callback = function()
      		local args = {
    [1] = "wearWalkStyle",
    [2] = 16744204409
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "swim", 
	Callback = function()
      		local args = {
    [1] = "wearWalkStyle",
    [2] = 16744217055
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
local Section = Tab:AddSection({
    Name = "Head"
})
Tab:AddButton({
	Name = "Headless",
	Callback = function()
      		local args = {
    [1] = "CharacterChange",
    [2] = {
        [1] = 1,
        [2] = 1,
        [3] = 1,
        [4] = 1,
        [5] = 1,
        [6] = 134082579
    },
    [3] = "by:REDz"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Cheek",
	Callback = function()
      		local args = {
    [1] = "CharacterChange",
    [2] = {
        [1] = 1,
        [2] = 1,
        [3] = 1,
        [4] = 1,
        [5] = 1,
        [6] = 746767604
    },
    [3] = "by:REDz"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l"):FireServer(unpack(args))
  	end    
})
local Section = Tab:AddSection({
    Name = "Horror Skin"
})
Tab:AddButton({
	Name = "Michael Myers",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 15133320948
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Mario Victim 1",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 14732524763
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Scary",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 15036977826
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Scary dog",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 14761007249
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Jeff The Killer",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 14502327402
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
  	end    
})
local Section = Tab:AddSection({
    Name = "Korblox Legs "
})
Tab:AddButton({
	Name = "Right",
	Callback = function()
      		local args = {
    [1] = "CharacterChange",
    [2] = {
        [1] = 1,
        [2] = 1,
        [3] = 1,
        [4] = 139607718,
        [5] = 1,
        [6] = 1
    },
    [3] = "by:REDz"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Left ",
	Callback = function()
      		local args = {
    [1] = "CharacterChange",
    [2] = {
        [1] = 1,
        [2] = 1,
        [3] = 1,
        [4] = 1,
        [5] = 139607673,
        [6] = 1
    },
    [3] = "by:REDz"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l"):FireServer(unpack(args))
  	end    
})
local Section = Tab:AddSection({
    Name = "Ice legs "
})
Tab:AddButton({
	Name = "Right",
	Callback = function()
      		local args = {
    [1] = "CharacterChange",
    [2] = {
        [1] = 1,
        [2] = 1,
        [3] = 1,
        [4] = 139572888,
        [5] = 1,
        [6] = 1
    },
    [3] = "by:REDz"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Left ",
	Callback = function()
      		local args = {
    [1] = "CharacterChange",
    [2] = {
        [1] = 1,
        [2] = 1,
        [3] = 1,
        [4] = 1,
        [5] = 139572789,
        [6] = 1
    },
    [3] = "by:REDz"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l"):FireServer(unpack(args))
  	end    
})
local Section = Tab:AddSection({
    Name = "Adidas Sport animation"
})
Tab:AddButton({
	Name = "Idle",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 18538150608
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "Run",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 18538133604
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "Walk",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 18538146480
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "jump",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 18538153691
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "Fall",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 18538153691
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
Tab:AddButton({
	Name = "Climb",
	Callback = function()
      		local args = {
    [1] = "wear",
    [2] = 18538170170
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
end
})
local Section = Tab:AddSection({
    Name = "Zombie "
})
Tab:AddButton({
	Name = "zombie leg",
	Callback = function()
      		local args = {
    [1] = "CharacterChange",
    [2] = {
        [1] = 1,
        [2] = 1,
        [3] = 1,
        [4] = 37754710,
        [5] = 1,
        [6] = 1
    },
    [3] = "by:REDz"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Avata1rOrigina1l"):FireServer(unpack(args))
  	end    
})
local Tab = Window:MakeTab({
Name = "Car",
Icon = "rbxassetid://4483345998",
PremiumOnly = false
})
local Section = Tab:AddSection({
    Name = "Velocity"
})

-- Variables
local CarSpeed = 200

-- Textbox for Car Speed
Tab:AddTextbox({
Name = "Car Speed",
Default = "",
TextDisappear = true,
Callback = function(value)
CarSpeed = tonumber(value)
end
})

-- Button to Update Car Speed
Tab:AddButton({
Name = "Update Speed",
Callback = function()
local args = {
[1] = "PlayerGiveSpeedLower",
[2] = CarSpeed
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sCa1r"):FireServer(unpack(args))
end
})
local Section = Tab:AddSection({
    Name = "Loop"
})

local toggleActive = false
local function loopDuke()
while toggleActive do
local args = {
    [1] = "Duke"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sCa1r"):FireServer(unpack(args))
wait(1.0) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop Duke",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopDuke()
end
end
})

local toggleActive = false
local function loopFlip()
while toggleActive do
local args = {
    [1] = "Flip"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sCa1r"):FireServer(unpack(args))
wait(1.0) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop Flip",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopFlip()
end
end
})

local toggleActive = false
local function loopSmoke()
while toggleActive do
local args = {
    [1] = "Smoke"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sCa1r"):FireServer(unpack(args))
wait(1.0) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop Smoke",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopSmoke()
end
end
})

local toggleActive = false
local function loopFire()
while toggleActive do
local args = {
    [1] = "Fire"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sCa1r"):FireServer(unpack(args))
wait(1.0) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop Fire",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopFire()
end
end
})
local Section = Tab:AddSection({
    Name = "Delete Vehicle"
})
Tab:AddButton({
	Name = "Delete Vehicle",
	Callback = function()
      	local args = {
    [1] = "DeleteAllVehicles"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Ca1r"):FireServer(unpack(args))	
  	end    
})
local Section = Tab:AddSection({
    Name = "Horse"
})
Tab:AddButton({
	Name = "Spawn Horse",
	Callback = function()
      	local args = {
    [1] = "PickingCar",
    [2] = "Horse"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Ca1r"):FireServer(unpack(args))
  	end    
})

local toggleActive = false
local function loopFire()
while toggleActive do
local args = {
    [1] = "BrownHorseFree"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Hors1eRemot1e"):FireServer(unpack(args))
wait(1.0)
local args = {
    [1] = "BlackHorseFree"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Hors1eRemot1e"):FireServer(unpack(args))
wait(1.0) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop color horse",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopFire()
end
end
})
local Section = Tab:AddSection({
    Name = "Jumpscare Car - GamePass"
})
Tab:AddButton({
	Name = "Screaming Woman",
	Callback = function()
      	 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-24.741954803466797, 3.0249993801116943, -66.39078521728516)
wait(0.1)
local args = {
    [1] = "PickingCar",
    [2] = "SchoolBus"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Ca1r"):FireServer(unpack(args))
wait(1)
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-35.15000534057617, 5.7094035148620605, -74.16535949707031)
wait(0.1)
local args = {
    [1] = "PickingCarMusicText",
    [2] = "892233254"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Player1sCa1r"):FireServer(unpack(args))
  	end    
})
local Section = Tab:AddSection({
    Name = "Truck"
})
Tab:AddButton({
	Name = "Spawn Truck",
	Callback = function()
      	local args = {
    [1] = "PickingCar",
    [2] = "Semi"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Ca1r"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Name Scripter - zalgo",
	Callback = function()
      	local args = {
    [1] = "ReturningSemiName",
    [2] = "S\205\138\204\144\205\129c\205\155\205\155\204\190r\205\139\205\132\204\191i\205\128\205\144\205\145p\205\138\204\144\205\152t\205\140\204\154\205\145e\205\140\204\149r\204\148\204\148\205\145"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Cemeter1y"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Name Admin - zalgo",
	Callback = function()
      	local args = {
    [1] = "ReturningSemiName",
    [2] = "A\205\139\204\189\205\131\204\183d\205\129\205\139\204\189\204\183m\204\191\204\147\205\132\204\183i\204\190\205\131\204\189\204\183n\204\189\204\144\204\154\204\183"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Cemeter1y"):FireServer(unpack(args))
  	end    
})
Tab:AddButton({
	Name = "Name Troll - zalgo",
	Callback = function()
      	local args = {
    [1] = "ReturningSemiName",
    [2] = "T\205\134\204\144\205\132 R\205\157\205\132\204\154 O\204\149\205\160 L\205\145\205\140\205\132 L\204\190\205\132\204\190"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Cemeter1y"):FireServer(unpack(args))
  	end    
})
local Tab = Window:MakeTab({
Name = "Tools",
Icon = "rbxassetid://4483345998",
PremiumOnly = false
})
local Section = Tab:AddSection({
    Name = "Guitar"
})
Tab:AddButton({
Name = "Guitar Eletric mixed with acoustic guitar",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-384.57574462890625, 18.507526397705078, 212.38763427734375)
wait(0.1)
local args = {
    [1] = "PickingTools",
    [2] = "Guitar"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
local args = {
    [1] = "PickingTools",
    [2] = "ElectricGuitar"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
local player = game.Players.LocalPlayer
local backpack = player:WaitForChild("Backpack")

local itemToDuplicate = backpack:FindFirstChild("Guitar") -- Nome do item

if itemToDuplicate then
    local clonedItem = itemToDuplicate:Clone() -- Clonar o item
    clonedItem.Parent = backpack -- Colocar o clone no inventário
    print("Item duplicado!")
else
    print("Item não encontrado no inventário.")
end
wait(0.1)
local player = game.Players.LocalPlayer
local backpack = player:WaitForChild("Backpack")

local itemToDuplicate = backpack:FindFirstChild("ElectricGuitar") -- Nome do item

if itemToDuplicate then
    local clonedItem = itemToDuplicate:Clone() -- Clonar o item
    clonedItem.Parent = backpack -- Colocar o clone no inventário
    print("Item duplicado!")
else
    print("Item não encontrado no inventário.")
end
wait(0.1)
-- Função para verificar e equipar itens
local function equiparItem(itemName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    
    if backpack then
        -- Verifica se o item já está no inventário
        local item = backpack:FindFirstChild(itemName)
        if item then
            -- Move o item para a mão do jogador, caso não esteja equipado
            local character = player.Character
            if character and not character:FindFirstChild(itemName) then
                item.Parent = character
                print(itemName .. " equipado!")
            else
                print(itemName .. " já está equipado.")
            end
        else
            print(itemName .. " não está no inventário.")
        end
    else
        print("Backpack não encontrado.")
    end
end

-- Checar e equipar Sniper e FireX
equiparItem("Guitar")
equiparItem("ElectricGuitar")
equiparItem("Guitar")
equiparItem("ElectricGuitar")
wait(2)
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(0, 50, 0)
wait(0.1)
-- Script para equipar automaticamente todos os itens do inventário
-- Certifique-se de ter permissão para usar scripts personalizados no jogo.

local player = game.Players.LocalPlayer -- Obtém o jogador local
local backpack = player:WaitForChild("Backpack") -- Referência ao inventário do jogador

local function equipAllItems()
    -- Itera sobre todos os itens na mochila (Backpack)
    for _, item in ipairs(backpack:GetChildren()) do
        -- Verifica se o item não está equipado
        if not player.Character:FindFirstChild(item.Name) then
            -- Tenta equipar o item
            item.Parent = player.Character
        end
    end
end

-- Chamando a função
equipAllItems()

-- Opcional: Conecte o script a eventos (como teclas ou botões)
-- Exemplo: Equipar itens ao pressionar uma tecla (usando ContextActionService)
local ContextActionService = game:GetService("ContextActionService")

local function onEquipAll(actionName, inputState, inputObject)
    if inputState == Enum.UserInputState.Begin then
        equipAllItems()
    end
end

-- Bind da tecla "E" para equipar todos os itens
ContextActionService:BindAction("EquipAll", onEquipAll, false, Enum.KeyCode.E)
    end
})
Tab:AddButton({
    Name = "Give Super Violão [by MatheuszinZK]",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/HeyXmatheus/XScripts/refs/heads/main/superGuitarra'))()
    end
})

Tab:AddButton({
    Name = "Give Super Guitarra",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/HeyXmatheus/XScripts/refs/heads/main/superGuitarraEletrica'))()
    end
})

Tab:AddButton({
    Name = "GIVE GUITAR BLEEDS EAR",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/HeyXmatheus/XScripts/refs/heads/main/superGuitarraEletrica'))()
        wait(0.1)
        loadstring(game:HttpGet('https://raw.githubusercontent.com/HeyXmatheus/XScripts/refs/heads/main/superGuitarra'))()
    end
})

local Section = Tab:AddSection({
    Name = "Config tool"
})

local args = {
    [1] = "PickingTools",
    [2] = ""
}

local function pegarItem(itemName)
    args[2] = itemName
    game:GetService("ReplicatedStorage"):WaitForChild("RE"):WaitForChild("1Too1l"):InvokeServer(unpack(args))
end

Tab:AddTextbox({
    Name = "Item Name",
    Default = "",
    TextDisappear = true,
    Callback = function(value)
        pegarItem(value)
    end
})

Tab:AddButton({
    Name = "Pegar Item",
    Callback = function()
        local itemName = ItemPickerTab:GetTextbox("Item Name").Value
        pegarItem(itemName)
    end
})
local Section = Tab:AddSection({
    Name = "Bomb"
})
Tab:AddButton({
Name = "FireX",
Callback = function()
local args = {
    [1] = "Bomb1NCD3NT"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Blo1wBomb1sServe1r"):FireServer(unpack(args))
wait(1)
local args = {
    [1] = "Bomb1NCD3NT"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Blo1wBomb1sServe1r"):FireServer(unpack(args))
wait(1)
local args = {
    [1] = "Bomb1NCD3NT"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Blo1wBomb1sServe1r"):FireServer(unpack(args))
wait(1)
end
})
Tab:AddButton({
Name = "Bomb",
Callback = function()
local player = game.Players.LocalPlayer
local backpack = player:WaitForChild("Backpack")

local itemToDuplicate = backpack:FindFirstChild("Bomb") -- Nome do item

if itemToDuplicate then
    local clonedItem = itemToDuplicate:Clone() -- Clonar o item
    clonedItem.Parent = backpack -- Colocar o clone no inventário
    print("Item duplicado!")
else
    print("Item não encontrado no inventário.")
end
wait(0.1)
-- Função para verificar e equipar itens
local function equiparItem(itemName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    
    if backpack then
        -- Verifica se o item já está no inventário
        local item = backpack:FindFirstChild(itemName)
        if item then
            -- Move o item para a mão do jogador, caso não esteja equipado
            local character = player.Character
            if character and not character:FindFirstChild(itemName) then
                item.Parent = character
                print(itemName .. " equipado!")
            else
                print(itemName .. " já está equipado.")
            end
        else
            print(itemName .. " não está no inventário.")
        end
    else
        print("Backpack não encontrado.")
    end
end

-- Checar e equipar Sniper e FireX
equiparItem("Bomb")
end
})
local Section = Tab:AddSection({
    Name = "Secret itens"
})
Tab:AddButton({
Name = "Crystal 1",
Callback = function()
local args = {
    [1] = "PickingTools",
    [2] = "Crystal"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
end
})
Tab:AddButton({
Name = "Crystal 2",
Callback = function()
local args = {
    [1] = "PickingTools",
    [2] = "Crystals"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
end
})
Tab:AddButton({
Name = "Couch",
Callback = function()
local args = {
    [1] = "PickingTools",
    [2] = "Couch"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
end
})
local Section = Tab:AddSection({
    Name = "Roses"
})
Tab:AddButton({
Name = "Pick Roses",
Callback = function()
local args = {
    [1] = "PickingTools",
    [2] = "Roses"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
end
})

local toggleActive = false
local function RosesColor()
while toggleActive do
local args = {
    [1] = "Roses",
    [2] = "http://www.roblox.com/asset/?id=5210399458"
}

game:GetService("Players").LocalPlayer.Character.Roses.ToolSound:FireServer(unpack(args))
wait(1.0) -- intervalo de 1 segundo entre cada repetição
local args = {
    [1] = "Roses",
    [2] = "http://www.roblox.com/asset/?id=5210414520"
}

game:GetService("Players").LocalPlayer.Character.Roses.ToolSound:FireServer(unpack(args))
wait(1.0)
local args = {
    [1] = "Roses",
    [2] = "http://www.roblox.com/asset/?id=5216708760"
}

game:GetService("Players").LocalPlayer.Character.Roses.ToolSound:FireServer(unpack(args))
wait(1.0)
end
end

Tab:AddToggle({
Name = "Roses Color",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
RosesColor()
end
end
})
local Section = Tab:AddSection({
    Name = "Tools Fake/Visual"
})
Tab:AddButton({
Name = "FE PUNCH",
Callback = function()
 loadstring(game:HttpGet(('http://pastefy.app/GvnHVjT5/raw'),true))()
end
})
Tab:AddButton({
Name = "Telekiness [FE]",
Callback = function()
 loadstring(game:HttpGet(('https://raw.githubusercontent.com/SAZXHUB/Control-update/main/README.md'),true))()
end
})
Tab:AddButton({
Name = "f3x",
Callback = function()
 loadstring(game:GetObjects("rbxassetid://6695644299")[1].Source)()
end
})
Tab:AddButton({
Name = "Btools",
Callback = function()
 loadstring(game:HttpGet("https://raw.githubusercontent.com/err0r129/PqpHadesBlair/main/Bao.lua"))()
end
})
Tab:AddButton({
Name = "Click TP",
Callback = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/err0r129/KptHadesBlair/main/Bao.lua"))()
end
})
local Section = Tab:AddSection({
    Name = "Taser"
})
Tab:AddButton({
	Name = "Give Taser",
	Callback = function()
      	local args = {
    [1] = "PickingTools",
    [2] = "Taser"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
  	end    
})

local toggleActive = false
local function loopTaser()
while toggleActive do
local args = {
    [1] = "Taser",
    [2] = "On"
}

game:GetService("Players").LocalPlayer.Character.Taser.ToolSound:FireServer(unpack(args))
wait(0.111111) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop Taser",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopTaser()
end
end
})
local Section = Tab:AddSection({
    Name = "FireX"
})
Tab:AddButton({
	Name = "Give FireX",
	Callback = function()
      	local args = {
    [1] = "PickingTools",
    [2] = "FireX"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
  	end    
})

local toggleActive = false
local function loopFireX()
while toggleActive do
local args = {
    [1] = "FireX",
    [2] = "On"
}

game:GetService("Players").LocalPlayer.Character.FireX.ToolSound:FireServer(unpack(args))
wait(0.111111111111111111111111) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop FireX",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopFireX()
end
end
})
local Section = Tab:AddSection({
    Name = "Basketball"
})
Tab:AddButton({
	Name = "Give Basketball",
	Callback = function()
      	local args = {
    [1] = "PickingTools",
    [2] = "Basketball"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))

--Ball

local player = game.Players.LocalPlayer
local backpack = player:WaitForChild("Backpack")

local itemToDuplicate = backpack:FindFirstChild("Basketball") -- Nome do item

if itemToDuplicate then
    local clonedItem = itemToDuplicate:Clone() -- Clonar o item
    clonedItem.Parent = backpack -- Colocar o clone no inventário
    print("Item duplicado!")
else
    print("Item não encontrado no inventário.")
end
  	end    
})

local toggleActive = false
local function loopBall()
while toggleActive do
local args = {
    [1] = Vector3.new(-30.919673919677734, 0.02500009536743164, 190.3595733642578)
}

game:GetService("Players").LocalPlayer.Character.Basketball.ClickEvent:FireServer(unpack(args))
wait(1) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop Ball",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopBall()
end
end
})
local Section = Tab:AddSection({
    Name = "Gun mod"
})
Tab:AddButton({
Name = "Give Sniper Fire",
Callback = function()
 local args = {
    [1] = "PickingTools",
    [2] = "Sniper"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
 local args = {
    [1] = "PickingTools",
    [2] = "PaperbagFire"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
-- Função para verificar e equipar itens
local function equiparItem(itemName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    
    if backpack then
        -- Verifica se o item já está no inventário
        local item = backpack:FindFirstChild(itemName)
        if item then
            -- Move o item para a mão do jogador, caso não esteja equipado
            local character = player.Character
            if character and not character:FindFirstChild(itemName) then
                item.Parent = character
                print(itemName .. " equipado!")
            else
                print(itemName .. " já está equipado.")
            end
        else
            print(itemName .. " não está no inventário.")
        end
    else
        print("Backpack não encontrado.")
    end
end

-- Checar e equipar Sniper e FireX
equiparItem("Sniper")
equiparItem("PaperbagFire")
    end
})
Tab:AddButton({
Name = "Equip all guns",
Callback = function()
local args = {
    [1] = "PickingTools",
    [2] = "Assault"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
local args = {
    [1] = "PickingTools",
    [2] = "Shotgun"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
local args = {
    [1] = "PickingTools",
    [2] = "GlockBrown"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
local args = {
    [1] = "PickingTools",
    [2] = "Sniper"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
-- Função para verificar e equipar itens
local function equiparItem(itemName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    
    if backpack then
        -- Verifica se o item já está no inventário
        local item = backpack:FindFirstChild(itemName)
        if item then
            -- Move o item para a mão do jogador, caso não esteja equipado
            local character = player.Character
            if character and not character:FindFirstChild(itemName) then
                item.Parent = character
                print(itemName .. " equipado!")
            else
                print(itemName .. " já está equipado.")
            end
        else
            print(itemName .. " não está no inventário.")
        end
    else
        print("Backpack não encontrado.")
    end
end

-- Checar e equipar Sniper e FireX
equiparItem("Sniper")
equiparItem("Shotgun")
equiparItem("Assault")
equiparItem("GlockBrown")
end
})
Tab:AddButton({
Name = "Give Gun Smoke",
Callback = function()
 local args = {
    [1] = "PickingTools",
    [2] = "Sniper"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
 local args = {
    [1] = "PickingTools",
    [2] = "FireX"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
-- Função para verificar e equipar itens
local function equiparItem(itemName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    
    if backpack then
        -- Verifica se o item já está no inventário
        local item = backpack:FindFirstChild(itemName)
        if item then
            -- Move o item para a mão do jogador, caso não esteja equipado
            local character = player.Character
            if character and not character:FindFirstChild(itemName) then
                item.Parent = character
                print(itemName .. " equipado!")
            else
                print(itemName .. " já está equipado.")
            end
        else
            print(itemName .. " não está no inventário.")
        end
    else
        print("Backpack não encontrado.")
    end
end

-- Checar e equipar Sniper e FireX
equiparItem("Sniper")
equiparItem("FireX")
    end
})

local toggleActive = false
local function loopSmoke()
while toggleActive do
local args = {
    [1] = "FireX",
    [2] = "On"
}

game:GetService("Players").LocalPlayer.Character.FireX.ToolSound:FireServer(unpack(args))
wait(0.111111111111111111111111) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop Smoke",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopSmoke()
end
end
})

Tab:AddButton({
Name = "Give Gun Taser",
Callback = function()
 local args = {
    [1] = "PickingTools",
    [2] = "Sniper"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
 local args = {
    [1] = "PickingTools",
    [2] = "Taser"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
-- Função para verificar e equipar itens
local function equiparItem(itemName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    
    if backpack then
        -- Verifica se o item já está no inventário
        local item = backpack:FindFirstChild(itemName)
        if item then
            -- Move o item para a mão do jogador, caso não esteja equipado
            local character = player.Character
            if character and not character:FindFirstChild(itemName) then
                item.Parent = character
                print(itemName .. " equipado!")
            else
                print(itemName .. " já está equipado.")
            end
        else
            print(itemName .. " não está no inventário.")
        end
    else
        print("Backpack não encontrado.")
    end
end

-- Checar e equipar Sniper e FireX
equiparItem("Sniper")
equiparItem("Taser")
    end
})

local toggleActive = false
local function loopTaser()
while toggleActive do
local args = {
    [1] = "Taser",
    [2] = "On"
}

game:GetService("Players").LocalPlayer.Character.FireX.ToolSound:FireServer(unpack(args))
wait(0.111111111111111111111111) -- intervalo de 1 segundo entre cada repetição
end
end

Tab:AddToggle({
Name = "loop Taser",
Default = false,
Callback = function(value)
toggleActive = value
if toggleActive then
loopTaser()
end
end
})
local Section = Tab:AddSection({
    Name = "box/bag"
})
Tab:AddButton({
Name = "Give Box",
Callback = function()
 local args = {
    [1] = "PickingTools",
    [2] = "Box"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
end
})
Tab:AddButton({
Name = "Active Smoke Box",
Callback = function()
     local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(9999999827968, 9999999827968, 9999999827968)
wait(0.1)
 local args = {
    [1] = "PickingTools",
    [2] = "FireX"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
-- Função para verificar e equipar itens
local function equiparItem(itemName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    
    if backpack then
        -- Verifica se o item já está no inventário
        local item = backpack:FindFirstChild(itemName)
        if item then
            -- Move o item para a mão do jogador, caso não esteja equipado
            local character = player.Character
            if character and not character:FindFirstChild(itemName) then
                item.Parent = character
                print(itemName .. " equipado!")
            else
                print(itemName .. " já está equipado.")
            end
        else
            print(itemName .. " não está no inventário.")
        end
    else
        print("Backpack não encontrado.")
    end
end

-- Checar e equipar Sniper e FireX
equiparItem("Box")
equiparItem("FireX")
wait(2)
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(7.159717559814453, 3.3000009059906006, 19.785301208496094)
end
})
Tab:AddButton({
Name = "Give Paperbag",
Callback = function()
 local args = {
    [1] = "PickingTools",
    [2] = "Paperbag"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
end
})
Tab:AddButton({
Name = "Active Paper bag Fire",
Callback = function()
     local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(9999999827968, 9999999827968, 9999999827968)
wait(0.1)
 local args = {
    [1] = "PickingTools",
    [2] = "PaperbagFire"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
wait(0.1)
-- Função para verificar e equipar itens
local function equiparItem(itemName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    
    if backpack then
        -- Verifica se o item já está no inventário
        local item = backpack:FindFirstChild(itemName)
        if item then
            -- Move o item para a mão do jogador, caso não esteja equipado
            local character = player.Character
            if character and not character:FindFirstChild(itemName) then
                item.Parent = character
                print(itemName .. " equipado!")
            else
                print(itemName .. " já está equipado.")
            end
        else
            print(itemName .. " não está no inventário.")
        end
    else
        print("Backpack não encontrado.")
    end
end

-- Checar e equipar Sniper e FireX
equiparItem("Paperbag")
equiparItem("PaperbagFire")
wait(2)
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(7.159717559814453, 3.3000009059906006, 19.785301208496094)
end
})
local Section = Tab:AddSection({
    Name = "box/bag"
})
local Tab = Window:MakeTab({
Name = "Teleports",
Icon = "rbxassetid://4483345998",
PremiumOnly = false
})
local Section = Tab:AddSection({
    Name = "locates"
})
Tab:AddButton({
Name = "Lobby",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(7.159717559814453, 3.3000009059906006, 19.785301208496094)
end
})
Tab:AddButton({
Name = "Wather",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-72.37123107910156, -10.816083908081055, 112.93341827392578)
end
})
Tab:AddButton({
Name = "Edge",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-1354.4154052734375, 76.11813354492188, -1278.5859375)
end
})
Tab:AddButton({
Name = "Void",
Callback = function()
     local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(9999999827968, 9999999827968, 9999999827968)
end
})
Tab:AddButton({
Name = "Commercial 1",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-242.68215942382812, 89.68680572509766, -549.6495361328125)
end
})
Tab:AddButton({
Name = "Commercial 2",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-630.480712890625, 26.586822509765625, 365.14093017578125)
end
})
Tab:AddButton({
Name = "Secret 1",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(223.24264526367188, -37.5954704284668, -153.50656127929688)
end
})
Tab:AddButton({
Name = "Secret 2",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-350.3148498535156, 45.385169982910156, -123.7399673461914)
end
})
Tab:AddButton({
Name = "Secret 3",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-271.9717712402344, 22.992469787597656, 1115.3104248046875)
end
})
Tab:AddButton({
Name = "Secret 4",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-35.98054122924805, -48.27098083496094, 220.8909912109375)
end
})
Tab:AddButton({
Name = "Secret 5",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(15.010516166687012, -29.14361000061035, -60.09798812866211)
end
})
Tab:AddButton({
Name = "Bow 1",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-589.1044311523438, 140.25389099121094, -60.75751876831055)
end
})
Tab:AddButton({
Name = "Bow 2",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(624.4569702148438, 133.63233947753906, -59.50937271118164)
end
})
Tab:AddButton({
Name = "School",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-288.21392822265625, 4.142392635345459, 212.0995635986328)
end
})
Tab:AddButton({
Name = "Hospital",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-306.9185485839844, 4.1286420822143555, 7.26304817199707)
end
})
Tab:AddButton({
Name = "Plane",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(450.3541564941406, -106.24927520751953, 112.56250762939453)
end
})
Tab:AddButton({
Name = "Police state",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(-118.54170227050781, 3.8526408672332764, -1.622152805328369)
end
})
Tab:AddButton({
Name = "Cinema",
Callback = function()
 local plr = game.Players.LocalPlayer
local char = plr.Character
local hrp = char.HumanoidRootPart

hrp.CFrame = CFrame.new(190.19032287597656, -26.225231170654297, -184.5957489013672)
end
})
OrionLib:Init()
