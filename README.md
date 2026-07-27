-- =============================================================================
--    HERMANOS CP v5.4 ULTRA-LIGHT & OPTIMIZED (INSTANT TOGGLE VERSION - UNLOCKED)
--    Binds Teclado: Z = Menú | F = Aim | X = Inv View
--    Binds Mando (Gamepad): L2 / LT = Apuntar Rápido | DPadDown = Toggle Aim
-- =============================================================================

-- ==================== LOCALIZACIÓN DE GLOBALES (OPTIMIZACIÓN VM) ====================
local game = game
local workspace = workspace
local type = type
local typeof = typeof
local pcall = pcall
local print = print
local task = task
local string = string
local math = math
local table = table
local pairs = pairs
local ipairs = ipairs
local tonumber = tonumber
local tostring = tostring
local tick = tick
local Color3 = Color3
local Vector3 = Vector3
local Vector2 = Vector2
local UDim2 = UDim2
local UDim = UDim
local Enum = Enum
local CFrame = CFrame
local Instance = Instance
local ColorSequence = ColorSequence
local ColorSequenceKeypoint = ColorSequenceKeypoint
local TweenInfo = TweenInfo

-- ==================== SERVICIOS REALES ====================
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local StarterPack = game:GetService("StarterPack")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

-- [[ HCP LANG START ]]
local _HCP_LANG = (type(_G) == "table" and _G.HCP_LANG) or nil
if not _HCP_LANG then
    local lp = game:GetService("Players").LocalPlayer
    local loc = (lp and lp.LocaleId and lp.LocaleId:lower()) or "es"
    _HCP_LANG = loc:match("^es") and "es" or "en"
end
local _L = (_HCP_LANG == "en") and {
    title = "HERMANOS CP v5.4 // EVOLUTION LIGHT",
    tabMain = "MAIN",
    tabCfg = "SETTINGS",
    aimbot = "AIMBOT",
    esp = "ESP VISUALS",
    inv = "INV VIEW",
    cfgSys = "CONFIGURATION SYSTEM (FILES)",
    saveCfg = "SAVE CONFIG",
    loadCfg = "LOAD CONFIG",
    aimMode = "AIM MODE",
    fovSize = "FOV SIZE / CIRCLE (DRAG)",
    smooth = "SMOOTH AIM (CONTROLLER / FOV)",
    target = "AIM TARGET",
    binds = "KEYBINDS (CLICK TO CHANGE)",
    modeToggle = "Key Toggle",
    modeFov = "FOV Circle",
    modeHold = "Controller",
    head = "Head",
    chest = "Chest",
    mixed = "Mixed",
    low = "Low",
    mid = "Medium",
    high = "High",
} or {
    title = "HERMANOS CP v5.4 // EVOLUTION LIGHT",
    tabMain = "PRINCIPAL",
    tabCfg = "CONFIG",
    aimbot = "AIMBOT",
    esp = "ESP VISUALS",
    inv = "INV VIEW",
    cfgSys = "SISTEMA DE CONFIG (ARCHIVOS)",
    saveCfg = "GUARDAR",
    loadCfg = "CARGAR",
    aimMode = "MODO DE AIM",
    fovSize = "TAMANO FOV / BOLITA (ARRASTRA)",
    smooth = "AIMBOT SUAVE (MANDO / FOV)",
    target = "OBJETIVO DE AIM",
    binds = "BINDS DE TECLAS (CLIC PARA CAMBIAR)",
    modeToggle = "Aim Tecla",
    modeFov = "Aim Bolita",
    modeHold = "Aim Mando",
    head = "Cabeza",
    chest = "Pecho",
    mixed = "Mixto",
    low = "Bajo",
    mid = "Medio",
    high = "Alto",
}
-- [[ HCP LANG END ]]

local CoreGuiService = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local HttpService = game:GetService("HttpService")

-- ==================== RESOLUCIÓN SEGURA DE APIs DEL EXECUTOR ====================
local function getExecutorGlobal(name)
    local genv = (type(getgenv) == "function" and getgenv()) or {}
    local fenv = (type(getfenv) == "function" and getfenv()) or {}
    local success, val = pcall(function()
        return genv[name] or fenv[name] or _G[name]
    end)
    return success and val or nil
end

local cloneref = getExecutorGlobal("cloneref")
local Drawing = getExecutorGlobal("Drawing")
local writefile = getExecutorGlobal("writefile")
local readfile = getExecutorGlobal("readfile")
local isfile = getExecutorGlobal("isfile")

while not Players.LocalPlayer do
    task.wait(0.1)
end
local LocalPlayer = Players.LocalPlayer

-- ==================== VARIABLES CENTRALES ====================
local Camera = workspace.CurrentCamera or workspace:WaitForChild("Camera")
local CONFIG_FILE = "HermanosCP_Clean_Config.json"

local saveConfiguration
local loadConfiguration
local targetController
local smoothController
local modeController

-- ==================== CONFIGURACIÓN CENTRALIZADA ====================
local Config = {
    Theme = {
        Background      = Color3.fromRGB(11, 11, 18),
        Header          = Color3.fromRGB(16, 16, 26),
        Stroke          = Color3.fromRGB(0, 210, 255),
        StrokeInactive  = Color3.fromRGB(30, 30, 45),
        GradientStart   = Color3.fromRGB(18, 11, 32),
        GradientEnd     = Color3.fromRGB(7, 7, 12),
        PlayerRow       = Color3.fromRGB(20, 20, 30),
        PlayerRowPinned = Color3.fromRGB(38, 22, 58),
        TextPrimary     = Color3.fromRGB(255, 255, 255),
        TextSecondary   = Color3.fromRGB(160, 175, 210),
        PinActive       = Color3.fromRGB(0, 210, 255),
        PinInactive     = Color3.fromRGB(35, 35, 50),
        TeamActive      = Color3.fromRGB(0, 255, 140),
        EspNormal       = Color3.fromRGB(0, 210, 255),
        EspPinned       = Color3.fromRGB(255, 200, 0),
        EspTeam         = Color3.fromRGB(0, 255, 140), 
        AuraFill        = Color3.fromRGB(0, 210, 255),
        AuraTeamFill    = Color3.fromRGB(0, 255, 100), 
        AuraOutline     = Color3.fromRGB(255, 255, 255),
        BtnOn           = Color3.fromRGB(0, 255, 140),
        BtnOff          = Color3.fromRGB(255, 65, 95),
        CloseBtn        = Color3.fromRGB(35, 18, 26),
        CloseBtnText    = Color3.fromRGB(255, 80, 100),
        ScrollBar       = Color3.fromRGB(0, 210, 255),
        TabActive       = Color3.fromRGB(0, 210, 255),
        TabInactive     = Color3.fromRGB(22, 22, 35),
        Gold            = Color3.fromRGB(255, 215, 0),
        FOVNormal       = Color3.fromRGB(0, 210, 255),
        FOVLocked       = Color3.fromRGB(255, 65, 95)
    },
    Binds = {
        ToggleMenu = Enum.KeyCode.Z,
        Aimbot = Enum.KeyCode.F,
        InvView = Enum.KeyCode.X,
        GamepadAim = Enum.KeyCode.ButtonL2,
        GamepadToggle = Enum.KeyCode.DPadDown
    },
    AimTarget = "Cabeza", 
    AimSmooth = "Medio",
    AimMode   = "FOV", 
    AimFOV    = 220,   
    ShowFOV   = true,
    VehicleCameraFix = true,
    AimOrigin = "Cámara",
    AutoExecute = false
}

-- ==================== ESTADO DEL SISTEMA ====================
local State = {
    aimEnabled = true,
    espEnabled = true,
    invViewEnabled = true,
    holdingAimTrigger = false,
    lockedTarget = nil,
    pinnedPlayers = {},
    autoPinned = {},
    teamPlayers = {}, 
    connections = {},
    alive = true,
    isBinding = nil, 
    currentTab = "Principal"
}

local MasterObjects = {}
local LastInventoryState = {}
local ToolNameCache = {}
local PlayerRowCache = {}
local LastToolScan = {}

-- ==================== UTILIDADES GLOBALES ====================
local function safeConnect(signal, callback)
    local conn = signal:Connect(callback)
    table.insert(State.connections, conn)
    return conn
end

local nameCounter = 0
local function generateName()
    nameCounter = nameCounter + 1
    return string.char(math.random(65, 90)) .. string.char(math.random(97, 122)) .. tostring(math.random(100, 999)) .. tostring(nameCounter)
end

