-- TSUNAMI SAFE ZONE SCRIPT
wait(1)

local player = game.Players.LocalPlayer

local function getChar()
    return player.Character or player.CharacterAdded:Wait()
end

local function getRoot()
    local c = getChar()
    return c:WaitForChild("HumanoidRootPart")
end

-- Coordenadas
local SAFE_ZONE = Vector3.new(669.8552, -6.4518, 220.5049)

-- Criar GUI
local gui = Instance.new("ScreenGui")
gui.Name = "SafeZoneGUI"
gui.ResetOnSpawn = false

pcall(function()
    gui.Parent = game:GetService("CoreGui")
end)

if gui.Parent ~= game:GetService("CoreGui") then
    gui.Parent = player:WaitForChild("PlayerGui")
end

-- BOTÃO ABRIR
local openBtn = Instance.new("TextButton")
openBtn.Size = UDim2.new(0, 180, 0, 80)
openBtn.Position = UDim2.new(0, 10, 0.4, 0)
openBtn.BackgroundColor3 = Color3.new(0.2, 0.8, 0.3)
openBtn.Text = "🌊 Show"
openBtn.TextSize = 24
openBtn.TextColor3 = Color3.new(1, 1, 1)
openBtn.Font = Enum.Font.GothamBold
openBtn.BorderSizePixel = 0
openBtn.Parent = gui

local openCorner = Instance.new("UICorner")
openCorner.CornerRadius = UDim.new(0, 15)
openCorner.Parent = openBtn

-- FRAME PRINCIPAL
local main = Instance.new("Frame")
main.Size = UDim2.new(0, 450, 0, 270)
main.Position = UDim2.new(0.5, -225, 0.5, -135)
main.BackgroundColor3 = Color3.new(0.1, 0.1, 0.15)
main.BorderSizePixel = 0
main.Visible = false
main.Active = true
main.Draggable = true
main.Parent = gui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 15)
mainCorner.Parent = main

-- HEADER
local header = Instance.new("Frame")
header.Size = UDim2.new(1, 0, 0, 60)
header.BackgroundColor3 = Color3.new(0.15, 0.15, 0.2)
header.BorderSizePixel = 0
header.Parent = main

local headerCorner = Instance.new("UICorner")
headerCorner.CornerRadius = UDim.new(0, 15)
headerCorner.Parent = header

-- TÍTULO
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 1, 0)
title.BackgroundTransparency = 1
title.Text = "🌊 TSUNAMI Show by karatekaff"
title.TextColor3 = Color3.new(0.2, 0.8, 0.3)
title.TextSize = 18
title.Font = Enum.Font.GothamBold
title.Parent = header

-- FECHAR
local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(1, -40, 0, 15)
closeBtn.BackgroundColor3 = Color3.new(1, 0.3, 0.3)
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.new(1, 1, 1)
closeBtn.TextSize = 16
closeBtn.Font = Enum.Font.GothamBold
closeBtn.BorderSizePixel = 0
closeBtn.Parent = header

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(1, 0)
closeCorner.Parent = closeBtn

-- BOTÃO TP
local tpBtn = Instance.new("TextButton")
tpBtn.Size = UDim2.new(1, -30, 0, 50)
tpBtn.Position = UDim2.new(0, 15, 0, 75)
tpBtn.BackgroundColor3 = Color3.new(0.2, 0.5, 0.8)
tpBtn.Text = "📍 TELEPORTAR PARA SAFE ZONE"
tpBtn.TextColor3 = Color3.new(1, 1, 1)
tpBtn.TextSize = 15
tpBtn.Font = Enum.Font.GothamBold
tpBtn.BorderSizePixel = 0
tpBtn.Parent = main

local tpCorner = Instance.new("UICorner")
tpCorner.CornerRadius = UDim.new(0, 10)
tpCorner.Parent = tpBtn

-- TOGGLE NOCLIP
local noclipFrame = Instance.new("Frame")
noclipFrame.Size = UDim2.new(1, -30, 0, 50)
noclipFrame.Position = UDim2.new(0, 15, 0, 135)
noclipFrame.BackgroundColor3 = Color3.new(0.15, 0.15, 0.2)
noclipFrame.BorderSizePixel = 0
noclipFrame.Parent = main

