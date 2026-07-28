local runService = game:GetService("RunService")

local estadoPuxar1x = false
local estadoPuxar2x = false
local conexaoFps = nil

-- Função responsável por limitar o FPS
local function gerenciarTravaFps(alvo)
    if conexaoFps then conexaoFps:Disconnect() conexaoFps = nil end
    if alvo == 0 then return end
    local t0 = os.clock()
    conexaoFps = runService.RenderStepped:Connect(function()
        local t1 = os.clock()
        while t1 - t0 < (1 / alvo) do t1 = os.clock() end
        t0 = t1
    end)
end

-- Lógica do Puxar Bola 1x (Trava 52 FPS)
local function TogglePuxarBola1x()
    estadoPuxar1x = not estadoPuxar1x
    if estadoPuxar1x then
        if estadoPuxar2x then estadoPuxar2x = false end
        gerenciarTravaFps(52)
    else
        gerenciarTravaFps(0)
    end
    return estadoPuxar1x
end

-- Lógica do Puxar Bola 2x (Trava 55 FPS)
local function TogglePuxarBola2x()
    estadoPuxar2x = not estadoPuxar2x
    if estadoPuxar2x then
        if estadoPuxar1x then estadoPuxar1x = false end
        gerenciarTravaFps(55)
    else
        gerenciarTravaFps(0)
    end
    return estadoPuxar2x
end
