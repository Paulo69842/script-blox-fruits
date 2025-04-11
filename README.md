
-- ✅ Anti-AFK
game:GetService("Players").LocalPlayer.Idled:connect(function()
    game:GetService("VirtualUser"):Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
    wait(1)
    game:GetService("VirtualUser"):Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
end)

-- 📌 Função de teleporte
function teleportTo(pos)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(pos)
end

-- 🔥 FARM NA MAGMA ISLAND (Magma NPCs)
local magmaNPC = "Magma Ninja" -- Pode mudar para Magma Admiral se quiser farm boss
_G.AutoMagma = true

spawn(function()
    while _G.AutoMagma do
        local enemies = workspace.Enemies:GetChildren()
        for _, npc in pairs(enemies) do
            if npc.Name == magmaNPC and npc:FindFirstChild("HumanoidRootPart") and npc.Humanoid.Health > 0 then
                repeat
                    wait()
                    teleportTo(npc.HumanoidRootPart.Position + Vector3.new(0,5,0))
                    game:GetService("VirtualInputManager"):SendKeyEvent(true, "Z", false, game)
                    game:GetService("VirtualInputManager"):SendKeyEvent(false, "Z", false, game)
                until npc.Humanoid.Health <= 0 or not _G.AutoMagma
            end
        end
        wait(1)
    end
end)

-- 🐉 AUTO V4 DRACO (Trial, Lever e Full Moon check)
_G.AutoV4 = true

spawn(function()
    while _G.AutoV4 do
        wait(3)

        -- Confere se é Lua Cheia
        local lighting = game:GetService("Lighting")
        if lighting:GetMoonPhase() == Enum.MoonPhase.Full then
            -- Teleporta pro Lever Room (ajuste a posição conforme necessário)
            teleportTo(Vector3.new(-5348, 400, -2734)) -- Exemplo de posição perto do lever

            wait(3)

            -- Ativa a alavanca (lever)
            local lever = workspace:FindFirstChild("Lever")
            if lever and lever:FindFirstChild("ClickDetector") then
                fireclickdetector(lever.ClickDetector)
            end

            wait(2)

            -- Teleporta para o TRIAL da raça Dragão (ajuste se necessário)
            teleportTo(Vector3.new(-5000, 300, -2750)) -- Exemplo de portal do Trial

            -- Aguarda conclusão manual do trial
            repeat wait(5) until not _G.AutoV4 or game.Players.LocalPlayer.Backpack:FindFirstChild("Awakening Orb")

            -- Depois do Trial, teleporta pro templo do tempo
            teleportTo(Vector3.new(-12548, 500, -7634)) -- Ajuste se precisar

            break -- para o loop após pegar a orb
        end
    end
end)

-- 🥋 Auto Buso
spawn(function()
    while wait(5) do
        if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
            game:GetService("VirtualInputManager"):SendKeyEvent(true, "J", false, game)
            game:GetService("VirtualInputManager"):SendKeyEvent(false, "J", false, game)
        end
    end
end)

end) -- fim do pcall