local function getSafeGuiParent()
    local success, parent = pcall(function()
        local target = (type(cloneref) == "function" and cloneref(CoreGuiService)) or CoreGuiService
        local testGui = Instance.new("ScreenGui")
        testGui.Parent = target
        testGui:Destroy()
        return target
    end)
    if success and parent then return parent end
    
    local playerGui = LocalPlayer:FindFirstChildOfClass("PlayerGui")
    if playerGui then return playerGui end
    
    return LocalPlayer:WaitForChild("PlayerGui", 5) or CoreGuiService
end

safeConnect(workspace:GetPropertyChangedSignal("CurrentCamera"), function()
    Camera = workspace.CurrentCamera or Camera
end)

local function fixCameraAndOffset()
    if not Config.VehicleCameraFix then return end
    local char = LocalPlayer.Character
    if not char then return end
    
    local hum = char:FindFirstChildOfClass("Humanoid")
    if hum then
        if hum.CameraOffset ~= Vector3.zero then hum.CameraOffset = Vector3.zero end
        if Camera.CameraSubject ~= hum then Camera.CameraSubject = hum end
    end
    if Camera.CameraType ~= Enum.CameraType.Custom then Camera.CameraType = Enum.CameraType.Custom end
end

safeConnect(Camera:GetPropertyChangedSignal("CameraSubject"), function() task.spawn(fixCameraAndOffset) end)
safeConnect(Camera:GetPropertyChangedSignal("CameraType"), function() task.spawn(fixCameraAndOffset) end)

local humanoidConnection
local function connectHumanoid(hum)
    if humanoidConnection then humanoidConnection:Disconnect() end
    humanoidConnection = hum:GetPropertyChangedSignal("CameraOffset"):Connect(function()
        if Config.VehicleCameraFix and hum.CameraOffset ~= Vector3.zero then
            hum.CameraOffset = Vector3.zero
        end
    end)
    table.insert(State.connections, humanoidConnection)
end

safeConnect(LocalPlayer.CharacterAdded, function(char)
    local hum = char:WaitForChild("Humanoid", 5)
    if hum then connectHumanoid(hum) end
    task.spawn(fixCameraAndOffset)
end)

if LocalPlayer.Character then
    local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if hum then connectHumanoid(hum) end
end

local function checkAndAutoTeam(player)
    if player == LocalPlayer then return end
    task.spawn(function()
        local success, isFriend = pcall(function() return LocalPlayer:IsFriendsWith(player.UserId) end)
        if success and isFriend then
            State.teamPlayers[player.Name] = true
            if State.lockedTarget == player then State.lockedTarget = nil end
        end
    end)
end

-- ==================== INTERFAZ MENÚ POLISHED ====================
local gui = Instance.new("ScreenGui")
gui.Name = generateName()
gui.IgnoreGuiInset = true
gui.ResetOnSpawn = false
gui.Parent = getSafeGuiParent()

-- Tamaño adaptable (celular mas compacto)
local cam = workspace.CurrentCamera
local vw = (cam and cam.ViewportSize.X) or 800
local vh = (cam and cam.ViewportSize.Y) or 600
local isMobileUI = UserInputService.TouchEnabled and (not UserInputService.KeyboardEnabled or vw < 700)
local frameW = isMobileUI and math.clamp(math.floor(vw * 0.92), 280, 380) or 460
local frameH = isMobileUI and math.clamp(math.floor(vh * 0.72), 380, 480) or 520

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, frameW, 0, frameH)
MainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
MainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
MainFrame.BackgroundColor3 = Config.Theme.Background
MainFrame.ClipsDescendants = true
MainFrame.Parent = gui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 12)
mainCorner.Parent = MainFrame

local mainStroke = Instance.new("UIStroke")
mainStroke.Color = Config.Theme.Stroke
mainStroke.Thickness = 1.2
mainStroke.Parent = MainFrame

local gradient = Instance.new("UIGradient")
gradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Config.Theme.GradientStart),
    ColorSequenceKeypoint.new(1, Config.Theme.GradientEnd),
})
gradient.Parent = MainFrame

local header = Instance.new("Frame")
header.Size = UDim2.new(1, 0, 0, 45)
header.BackgroundColor3 = Config.Theme.Header
header.Parent = MainFrame

local headerCorner = Instance.new("UICorner")
headerCorner.CornerRadius = UDim.new(0, 12)
headerCorner.Parent = header

local title = Instance.new("TextLabel")
title.Font = Enum.Font.GothamBold
title.TextSize = 13
title.TextColor3 = Config.Theme.TextPrimary
title.Size = UDim2.new(1, -80, 1, 0)
title.Position = UDim2.new(0, 15, 0, 0)
title.BackgroundTransparency = 1
title.Text = _L.title
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = header

-- Boton minimizar (-)
local minBtn = Instance.new("TextButton")
minBtn.Size = UDim2.new(0, 28, 0, 28)
minBtn.Position = UDim2.new(1, -70, 0.5, -14)
minBtn.Text = "−"
minBtn.TextSize = 18
minBtn.Font = Enum.Font.GothamBold
minBtn.TextColor3 = Color3.fromRGB(255, 210, 80)
minBtn.BackgroundColor3 = Color3.fromRGB(40, 35, 18)
minBtn.Parent = header
local minBtnCorner = Instance.new("UICorner")
minBtnCorner.CornerRadius = UDim.new(0, 6)
minBtnCorner.Parent = minBtn
local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 28, 0, 28)
closeBtn.Position = UDim2.new(1, -38, 0.5, -14)
closeBtn.Text = "×"
closeBtn.TextSize = 18
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextColor3 = Config.Theme.CloseBtnText
closeBtn.BackgroundColor3 = Config.Theme.CloseBtn
closeBtn.Parent = header

local closeBtnCorner = Instance.new("UICorner")
closeBtnCorner.CornerRadius = UDim.new(0, 6)
closeBtnCorner.Parent = closeBtn

closeBtn.MouseEnter:Connect(function()
    TweenService:Create(closeBtn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(80, 25, 40)}):Play()
end)
closeBtn.MouseLeave:Connect(function()
    TweenService:Create(closeBtn, TweenInfo.new(0.15), {BackgroundColor3 = Config.Theme.CloseBtn}):Play()
end)

-- Bolita flotante para reabrir el menu (movil o siempre disponible)
local openBall = Instance.new("ImageButton")
openBall.Name = "HCPOpenBall"
openBall.Size = UDim2.new(0, 50, 0, 50)
openBall.Position = UDim2.new(1, -64, 0.55, 0)
openBall.BackgroundColor3 = Color3.fromRGB(0, 160, 255)
openBall.BorderSizePixel = 0
openBall.Visible = false
openBall.AutoButtonColor = false
openBall.Parent = gui
local openBallCorner = Instance.new("UICorner")
openBallCorner.CornerRadius = UDim.new(1, 0)
openBallCorner.Parent = openBall
local openBallStroke = Instance.new("UIStroke")
openBallStroke.Color = Color3.fromRGB(255, 255, 255)
openBallStroke.Thickness = 2
openBallStroke.Transparency = 0.35
openBallStroke.Parent = openBall
local openBallTxt = Instance.new("TextLabel")
openBallTxt.Size = UDim2.new(1, 0, 1, 0)
openBallTxt.BackgroundTransparency = 1
openBallTxt.Font = Enum.Font.GothamBold
openBallTxt.TextSize = 12
openBallTxt.TextColor3 = Color3.fromRGB(255, 255, 255)
openBallTxt.Text = "HCP"
openBallTxt.Parent = openBall

local ballDrag, ballStart, ballPos
openBall.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
        ballDrag = true
        ballStart = input.Position
        ballPos = openBall.Position
    end
end)
safeConnect(UserInputService.InputChanged, function(input)
    if ballDrag and (input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseMovement) then
        local d = input.Position - ballStart
        openBall.Position = UDim2.new(ballPos.X.Scale, ballPos.X.Offset + d.X, ballPos.Y.Scale, ballPos.Y.Offset + d.Y)
    end
end)
safeConnect(UserInputService.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
        ballDrag = false
    end
end)

openBall.MouseButton1Click:Connect(function()
    MainFrame.Visible = true
    openBall.Visible = false
end)

-- Al minimizar: mostrar bolita
minBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
    openBall.Visible = true
end)

-- PANEL DE PESTAÑAS
local TabBar = Instance.new("Frame")
TabBar.Size = UDim2.new(1, -20, 0, 34)
TabBar.Position = UDim2.new(0, 10, 0, 55)
TabBar.BackgroundTransparency = 1
TabBar.Parent = MainFrame

local tabLayout = Instance.new("UIListLayout")
tabLayout.FillDirection = Enum.FillDirection.Horizontal
tabLayout.Padding = UDim.new(0, 8)
tabLayout.Parent = TabBar

