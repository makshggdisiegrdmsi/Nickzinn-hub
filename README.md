local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "NickzinBrainrotHub"
ScreenGui.Parent = game.CoreGui

local function makeRounded(frame, radius)
    local corner = Instance.new("UICorner")
    corner.CornerRadius = radius
    corner.Parent = frame
end

-- Botão ÚNICO Nickzin Hub 😈
local nickzinButton = Instance.new("TextButton")
nickzinButton.Size = UDim2.new(0, 180, 0, 45)
nickzinButton.Position = UDim2.new(0, 10, 0, 10)
nickzinButton.BackgroundColor3 = Color3.fromRGB(120, 20, 120)
nickzinButton.BorderSizePixel = 0
nickzinButton.Text = "Nickzin Hub 😈"
nickzinButton.Font = Enum.Font.GothamBold
nickzinButton.TextSize = 22
nickzinButton.TextColor3 = Color3.fromRGB(255,255,255)
nickzinButton.Parent = ScreenGui
makeRounded(nickzinButton, UDim.new(0, 10))

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 370, 0, 430)
MainFrame.Position = UDim2.new(0.5, -185, 0.5, -215)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
MainFrame.Visible = false
MainFrame.Parent = ScreenGui
makeRounded(MainFrame, UDim.new(0, 14))
MainFrame.BorderSizePixel = 0

local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, -20, 0, 40)
titleLabel.Position = UDim2.new(0, 10, 0, 10)
titleLabel.BackgroundTransparency = 1
titleLabel.TextColor3 = Color3.fromRGB(230, 0, 230)
titleLabel.Font = Enum.Font.GothamBold
titleLabel.TextSize = 22
titleLabel.Text = "Nickzin Brainrot Hub v2.0"
titleLabel.TextXAlignment = Enum.TextXAlignment.Left
titleLabel.Parent = MainFrame

local emojiLabel = Instance.new("TextLabel")
emojiLabel.Size = UDim2.new(0, 30, 0, 30)
emojiLabel.Position = UDim2.new(0, 10, 0, 50)
emojiLabel.BackgroundTransparency = 1
emojiLabel.TextColor3 = Color3.fromRGB(230, 0, 230)
emojiLabel.Font = Enum.Font.GothamBold
emojiLabel.TextSize = 26
emojiLabel.Text = "😈"
emojiLabel.Parent = MainFrame

local tabsFrame = Instance.new("Frame")
tabsFrame.Size = UDim2.new(1, -20, 0, 37)
tabsFrame.Position = UDim2.new(0, 10, 0, 85)
tabsFrame.BackgroundTransparency = 1
tabsFrame.Parent = MainFrame

local tabsNames = {"🧠 Cheats", "👁 Visual", "☠️ Troll", "⚙ Configs", "Steal🎯"}
local tabsButtons = {}
local tabsContentFrames = {}

local selectedTab = nil
local function createTab(name, index)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 70, 1, 0)
    btn.Position = UDim2.new(0, (index - 1) * 75, 0, 0)
    btn.BackgroundColor3 = Color3.fromRGB(80, 0, 130)
    btn.BorderSizePixel = 0
    btn.Text = name
    btn.TextColor3 = Color3.fromRGB(230, 230, 230)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 14
    btn.Parent = tabsFrame
    makeRounded(btn, UDim.new(0, 6))

    local contentFrame = Instance.new("ScrollingFrame")
    contentFrame.Size = UDim2.new(1, -20, 1, -140)
    contentFrame.Position = UDim2.new(0, 10, 0, 128)
    contentFrame.BackgroundTransparency = 1
    contentFrame.ScrollBarThickness = 6
    contentFrame.CanvasSize = UDim2.new(0, 0, 2, 0)
    contentFrame.Parent = MainFrame
    contentFrame.Visible = false

    btn.MouseButton1Click:Connect(function()
        for _, b in pairs(tabsButtons) do
            b.BackgroundColor3 = Color3.fromRGB(80, 0, 130)
        end
        for _, f in pairs(tabsContentFrames) do
            f.Visible = false
        end
        btn.BackgroundColor3 = Color3.fromRGB(200, 0, 200)
        contentFrame.Visible = true
        selectedTab = name
    end)

    tabsButtons[index] = btn
    tabsContentFrames[index] = contentFrame
    return contentFrame
end

