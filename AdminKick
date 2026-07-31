local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- CONFIG
local ADMINS = {
	["SeuUsuarioAqui"] = true, -- COLOCA SEU NOME AQUI
}

-- 1. CRIA O REMOTEEVENT AUTOMATICAMENTE
local KickEvent = ReplicatedStorage:FindFirstChild("KickPlayerEvent")
if not KickEvent then
	KickEvent = Instance.new("RemoteEvent")
	KickEvent.Name = "KickPlayerEvent"
	KickEvent.Parent = ReplicatedStorage
end

-- 2. SERVIDOR RECEBE E DÁ KICK DE VERDADE
KickEvent.OnServerEvent:Connect(function(adminPlayer, targetName, reason)
	if not ADMINS[adminPlayer.Name] then return end -- só admin
	
	local target = Players:FindFirstChild(targetName)
	if target then
		target:Kick(reason or "Kicked by Admin")
		print("[ADMIN] " .. adminPlayer.Name .. " kicked " .. targetName)
	end
end)

-- 3. FUNÇÃO PRA CRIAR A GUI PRA CADA PLAYER
local function createGuiForPlayer(player)
	local gui = Instance.new("ScreenGui")
	gui.Name = "AdminKickGui"
	gui.ResetOnSpawn = false
	gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	gui.Parent = player:WaitForChild("PlayerGui")

	local main = Instance.new("Frame")
	main.Size = UDim2.new(0, 300, 0, 400)
	main.Position = UDim2.new(0, 10, 0.5, -200)
	main.BackgroundColor3 = Color3.fromRGB(20,20,20)
	main.BorderSizePixel = 0
	main.Parent = gui
	
	Instance.new("UICorner", main).CornerRadius = UDim.new(0,8)

	local title = Instance.new("TextLabel")
	title.Size = UDim2.new(1, 0, 0, 35)
	title.Text = "Player List"
	title.TextColor3 = Color3.new(1,1,1)
	title.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
	title.Font = Enum.Font.GothamBold
	title.TextSize = 16
	title.Parent = main
	Instance.new("UICorner", title).CornerRadius = UDim.new(0,8)

	local list = Instance.new("ScrollingFrame")
	list.Size = UDim2.new(1, -10, 1, -45)
	list.Position = UDim2.new(0, 5, 0, 40)
	list.BackgroundTransparency = 1
	list.ScrollBarThickness = 6
	list.Parent = main
	
	local layout = Instance.new("UIListLayout")
	layout.Padding = UDim.new(0,4)
	layout.Parent = list

	-- FUNÇÃO QUE ATUALIZA A LISTA
	local function refresh()
		list:ClearAllChildren()
		layout.Parent = list
		