local function createTabButton(text, parent)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.5, -4, 1, 0)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 11
    btn.Text = text
    btn.TextColor3 = Config.Theme.TextPrimary
    btn.BackgroundColor3 = Config.Theme.TabInactive
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 6)
    corner.Parent = btn
    
    local stroke = Instance.new("UIStroke")
    stroke.Thickness = 1
    stroke.Color = Config.Theme.StrokeInactive
    stroke.Parent = btn
    
    btn.Parent = parent
    return btn, stroke
end

local TabPrincipalBtn, tabPStroke = createTabButton(_L.tabMain, TabBar)
local TabConfigBtn, tabCStroke = createTabButton("⚙️ " .. _L.tabCfg, TabBar)

local ContentPrincipal = Instance.new("Frame")
ContentPrincipal.Size = UDim2.new(1, -20, 1, -105)
ContentPrincipal.Position = UDim2.new(0, 10, 0, 100)
ContentPrincipal.BackgroundTransparency = 1
ContentPrincipal.Parent = MainFrame

local ContentConfig = Instance.new("ScrollingFrame")
ContentConfig.Size = UDim2.new(1, -20, 1, -105)
ContentConfig.Position = UDim2.new(0, 10, 0, 100)
ContentConfig.BackgroundTransparency = 1
ContentConfig.Visible = false
ContentConfig.AutomaticCanvasSize = Enum.AutomaticSize.Y
ContentConfig.ScrollBarThickness = 2
ContentConfig.ScrollBarImageColor3 = Config.Theme.ScrollBar
ContentConfig.Parent = MainFrame

local function switchTab(tabName)
    State.currentTab = tabName
    local tInfo = TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    
    if tabName == "Principal" then
        TweenService:Create(TabPrincipalBtn, tInfo, {BackgroundColor3 = Config.Theme.TabActive}):Play()
        TweenService:Create(TabConfigBtn, tInfo, {BackgroundColor3 = Config.Theme.TabInactive}):Play()
        TweenService:Create(tabPStroke, tInfo, {Color = Config.Theme.TabActive}):Play()
        TweenService:Create(tabCStroke, tInfo, {Color = Config.Theme.StrokeInactive}):Play()
        TabPrincipalBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
        TabConfigBtn.TextColor3 = Config.Theme.TextPrimary
        ContentPrincipal.Visible = true
        ContentConfig.Visible = false
    else
        TweenService:Create(TabPrincipalBtn, tInfo, {BackgroundColor3 = Config.Theme.TabInactive}):Play()
        TweenService:Create(TabConfigBtn, tInfo, {BackgroundColor3 = Config.Theme.TabActive}):Play()
        TweenService:Create(tabPStroke, tInfo, {Color = Config.Theme.StrokeInactive}):Play()
        TweenService:Create(tabCStroke, tInfo, {Color = Config.Theme.TabActive}):Play()
        TabPrincipalBtn.TextColor3 = Config.Theme.TextPrimary
        TabConfigBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
        ContentPrincipal.Visible = false
        ContentConfig.Visible = true
    end
end
switchTab("Principal")

local function addTabHover(btn, stroke, tabName)
    btn.MouseEnter:Connect(function()
        if State.currentTab ~= tabName then
            TweenService:Create(btn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(28, 28, 42)}):Play()
            TweenService:Create(stroke, TweenInfo.new(0.15), {Color = Color3.fromRGB(60, 60, 85)}):Play()
        end
    end)
    btn.MouseLeave:Connect(function()
        if State.currentTab ~= tabName then
            TweenService:Create(btn, TweenInfo.new(0.15), {BackgroundColor3 = Config.Theme.TabInactive}):Play()
            TweenService:Create(stroke, TweenInfo.new(0.15), {Color = Config.Theme.StrokeInactive}):Play()
        end
    end)
end
addTabHover(TabPrincipalBtn, tabPStroke, "Principal")
addTabHover(TabConfigBtn, tabCStroke, "Config")

TabPrincipalBtn.MouseButton1Click:Connect(function() switchTab("Principal") end)
TabConfigBtn.MouseButton1Click:Connect(function() switchTab("Config") end)

-- PANEL DE BOTONES PRINCIPALES
local TogglePanel = Instance.new("Frame")
TogglePanel.Size = UDim2.new(1, 0, 0, 35)
TogglePanel.Position = UDim2.new(0, 0, 0, 0)
TogglePanel.BackgroundTransparency = 1
TogglePanel.Parent = ContentPrincipal

local grid = Instance.new("UIGridLayout")
grid.CellSize = UDim2.new(0.32, 0, 0, 32)
grid.CellPadding = UDim2.new(0, 6, 0, 6)
grid.Parent = TogglePanel

local function createToggleButton(parent, text)
    local btn = Instance.new("TextButton")
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 10
    btn.TextColor3 = Config.Theme.TextPrimary
    btn.Text = text
    
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 6)
    btnCorner.Parent = btn

    local btnStroke = Instance.new("UIStroke")
    btnStroke.Thickness = 1
    btnStroke.Color = Color3.fromRGB(255,255,255)
    btnStroke.Transparency = 0.85
    btnStroke.Parent = btn
    
    btn.MouseEnter:Connect(function()
        TweenService:Create(btnStroke, TweenInfo.new(0.15), {Transparency = 0.5}):Play()
    end)
    btn.MouseLeave:Connect(function()
        TweenService:Create(btnStroke, TweenInfo.new(0.15), {Transparency = 0.85}):Play()
    end)
    
    btn.Parent = parent
    return btn
end

local AimToggleBtn = createToggleButton(TogglePanel, _L.aimbot)
local EspToggleBtn = createToggleButton(TogglePanel, "ESP VISUALS")
local InvToggleBtn = createToggleButton(TogglePanel, "INV VIEW")

local scroll = Instance.new("ScrollingFrame")
scroll.Size = UDim2.new(1, 0, 1, -45)
scroll.Position = UDim2.new(0, 0, 0, 45)
scroll.BackgroundTransparency = 1
scroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
scroll.ScrollBarThickness = 3
scroll.ScrollBarImageColor3 = Config.Theme.ScrollBar
scroll.Parent = ContentPrincipal

local layout = Instance.new("UIListLayout")
layout.SortOrder = Enum.SortOrder.LayoutOrder
layout.Padding = UDim.new(0, 6)
layout.Parent = scroll

local function updateMainButtons()
    local tInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    
    TweenService:Create(AimToggleBtn, tInfo, {BackgroundColor3 = State.aimEnabled and Config.Theme.BtnOn or Config.Theme.BtnOff}):Play()
    AimToggleBtn.Text = "AIM: " .. (State.aimEnabled and "ON" or "OFF")
    AimToggleBtn.TextColor3 = State.aimEnabled and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary
    
    TweenService:Create(EspToggleBtn, tInfo, {BackgroundColor3 = State.espEnabled and Config.Theme.BtnOn or Config.Theme.BtnOff}):Play()
    EspToggleBtn.Text = "ESP: " .. (State.espEnabled and "ON" or "OFF")
    EspToggleBtn.TextColor3 = State.espEnabled and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary

    TweenService:Create(InvToggleBtn, tInfo, {BackgroundColor3 = State.invViewEnabled and Config.Theme.BtnOn or Config.Theme.BtnOff}):Play()
    InvToggleBtn.Text = "INV: " .. (State.invViewEnabled and "ON" or "OFF")
    InvToggleBtn.TextColor3 = State.invViewEnabled and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary

end
updateMainButtons()

AimToggleBtn.MouseButton1Click:Connect(function() 
    State.aimEnabled = not State.aimEnabled 
    if not State.aimEnabled then State.lockedTarget = nil end
    updateMainButtons() 
    saveConfiguration()
end)
EspToggleBtn.MouseButton1Click:Connect(function() 
    State.espEnabled = not State.espEnabled
    updateMainButtons() 
    saveConfiguration()
end)
InvToggleBtn.MouseButton1Click:Connect(function() 
    State.invViewEnabled = not State.invViewEnabled
    updateMainButtons() 
    saveConfiguration()
end)