local cheatsFrame = createTab(tabsNames[1], 1)
local visualFrame = createTab(tabsNames[2], 2)
local trollFrame = createTab(tabsNames[3], 3)
local configFrame = createTab(tabsNames[4], 4)
local stealFrame = createTab(tabsNames[5], 5)

tabsButtons[1].BackgroundColor3 = Color3.fromRGB(200, 0, 200)
tabsContentFrames[1].Visible = true
selectedTab = tabsNames[1]

local function createFunctionalToggle(text, emoji, parent, posY, onToggle)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 0, 28)
    frame.Position = UDim2.new(0, 0, 0, posY)
    frame.BackgroundTransparency = 1
    frame.Parent = parent

    local label = Instance.new("TextLabel")
    label.Text = emoji .. " | " .. text
    label.TextColor3 = Color3.fromRGB(230, 230, 230)
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0, 5, 0, 0)
    label.Size = UDim2.new(1, -40, 1, 0)
    label.Font = Enum.Font.GothamBold
    label.TextSize = 16
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = frame

    local toggleBtn = Instance.new("TextButton")
    toggleBtn.Size = UDim2.new(0, 32, 0, 22)
    toggleBtn.Position = UDim2.new(1, -35, 0, 3)
    toggleBtn.BackgroundColor3 = Color3.fromRGB(80, 0, 130)
    toggleBtn.BorderSizePixel = 0
    toggleBtn.Text = ""
    toggleBtn.Parent = frame
    toggleBtn.AutoButtonColor = false
    toggleBtn.ZIndex = 5
    makeRounded(toggleBtn, UDim.new(0,6))

    local toggled = false
    local function update()
        if toggled then
            toggleBtn.BackgroundColor3 = Color3.fromRGB(200, 0, 200)
            toggleBtn.Text = "✔"
            toggleBtn.TextColor3 = Color3.fromRGB(255,255,255)
        else
            toggleBtn.BackgroundColor3 = Color3.fromRGB(80, 0, 130)
            toggleBtn.Text = ""
        end
    end
    update()

    toggleBtn.MouseButton1Click:Connect(function()
        toggled = not toggled
        update()
        onToggle(toggled)
    end)

    return frame
end

-- Funções Steal🎯
local floatConnection = nil
local infiniteJumpConnection = nil

local function stealTpBase()
    print("Tp base: Pegando brainrot, ignorando trancas, teleportando para o spawn!")
    -- Adapte para seu jogo!
end

local function stealFloat(state)
    if state then
        print("Float ativado: Flutuando 1 metro acima e movendo na direção da câmera!")
        if floatConnection then floatConnection:Disconnect() end
        floatConnection = game:GetService("RunService").RenderStepped:Connect(function()
            local char = LocalPlayer.Character
            if char and char:FindFirstChild("HumanoidRootPart") then
                local cam = workspace.CurrentCamera
                local root = char.HumanoidRootPart
                local dir = cam.CFrame.LookVector
                root.Velocity = Vector3.new(dir.X*16, 6, dir.Z*16)
            end
        end)
    else
        print("Float desativado!")
        if floatConnection then floatConnection:Disconnect(); floatConnection = nil end
        local char = LocalPlayer.Character
        if char and char:FindFirstChild("HumanoidRootPart") then
            char.HumanoidRootPart.Velocity = Vector3.new(0,0,0)
        end
    end
end

local function stealInfiniteJump(state)
    if state then
        print("Infinite Jump ativado!")
        if infiniteJumpConnection then infiniteJumpConnection:Disconnect() end
        infiniteJumpConnection = UserInputService.JumpRequest:Connect(function()
            local humanoid = LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            if humanoid then
                humanoid:ChangeState("Jumping")
            end
        end)
    else
        print("Infinite Jump desativado!")
        if infiniteJumpConnection then infiniteJumpConnection:Disconnect(); infiniteJumpConnection = nil end
    end
end

local function ativarFuncao(nomeFuncao, estado)
    print(nomeFuncao .. " agora está " .. (estado and "ATIVADO" or "DESATIVADO"))
    if nomeFuncao == "TpBase" then
        if estado then stealTpBase() end
    elseif nomeFuncao == "Float" then
        stealFloat(estado)
    elseif nomeFuncao == "InfiniteJump" then
        stealInfiniteJump(estado)
    end
    -- Adicione a lógica dos outros comandos do seu jogo aqui