local noclipCorner = Instance.new("UICorner")
noclipCorner.CornerRadius = UDim.new(0, 8)
noclipCorner.Parent = noclipFrame

local noclipLabel = Instance.new("TextLabel")
noclipLabel.Size = UDim2.new(0.6, 0, 1, 0)
noclipLabel.Position = UDim2.new(0, 10, 0, 0)
noclipLabel.BackgroundTransparency = 1
noclipLabel.Text = "👻 NOCLIP"
noclipLabel.TextColor3 = Color3.new(1, 1, 1)
noclipLabel.TextSize = 14
noclipLabel.Font = Enum.Font.GothamBold
noclipLabel.TextXAlignment = Enum.TextXAlignment.Left
noclipLabel.Parent = noclipFrame

local noclipToggle = Instance.new("TextButton")
noclipToggle.Size = UDim2.new(0, 60, 0, 30)
noclipToggle.Position = UDim2.new(1, -70, 0.5, -15)
noclipToggle.BackgroundColor3 = Color3.new(0.4, 0.4, 0.45)
noclipToggle.Text = "OFF"
noclipToggle.TextColor3 = Color3.new(1, 1, 1)
noclipToggle.TextSize = 12
noclipToggle.Font = Enum.Font.GothamBold
noclipToggle.BorderSizePixel = 0
noclipToggle.Parent = noclipFrame

local noclipToggleCorner = Instance.new("UICorner")
noclipToggleCorner.CornerRadius = UDim.new(0, 8)
noclipToggleCorner.Parent = noclipToggle

local noclipEnabled = false
noclipToggle.MouseButton1Click:Connect(function()
    noclipEnabled = not noclipEnabled
    if noclipEnabled then
        noclipToggle.BackgroundColor3 = Color3.new(0.2, 0.8, 0.3)
        noclipToggle.Text = "ON"
    else
        noclipToggle.BackgroundColor3 = Color3.new(0.4, 0.4, 0.45)
        noclipToggle.Text = "OFF"
    end
end)

-- TEXTO DE INSTRUÇÃO
local instruction = Instance.new("TextLabel")
instruction.Size = UDim2.new(1, -30, 0, 50)
instruction.Position = UDim2.new(0, 15, 0, 195)
instruction.BackgroundColor3 = Color3.new(0.15, 0.15, 0.2)
instruction.Text = "⚠️ Espera o tsunami chegar perto e entra na safe zone"
instruction.TextColor3 = Color3.new(1, 1, 1)
instruction.TextSize = 13
instruction.Font = Enum.Font.Gotham
instruction.TextScaled = true
instruction.TextWrapped = true
instruction.BorderSizePixel = 0
instruction.Parent = main

local instructionCorner = Instance.new("UICorner")
instructionCorner.CornerRadius = UDim.new(0, 8)
instructionCorner.Parent = instruction

-- FUNÇÃO TP
tpBtn.MouseButton1Click:Connect(function()
    pcall(function()
        local root = getRoot()
        root.CFrame = CFrame.new(SAFE_ZONE + Vector3.new(0, 3, 0))
    end)
end)

-- ABRIR/FECHAR
openBtn.MouseButton1Click:Connect(function()
    main.Visible = not main.Visible
    if main.Visible then
        openBtn.Text = "🌊 FECHAR"
        openBtn.BackgroundColor3 = Color3.new(1, 0.3, 0.3)
    else
        openBtn.Text = "🌊 Show"
        openBtn.BackgroundColor3 = Color3.new(0.2, 0.8, 0.3)
    end
end)

closeBtn.MouseButton1Click:Connect(function()
    main.Visible = false
    openBtn.Text = "🌊 Show"
    openBtn.BackgroundColor3 = Color3.new(0.2, 0.8, 0.3)
end)

-- SISTEMA DE NOCLIP
game:GetService("RunService").Stepped:Connect(function()
    if noclipEnabled then
        pcall(function()
            local char = getChar()
            for _, v in pairs(char:GetDescendants()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end
            end
        end)
    end
end)

print("✅ TSUNAMI SAFE ZONE CARREGADO!")