-- ==================== CREADOR DE BOTÓN CÍCLICO INTELIGENTE ====================
local function createCycleConfigSection(titleText, buttonsData, callback)
    local sectionFrame = Instance.new("Frame")
    sectionFrame.Size = UDim2.new(1, 0, 0, 58)
    sectionFrame.BackgroundTransparency = 1
    
    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(1, 0, 0, 18)
    lbl.Font = Enum.Font.GothamBold
    lbl.TextSize = 11
    lbl.TextColor3 = Config.Theme.TextSecondary
    lbl.Text = titleText:upper()
    lbl.TextXAlignment = Enum.TextXAlignment.Left
    lbl.BackgroundTransparency = 1
    lbl.Parent = sectionFrame

    local cycleBtn = Instance.new("TextButton")
    cycleBtn.Size = UDim2.new(1, 0, 0, 32)
    cycleBtn.Position = UDim2.new(0, 0, 0, 22)
    cycleBtn.Font = Enum.Font.GothamBold
    cycleBtn.TextSize = 10
    cycleBtn.BackgroundColor3 = Config.Theme.TabInactive
    cycleBtn.TextColor3 = Config.Theme.TextPrimary
    
    local optCorner = Instance.new("UICorner")
    optCorner.CornerRadius = UDim.new(0, 6)
    optCorner.Parent = cycleBtn

    local optStroke = Instance.new("UIStroke")
    optStroke.Thickness = 1
    optStroke.Color = Config.Theme.StrokeInactive
    optStroke.Parent = cycleBtn

    local currentIndex = 1

    local function updateText()
        cycleBtn.Text = "►  " .. buttonsData[currentIndex].Label:upper() .. "  ◄"
    end

    cycleBtn.MouseEnter:Connect(function()
        TweenService:Create(cycleBtn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(28, 28, 42)}):Play()
    end)
    cycleBtn.MouseLeave:Connect(function()
        TweenService:Create(cycleBtn, TweenInfo.new(0.15), {BackgroundColor3 = Config.Theme.TabInactive}):Play()
    end)

    cycleBtn.MouseButton1Click:Connect(function()
        currentIndex = (currentIndex % #buttonsData) + 1
        local chosenOpt = buttonsData[currentIndex]
        
        callback(chosenOpt.Value)
        updateText()

        TweenService:Create(cycleBtn, TweenInfo.new(0.1), {BackgroundColor3 = Config.Theme.TabActive}):Play()
        cycleBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
        task.delay(0.15, function()
            TweenService:Create(cycleBtn, TweenInfo.new(0.15), {BackgroundColor3 = Config.Theme.TabInactive}):Play()
            cycleBtn.TextColor3 = Config.Theme.TextPrimary
        end)

        saveConfiguration()
    end)
    
    cycleBtn.Parent = sectionFrame
    sectionFrame.Parent = ContentConfig

    local controller = {}
    function controller.setValue(val)
        for i, opt in ipairs(buttonsData) do
            if opt.Value == val then
                currentIndex = i
                updateText()
                break
            end
        end
    end

    return controller
end

local configLayout = Instance.new("UIListLayout")
configLayout.SortOrder = Enum.SortOrder.LayoutOrder
configLayout.Padding = UDim.new(0, 14)
configLayout.Parent = ContentConfig

-- SECCIÓN ARCHIVOS
local saveLoadSection = Instance.new("Frame")
saveLoadSection.Size = UDim2.new(1, 0, 0, 58)
saveLoadSection.BackgroundTransparency = 1
saveLoadSection.Parent = ContentConfig

local saveLoadLbl = Instance.new("TextLabel")
saveLoadLbl.Size = UDim2.new(1, 0, 0, 18)
saveLoadLbl.Font = Enum.Font.GothamBold
saveLoadLbl.TextSize = 11
saveLoadLbl.TextColor3 = Config.Theme.TextSecondary
saveLoadLbl.Text = _L.cfgSys
saveLoadLbl.TextXAlignment = Enum.TextXAlignment.Left
saveLoadLbl.BackgroundTransparency = 1
saveLoadLbl.Parent = saveLoadSection

local slContainer = Instance.new("Frame")
slContainer.Size = UDim2.new(1, 0, 0, 32)
slContainer.Position = UDim2.new(0, 0, 0, 22)
slContainer.BackgroundTransparency = 1
slContainer.Parent = saveLoadSection

local slLayout = Instance.new("UIListLayout")
slLayout.FillDirection = Enum.FillDirection.Horizontal
slLayout.Padding = UDim.new(0, 8)
slLayout.Parent = slContainer

local saveBtn = Instance.new("TextButton")
saveBtn.Size = UDim2.new(0.5, -4, 1, 0)
saveBtn.Font = Enum.Font.GothamBold
saveBtn.TextSize = 10
saveBtn.BackgroundColor3 = Config.Theme.TabInactive
saveBtn.TextColor3 = Config.Theme.TextPrimary
saveBtn.Text = "💾 " .. _L.saveCfg
saveBtn.Parent = slContainer

local saveCorner = Instance.new("UICorner")
saveCorner.CornerRadius = UDim.new(0, 6)
saveCorner.Parent = saveBtn

local loadBtn = Instance.new("TextButton")
loadBtn.Size = UDim2.new(0.5, -4, 1, 0)
loadBtn.Font = Enum.Font.GothamBold
loadBtn.TextSize = 10
loadBtn.BackgroundColor3 = Config.Theme.TabInactive
loadBtn.TextColor3 = Config.Theme.TextPrimary
loadBtn.Text = "📂 " .. _L.loadCfg
loadBtn.Parent = slContainer

local loadCorner = Instance.new("UICorner")
loadCorner.CornerRadius = UDim.new(0, 6)
loadCorner.Parent = loadBtn

-- SECCIÓN FOV INPUT
local fovSection = Instance.new("Frame")
fovSection.Size = UDim2.new(1, 0, 0, 70)
fovSection.BackgroundTransparency = 1
fovSection.Parent = ContentConfig

local fovLbl = Instance.new("TextLabel")
fovLbl.Size = UDim2.new(1, -60, 0, 18)
fovLbl.Font = Enum.Font.GothamBold
fovLbl.TextSize = 11
fovLbl.TextColor3 = Config.Theme.TextSecondary
fovLbl.Text = _L.fovSize
fovLbl.TextXAlignment = Enum.TextXAlignment.Left
fovLbl.BackgroundTransparency = 1
fovLbl.Parent = fovSection

local fovValueLbl = Instance.new("TextLabel")
fovValueLbl.Size = UDim2.new(0, 55, 0, 18)
fovValueLbl.Position = UDim2.new(1, -55, 0, 0)
fovValueLbl.Font = Enum.Font.GothamBold
fovValueLbl.TextSize = 12
fovValueLbl.TextColor3 = Config.Theme.TabActive
fovValueLbl.Text = tostring(Config.AimFOV)
fovValueLbl.TextXAlignment = Enum.TextXAlignment.Right
fovValueLbl.BackgroundTransparency = 1
fovValueLbl.Parent = fovSection

-- Barra FOV (movil y PC): arrastrar = aplica solo
local FOV_MIN, FOV_MAX = 40, 400
local fovTrack = Instance.new("Frame")
fovTrack.Size = UDim2.new(1, 0, 0, 16)
fovTrack.Position = UDim2.new(0, 0, 0, 32)
fovTrack.BackgroundColor3 = Config.Theme.TabInactive
fovTrack.BorderSizePixel = 0
fovTrack.Parent = fovSection
local fovTrackCorner = Instance.new("UICorner")
fovTrackCorner.CornerRadius = UDim.new(1, 0)
fovTrackCorner.Parent = fovTrack

local fovFill = Instance.new("Frame")
fovFill.Size = UDim2.new(math.clamp((Config.AimFOV - FOV_MIN) / (FOV_MAX - FOV_MIN), 0, 1), 0, 1, 0)
fovFill.BackgroundColor3 = Config.Theme.TabActive
fovFill.BorderSizePixel = 0
fovFill.Parent = fovTrack
local fovFillCorner = Instance.new("UICorner")
fovFillCorner.CornerRadius = UDim.new(1, 0)
fovFillCorner.Parent = fovFill

local fovKnob = Instance.new("Frame")
fovKnob.Size = UDim2.new(0, 22, 0, 22)
fovKnob.AnchorPoint = Vector2.new(0.5, 0.5)
fovKnob.Position = UDim2.new(math.clamp((Config.AimFOV - FOV_MIN) / (FOV_MAX - FOV_MIN), 0, 1), 0, 0.5, 0)
fovKnob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
fovKnob.BorderSizePixel = 0
fovKnob.ZIndex = 2
fovKnob.Parent = fovTrack
local fovKnobCorner = Instance.new("UICorner")
fovKnobCorner.CornerRadius = UDim.new(1, 0)
fovKnobCorner.Parent = fovKnob
local fovKnobStroke = Instance.new("UIStroke")
fovKnobStroke.Color = Config.Theme.TabActive
fovKnobStroke.Thickness = 2
fovKnobStroke.Parent = fovKnob

local function applyFovFromAlpha(alpha)
    alpha = math.clamp(alpha, 0, 1)
    local val = math.floor(FOV_MIN + alpha * (FOV_MAX - FOV_MIN) + 0.5)
    Config.AimFOV = val
    fovFill.Size = UDim2.new(alpha, 0, 1, 0)
    fovKnob.Position = UDim2.new(alpha, 0, 0.5, 0)
    fovValueLbl.Text = tostring(val)
end

local function updateFovSliderUI()
    local alpha = math.clamp((Config.AimFOV - FOV_MIN) / (FOV_MAX - FOV_MIN), 0, 1)
    fovFill.Size = UDim2.new(alpha, 0, 1, 0)
    fovKnob.Position = UDim2.new(alpha, 0, 0.5, 0)
    fovValueLbl.Text = tostring(Config.AimFOV)
end

local fovDragging = false
local function fovFromInput(input)
    local absPos = fovTrack.AbsolutePosition.X
    local absSize = fovTrack.AbsoluteSize.X
    if absSize <= 0 then return end
    local alpha = (input.Position.X - absPos) / absSize
    applyFovFromAlpha(alpha)
end

fovTrack.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        fovDragging = true
        fovFromInput(input)
    end
end)
fovKnob.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        fovDragging = true
    end
