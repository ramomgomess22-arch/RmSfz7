-- Ant Bola Pedra By ChatGPT

-- Interface
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui")
gui.Name = "AntBolaPedraGui"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

-- Botão principal (Lag)
local button = Instance.new("TextButton")
button.Parent = gui
button.Size = UDim2.new(0, 70, 0, 70)
button.Position = UDim2.new(0, 100, 0, 150)
button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
button.TextColor3 = Color3.fromRGB(255, 255, 255)
button.Text = "OFF"
button.Font = Enum.Font.GothamBold
button.TextSize = 20
button.BackgroundTransparency = 0.1
button.AutoButtonColor = true
button.Active = true
button.Draggable = true
button.AnchorPoint = Vector2.new(0.5, 0.5)

-- Deixa o botão redondo
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(1, 0)
corner.Parent = button

-- Efeito de sombra
local shadow = Instance.new("UIStroke")
shadow.Color = Color3.fromRGB(255, 255, 255)
shadow.Thickness = 1.5
shadow.Parent = button

-- Botão de esconder/mostrar
local toggleGui = Instance.new("TextButton")
toggleGui.Parent = gui
toggleGui.Size = UDim2.new(0, 140, 0, 35)
toggleGui.Position = UDim2.new(0, 10, 0, 10)
toggleGui.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
toggleGui.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleGui.Text = "Ant Bola Pedra"
toggleGui.Font = Enum.Font.GothamBold
toggleGui.TextSize = 14
toggleGui.AutoButtonColor = true
toggleGui.Active = true
toggleGui.Draggable = true

local toggleCorner = Instance.new("UICorner")
toggleCorner.CornerRadius = UDim.new(0, 10)
toggleCorner.Parent = toggleGui

-- Variáveis de controle
local lagAtivo = false
local visivel = true

-- Função principal (Lag Switch)
button.MouseButton1Click:Connect(function()
	lagAtivo = not lagAtivo
	if lagAtivo then
		button.Text = "ON"
		button.BackgroundColor3 = Color3.fromRGB(0, 200, 100)
		shadow.Color = Color3.fromRGB(0, 255, 150)
		settings().Network.IncomingReplicationLag = 8
	else
		button.Text = "OFF"
		button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
		shadow.Color = Color3.fromRGB(255, 255, 255)
		settings().Network.IncomingReplicationLag = 0
	end
end)

-- Mostrar/Esconder Lag Switch
toggleGui.MouseButton1Click:Connect(function()
	visivel = not visivel
	button.Visible = visivel
	toggleGui.Text = "Ant Bola Pedra"
end)
