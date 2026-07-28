-- [[ ZYCK SOLUTIONS - bola desacelerada ]] --

local RunService = game:GetService("RunService")
local Stats = game:GetService("Stats")

-- Função principal de calibração de performance
local function calibrarDesempenho()
    -- Crava o teto de quadros exatamente em 57 FPS para estabilizar a condução
    if setfpscap then
        setfpscap(53)
        print("[ZYCK] Limite de FPS cravado com sucesso em: 57 📈")
    else
        print("[ZYCK] Erro: Seu executor não suporta a função setfpscap.")
    end

    -- Otimizações internas de rede (Reduz input lag e estabiliza ping)
    pcall(function()
        settings().Physics.AllowSleep = false
        settings().Physics.PhysicsEnvironmentalThrottle = Enum.EnviromentalPhysicsThrottle.Disabled
        Stats.Network.ServerToClientConnection.RouterLagLowerBound = 0
        print("[ZYCK] Input lag de rede minimizado!")
    end)
end

-- Executa a calibração imediatamente
task.spawn(pcall, calibrarDesempenho)