end)
safeConnect(UserInputService.InputChanged, function(input)
    if not fovDragging then return end
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        fovFromInput(input)
    end
end)
safeConnect(UserInputService.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        if fovDragging then
            fovDragging = false
            saveConfiguration()
        end
    end
end)

-- compat: referencias viejas a fovInput (por si algo las usa)
local fovInput = nil

targetController = createCycleConfigSection(_L.target, {
    {Label = "👤 " .. _L.head, Value = "Cabeza"}, {Label = "👕 " .. _L.chest, Value = "Pecho"}, {Label = "🔀 " .. _L.mixed, Value = "Mixto"}
}, function(value) Config.AimTarget = value; State.lockedTarget = nil end)

smoothController = createCycleConfigSection(_L.smooth, {
    {Label = "⚡ " .. _L.low, Value = "Bajo"}, {Label = "🛡️ " .. _L.mid, Value = "Medio"}, {Label = "🍃 " .. _L.high, Value = "Alto"}
}, function(value) Config.AimSmooth = value end)

modeController = createCycleConfigSection(_L.aimMode, {
    {Label = _L.modeToggle, Value = "Toggle"}, 
    {Label = _L.modeFov, Value = "FOV"}, 
    {Label = _L.modeHold, Value = "Hold"}
}, function(value) Config.AimMode = value end)

-- SECCIÓN BINDS
local bindSectionFrame = Instance.new("Frame")
bindSectionFrame.Size = UDim2.new(1, 0, 0, 58)
bindSectionFrame.BackgroundTransparency = 1
bindSectionFrame.Parent = ContentConfig

local bindLbl = Instance.new("TextLabel")
bindLbl.Size = UDim2.new(1, 0, 0, 18)
bindLbl.Font = Enum.Font.GothamBold
bindLbl.TextSize = 11
bindLbl.TextColor3 = Config.Theme.TextSecondary
bindLbl.Text = _L.binds
bindLbl.TextXAlignment = Enum.TextXAlignment.Left
bindLbl.BackgroundTransparency = 1
bindLbl.Parent = bindSectionFrame

local bindContainer = Instance.new("Frame")
bindContainer.Size = UDim2.new(1, 0, 0, 32)
bindContainer.Position = UDim2.new(0, 0, 0, 22)
bindContainer.BackgroundTransparency = 1
bindContainer.Parent = bindSectionFrame

local bindLayout = Instance.new("UIListLayout")
bindLayout.FillDirection = Enum.FillDirection.Horizontal
bindLayout.Padding = UDim.new(0, 6)
bindLayout.Parent = bindContainer

local bindButtons = {}
local bindActions = {"ToggleMenu", "Aimbot", "InvView"}
local bindLabels = {ToggleMenu = "Menú", Aimbot = "Aim", InvView = "Inv"}

for _, action in ipairs(bindActions) do
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.33, -4, 1, 0)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 10
    btn.BackgroundColor3 = Config.Theme.TabInactive
    btn.TextColor3 = Config.Theme.TextPrimary
    btn.Parent = bindContainer
    
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 6)
    btnCorner.Parent = btn
    
    local bStroke = Instance.new("UIStroke")
    bStroke.Thickness = 1
    bStroke.Color = Config.Theme.StrokeInactive
    bStroke.Parent = btn
    
    bindButtons[action] = btn

    btn.MouseEnter:Connect(function()
        if State.isBinding ~= action then TweenService:Create(btn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(28, 28, 42)}):Play() end
    end)
    btn.MouseLeave:Connect(function()
        if State.isBinding ~= action then TweenService:Create(btn, TweenInfo.new(0.15), {BackgroundColor3 = Config.Theme.TabInactive}):Play() end
    end)

    btn.MouseButton1Click:Connect(function()
        if State.isBinding then return end
        State.isBinding = action
        btn.Text = "...¡Presiona!..."
        TweenService:Create(btn, TweenInfo.new(0.1), {BackgroundColor3 = Config.Theme.PinActive}):Play()
        btn.TextColor3 = Color3.fromRGB(10, 10, 18)
    end)
end

local function updateBindUiTexts()
    for action, btn in pairs(bindButtons) do
        if State.isBinding ~= action then
            btn.Text = bindLabels[action] .. ": [" .. Config.Binds[action].Name .. "]"
            btn.BackgroundColor3 = Config.Theme.TabInactive
            btn.TextColor3 = Config.Theme.TextPrimary
        end
    end
end

local function syncConfigUi()
    if targetController then targetController.setValue(Config.AimTarget) end
    if smoothController then smoothController.setValue(Config.AimSmooth) end
    if modeController then modeController.setValue(Config.AimMode) end
    
    updateBindUiTexts()
    if updateFovSliderUI then
        updateFovSliderUI()
    end
end

-- ==================== MOTOR DE CONFIGURACIONES AUTOMÁTICO ====================
saveConfiguration = function()
    if not (type(writefile) == "function") then return false end
    local saveData = {
        AimTarget = Config.AimTarget, AimSmooth = Config.AimSmooth, AimMode = Config.AimMode,
        AimFOV = Config.AimFOV, ShowFOV = Config.ShowFOV, AutoExecute = Config.AutoExecute,
        Binds = {ToggleMenu = Config.Binds.ToggleMenu.Name, Aimbot = Config.Binds.Aimbot.Name, InvView = Config.Binds.InvView.Name},
        Toggles = {aimEnabled = State.aimEnabled, espEnabled = State.espEnabled, invViewEnabled = State.invViewEnabled}
    }
    local success, encoded = pcall(function() return HttpService:JSONEncode(saveData) end)
    if success and encoded then
        pcall(function() writefile(CONFIG_FILE, encoded) end)
        return true
    end
    return false
end

loadConfiguration = function()
    if not (type(readfile) == "function" and type(isfile) == "function") or not isfile(CONFIG_FILE) then return false end
    local success, content = pcall(function() return readfile(CONFIG_FILE) end)
    if not success or not content then return false end
    local decodeSuccess, decoded = pcall(function() return HttpService:JSONDecode(content) end)
    if not decodeSuccess or type(decoded) ~= "table" then return false end
    
    if decoded.AimTarget ~= nil then Config.AimTarget = decoded.AimTarget end
    if decoded.AimSmooth ~= nil then Config.AimSmooth = decoded.AimSmooth end
    if decoded.AimMode ~= nil then Config.AimMode = decoded.AimMode end
    if decoded.AimFOV ~= nil then Config.AimFOV = tonumber(decoded.AimFOV) or Config.AimFOV end
    if decoded.ShowFOV ~= nil then Config.ShowFOV = decoded.ShowFOV end
    
    if type(decoded.Binds) == "table" then
        for action, keyName in pairs(decoded.Binds) do
            if Config.Binds[action] and Enum.KeyCode[keyName] then Config.Binds[action] = Enum.KeyCode[keyName] end
        end
    end
    if type(decoded.Toggles) == "table" then
        if decoded.Toggles.aimEnabled ~= nil then State.aimEnabled = decoded.Toggles.aimEnabled end
        if decoded.Toggles.espEnabled ~= nil then State.espEnabled = decoded.Toggles.espEnabled end
        if decoded.Toggles.invViewEnabled ~= nil then State.invViewEnabled = decoded.Toggles.invViewEnabled end
    end
    syncConfigUi()
    updateMainButtons()
    return true
end

syncConfigUi()

saveBtn.MouseButton1Click:Connect(function()
    if saveConfiguration() then
        saveBtn.Text = "✅ GUARDADO"; saveBtn.BackgroundColor3 = Config.Theme.TeamActive; saveBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
        task.delay(1.5, function() saveBtn.Text = "💾 " .. _L.saveCfg; saveBtn.BackgroundColor3 = Config.Theme.TabInactive; saveBtn.TextColor3 = Config.Theme.TextPrimary end)
    else
        saveBtn.Text = "❌ ERROR"; saveBtn.BackgroundColor3 = Config.Theme.BtnOff
        task.delay(1.5, function() saveBtn.Text = "💾 " .. _L.saveCfg; saveBtn.BackgroundColor3 = Config.Theme.TabInactive end)
    end
end)

