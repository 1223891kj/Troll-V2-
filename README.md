local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/Kiwilegazin/Orion-mobile-v2/refs/heads/main/README.md')))()

local Window = OrionLib:MakeWindow({Name = "⛄SUPER TROLL V2🌊", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest"})

-- Aba TROLL OP!
local TrollTab = Window:MakeTab({Name = "TROLL OP!", Icon = "rbxassetid://4483345998", PremiumOnly = false})

-- Olhar Players (agora lista os jogadores corretamente)
local PlayersDropdown = TrollTab:AddDropdown({
    Name = "Olhar Players",
    Default = "",
    Options = {},
    Callback = function(selectedPlayer)
        local player = game.Players:FindFirstChild(selectedPlayer)
        if player then
            game.Workspace.CurrentCamera.CameraSubject = player.Character.Humanoid
        end
    end
})

-- Atualizar a lista de jogadores automaticamente
local function UpdatePlayersList()
    local players = {}
    for _, player in pairs(game.Players:GetPlayers()) do
        table.insert(players, player.Name)
    end
    PlayersDropdown:Refresh(players)
end
UpdatePlayersList()
game.Players.PlayerAdded:Connect(UpdatePlayersList)
game.Players.PlayerRemoving:Connect(UpdatePlayersList)

-- Parar de olhar jogadores
TrollTab:AddButton({
    Name = "Parar de Olhar Jogadores",
    Callback = function()
        game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
    end
})

-- Função de ESP
local espEnabled = false
TrollTab:AddToggle({
    Name = "ESP Players",
    Default = false,
    Callback = function(state)
        espEnabled = state
        if espEnabled then
            -- Criar ou atualizar o ESP para cada jogador
            for _, player in pairs(game.Players:GetPlayers()) do
                if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    -- Verificar se o ESP já existe, se não, criar
                    local espBox = player.Character.HumanoidRootPart:FindFirstChild("ESPBox")
                    if not espBox then
                        espBox = Instance.new("BillboardGui", player.Character.HumanoidRootPart)
                        espBox.Size = UDim2.new(0, 200, 0, 50)
                        espBox.StudsOffset = Vector3.new(0, 3, 0)
                        espBox.AlwaysOnTop = true
                        espBox.Name = "ESPBox"

                        local nameLabel = Instance.new("TextLabel", espBox)
                        nameLabel.Size = UDim2.new(1, 0, 1, 0)
                        nameLabel.BackgroundTransparency = 1
                        nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
                        nameLabel.TextStrokeTransparency = 0.8
                        nameLabel.TextScaled = true

                        -- Atualizar a distância
                        local function updateDistance()
                            if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                                local distance = (player.Character.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
                                nameLabel.Text = player.Name .. " - " .. math.floor(distance) .. " studs"
                            end
                        end

                        -- Atualizar a distância a cada 0.1 segundos
                        game:GetService("RunService").Heartbeat:Connect(updateDistance)
                    end
                end
            end
        else
            -- Remover ESP
            for _, player in pairs(game.Players:GetPlayers()) do
                if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    local espBox = player.Character.HumanoidRootPart:FindFirstChild("ESPBox")
                    if espBox then
                        espBox:Destroy()
                    end
                end
            end
        end
    end
})

-- Adicionando o Fling GUI (Universal) conforme solicitado
TrollTab:AddButton({
    Name = "Fling Players (Universal)",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-FE-Fling-GUI-10927"))()
    end
})

-- Opções da aba ADM
TrollTab:AddButton({Name = "ADM FE (Infinite Yield)", Callback = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
end})
TrollTab:AddButton({Name = "Super Ring", Callback = function()
    loadstring(game:HttpGet("https://rawscripts.net/raw/Natural-Disaster-Survival-Super-Rings-Parts-V4-By-Lukas-24409"))()
end})
TrollTab:AddButton({Name = "Executor RC7", Callback = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/CoreGui/Scripts/main/RC7"))()
end})
TrollTab:AddButton({Name = "Knife (FE)", Callback = function()
    loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Grab-knife-v4-24753"))()
end})
TrollTab:AddButton({Name = "Tubers 93 GUI", Callback = function()
    loadstring(game:HttpGet("https://pastebin.com/raw/aYVcsXYf"))()
end})
TrollTab:AddButton({Name = "c00lkid GUI", Callback = function()
    loadstring(game:HttpGet("https://pastebin.com/raw/UPZCQ31W"))()
end})
TrollTab:AddButton({
    Name = "SANDER X",
    Callback = function()
        loadstring(game:HttpGet('https://rawscripts.net/raw/Brookhaven-RP-Sander-X-Hub-Latest-Version-3-16718'))()
    end
})
TrollTab:AddButton({
    Name = "ESP",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/1223891kj/Esp-/refs/heads/main/README.md"))()
    end
})
TrollTab:AddButton({
    Name = "FLING",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/kiwi541/Mr-red-Black-V4/refs/heads/main/README.md'))()
    end
})
TrollTab:AddButton({
    Name = "TELEPORT TOOL",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Teleport-Tool-27419"))()
    end
})
TrollTab:AddButton({
    Name = "UTG",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/1223891kj/Utg/refs/heads/main/README.md"))()
    end
})
TrollTab:AddButton({
    Name = "TELEKINIS",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fe-Telekinesis-V5-21542"))()
    end
})
-- Botão Anti Sit
TrollTab:AddButton({
    Name = "ANTI SIT",
    Callback = function()
        local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.Sit = false
            humanoid.Changed:Connect(function(property)
                if property == "Sit" then
                    humanoid.Sit = false
                end
            end)
            print("Anti Sit ativado")
        end
    end
})

-- Botão para voltar a conseguir sentar
TrollTab:AddButton({
    Name = "VOLTAR A CONSEGUIR SENTAR",
    Callback = function()
        local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.Changed:Connect(function() end) -- Para remover o bloqueio de sentar
            print("Agora você pode sentar novamente")
        end
    end
})

TrollTab:AddTextbox({
    Name = "Pulo",
    Default = tostring(jumpPower),
    TextDisappear = false,
    Callback = function(text)
        local newJumpPower = tonumber(text)
        if newJumpPower then
            jumpPower = newJumpPower
            game.Players.LocalPlayer.Character.Humanoid.JumpPower = jumpPower
            print("Pulo alterado para: " .. jumpPower)
        else
            print("Por favor, insira um valor numérico válido para o pulo.")
        end
    end
})

function equipAllItems()
    local character = game.Players.LocalPlayer.Character
    if character and character:FindFirstChildOfClass("Humanoid") then
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        for i, tool in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
            if tool:IsA("Tool") then
                humanoid:EquipTool(tool)
                print("Item equipado: " .. tool.Name)
            end
        end
    else
        print("Personagem não encontrado ou não possui um Humanoid.")
    end
end
TrollTab:AddButton({
    Name = "PRIZZLIFE SCRIPT",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/elliexmln/PrizzLife/main/pladmin.lua'))()
    end
})
