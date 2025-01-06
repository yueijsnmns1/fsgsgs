-- Carregando a biblioteca para criar a interface
local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()

-- Criando a interface de usuário
local UI = Lib:Create{
    Theme = "Dark", -- Tema da interface
    Size = UDim2.new(0, 555, 0, 400) -- Tamanho padrão da UI
}

-- Criando a aba principal
local Main = UI:Tab{
    Name = "Main"
}

-- Adicionando um divisor na aba principal
local Divider = Main:Divider{
    Name = "Funções"
}

-- Função para teleportar o jogador para um local específico
local function TeleportTo(locationName)
    local player = game.Players.LocalPlayer
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        if locationName == "Ilha1" then
            character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(100, 10, 100))  -- Exemplo de coordenadas da Ilha 1
        elseif locationName == "Ilha2" then
            character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(200, 10, 200))  -- Exemplo de coordenadas da Ilha 2
        elseif locationName == "Ilha3" then
            character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(300, 10, 300))  -- Exemplo de coordenadas da Ilha 3
        elseif locationName == "SegundoSia" then
            character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(400, 10, 400))  -- Coordenadas do segundo local
        elseif locationName == "TerceiroSia" then
            character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(500, 10, 500))  -- Coordenadas do terceiro local
        else
            print("Local não encontrado!")
        end
        print("Teleportando para " .. locationName)
    end
end

-- Botão para teleportar para a Ilha 1
local TeleportIlha1 = Divider:Button{
    Name = "Teleporte para Ilha 1",
    Description = "Teleporta para a Ilha 1.",
    Callback = function()
        TeleportTo("Ilha1")
    end
}

-- Botão para teleportar para a Ilha 2
local TeleportIlha2 = Divider:Button{
    Name = "Teleporte para Ilha 2",
    Description = "Teleporta para a Ilha 2.",
    Callback = function()
        TeleportTo("Ilha2")
    end
}

-- Botão para teleportar para a Ilha 3
local TeleportIlha3 = Divider:Button{
    Name = "Teleporte para Ilha 3",
    Description = "Teleporta para a Ilha 3.",
    Callback = function()
        TeleportTo("Ilha3")
    end
}

-- Botão para teleportar para o segundo Sia
local TeleportSegundoSia = Divider:Button{
    Name = "Teleporte para Segundo Sia",
    Description = "Teleporta para o Segundo Sia.",
    Callback = function()
        TeleportTo("SegundoSia")
    end
}

-- Botão para teleportar para o terceiro Sia
local TeleportTerceiroSia = Divider:Button{
    Name = "Teleporte para Terceiro Sia",
    Description = "Teleporta para o Terceiro Sia.",
    Callback = function()
        TeleportTo("TerceiroSia")
    end
}

-- Função para matar todos os jogadores (não modificado)
local KillAll = Divider:Button{
    Name = "Matar todos",
    Description = "Mata todos os jogadores no jogo!",
    Callback = function()
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character and player.Character:FindFirstChild("Humanoid") then
                player.Character.Humanoid.Health = 0 -- Matar o jogador
            end
        end
        print("Todos os jogadores foram mortos.")
    end
}

-- Função para criar o ESP (azul) como já foi configurado anteriormente
local function CreateESP(player)
    local espPart = Instance.new("BillboardGui")
    espPart.Adornee = player.Character:WaitForChild("Head")
    espPart.Parent = player.Character
    espPart.Size = UDim2.new(0, 100, 0, 100)
    espPart.StudsOffset = Vector3.new(0, 2, 0)

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 1, 0)
    frame.BackgroundColor3 = Color3.fromRGB(0, 0, 255) -- Cor azul
    frame.BorderSizePixel = 0
    frame.Parent = espPart

    ESPs[player] = espPart
end

-- Função para remover o ESP de um jogador
local function RemoveESP(player)
    if ESPs[player] then
        ESPs[player]:Destroy()
        ESPs[player] = nil
    end
end

-- Tabela para armazenar os ESPs criados para os jogadores
local ESPs = {}

-- Função para atualizar os ESPs quando um jogador entrar
game.Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        if ESPEnabled then
            CreateESP(player)
        end
    end)
end)

-- Função para remover ESP quando um jogador sair
game.Players.PlayerRemoving:Connect(function(player)
    RemoveESP(player)
end)