loadBtn.MouseButton1Click:Connect(function()
    if loadConfiguration() then
        loadBtn.Text = "✅ CARGADO"; loadBtn.BackgroundColor3 = Config.Theme.TeamActive; loadBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
        task.delay(1.5, function() loadBtn.Text = "📂 " .. _L.loadCfg; loadBtn.BackgroundColor3 = Config.Theme.TabInactive; loadBtn.TextColor3 = Config.Theme.TextPrimary end)
    else
        loadBtn.Text = "❌ VACÍO"; loadBtn.BackgroundColor3 = Config.Theme.BtnOff
        task.delay(1.5, function() loadBtn.Text = "📂 " .. _L.loadCfg; loadBtn.BackgroundColor3 = Config.Theme.TabInactive end)
    end
end)

local function getMyRootPosition()
    local char = LocalPlayer.Character
    if char then
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum and hum.SeatPart then return hum.SeatPart.Position end
        local root = char:FindFirstChild("HumanoidRootPart")
        if root then return root.Position end
    end
    return Camera.CFrame.Position
end

-- ==================== RENDERING VISUAL UNIFICADO ====================
local function renderPlayerList()
    local activePlayers, playerList = {}, {}
    for _, player in ipairs(Players:GetPlayers()) do 
        if player ~= LocalPlayer then activePlayers[player.Name] = true; table.insert(playerList, player) end 
    end
    for name, frame in pairs(PlayerRowCache) do 
        if not activePlayers[name] then frame:Destroy(); PlayerRowCache[name] = nil end 
    end

    table.sort(playerList, function(a, b)
        local aPinned = State.pinnedPlayers[a.Name] and 1 or 0
        local bPinned = State.pinnedPlayers[b.Name] and 1 or 0
        if aPinned ~= bPinned then return aPinned > bPinned end
        return a.Name < b.Name
    end)

    for order, player in ipairs(playerList) do
        local isPinned, isTeam = State.pinnedPlayers[player.Name], State.teamPlayers[player.Name]
        local playerWrapper = PlayerRowCache[player.Name]
        
        if not playerWrapper then
            playerWrapper = Instance.new("Frame")
            playerWrapper.Size = UDim2.new(1, -6, 0, 40)
            
            local wrapperCorner = Instance.new("UICorner")
            wrapperCorner.CornerRadius = UDim.new(0, 6)
            wrapperCorner.Parent = playerWrapper
            
            local userBtn = Instance.new("TextLabel")
            userBtn.Name = "UserBtn"
            userBtn.Size = UDim2.new(1, -120, 1, 0)
            userBtn.Position = UDim2.new(0, 10, 0, 0)
            userBtn.BackgroundTransparency = 1
            userBtn.Font = Enum.Font.GothamBold
            userBtn.TextSize = 11
            userBtn.TextXAlignment = Enum.TextXAlignment.Left
            userBtn.Parent = playerWrapper

            local teamBtn = Instance.new("TextButton")
            teamBtn.Name = "TeamBtn"
            teamBtn.Size = UDim2.new(0, 50, 0, 24)
            teamBtn.Position = UDim2.new(1, -105, 0.5, -12)
            teamBtn.Font = Enum.Font.GothamBold
            teamBtn.TextSize = 9
            teamBtn.TextColor3 = Config.Theme.TextPrimary
            
            local teamCorner = Instance.new("UICorner")
            teamCorner.CornerRadius = UDim.new(0, 4)
            teamCorner.Parent = teamBtn
            teamBtn.Parent = playerWrapper

            local pinBtn = Instance.new("TextButton")
            pinBtn.Name = "PinBtn"
            pinBtn.Size = UDim2.new(0, 45, 0, 24)
            pinBtn.Position = UDim2.new(1, -50, 0.5, -12)
            pinBtn.Font = Enum.Font.GothamBold
            pinBtn.TextSize = 9
            pinBtn.TextColor3 = Config.Theme.TextPrimary
            
            local pinCorner = Instance.new("UICorner")
            pinCorner.CornerRadius = UDim.new(0, 4)
            pinCorner.Parent = pinBtn
            pinBtn.Parent = playerWrapper

            teamBtn.MouseButton1Click:Connect(function() State.teamPlayers[player.Name] = not State.teamPlayers[player.Name] or nil; renderPlayerList(); saveConfiguration() end)
            pinBtn.MouseButton1Click:Connect(function() 
                if State.pinnedPlayers[player.Name] then State.pinnedPlayers[player.Name] = nil; State.autoPinned[player.Name] = nil else State.pinnedPlayers[player.Name] = true end
                renderPlayerList(); saveConfiguration()
            end)
            
            PlayerRowCache[player.Name] = playerWrapper
            playerWrapper.Parent = scroll
        end

        playerWrapper.LayoutOrder = order
        playerWrapper.BackgroundColor3 = isPinned and Config.Theme.PlayerRowPinned or Config.Theme.PlayerRow
        
        local userBtn = playerWrapper:FindFirstChild("UserBtn")
        local teamBtn = playerWrapper:FindFirstChild("TeamBtn")
        local pinBtn = playerWrapper:FindFirstChild("PinBtn")
        
        if userBtn then 
            userBtn.TextColor3 = isTeam and Config.Theme.EspTeam or (isPinned and Config.Theme.EspPinned or Config.Theme.TextPrimary)
            userBtn.Text = (isTeam and "[ALIADO] " or (isPinned and "[TARGET] " or "")) .. player.DisplayName 
        end
        if teamBtn then 
            teamBtn.BackgroundColor3 = isTeam and Config.Theme.TeamActive or Config.Theme.PinInactive
            teamBtn.Text = isTeam and "No Team" or "Team"; teamBtn.TextColor3 = isTeam and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary
        end
        if pinBtn then 
            pinBtn.BackgroundColor3 = isPinned and Config.Theme.PinActive or Config.Theme.PinInactive
            pinBtn.Text = isPinned and "Unpin" or "Pin"; pinBtn.TextColor3 = isPinned and Color3.fromRGB(10,10,18) or Config.Theme.TextPrimary
        end
    end
end

local function getRarityColor(rarity)
    local colors = {Common = Color3.fromRGB(0, 255, 100), Rare = Color3.fromRGB(0, 150, 255), Epic = Color3.fromRGB(180, 50, 255), Legendary = Color3.fromRGB(255, 200, 0)}
    return colors[rarity] or Color3.fromRGB(255, 255, 255)
end

local function matchToolName(tool)
    if not tool then return "Unknown" end
    local name = tool.Name
    if ToolNameCache[name] then return ToolNameCache[name] end
    local handle = tool:FindFirstChild("Handle")
    if not handle then ToolNameCache[name] = name; return name end
    local names = {}
    for _, child in ipairs(handle:GetChildren()) do names[child.Name] = true end
    for _, source in ipairs({ReplicatedStorage:FindFirstChild("Items"), StarterPack}) do
        if source then
            for _, item in ipairs(source:GetDescendants()) do
                if item:IsA("Tool") and item:FindFirstChild("Handle") then
                    local matches = true
                    for childName in pairs(names) do if not item.Handle:FindFirstChild(childName) then matches = false; break end end
                    if matches then ToolNameCache[name] = item.Name; return item.Name end
                end
            end
        end
    end
    ToolNameCache[name] = name; return name
end

-- ==================== ESCANEO DE MOCHILAS ====================
local function getPlayerTools(player)
    local now = tick()
    if LastToolScan[player.Name] and (now - LastToolScan[player.Name].time < 1.5) then
        return LastToolScan[player.Name].tools
    end

    local tools = {}
    if not player then return tools end
    local hasLegendary = false
    local backpack = player:FindFirstChildOfClass("Backpack")
    local character = player.Character
    
    local function scanContainer(container)
        if not container then return end
        for _, tool in ipairs(container:GetChildren()) do
            if tool:IsA("Tool") then
                local realName = matchToolName(tool)
                local rarity = tool:GetAttribute("RarityName") or "Common"
                if rarity == "Legendary" then hasLegendary = true end
                table.insert(tools, {name = realName, rarity = rarity, equipped = (container == character)})
            end
        end
    end
    scanContainer(backpack); scanContainer(character)
    
    if hasLegendary then
        if not State.pinnedPlayers[player.Name] then 
            State.pinnedPlayers[player.Name] = true 
            State.autoPinned[player.Name] = true 
            task.spawn(renderPlayerList) 
        end
    else
        if State.autoPinned[player.Name] then 
            State.pinnedPlayers[player.Name] = nil 
            State.autoPinned[player.Name] = nil 
            task.spawn(renderPlayerList) 
        end
    end

    LastToolScan[player.Name] = {time = now, tools = tools}
    return tools
