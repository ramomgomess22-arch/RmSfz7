local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer

local manualJump = false

-- Só detecta toque no botão de pular
UserInputService.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.Space or input.UserInputType == Enum.UserInputType.Touch then
        manualJump = true
        wait(0.1) -- Pequeno delay para mobile
        manualJump = false
    end
end)

-- Desabilita auto jump SEM loop pesado
local function disableAutoJump()
    local character = player.Character
    if character then
        local humanoid = character:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.AutoJumpEnabled = false
        end
    end
end

-- Executa só uma vez quando entra no jogo
disableAutoJump()

-- Reaplica só no respawn (raro)
player.CharacterAdded:Connect(disableAutoJump)

print("Anti-AutoJump Mobile ativado!")
