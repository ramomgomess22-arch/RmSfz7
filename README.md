local runService = game:GetService("RunService")

local estadoPuxar2x = false
local conexaoFps2x = nil

local function gerenciarTravaFps2x(alvo)
    if conexaoFps2x then conexaoFps2x:Disconnect() conexaoFps2x = nil end
    if alvo == 0 then return end
    local t0 = os.clock()
    conexaoFps2x = runService.RenderStepped:Connect(function()
        local t1 = os.clock()
        while t1 - t0 < (1 / alvo) do t1 = os.clock() end
        t0 = t1
    end)
end

local function TogglePuxarBola2x()
    estadoPuxar2x = not estadoPuxar2x
    if estadoPuxar2x then
        gerenciarTravaFps2x(55)
    else
        gerenciarTravaFps2x(0)
    end
    return estadoPuxar2x
end