end

local function getOrCreateMasterEsp(player)
    if MasterObjects[player.Name] then return MasterObjects[player.Name] end
    local char = player.Character
    if not char then return nil end
    local head = char:FindFirstChild("Head")
    if not head then return nil end
    
    local billboard = Instance.new("BillboardGui")
    billboard.Name = "BsMasterEsp"; billboard.Size = UDim2.new(0, 180, 0, 180); billboard.StudsOffset = Vector3.new(0, 3.5, 0); billboard.AlwaysOnTop = true; billboard.Parent = head

    local mainLayoutFrame = Instance.new("Frame")
    mainLayoutFrame.Size = UDim2.new(1, 0, 1, 0)
    mainLayoutFrame.BackgroundTransparency = 1
    mainLayoutFrame.Parent = billboard
    
    local listLayout = Instance.new("UIListLayout")
    listLayout.FillDirection = Enum.FillDirection.Vertical
    listLayout.SortOrder = Enum.SortOrder.LayoutOrder
    listLayout.Padding = UDim.new(0, 4)
    listLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    listLayout.Parent = mainLayoutFrame

    local espLabel = Instance.new("TextLabel")
    espLabel.Name = "EspLabel"
    espLabel.Size = UDim2.new(1, 0, 0, 38)
    espLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    espLabel.BackgroundTransparency = 0.65
    espLabel.Font = Enum.Font.GothamBold
    espLabel.TextStrokeTransparency = 0.4
    espLabel.LayoutOrder = 1
    
    local labelCorner = Instance.new("UICorner")
    labelCorner.CornerRadius = UDim.new(0, 5)
    labelCorner.Parent = espLabel
    espLabel.Parent = mainLayoutFrame

    local invContainer = Instance.new("Frame")
    invContainer.Name = "InvContainer"
    invContainer.Size = UDim2.new(1, 0, 0, 120)
    invContainer.BackgroundTransparency = 1
    invContainer.LayoutOrder = 2
    invContainer.Parent = mainLayoutFrame
    
    local invLayout = Instance.new("UIListLayout")
    invLayout.FillDirection = Enum.FillDirection.Vertical
    invLayout.SortOrder = Enum.SortOrder.LayoutOrder
    invLayout.Padding = UDim.new(0, 2)
    invLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    invLayout.Parent = invContainer

    MasterObjects[player.Name] = {Gui = billboard, EspLabel = espLabel, InvContainer = invContainer}
    return MasterObjects[player.Name]
end

local function removeMasterEsp(player)
    local master = MasterObjects[player.Name]
    if master then
        if master.Gui then master.Gui:Destroy() end
        MasterObjects[player.Name] = nil; LastInventoryState[player] = nil
    end
end

-- ==================== MOTOR VISUAL GENERAL ====================
local function updateVisuals()
    if not State.alive then return end
    local myPosition = getMyRootPosition()

    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            local char = player.Character
            if char then
                local head, root, hum = char:FindFirstChild("Head"), char:FindFirstChild("HumanoidRootPart"), char:FindFirstChildOfClass("Humanoid")
                if head and root and hum then
                    local isPinned, isTeam = State.pinnedPlayers[player.Name], State.teamPlayers[player.Name]
                    
                    if hum.Health > 0 then
                        local master = getOrCreateMasterEsp(player)
                        if master and master.Gui and master.Gui.Parent == head then
                            master.Gui.Enabled = true
                            
                            local distance = (root.Position - myPosition).Magnitude
                            local textScale = math.clamp(12 - (distance / 400), 7.5, 11.5)

                            if State.espEnabled then
                                master.EspLabel.Visible = true
                                master.EspLabel.TextColor3 = isTeam and Config.Theme.EspTeam or (isPinned and Config.Theme.EspPinned or Config.Theme.EspNormal)
                                master.EspLabel.TextSize = textScale
                                local tagPrefix = isTeam and "[ALIADO]\n" or (isPinned and "[TARGET]\n" or "")
                                master.EspLabel.Text = string.format("%s%s\n%d HP", tagPrefix, player.DisplayName, math.floor(hum.Health))
                            else
                                master.EspLabel.Visible = false
                            end

                            if State.invViewEnabled then
                                master.InvContainer.Visible = true
                                local tools = getPlayerTools(player)
                                local inventoryString = ""
                                for _, toolData in ipairs(tools) do inventoryString = inventoryString .. toolData.name .. toolData.rarity .. tostring(toolData.equipped) end
                                
                                if LastInventoryState[player] ~= inventoryString then
                                    LastInventoryState[player] = inventoryString
                                    for _, child in ipairs(master.InvContainer:GetChildren()) do if child:IsA("TextLabel") then child:Destroy() end end
                                    for i, toolData in ipairs(tools) do
                                        local line = Instance.new("TextLabel")
                                        line.Size = UDim2.new(0, 145, 0, 14)
                                        line.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
                                        line.BackgroundTransparency = 0.7
                                        line.Font = Enum.Font.GothamBold
                                        line.TextStrokeTransparency = 0.5
                                        line.Text = " " .. toolData.name .. " "
                                        line.TextColor3 = getRarityColor(toolData.rarity)
                                        line.LayoutOrder = i
                                        
                                        local lineCorner = Instance.new("UICorner")
                                        lineCorner.CornerRadius = UDim.new(0, 4)
                                        lineCorner.Parent = line
                                        
                                        if toolData.equipped then line.Text = "👉 " .. toolData.name; line.BackgroundColor3 = Color3.fromRGB(25, 15, 35) end
                                        line.Parent = master.InvContainer
                                    end
                                end
                                for _, child in ipairs(master.InvContainer:GetChildren()) do if child:IsA("TextLabel") then child.TextSize = textScale end end
                            else
                                master.InvContainer.Visible = false
                            end
                        else
                            removeMasterEsp(player)
                        end

                        if isTeam or isPinned then
                            local hl = char:FindFirstChild("BsAura")
                            if not hl then 
                                hl = Instance.new("Highlight")
                                hl.Name = "BsAura"
                                hl.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                                hl.OutlineColor = Config.Theme.AuraOutline
                                hl.Parent = char 
                            end
                            hl.FillColor = isTeam and Config.Theme.AuraTeamFill or Config.Theme.AuraFill; hl.FillTransparency = 0.65 + math.sin(tick() * 4) * 0.08
                        else
                            local hl = char:FindFirstChild("BsAura")
                            if hl then hl:Destroy() end
                        end
                    else
                        removeMasterEsp(player)
                        local hl = char:FindFirstChild("BsAura")
                        if hl then hl:Destroy() end
                    end
                else
                    removeMasterEsp(player)
                end
            else
                removeMasterEsp(player)
            end
        end
    end
end

-- ==================== CÍRCULO FOV ADAPTABLE (UI / COMPATIBLE CON DELTA) ====================
local FovGuiFrame = Instance.new("Frame")
FovGuiFrame.Name = "HCP_FOV_Circle"
FovGuiFrame.AnchorPoint = Vector2.new(0.5, 0.5)
FovGuiFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
FovGuiFrame.BackgroundTransparency = 1
FovGuiFrame.Visible = false
FovGuiFrame.Parent = gui

local FovCorner = Instance.new("UICorner")
FovCorner.CornerRadius = UDim.new(1, 0)
FovCorner.Parent = FovGuiFrame

local FovStroke = Instance.new("UIStroke")
FovStroke.Thickness = 1.5
FovStroke.Color = Config.Theme.FOVNormal
FovStroke.Transparency = 0
FovStroke.Parent = FovGuiFrame

local FOVCircle = {
    Visible = false,
    Radius = Config.AimFOV,
    Color = Config.Theme.FOVNormal
}

local function getInternalPartName(targetMode, char)
    if not char then return nil end
    local head, torso = char:FindFirstChild("Head"), char:FindFirstChild("UpperTorso") or char:FindFirstChild("Torso")
    if targetMode == "Cabeza" then return head and "Head" or nil
    elseif targetMode == "Pecho" then return torso and torso.Name or nil
    elseif targetMode == "Mixto" then 
        local hum = char:FindFirstChildOfClass("Humanoid")
        return (hum and hum.Health > 30) and (head and "Head" or (torso and torso.Name or nil)) or (torso and torso.Name or (head and "Head" or nil))
    end
    return "Head"
end

