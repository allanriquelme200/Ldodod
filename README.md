-- Criando a UI Toggle
local screenGui = Instance.new("ScreenGui")
local mainFrame = Instance.new("Frame")
local toggleButton = Instance.new("TextButton")
local controlFrame = Instance.new("Frame")
local startButton = Instance.new("TextButton")
local stopButton = Instance.new("TextButton")
local tpButton = Instance.new("TextButton")
local bypassButton = Instance.new("TextButton")
local statusLabel = Instance.new("TextLabel")

screenGui.Parent = game.CoreGui
screenGui.Name = "FlorianopolisRPHub"

mainFrame.Parent = screenGui
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
mainFrame.Position = UDim2.new(0.5, -150, 0.5, -150)
mainFrame.Size = UDim2.new(0, 300, 0, 400)
mainFrame.Visible = false

toggleButton.Parent = screenGui
toggleButton.Size = UDim2.new(0, 50, 0, 50)
toggleButton.Position = UDim2.new(0.5, -25, 0.5, -25)
toggleButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
toggleButton.Text = "▶️"

controlFrame.Parent = mainFrame
controlFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
controlFrame.Size = UDim2.new(1, 0, 1, 0)

startButton.Parent = controlFrame
startButton.Size = UDim2.new(0.8, 0, 0.2, 0)
startButton.Position = UDim2.new(0.1, 0, 0.05, 0)
startButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
startButton.Text = "Iniciar Auto Farm"

stopButton.Parent = controlFrame
stopButton.Size = UDim2.new(0.8, 0, 0.2, 0)
stopButton.Position = UDim2.new(0.1, 0, 0.3, 0)
stopButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
stopButton.Text = "Parar Auto Farm"

tpButton.Parent = controlFrame
tpButton.Size = UDim2.new(0.8, 0, 0.2, 0)
tpButton.Position = UDim2.new(0.1, 0, 0.55, 0)
tpButton.BackgroundColor3 = Color3.fromRGB(0, 0, 255)
tpButton.Text = "Teleporte para Lixeira"

bypassButton.Parent = controlFrame
bypassButton.Size = UDim2.new(0.8, 0, 0.2, 0)
bypassButton.Position = UDim2.new(0.1, 0, 0.8, 0)
bypassButton.BackgroundColor3 = Color3.fromRGB(255, 165, 0)
bypassButton.Text = "Bypass Interação"

statusLabel.Parent = controlFrame
statusLabel.Size = UDim2.new(0.8, 0, 0.2, 0)
statusLabel.Position = UDim2.new(0.1, 0, 1.05, 0)
statusLabel.Text = "Status: Inativo"
statusLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
statusLabel.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Lógica do Auto Farm
local farming = false

local function startAutoFarm()
    farming = true
    statusLabel.Text = "Status: Ativo"
    
    while farming do
        local player = game.Players.LocalPlayer
        local char = player.Character
        if char then
            local lixo = workspace:FindFirstChild("Lixo")
            local lixeira = workspace:FindFirstChild("Lixeira")
            if lixo and lixeira then
                -- Coleta o lixo
                char:MoveTo(lixo.Position)
                wait(2)
                -- Simula a interação
                keypress(0x45)
                wait(1)
                -- Entrega na lixeira
                char:MoveTo(lixeira.Position)
                wait(2)
                keypress(0x45)
            end
        end
        wait(2)
    end
end

local function stopAutoFarm()
    farming = false
    statusLabel.Text = "Status: Inativo"
end

-- Função de Teleporte
local function teleportToLixeira()
    local lixeira = workspace:FindFirstChild("Lixeira")
    if lixeira then
        local player = game.Players.LocalPlayer
        local char = player.Character
        if char then
            char:MoveTo(lixeira.Position)
        end
    end
end

-- Função de Bypass
local function bypassInteraction()
    local porta = workspace:FindFirstChild("Porta")
    if porta then
        keypress(0x45)
    end
end

-- Função para alternar a visibilidade da UI
toggleButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
    toggleButton.Text = mainFrame.Visible and "❌" or "▶️"
end)

startButton.MouseButton1Click:Connect(function()
    if not farming then
        startAutoFarm()
    end
end)

stopButton.MouseButton1Click:Connect(function()
    if farming then
        stopAutoFarm()
    end
end)

tpButton.MouseButton1Click:Connect(function()
    teleportToLixeira()
end)

bypassButton.MouseButton1Click:Connect(function()
    bypassInteraction()
end)

-- Função para simular pressionar teclas
function keypress(keyCode)
    -- Adapte conforme o executor que você utiliza
end

function keyrelease(keyCode)
    -- Adapte conforme o executor que você utiliza
