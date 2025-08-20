--// Super Pulo v1.0
-- Local Script (funciona em todos executores)

-- Criar ScreenGui
local gui = Instance.new("ScreenGui")
gui.Name = "SuperPuloGui"
pcall(function()
    gui.Parent = game:GetService("CoreGui")
end)

-- Variável de toggle
local aberto = true

-- Botão Bola 🛸
local toggle = Instance.new("TextButton")
toggle.Parent = gui
toggle.Size = UDim2.new(0,50,0,50)
toggle.Position = UDim2.new(0,20,0.5,-25)
toggle.BackgroundColor3 = Color3.fromRGB(0,0,0)
toggle.Text = "🛸"
toggle.TextSize = 28
toggle.TextColor3 = Color3.fromRGB(255,255,255)
toggle.Font = Enum.Font.SourceSansBold
toggle.BorderSizePixel = 2
toggle.BorderColor3 = Color3.fromRGB(0,170,255)

local cornerT = Instance.new("UICorner",toggle)
cornerT.CornerRadius = UDim.new(1,0)

-- Frame Principal
local main = Instance.new("Frame", gui)
main.Size = UDim2.new(0,300,0,180)
main.Position = UDim2.new(0.5,-150,0.5,-90)
main.BackgroundColor3 = Color3.fromRGB(0,170,255)
main.Visible = true

local cornerM = Instance.new("UICorner",main)
cornerM.CornerRadius = UDim.new(0,15)

-- Gradient animado
local gradient = Instance.new("UIGradient", main)
gradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(0,255,255)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(0,0,255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(0,0,139))
}

task.spawn(function()
    while task.wait(0.05) do
        gradient.Rotation = (gradient.Rotation + 1) % 360
    end
end)

-- Título
local title = Instance.new("TextLabel", main)
title.Size = UDim2.new(1,0,0,40)
title.BackgroundTransparency = 1
title.Text = "super pulo v1.0"
title.TextColor3 = Color3.fromRGB(255,255,255)
title.Font = Enum.Font.Fantasy
title.TextSize = 26
title.TextStrokeTransparency = 0
title.TextStrokeColor3 = Color3.fromRGB(0,0,0)

-- Caixa de texto
local jumpBox = Instance.new("TextBox", main)
jumpBox.Size = UDim2.new(0.8,0,0,40)
jumpBox.Position = UDim2.new(0.1,0,0.5,-20)
jumpBox.PlaceholderText = "Força do pulo"
jumpBox.Text = ""
jumpBox.Font = Enum.Font.SourceSansBold
jumpBox.TextSize = 18
jumpBox.TextColor3 = Color3.fromRGB(0,0,0)
jumpBox.BackgroundColor3 = Color3.fromRGB(255,255,255)

local cornerB = Instance.new("UICorner", jumpBox)
cornerB.CornerRadius = UDim.new(0,10)

-- Botão aplicar
local apply = Instance.new("TextButton", main)
apply.Size = UDim2.new(0.5,0,0,40)
apply.Position = UDim2.new(0.25,0,0.8,-20)
apply.BackgroundColor3 = Color3.fromRGB(0,0,0)
apply.Text = "Aplicar Pulo"
apply.TextSize = 20
apply.TextColor3 = Color3.fromRGB(255,255,255)
apply.Font = Enum.Font.SourceSansBold

local cornerA = Instance.new("UICorner", apply)
cornerA.CornerRadius = UDim.new(0,10)

-- Aplicar força do pulo
apply.MouseButton1Click:Connect(function()
    local val = tonumber(jumpBox.Text)
    local hum = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if val and hum then
        hum.UseJumpPower = true
        hum.JumpPower = val
    end
end)

-- Abrir/Fechar
toggle.MouseButton1Click:Connect(function()
    aberto = not aberto
    main.Visible = aberto
end)