local function getClosestTarget()
    -- Modo FOV / Hold (gatillo): reevalúa y puede cambiar de target fácilmente
    if Config.AimMode == "FOV" or Config.AimMode == "Hold" then
        local closest, minDist = nil, Config.AimFOV
        local center = Camera.ViewportSize / 2
        local current = State.lockedTarget
        local currentDist = math.huge

        for _, plr in ipairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer and not State.teamPlayers[plr.Name] then
                local char = plr.Character
                if char then
                    local hum = char:FindFirstChildOfClass("Humanoid")
                    if hum and hum.Health > 0 then
                        local partName = getInternalPartName(Config.AimTarget, char)
                        local part = partName and char:FindFirstChild(partName)
                        if part and part:IsA("BasePart") then
                            local pos, onScreen = Camera:WorldToViewportPoint(part.Position)
                            if onScreen then
                                local dist = (Vector2.new(pos.X, pos.Y) - center).Magnitude
                                if dist < minDist then
                                    minDist = dist
                                    closest = plr
                                end
                                if current and plr == current then
                                    currentDist = dist
                                end
                            end
                        end
                    end
                end
            end
        end

        if current then
            local char = current.Character
            local hum = char and char:FindFirstChildOfClass("Humanoid")
            if State.teamPlayers[current.Name] or not char or not hum or hum.Health <= 0 or currentDist > Config.AimFOV then
                State.lockedTarget = nil
                current = nil
            end
        end

        if closest then
            if not current then
                State.lockedTarget = closest
            elseif closest ~= current and minDist < (currentDist * 0.72) then
                State.lockedTarget = closest
            end
        else
            State.lockedTarget = nil
        end
        return State.lockedTarget
    end

    -- Toggle: lock normal
    local locked = State.lockedTarget
    if locked then
        local char = locked.Character
        local hum = char and char:FindFirstChildOfClass("Humanoid")
        if State.teamPlayers[locked.Name] or not char or not hum or hum.Health <= 0 then
            State.lockedTarget = nil
            locked = nil
        end
    end
    if locked then return locked end

    local closest, minDist = nil, Config.AimFOV
    local center = Camera.ViewportSize / 2

    for _, plr in ipairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer and not State.teamPlayers[plr.Name] then
            local char = plr.Character
            if char then
                local hum = char:FindFirstChildOfClass("Humanoid")
                if hum and hum.Health > 0 then
                    local partName = getInternalPartName(Config.AimTarget, char)
                    local part = partName and char:FindFirstChild(partName)
                    if part and part:IsA("BasePart") then
                        local pos, onScreen = Camera:WorldToViewportPoint(part.Position)
                        if onScreen then
                            local dist = (Vector2.new(pos.X, pos.Y) - center).Magnitude
                            if dist < minDist then minDist = dist; closest = plr end
                        end
                    end
                end
            end
        end
    end
    State.lockedTarget = closest
    return closest
end

-- ==================== BUCLE DE ACTUALIZACIÓN VISUAL REGULADO ====================
task.spawn(function()
    while State.alive do
        updateVisuals()
        task.wait(0.03) 
    end
end)

safeConnect(RunService.RenderStepped, function(dt)
    local isFovVisible = (Config.ShowFOV and Config.AimMode == "FOV")
    FovGuiFrame.Visible = isFovVisible
    if isFovVisible then
        local diameter = Config.AimFOV * 2
        FovGuiFrame.Size = UDim2.new(0, diameter, 0, diameter)
        FovStroke.Color = State.lockedTarget and Config.Theme.FOVLocked or Config.Theme.FOVNormal
    end
end)

RunService:BindToRenderStep("BlockSpinAimbot", Enum.RenderPriority.Camera.Value + 1, function(dt)
    if not State.alive then return end
    local shouldAim = false
    if Config.AimMode == "Toggle" then shouldAim = State.aimEnabled
    elseif Config.AimMode == "FOV" then shouldAim = State.holdingAimTrigger or State.aimEnabled
    elseif Config.AimMode == "Hold" then shouldAim = State.holdingAimTrigger end
    if not shouldAim then return end

    local target = getClosestTarget()
    if target and target.Character then
        local partName = getInternalPartName(Config.AimTarget, target.Character)
        local part = partName and target.Character:FindFirstChild(partName)
        if part and part:IsA("BasePart") then
            local camPos = Camera.CFrame.Position
            local targetPos = part.Position
            if (targetPos - camPos).Magnitude < 0.5 then return end

            -- Look estable (sin roll, sin meterse detras)
            local desired = CFrame.new(camPos, targetPos)
            local ok, x, y = pcall(function()
                local a, b = desired:ToEulerAnglesYXZ()
                return a, b
            end)
            if ok then
                x = math.clamp(x, math.rad(-80), math.rad(80))
                desired = CFrame.new(camPos) * CFrame.fromEulerAnglesYXZ(x, y, 0)
            end

            -- BLOQUEO DURO:
            -- Toggle / Hold / Suave=Bajo  => lock instantaneo (pegado al target)
            -- Medio / Alto               => un poco de suavizado
            local hardLock = (Config.AimMode == "Toggle") or (Config.AimMode == "Hold") or (Config.AimSmooth == "Bajo")
            if hardLock then
                Camera.CFrame = desired
            else
                local lerpAlpha = 1
                if Config.AimSmooth == "Medio" then
                    lerpAlpha = 1 - math.exp(-22 * dt)
                else -- Alto
                    lerpAlpha = 1 - math.exp(-10 * dt)
                end
                Camera.CFrame = Camera.CFrame:Lerp(desired, math.clamp(lerpAlpha, 0, 1))
            end
        end
    end
end)

-- ==================== ENTRADAS DE USUARIO (TECLADO, RATÓN, MANDOS) ====================
safeConnect(UserInputService.InputBegan, function(input, gpe)
    if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == Config.Binds.GamepadAim then State.holdingAimTrigger = true end
    if State.isBinding then
        if input.UserInputType == Enum.UserInputType.Keyboard then
            local action = State.isBinding
            Config.Binds[action] = input.KeyCode; State.isBinding = nil; syncConfigUi()
            saveConfiguration() 
        end
        return
    end
    if gpe then return end
    
    if input.KeyCode == Config.Binds.ToggleMenu then 
        MainFrame.Visible = not MainFrame.Visible
    elseif input.KeyCode == Config.Binds.Aimbot or input.KeyCode == Config.Binds.GamepadToggle then
        State.aimEnabled = not State.aimEnabled; if not State.aimEnabled then State.lockedTarget = nil end; updateMainButtons(); saveConfiguration()
    elseif input.KeyCode == Config.Binds.InvView then State.invViewEnabled = not State.invViewEnabled; updateMainButtons(); saveConfiguration() end
end)

safeConnect(UserInputService.InputEnded, function(input, gpe)
    if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == Config.Binds.GamepadAim then State.holdingAimTrigger = false; State.lockedTarget = nil end
end)

-- ==================== SISTEMA DE ARRASTRE TOTALMENTE LIBRE ====================
local dragging = false
local dragStart = Vector3.zero
local startPos = UDim2.new()

header.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = MainFrame.Position
    end
end)

safeConnect(UserInputService.InputChanged, function(input)
    if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

safeConnect(UserInputService.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = false
    end
end)

-- ==================== LIMPIEZA TOTAL DEL SISTEMA ====================
local function cleanup()
    State.alive = false
    pcall(function() 
        RunService:UnbindFromRenderStep("BlockSpinAimbot") 
    end)
    
    if FovGuiFrame then pcall(function() FovGuiFrame:Destroy() end) end
    
    for _, conn in ipairs(State.connections) do 
        pcall(function() conn:Disconnect() end) 
    end
    
    for _, p in ipairs(Players:GetPlayers()) do
        removeMasterEsp(p)
        if p.Character then 
            local h1 = p.Character:FindFirstChild("BsAura")
            if h1 then h1:Destroy() end 
        end
    end
end

closeBtn.MouseButton1Click:Connect(function() cleanup(); gui:Destroy() end)
safeConnect(Players.PlayerAdded, function(p) checkAndAutoTeam(p); renderPlayerList() end)
safeConnect(Players.PlayerRemoving, function(player)
    removeMasterEsp(player)
    State.teamPlayers[player.Name] = nil; State.pinnedPlayers[player.Name] = nil; State.autoPinned[player.Name] = nil
    local row = PlayerRowCache[player.Name]; if row then row:Destroy(); PlayerRowCache[player.Name] = nil end
    renderPlayerList()
end)

for _, p in ipairs(Players:GetPlayers()) do if p ~= LocalPlayer then checkAndAutoTeam(p) end end
renderPlayerList()
task.spawn(loadConfiguration)
print("[Hermanos CP] Fix de FOV nativo UI cargado con éxito para Delta.")