end

local function addToggle(tabFrame, emoji, text, posY, funcName)
    return createFunctionalToggle(text, emoji, tabFrame, posY, function(state)
        ativarFuncao(funcName, state)
    end)
end

-- Cheats 🧠
local yPos = 0
addToggle(cheatsFrame, "🧠", "Auto-Kill & Loop de Kill", yPos, "AutoKill"); yPos = yPos + 32
addToggle(cheatsFrame, "🔪", "Massacre Coletivo", yPos, "MassacreColetivo"); yPos = yPos + 32
addToggle(cheatsFrame, "🌾", "Auto-Farm de Regiões", yPos, "AutoFarm"); yPos = yPos + 32
addToggle(cheatsFrame, "🧲", "Magnet Global", yPos, "MagnetGlobal"); yPos = yPos + 32
addToggle(cheatsFrame, "⚔️", "Auto-Equip / Auto-Use", yPos, "AutoEquipUse"); yPos = yPos + 32
addToggle(cheatsFrame, "🦅", "Fly + Super Speed + Noclip", yPos, "FlySuperSpeedNoclip"); yPos = yPos + 32
addToggle(cheatsFrame, "📡", "Teleport Inteligente", yPos, "TeleportInteligente"); yPos = yPos + 32
addToggle(cheatsFrame, "⬆️", "Subida Aérea Estratégica", yPos, "SubidaAerea"); yPos = yPos + 32

-- Visual 👁
yPos = 0
addToggle(visualFrame, "🔍", "ESP Avançado com Filtros", yPos, "ESPAvancado"); yPos = yPos + 32
addToggle(visualFrame, "🎮", "Controle de Player (Possessão)", yPos, "ControlePlayer"); yPos = yPos + 32
addToggle(visualFrame, "📷", "Modo Câmera Livre", yPos, "CameraLivre"); yPos = yPos + 32
addToggle(visualFrame, "✨", "Highlight de Objetos Customizável", yPos, "HighlightObjetos"); yPos = yPos + 32

-- Troll ☠️
yPos = 0
addToggle(trollFrame, "💀", "GodMode+", yPos, "GodMode"); yPos = yPos + 32
addToggle(trollFrame, "👻", "Modo Sombra", yPos, "ModoSombra"); yPos = yPos + 32
addToggle(trollFrame, "🥷", "Silent Kill", yPos, "SilentKill"); yPos = yPos + 32
addToggle(trollFrame, "🔒", "Player Lock", yPos, "PlayerLock"); yPos = yPos + 32
addToggle(trollFrame, "💬", "Auto-Provocação", yPos, "AutoProvocacao"); yPos = yPos + 32

-- Configs ⚙
yPos = 0
addToggle(configFrame, "🌀", "Slow-Mo Mode", yPos, "SlowMoMode"); yPos = yPos + 32
addToggle(configFrame, "📉", "Dark UI (Modo Corrompido)", yPos, "DarkUI"); yPos = yPos + 32
addToggle(configFrame, "📡", "Interceptor de Chat", yPos, "InterceptorChat"); yPos = yPos + 32
addToggle(configFrame, "🛑", "Block All Reports", yPos, "BlockAllReports"); yPos = yPos + 32
addToggle(configFrame, "📲", "Webhook Mode", yPos, "WebhookMode"); yPos = yPos + 32

-- Steal🎯
yPos = 0
addToggle(stealFrame, "🎯", "Tp base", yPos, "TpBase"); yPos = yPos + 32
addToggle(stealFrame, "🎯", "Float", yPos, "Float"); yPos = yPos + 32
addToggle(stealFrame, "🎯", "Infinite Jump", yPos, "InfiniteJump"); yPos = yPos + 32

-- Movimentação da UI
local function makeMovable(guiObject)
    local dragging = false
    local dragInput
    local dragStart
    local startPos

    guiObject.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            dragStart = input.Position
            startPos = guiObject.Position

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    guiObject.InputChanged:Connect(function(input)
        if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
            dragInput = input
        end
    end)

    UserInputService.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            guiObject.Position = UDim2.new(
                startPos.X.Scale,
                startPos.X.Offset + delta.X,
                startPos.Y.Scale,
                startPos.Y.Offset + delta.Y
            )
        end
    end)
end

makeMovable(MainFrame)

nickzinButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)# Nickzinn-hub
