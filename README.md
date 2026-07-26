-- =============================================================================
--    HERMANOS CP v5.4 ULTRA-LIGHT & OPTIMIZED (UNLOCKED - FOV FIXED)
-- =============================================================================

local _Gms = game
local _Wsp = workspace
local _Plrs = _Gms:GetService("Players")
local _RepS = _Gms:GetService("ReplicatedStorage")
local _StkP = _Gms:GetService("StarterPack")
local _RunS = _Gms:GetService("RunService")
local _Uis = _Gms:GetService("UserInputService")

-- [[ HCP LANG START ]]
local _HCP_LANG = (type(_G) == "table" and _G.HCP_LANG) or nil
if not _HCP_LANG then
    local lp = game:GetService("Players").LocalPlayer
    local loc = (lp and lp.LocaleId and lp.LocaleId:lower()) or "es"
    _HCP_LANG = loc:match("^es") and "es" or "en"
end
local _L = (_HCP_LANG == "en") and {
    title = "HERMANOS CP v5.4 // UNLOCKED EDITION",
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
    skel = "SKELETON ESP STYLE",
    binds = "KEYBINDS (CLICK TO CHANGE)",
    distEsp = "MAX ESP DISTANCE: %s STUDS",
    modeToggle = "Toggle (PC Key)",
    modeFov = "Circle (Pad FOV)",
    modeHold = "Trigger / RMB",
    head = "Head",
    chest = "Chest",
    mixed = "Mixed",
    low = "Low",
    mid = "Medium",
    high = "High",
    off = "Off",
    gold = "Gold",
    white = "White",
    cyan = "Cyan",
    menu = "Menu",
} or {
    title = "HERMANOS CP v5.4 // UNLOCKED EDITION",
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
    skel = "ESP PALITOS (SKELETON)",
    binds = "BINDS DE TECLAS (CLIC PARA CAMBIAR)",
    distEsp = "DISTANCIA MAX ESP: %s STUDS",
    modeToggle = "Toggle (Tecla)",
    modeFov = "Circulo (Mando)",
    modeHold = "Gatillo / M2",
    head = "Cabeza",
    chest = "Pecho",
    mixed = "Mixto",
    low = "Bajo",
    mid = "Medio",
    high = "Alto",
    off = "Off",
    gold = "Oro",
    white = "Blanco",
    cyan = "Cyan",
    menu = "Menu",
}
-- [[ HCP LANG END ]]

local _Cgs = _Gms:GetService("CoreGui")
local _Tws = _Gms:GetService("TweenService")
local _Hts = _Gms:GetService("HttpService")

local function _getEnv(name)
    local g = (type(getgenv) == "function" and getgenv()) or {}
    local f = (type(getfenv) == "function" and getfenv()) or {}
    local ok, val = pcall(function() return g[name] or f[name] or _G[name] end)
    return ok and val or nil
end

local _cloneref = _getEnv("cloneref")
local _Drawing = _getEnv("Drawing")
local _writefile = _getEnv("writefile")
local _readfile = _getEnv("readfile")
local _isfile = _getEnv("isfile")

while not _Plrs.LocalPlayer do
    task.wait(0.1)
end
local _LP = _Plrs.LocalPlayer
local _Cam = _Wsp.CurrentCamera or _Wsp:WaitForChild("Camera")
local _CfgFile = "HermanosCP_v54_Config.json"

local _saveConfig
local _loadConfig

local _Cfg = {
    Theme = {
        Background      = Color3.fromRGB(10, 10, 18),
        Header          = Color3.fromRGB(18, 12, 32),
        Stroke          = Color3.fromRGB(0, 210, 255),
        GradientStart   = Color3.fromRGB(15, 8, 30),
        GradientEnd     = Color3.fromRGB(5, 5, 10),
        PlayerRow       = Color3.fromRGB(24, 18, 38),
        PlayerRowPinned = Color3.fromRGB(45, 20, 70),
        TextPrimary     = Color3.fromRGB(255, 255, 255),
        TextSecondary   = Color3.fromRGB(180, 200, 255),
        PinActive       = Color3.fromRGB(0, 210, 255),
        PinInactive     = Color3.fromRGB(40, 35, 60),
        TeamActive      = Color3.fromRGB(0, 255, 130),
        EspNormal       = Color3.fromRGB(0, 210, 255),
        EspPinned       = Color3.fromRGB(255, 215, 0),
        EspTeam         = Color3.fromRGB(0, 255, 130), 
        AuraFill        = Color3.fromRGB(0, 210, 255),
        AuraTeamFill    = Color3.fromRGB(0, 255, 100), 
        AuraOutline     = Color3.fromRGB(255, 255, 255),
        BtnOn           = Color3.fromRGB(0, 255, 130),
        BtnOff          = Color3.fromRGB(255, 50, 80),
        CloseBtn        = Color3.fromRGB(40, 15, 25),
        CloseBtnText    = Color3.fromRGB(255, 70, 90),
        ScrollBar       = Color3.fromRGB(0, 210, 255),
        TabActive       = Color3.fromRGB(0, 210, 255),
        TabInactive     = Color3.fromRGB(20, 15, 30),
        Gold            = Color3.fromRGB(255, 215, 0),
        FOVNormal       = Color3.fromRGB(0, 210, 255),
        FOVLocked       = Color3.fromRGB(255, 50, 80)
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
    WallCheck  = false, 
    MaxNormalDistance = 1200, 
    MaxSpecialDistance = 1800,
    SkeletonStyle = "Oro",
    VehicleCameraFix = true, 
    AimOrigin = "Cámara", 
    AutoExecute = false
}

local _St = {
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

local _MasterObj = {}
local _LastInvState = {}
local _ToolCache = {}
local _RowCache = {}
local _SkelCache = {}
local _LastScan = {} 

local function _safeConn(signal, cb)
    local conn = signal:Connect(cb)
    table.insert(_St.connections, conn)
    return conn
end

local _cnt = 0
local function _genName()
    _cnt = _cnt + 1
    return string.char(math.random(65, 90)) .. string.char(math.random(97, 122)) .. tostring(math.random(100, 999)) .. tostring(_cnt)
end

local _hasDrawing = (type(_Drawing) == "table" and type(_Drawing.new) == "function")

local function _getSafeParent()
    local ok, p = pcall(function()
        local t = (type(_cloneref) == "function" and _cloneref(_Cgs)) or _Cgs
        local test = Instance.new("ScreenGui")
        test.Parent = t
        test:Destroy()
        return t
    end)
    if ok and p then return p end
    local pGui = _LP:FindFirstChildOfClass("PlayerGui")
    if pGui then return pGui end
    return _LP:WaitForChild("PlayerGui", 5) or _Cgs
end

_safeConn(_Wsp:GetPropertyChangedSignal("CurrentCamera"), function()
    _Cam = _Wsp.CurrentCamera or _Cam
end)

local function _fixCam()
    if not _Cfg.VehicleCameraFix then return end
    local char = _LP.Character
    if not char then return end
    local hum = char:FindFirstChildOfClass("Humanoid")
    if hum then
        if hum.CameraOffset ~= Vector3.zero then hum.CameraOffset = Vector3.zero end
        if _Cam.CameraSubject ~= hum then _Cam.CameraSubject = hum end
    end
    if _Cam.CameraType ~= Enum.CameraType.Custom then _Cam.CameraType = Enum.CameraType.Custom end
end

_safeConn(_Cam:GetPropertyChangedSignal("CameraSubject"), function() task.spawn(_fixCam) end)
_safeConn(_Cam:GetPropertyChangedSignal("CameraType"), function() task.spawn(_fixCam) end)

local _humConn
local function _connHum(hum)
    if _humConn then _humConn:Disconnect() end
    _humConn = hum:GetPropertyChangedSignal("CameraOffset"):Connect(function()
        if _Cfg.VehicleCameraFix and hum.CameraOffset ~= Vector3.zero then
            hum.CameraOffset = Vector3.zero
        end
    end)
    table.insert(_St.connections, _humConn)
end

_safeConn(_LP.CharacterAdded, function(char)
    local hum = char:WaitForChild("Humanoid", 5)
    if hum then _connHum(hum) end
    task.spawn(_fixCam)
end)

if _LP.Character then
    local hum = _LP.Character:FindFirstChildOfClass("Humanoid")
    if hum then _connHum(hum) end
end

local function _autoTeam(plr)
    if plr == _LP then return end
    task.spawn(function()
        local ok, isF = pcall(function() return _LP:IsFriendsWith(plr.UserId) end)
        if ok and isF then
            _St.teamPlayers[plr.Name] = true
            if _St.lockedTarget == plr then _St.lockedTarget = nil end
        end
    end)
end

local _gui = Instance.new("ScreenGui")
_gui.Name = _genName()
_gui.IgnoreGuiInset = true
_gui.ResetOnSpawn = false
_gui.Parent = _getSafeParent()

local function _showNotif(msg, col)
    local f = Instance.new("Frame")
    f.Size = UDim2.new(0, 230, 0, 50)
    f.Position = UDim2.new(1, 20, 0.9, -10)
    f.BackgroundColor3 = _Cfg.Theme.Background
    f.BorderSizePixel = 0
    f.Parent = _gui

    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 8)
    c.Parent = f

    local st = Instance.new("UIStroke")
    st.Color = col or _Cfg.Theme.Stroke
    st.Thickness = 1.5
    st.Parent = f

    local t = Instance.new("TextLabel")
    t.Size = UDim2.new(1, -16, 1, 0)
    t.Position = UDim2.new(0, 10, 0, 0)
    t.BackgroundTransparency = 1
    t.Font = Enum.Font.GothamBold
    t.TextSize = 10
    t.TextColor3 = _Cfg.Theme.TextPrimary
    t.Text = msg
    t.TextXAlignment = Enum.TextXAlignment.Left
    t.TextWrapped = true
    t.Parent = f

    _Tws:Create(f, TweenInfo.new(0.4, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
        Position = UDim2.new(1, -250, 0.9, -10)
    }):Play()

    task.delay(3.5, function()
        local tw = _Tws:Create(f, TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
            Position = UDim2.new(1, 20, 0.9, -10)
        })
        _Tws:Create(t, TweenInfo.new(0.3), {TextTransparency = 1}):Play()
        _Tws:Create(st, TweenInfo.new(0.3), {Transparency = 1}):Play()
        tw.Completed:Connect(function() f:Destroy() end)
        tw:Play()
    end)
end

local _cam = workspace.CurrentCamera
local _vw = (_cam and _cam.ViewportSize.X) or 800
local _vh = (_cam and _cam.ViewportSize.Y) or 600
local _isMob = _Uis.TouchEnabled and (not _Uis.KeyboardEnabled or _vw < 700)
local _fw = _isMob and math.clamp(math.floor(_vw * 0.92), 280, 380) or 460
local _fh = _isMob and math.clamp(math.floor(_vh * 0.72), 400, 520) or 560

local _MainF = Instance.new("Frame")
_MainF.Size = UDim2.new(0, _fw, 0, _fh)
_MainF.AnchorPoint = Vector2.new(0.5, 0.5)
_MainF.Position = UDim2.new(0.5, 0, 0.5, 0)
_MainF.BackgroundColor3 = _Cfg.Theme.Background
_MainF.ClipsDescendants = true
_MainF.Parent = _gui

local _mC = Instance.new("UICorner")
_mC.CornerRadius = UDim.new(0, 15)
_mC.Parent = _MainF

local _mS = Instance.new("UIStroke")
_mS.Color = _Cfg.Theme.Stroke
_mS.Thickness = 1.5
_mS.Parent = _MainF

local _mGr = Instance.new("UIGradient")
_mGr.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, _Cfg.Theme.GradientStart),
    ColorSequenceKeypoint.new(1, _Cfg.Theme.GradientEnd),
})
_mGr.Parent = _MainF

local _Hdr = Instance.new("Frame")
_Hdr.Size = UDim2.new(1, 0, 0, 45)
_Hdr.BackgroundColor3 = _Cfg.Theme.Header
_Hdr.Parent = _MainF

local _hC = Instance.new("UICorner")
_hC.CornerRadius = UDim.new(0, 15)
_hC.Parent = _Hdr

local _hT = Instance.new("TextLabel")
_hT.Font = Enum.Font.GothamBold
_hT.TextSize = 13
_hT.TextColor3 = _Cfg.Theme.TextPrimary
_hT.Size = UDim2.new(1, -90, 1, 0)
_hT.Position = UDim2.new(0, 15, 0, 0)
_hT.BackgroundTransparency = 1
_hT.Text = _L.title
_hT.TextXAlignment = Enum.TextXAlignment.Left
_hT.Parent = _Hdr

local _MinBtn = Instance.new("TextButton")
_MinBtn.Size = UDim2.new(0, 32, 0, 32)
_MinBtn.Position = UDim2.new(1, -76, 0.5, -16)
_MinBtn.Text = "−"
_MinBtn.TextSize = 18
_MinBtn.Font = Enum.Font.GothamBold
_MinBtn.TextColor3 = Color3.fromRGB(255, 210, 80)
_MinBtn.BackgroundColor3 = Color3.fromRGB(40, 35, 18)
_MinBtn.Parent = _Hdr
local _mbC = Instance.new("UICorner")
_mbC.CornerRadius = UDim.new(0, 8)
_mbC.Parent = _MinBtn

local _ClsBtn = Instance.new("TextButton")
_ClsBtn.Size = UDim2.new(0, 32, 0, 32)
_ClsBtn.Position = UDim2.new(1, -40, 0.5, -16)
_ClsBtn.Text = "X"
_ClsBtn.Font = Enum.Font.GothamBold
_ClsBtn.TextColor3 = _Cfg.Theme.CloseBtnText
_ClsBtn.BackgroundColor3 = _Cfg.Theme.CloseBtn
_ClsBtn.Parent = _Hdr

local _cbC = Instance.new("UICorner")
_cbC.CornerRadius = UDim.new(0, 8)
_cbC.Parent = _ClsBtn

_ClsBtn.MouseEnter:Connect(function()
    _Tws:Create(_ClsBtn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(70, 20, 35)}):Play()
end)
_ClsBtn.MouseLeave:Connect(function()
    _Tws:Create(_ClsBtn, TweenInfo.new(0.15), {BackgroundColor3 = _Cfg.Theme.CloseBtn}):Play()
end)

local _OpenBall = Instance.new("ImageButton")
_OpenBall.Name = "HCPOpenBall"
_OpenBall.Size = UDim2.new(0, 50, 0, 50)
_OpenBall.Position = UDim2.new(1, -64, 0.55, 0)
_OpenBall.BackgroundColor3 = Color3.fromRGB(0, 160, 255)
_OpenBall.BorderSizePixel = 0
_OpenBall.Visible = false
_OpenBall.AutoButtonColor = false
_OpenBall.Parent = _gui
local _obC = Instance.new("UICorner")
_obC.CornerRadius = UDim.new(1, 0)
_obC.Parent = _OpenBall
local _obS = Instance.new("UIStroke")
_obS.Color = Color3.fromRGB(255, 255, 255)
_obS.Thickness = 2
_obS.Transparency = 0.35
_obS.Parent = _OpenBall
local _obT = Instance.new("TextLabel")
_obT.Size = UDim2.new(1, 0, 1, 0)
_obT.BackgroundTransparency = 1
_obT.Font = Enum.Font.GothamBold
_obT.TextSize = 12
_obT.TextColor3 = Color3.fromRGB(255, 255, 255)
_obT.Text = "HCP"
_obT.Parent = _OpenBall

local _bDrag, _bStart, _bPos
_OpenBall.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
        _bDrag = true; _bStart = input.Position; _bPos = _OpenBall.Position
    end
end)
_Uis.InputChanged:Connect(function(input)
    if _bDrag and (input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseMovement) then
        local d = input.Position - _bStart
        _OpenBall.Position = UDim2.new(_bPos.X.Scale, _bPos.X.Offset + d.X, _bPos.Y.Scale, _bPos.Y.Offset + d.Y)
    end
end)
_Uis.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
        _bDrag = false
    end
end)
_OpenBall.MouseButton1Click:Connect(function()
    _MainF.Visible = true
    _OpenBall.Visible = false
end)
_MinBtn.MouseButton1Click:Connect(function()
    _MainF.Visible = false
    _OpenBall.Visible = true
end)

local _TabBar = Instance.new("Frame")
_TabBar.Size = UDim2.new(1, -20, 0, 32)
_TabBar.Position = UDim2.new(0, 10, 0, 55)
_TabBar.BackgroundTransparency = 1
_TabBar.Parent = _MainF

local _tbL = Instance.new("UIListLayout")
_tbL.FillDirection = Enum.FillDirection.Horizontal
_tbL.Padding = UDim.new(0, 6)
_tbL.Parent = _TabBar

local _TabPrin = Instance.new("TextButton")
_TabPrin.Size = UDim2.new(0.5, -3, 1, 0)
_TabPrin.Font = Enum.Font.GothamBold
_TabPrin.TextSize = 11
_TabPrin.Text = _L.tabMain
_TabPrin.TextColor3 = _Cfg.Theme.TextPrimary
_TabPrin.Parent = _TabBar

local _tpC = Instance.new("UICorner")
_tpC.CornerRadius = UDim.new(0, 6)
_tpC.Parent = _TabPrin

local _TabCfg = Instance.new("TextButton")
_TabCfg.Size = UDim2.new(0.5, -3, 1, 0)
_TabCfg.Font = Enum.Font.GothamBold
_TabCfg.TextSize = 11
_TabCfg.Text = "⚙️ " .. _L.tabCfg
_TabCfg.TextColor3 = _Cfg.Theme.TextPrimary
_TabCfg.Parent = _TabBar

local _tcC = Instance.new("UICorner")
_tcC.CornerRadius = UDim.new(0, 6)
_tcC.Parent = _TabCfg

local _ContPrin = Instance.new("Frame")
_ContPrin.Size = UDim2.new(1, -20, 1, -105)
_ContPrin.Position = UDim2.new(0, 10, 0, 95)
_ContPrin.BackgroundTransparency = 1
_ContPrin.Parent = _MainF

local _ContCfg = Instance.new("ScrollingFrame")
_ContCfg.Size = UDim2.new(1, -20, 1, -105)
_ContCfg.Position = UDim2.new(0, 10, 0, 95)
_ContCfg.BackgroundTransparency = 1
_ContCfg.Visible = false
_ContCfg.AutomaticCanvasSize = Enum.AutomaticSize.Y
_ContCfg.ScrollBarThickness = 3
_ContCfg.ScrollBarImageColor3 = _Cfg.Theme.ScrollBar
_ContCfg.Parent = _MainF

local function _switchTab(name)
    _St.currentTab = name
    local ti = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    if name == "Principal" then
        _Tws:Create(_TabPrin, ti, {BackgroundColor3 = _Cfg.Theme.TabActive}):Play()
        _Tws:Create(_TabCfg, ti, {BackgroundColor3 = _Cfg.Theme.TabInactive}):Play()
        _TabPrin.TextColor3 = Color3.fromRGB(10, 10, 20)
        _TabCfg.TextColor3 = _Cfg.Theme.TextPrimary
        _ContPrin.Visible = true
        _ContCfg.Visible = false
    else
        _Tws:Create(_TabPrin, ti, {BackgroundColor3 = _Cfg.Theme.TabInactive}):Play()
        _Tws:Create(_TabCfg, ti, {BackgroundColor3 = _Cfg.Theme.TabActive}):Play()
        _TabPrin.TextColor3 = _Cfg.Theme.TextPrimary
        _TabCfg.TextColor3 = Color3.fromRGB(10, 10, 20)
        _ContPrin.Visible = false
        _ContCfg.Visible = true
    end
end
_switchTab("Principal")

local function _addHover(b, n)
    b.MouseEnter:Connect(function()
        if _St.currentTab ~= n then _Tws:Create(b, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(30, 25, 45)}):Play() end
    end)
    b.MouseLeave:Connect(function()
        if _St.currentTab ~= n then _Tws:Create(b, TweenInfo.new(0.15), {BackgroundColor3 = _Cfg.Theme.TabInactive}):Play() end
    end)
end
_addHover(_TabPrin, "Principal")
_addHover(_TabCfg, "Config")

_TabPrin.MouseButton1Click:Connect(function() _switchTab("Principal") end)
_TabCfg.MouseButton1Click:Connect(function() _switchTab("Config") end)

local _TogPanel = Instance.new("Frame")
_TogPanel.Size = UDim2.new(1, 0, 0, 50)
_TogPanel.Position = UDim2.new(0, 0, 0, 5)
_TogPanel.BackgroundTransparency = 1
_TogPanel.Parent = _ContPrin

local _grid = Instance.new("UIGridLayout")
_grid.CellSize = UDim2.new(0.32, 0, 0, 30)
_grid.CellPadding = UDim2.new(0, 6, 0, 6)
_grid.Parent = _TogPanel

local function _createTogBtn(p, txt)
    local b = Instance.new("TextButton")
    b.Font = Enum.Font.GothamBold
    b.TextSize = 9
    b.TextColor3 = _Cfg.Theme.TextPrimary
    b.Text = txt
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 6)
    c.Parent = b
    b.MouseEnter:Connect(function() _Tws:Create(b, TweenInfo.new(0.15), {TextStrokeTransparency = 0.5}):Play() end)
    b.MouseLeave:Connect(function() _Tws:Create(b, TweenInfo.new(0.15), {TextStrokeTransparency = 1}):Play() end)
    b.Parent = p
    return b
end

local _AimBtn = _createTogBtn(_TogPanel, _L.aimbot)
local _EspBtn = _createTogBtn(_TogPanel, "ESP VISUALS")
local _InvBtn = _createTogBtn(_TogPanel, "INV VIEW")

local _scroll = Instance.new("ScrollingFrame")
_scroll.Size = UDim2.new(1, 0, 1, -55)
_scroll.Position = UDim2.new(0, 0, 0, 55)
_scroll.BackgroundTransparency = 1
_scroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
_scroll.ScrollBarThickness = 4
_scroll.ScrollBarImageColor3 = _Cfg.Theme.ScrollBar
_scroll.Parent = _ContPrin

local _sLayout = Instance.new("UIListLayout")
_sLayout.SortOrder = Enum.SortOrder.LayoutOrder
_sLayout.Padding = UDim.new(0, 5)
_sLayout.Parent = _scroll

local function _updateMainBtns()
    local ti = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    _Tws:Create(_AimBtn, ti, {BackgroundColor3 = _St.aimEnabled and _Cfg.Theme.BtnOn or _Cfg.Theme.BtnOff}):Play()
    _AimBtn.Text = "AIMBOT: " .. (_St.aimEnabled and "ON" or "OFF")
    _AimBtn.TextColor3 = _St.aimEnabled and Color3.fromRGB(10,10,20) or _Cfg.Theme.TextPrimary

    _Tws:Create(_EspBtn, ti, {BackgroundColor3 = _St.espEnabled and _Cfg.Theme.BtnOn or _Cfg.Theme.BtnOff}):Play()
    _EspBtn.Text = "ESP VISUALS: " .. (_St.espEnabled and "ON" or "OFF")
    _EspBtn.TextColor3 = _St.espEnabled and Color3.fromRGB(10,10,20) or _Cfg.Theme.TextPrimary

    _Tws:Create(_InvBtn, ti, {BackgroundColor3 = _St.invViewEnabled and _Cfg.Theme.BtnOn or _Cfg.Theme.BtnOff}):Play()
    _InvBtn.Text = "INV VIEW: " .. (_St.invViewEnabled and "ON" or "OFF")
    _InvBtn.TextColor3 = _St.invViewEnabled and Color3.fromRGB(10,10,20) or _Cfg.Theme.TextPrimary
end
_updateMainBtns()

_AimBtn.MouseButton1Click:Connect(function() 
    _St.aimEnabled = not _St.aimEnabled 
    if not _St.aimEnabled then _St.lockedTarget = nil end
    _updateMainBtns() 
    _saveConfig()
end)
_EspBtn.MouseButton1Click:Connect(function() 
    _St.espEnabled = not _St.espEnabled
    _updateMainBtns() 
    _saveConfig()
end)
_InvBtn.MouseButton1Click:Connect(function() 
    _St.invViewEnabled = not _St.invViewEnabled
    _updateMainBtns() 
    _saveConfig()
end)

local _cfgLayout = Instance.new("UIListLayout")
_cfgLayout.SortOrder = Enum.SortOrder.LayoutOrder
_cfgLayout.Padding = UDim.new(0, 14)
_cfgLayout.Parent = _ContCfg

local function _createConfigSec(tText, bData, cb)
    local f = Instance.new("Frame")
    f.Size = UDim2.new(1, 0, 0, 55)
    f.BackgroundTransparency = 1
    
    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(1, 0, 0, 18)
    lbl.Font = Enum.Font.GothamBold
    lbl.TextSize = 11
    lbl.TextColor3 = _Cfg.Theme.TextSecondary
    lbl.Text = tText:upper()
    lbl.TextXAlignment = Enum.TextXAlignment.Left
    lbl.BackgroundTransparency = 1
    lbl.Parent = f

    local bc = Instance.new("Frame")
    bc.Size = UDim2.new(1, 0, 0, 32)
    bc.Position = UDim2.new(0, 0, 0, 20)
    bc.BackgroundTransparency = 1

    local bl = Instance.new("UIListLayout")
    bl.FillDirection = Enum.FillDirection.Horizontal
    bl.Padding = UDim.new(0, 6)
    bl.Parent = bc

    local cBtns = {}
    local wShare = 1 / #bData
    local ti = TweenInfo.new(0.15, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)

    for _, opt in ipairs(bData) do
        local ob = Instance.new("TextButton")
        ob.Size = UDim2.new(wShare, -4, 1, 0)
        ob.Font = Enum.Font.GothamBold
        ob.TextSize = 9
        ob.TextScaled = true
        ob.TextWrapped = true
        ob.Text = opt.Label
        local ts = Instance.new("UITextSizeConstraint")
        ts.MaxTextSize = 10
        ts.MinTextSize = 7
        ts.Parent = ob
        local oc = Instance.new("UICorner")
        oc.CornerRadius = UDim.new(0, 5)
        oc.Parent = ob
        cBtns[opt.Value] = ob

        ob.MouseEnter:Connect(function()
            if ob.BackgroundColor3 ~= _Cfg.Theme.TabActive then _Tws:Create(ob, ti, {BackgroundColor3 = Color3.fromRGB(30, 25, 45)}):Play() end
        end)
        ob.MouseLeave:Connect(function()
            if ob.BackgroundColor3 ~= _Cfg.Theme.TabActive then _Tws:Create(ob, ti, {BackgroundColor3 = _Cfg.Theme.TabInactive}):Play() end
        end)

        ob.MouseButton1Click:Connect(function()
            cb(opt.Value)
            for val, b in pairs(cBtns) do
                local act = (val == opt.Value)
                _Tws:Create(b, ti, {BackgroundColor3 = act and _Cfg.Theme.TabActive or _Cfg.Theme.TabInactive}):Play()
                b.TextColor3 = act and Color3.fromRGB(10, 10, 20) or _Cfg.Theme.TextSecondary
            end
            _saveConfig() 
        end)
        ob.Parent = bc
    end
    bc.Parent = f
    f.Parent = _ContCfg
    return cBtns
end

local _saveLoadSec = Instance.new("Frame")
_saveLoadSec.Size = UDim2.new(1, 0, 0, 55)
_saveLoadSec.BackgroundTransparency = 1
_saveLoadSec.Parent = _ContCfg

local _slLbl = Instance.new("TextLabel")
_slLbl.Size = UDim2.new(1, 0, 0, 18)
_slLbl.Font = Enum.Font.GothamBold
_slLbl.TextSize = 11
_slLbl.TextColor3 = _Cfg.Theme.TextSecondary
_slLbl.Text = _L.cfgSys
_slLbl.TextXAlignment = Enum.TextXAlignment.Left
_slLbl.BackgroundTransparency = 1
_slLbl.Parent = _saveLoadSec

local _slCont = Instance.new("Frame")
_slCont.Size = UDim2.new(1, 0, 0, 32)
_slCont.Position = UDim2.new(0, 0, 0, 20)
_slCont.BackgroundTransparency = 1
_slCont.Parent = _saveLoadSec

local _slL = Instance.new("UIListLayout")
_slL.FillDirection = Enum.FillDirection.Horizontal
_slL.Padding = UDim.new(0, 6)
_slL.Parent = _slCont

local _saveBtn = Instance.new("TextButton")
_saveBtn.Size = UDim2.new(0.5, -3, 1, 0)
_saveBtn.Font = Enum.Font.GothamBold
_saveBtn.TextSize = 10
_saveBtn.BackgroundColor3 = _Cfg.Theme.TabInactive
_saveBtn.TextColor3 = _Cfg.Theme.TextPrimary
_saveBtn.Text = "💾 " .. _L.saveCfg
_saveBtn.Parent = _slCont

local _sbc = Instance.new("UICorner")
_sbc.CornerRadius = UDim.new(0, 5)
_sbc.Parent = _saveBtn

local _loadBtn = Instance.new("TextButton")
_loadBtn.Size = UDim2.new(0.5, -3, 1, 0)
_loadBtn.Font = Enum.Font.GothamBold
_loadBtn.TextSize = 10
_loadBtn.BackgroundColor3 = _Cfg.Theme.TabInactive
_loadBtn.TextColor3 = _Cfg.Theme.TextPrimary
_loadBtn.Text = "📂 " .. _L.loadCfg
_loadBtn.Parent = _slCont

local _lbc = Instance.new("UICorner")
_lbc.CornerRadius = UDim.new(0, 5)
_lbc.Parent = _loadBtn

local _aimModeBtns = _createConfigSec(_L.aimMode, {
    {Label = _L.modeToggle, Value = "Toggle"},
    {Label = _L.modeFov, Value = "FOV"},
    {Label = _L.modeHold, Value = "Hold"}
}, function(val)
    _Cfg.AimMode = val
    _St.lockedTarget = nil
end)

local _fovSec = Instance.new("Frame")
_fovSec.Size = UDim2.new(1, 0, 0, 70)
_fovSec.BackgroundTransparency = 1
_fovSec.Parent = _ContCfg

local _fovLbl = Instance.new("TextLabel")
_fovLbl.Size = UDim2.new(1, -60, 0, 18)
_fovLbl.Font = Enum.Font.GothamBold
_fovLbl.TextSize = 11
_fovLbl.TextColor3 = _Cfg.Theme.TextSecondary
_fovLbl.Text = _L.fovSize
_fovLbl.TextXAlignment = Enum.TextXAlignment.Left
_fovLbl.BackgroundTransparency = 1
_fovLbl.Parent = _fovSec

local _fovValLbl = Instance.new("TextLabel")
_fovValLbl.Size = UDim2.new(0, 55, 0, 18)
_fovValLbl.Position = UDim2.new(1, -55, 0, 0)
_fovValLbl.Font = Enum.Font.GothamBold
_fovValLbl.TextSize = 12
_fovValLbl.TextColor3 = _Cfg.Theme.TabActive
_fovValLbl.Text = tostring(_Cfg.AimFOV)
_fovValLbl.TextXAlignment = Enum.TextXAlignment.Right
_fovValLbl.BackgroundTransparency = 1
_fovValLbl.Parent = _fovSec

local _FOV_MIN, _FOV_MAX = 40, 400
local _fovTrack = Instance.new("Frame")
_fovTrack.Size = UDim2.new(1, 0, 0, 16)
_fovTrack.Position = UDim2.new(0, 0, 0, 32)
_fovTrack.BackgroundColor3 = _Cfg.Theme.TabInactive
_fovTrack.BorderSizePixel = 0
_fovTrack.Parent = _fovSec
local _fovTrackC = Instance.new("UICorner")
_fovTrackC.CornerRadius = UDim.new(1, 0)
_fovTrackC.Parent = _fovTrack

local _fovFill = Instance.new("Frame")
_fovFill.Size = UDim2.new(math.clamp((_Cfg.AimFOV - _FOV_MIN) / (_FOV_MAX - _FOV_MIN), 0, 1), 0, 1, 0)
_fovFill.BackgroundColor3 = _Cfg.Theme.TabActive
_fovFill.BorderSizePixel = 0
_fovFill.Parent = _fovTrack
local _fovFillC = Instance.new("UICorner")
_fovFillC.CornerRadius = UDim.new(1, 0)
_fovFillC.Parent = _fovFill

local _fovKnob = Instance.new("Frame")
_fovKnob.Size = UDim2.new(0, 22, 0, 22)
_fovKnob.AnchorPoint = Vector2.new(0.5, 0.5)
_fovKnob.Position = UDim2.new(math.clamp((_Cfg.AimFOV - _FOV_MIN) / (_FOV_MAX - _FOV_MIN), 0, 1), 0, 0.5, 0)
_fovKnob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
_fovKnob.BorderSizePixel = 0
_fovKnob.ZIndex = 2
_fovKnob.Parent = _fovTrack
local _fovKnobC = Instance.new("UICorner")
_fovKnobC.CornerRadius = UDim.new(1, 0)
_fovKnobC.Parent = _fovKnob
local _fovKnobS = Instance.new("UIStroke")
_fovKnobS.Color = _Cfg.Theme.TabActive
_fovKnobS.Thickness = 2
_fovKnobS.Parent = _fovKnob

local function _applyFovAlpha(alpha)
    alpha = math.clamp(alpha, 0, 1)
    local val = math.floor(_FOV_MIN + alpha * (_FOV_MAX - _FOV_MIN) + 0.5)
    _Cfg.AimFOV = val
    _fovFill.Size = UDim2.new(alpha, 0, 1, 0)
    _fovKnob.Position = UDim2.new(alpha, 0, 0.5, 0)
    _fovValLbl.Text = tostring(val)
    if _FOVCircle then pcall(function() _FOVCircle.Radius = _Cfg.AimFOV end) end
end

local function _updateFovSliderUI()
    local alpha = math.clamp((_Cfg.AimFOV - _FOV_MIN) / (_FOV_MAX - _FOV_MIN), 0, 1)
    _fovFill.Size = UDim2.new(alpha, 0, 1, 0)
    _fovKnob.Position = UDim2.new(alpha, 0, 0.5, 0)
    _fovValLbl.Text = tostring(_Cfg.AimFOV)
end

local _fovDragging = false
local function _fovFromInput(input)
    local absPos = _fovTrack.AbsolutePosition.X
    local absSize = _fovTrack.AbsoluteSize.X
    if absSize <= 0 then return end
    _applyFovAlpha((input.Position.X - absPos) / absSize)
end

_fovTrack.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        _fovDragging = true
        _fovFromInput(input)
    end
end)
_fovKnob.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        _fovDragging = true
    end
end)
_safeConn(_Uis.InputChanged, function(input)
    if not _fovDragging then return end
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        _fovFromInput(input)
    end
end)
_safeConn(_Uis.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        if _fovDragging then
            _fovDragging = false
            _saveConfig()
        end
    end
end)

local _sliderSec = Instance.new("Frame")
_sliderSec.Size = UDim2.new(1, 0, 0, 65)
_sliderSec.BackgroundTransparency = 1
_sliderSec.Parent = _ContCfg

local _sliderLbl = Instance.new("TextLabel")
_sliderLbl.Size = UDim2.new(1, 0, 0, 18)
_sliderLbl.Font = Enum.Font.GothamBold
_sliderLbl.TextSize = 11
_sliderLbl.TextColor3 = _Cfg.Theme.TextSecondary
_sliderLbl.Text = string.format(_L.distEsp, tostring(_Cfg.MaxNormalDistance))
_sliderLbl.TextXAlignment = Enum.TextXAlignment.Left
_sliderLbl.BackgroundTransparency = 1
_sliderLbl.Parent = _sliderSec

local _sliderCont = Instance.new("Frame")
_sliderCont.Size = UDim2.new(1, 0, 0, 32)
_sliderCont.Position = UDim2.new(0, 0, 0, 22)
_sliderCont.BackgroundColor3 = _Cfg.Theme.TabInactive
_sliderCont.Parent = _sliderSec

local _slc = Instance.new("UICorner")
_slc.CornerRadius = UDim.new(0, 6)
_slc.Parent = _sliderCont

local _sliderBar = Instance.new("Frame")
_sliderBar.Size = UDim2.new(1, -20, 0, 6)
_sliderBar.Position = UDim2.new(0, 10, 0.5, -3)
_sliderBar.BackgroundColor3 = Color3.fromRGB(40, 35, 60)
_sliderBar.BorderSizePixel = 0
_sliderBar.Parent = _sliderCont

local _sbc2 = Instance.new("UICorner")
_sbc2.CornerRadius = UDim.new(0, 3)
_sbc2.Parent = _sliderBar

local _sliderFill = Instance.new("Frame")
_sliderFill.BackgroundColor3 = _Cfg.Theme.TabActive
_sliderFill.BorderSizePixel = 0
_sliderFill.Parent = _sliderBar

local _sfc = Instance.new("UICorner")
_sfc.CornerRadius = UDim.new(0, 3)
_sfc.Parent = _sliderFill

local _sliderBtn = Instance.new("TextButton")
_sliderBtn.Size = UDim2.new(0, 14, 0, 14)
_sliderBtn.BackgroundColor3 = _Cfg.Theme.TextPrimary
_sliderBtn.Text = ""
_sliderBtn.Parent = _sliderBar

local _sbtnc = Instance.new("UICorner")
_sbtnc.CornerRadius = UDim.new(1, 0)
_sbtnc.Parent = _sliderBtn

local _minDist = 100
local _maxDist = 5000
local _sliderDrag = false

local function _updateSlider(val)
    local pct = math.clamp((val - _minDist) / (_maxDist - _minDist), 0, 1)
    _sliderBtn.Position = UDim2.new(pct, -7, 0.5, -7)
    _sliderFill.Size = UDim2.new(pct, 0, 1, 0)
    _sliderLbl.Text = string.format(_L.distEsp, tostring(val))
end

_sliderBtn.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        _sliderDrag = true
    end
end)

_safeConn(_Uis.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        if _sliderDrag then
            _sliderDrag = false
            _saveConfig() 
        end
    end
end)

_safeConn(_Uis.InputChanged, function(input)
    if _sliderDrag and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local bSize = _sliderBar.AbsoluteSize.X
        if bSize > 0 then
            local mX = input.Position.X - _sliderBar.AbsolutePosition.X
            local pct = math.clamp(mX / bSize, 0, 1)
            local val = math.floor(_minDist + (pct * (_maxDist - _minDist)))
            _Cfg.MaxNormalDistance = val
            _Cfg.MaxSpecialDistance = math.floor(val * 1.5)
            _updateSlider(val)
        end
    end
end)

_updateSlider(_Cfg.MaxNormalDistance)

local _skelBtns = _createConfigSec(_L.skel, {
    {Label = "❌ " .. _L.off, Value = "Off"}, {Label = "🟡 " .. _L.gold, Value = "Oro"}, {Label = "⚪ " .. _L.white, Value = "Blanco"}, {Label = "🔵 " .. _L.cyan, Value = "Equipo"}
}, function(val) _Cfg.SkeletonStyle = val end)

local _targetBtns = _createConfigSec(_L.target, {
    {Label = "👤 " .. _L.head, Value = "Cabeza"}, {Label = _L.chest, Value = "Pecho"}, {Label = "🔀 " .. _L.mixed, Value = "Mixto"}
}, function(val) _Cfg.AimTarget = val; _St.lockedTarget = nil end)

local _smoothBtns = _createConfigSec(_L.smooth, {
    {Label = "⚡ " .. _L.low, Value = "Bajo"}, {Label = "🛡️ " .. _L.mid, Value = "Medio"}, {Label = "🍃 " .. _L.high, Value = "Alto"}
}, function(val) _Cfg.AimSmooth = val end)

local _bindSec = Instance.new("Frame")
_bindSec.Size = UDim2.new(1, 0, 0, 55)
_bindSec.BackgroundTransparency = 1
_bindSec.Parent = _ContCfg

local _bindLbl = Instance.new("TextLabel")
_bindLbl.Size = UDim2.new(1, 0, 0, 18)
_bindLbl.Font = Enum.Font.GothamBold
_bindLbl.TextSize = 11
_bindLbl.TextColor3 = _Cfg.Theme.TextSecondary
_bindLbl.Text = _L.binds
_bindLbl.TextXAlignment = Enum.TextXAlignment.Left
_bindLbl.BackgroundTransparency = 1
_bindLbl.Parent = _bindSec

local _bindCont = Instance.new("Frame")
_bindCont.Size = UDim2.new(1, 0, 0, 32)
_bindCont.Position = UDim2.new(0, 0, 0, 20)
_bindCont.BackgroundTransparency = 1
_bindCont.Parent = _bindSec

local _bindL = Instance.new("UIListLayout")
_bindL.FillDirection = Enum.FillDirection.Horizontal
_bindL.Padding = UDim.new(0, 6)
_bindL.Parent = _bindCont

local _bindBtns = {}
local _actions = {"ToggleMenu", "Aimbot", "InvView"}
local _bLabels = {ToggleMenu = _L.menu, Aimbot = "Aim", InvView = "Inv"}

for _, act in ipairs(_actions) do
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.32, -4, 1, 0)
    b.Font = Enum.Font.GothamBold
    b.TextSize = 9
    b.BackgroundColor3 = _Cfg.Theme.TabInactive
    b.TextColor3 = _Cfg.Theme.TextPrimary
    b.Parent = _bindCont
    
    local bc = Instance.new("UICorner")
    bc.CornerRadius = UDim.new(0, 5)
    bc.Parent = b
    _bindBtns[act] = b

    b.MouseEnter:Connect(function()
        if _St.isBinding ~= act then _Tws:Create(b, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(30, 25, 45)}):Play() end
    end)
    b.MouseLeave:Connect(function()
        if _St.isBinding ~= act then _Tws:Create(b, TweenInfo.new(0.15), {BackgroundColor3 = _Cfg.Theme.TabInactive}):Play() end
    end)

    b.MouseButton1Click:Connect(function()
        if _St.isBinding then return end
        _St.isBinding = act
        b.Text = "...¡Presiona!..."
        b.BackgroundColor3 = _Cfg.Theme.PinActive
    end)
end

local function _updateBindsUi()
    for act, b in pairs(_bindBtns) do
        if _St.isBinding ~= act then
            b.Text = _bLabels[act] .. ": [" .. _Cfg.Binds[act].Name .. "]"
            b.BackgroundColor3 = _Cfg.Theme.TabInactive
            b.TextColor3 = _Cfg.Theme.TextPrimary
        end
    end
end

local function _syncUi()
    local function setAct(b, act)
        b.BackgroundColor3 = act and _Cfg.Theme.TabActive or _Cfg.Theme.TabInactive
        b.TextColor3 = act and Color3.fromRGB(10,10,20) or _Cfg.Theme.TextSecondary
    end
    for val, b in pairs(_aimModeBtns) do setAct(b, val == _Cfg.AimMode) end
    for val, b in pairs(_skelBtns) do setAct(b, val == _Cfg.SkeletonStyle) end
    for val, b in pairs(_targetBtns) do setAct(b, val == _Cfg.AimTarget) end
    for val, b in pairs(_smoothBtns) do setAct(b, val == _Cfg.AimSmooth) end
    
    if _sliderBtn and _sliderFill and _sliderLbl then
        _updateSlider(_Cfg.MaxNormalDistance)
    end
    _updateBindsUi()
    if _updateFovSliderUI then
        _updateFovSliderUI()
    end
end

_saveConfig = function()
    if not (type(_writefile) == "function") then return false end
    local sData = {
        AimTarget = _Cfg.AimTarget, AimSmooth = _Cfg.AimSmooth, AimMode = _Cfg.AimMode,
        AimFOV = _Cfg.AimFOV, ShowFOV = _Cfg.ShowFOV, SkeletonStyle = _Cfg.SkeletonStyle,
        MaxNormalDistance = _Cfg.MaxNormalDistance, AutoExecute = _Cfg.AutoExecute,
        Binds = {ToggleMenu = _Cfg.Binds.ToggleMenu.Name, Aimbot = _Cfg.Binds.Aimbot.Name, InvView = _Cfg.Binds.InvView.Name},
        Toggles = {aimEnabled = _St.aimEnabled, espEnabled = _St.espEnabled, invViewEnabled = _St.invViewEnabled}
    }
    local ok, enc = pcall(function() return _Hts:JSONEncode(sData) end)
    if ok and enc then
        pcall(function() _writefile(_CfgFile, enc) end)
        return true
    end
    return false
end

_loadConfig = function()
    if not (type(_readfile) == "function" and type(_isfile) == "function") or not _isfile(_CfgFile) then return false end
    local ok, content = pcall(function() return _readfile(_CfgFile) end)
    if not ok or not content then return false end
    local decOk, dec = pcall(function() return _Hts:JSONDecode(content) end)
    if not decOk or type(dec) ~= "table" then return false end
    
    if dec.AimTarget ~= nil then _Cfg.AimTarget = dec.AimTarget end
    if dec.AimSmooth ~= nil then _Cfg.AimSmooth = dec.AimSmooth end
    if dec.AimMode ~= nil then _Cfg.AimMode = dec.AimMode end
    if dec.AimFOV ~= nil then _Cfg.AimFOV = tonumber(dec.AimFOV) or _Cfg.AimFOV end
    if dec.ShowFOV ~= nil then _Cfg.ShowFOV = dec.ShowFOV end
    if dec.SkeletonStyle ~= nil then _Cfg.SkeletonStyle = dec.SkeletonStyle end
    if dec.MaxNormalDistance ~= nil then 
        _Cfg.MaxNormalDistance = dec.MaxNormalDistance 
        _Cfg.MaxSpecialDistance = math.floor(dec.MaxNormalDistance * 1.5)
    end
    
    if type(dec.Binds) == "table" then
        for act, kName in pairs(dec.Binds) do
            if _Cfg.Binds[act] and Enum.KeyCode[kName] then _Cfg.Binds[act] = Enum.KeyCode[kName] end
        end
    end
    if type(dec.Toggles) == "table" then
        if dec.Toggles.aimEnabled ~= nil then _St.aimEnabled = dec.Toggles.aimEnabled end
        if dec.Toggles.espEnabled ~= nil then _St.espEnabled = dec.Toggles.espEnabled end
        if dec.Toggles.invViewEnabled ~= nil then _St.invViewEnabled = dec.Toggles.invViewEnabled end
    end
    _syncUi()
    _updateMainBtns()
    return true
end

_syncUi()

_saveBtn.MouseButton1Click:Connect(function()
    if _saveConfig() then
        _saveBtn.Text = "✅ ¡GUARDADO!"; _saveBtn.BackgroundColor3 = _Cfg.Theme.TeamActive; _saveBtn.TextColor3 = Color3.fromRGB(10, 10, 20)
        task.delay(1.5, function() _saveBtn.Text = "💾 " .. _L.saveCfg; _saveBtn.BackgroundColor3 = _Cfg.Theme.TabInactive; _saveBtn.TextColor3 = _Cfg.Theme.TextPrimary end)
    else
        _saveBtn.Text = "❌ ERROR"; _saveBtn.BackgroundColor3 = _Cfg.Theme.BtnOff
        task.delay(1.5, function() _saveBtn.Text = "💾 " .. _L.saveCfg; _saveBtn.BackgroundColor3 = _Cfg.Theme.TabInactive end)
    end
end)

_loadBtn.MouseButton1Click:Connect(function()
    if _loadConfig() then
        _loadBtn.Text = "✅ ¡CARGADO!"; _loadBtn.BackgroundColor3 = _Cfg.Theme.TeamActive; _loadBtn.TextColor3 = Color3.fromRGB(10, 10, 20)
        task.delay(1.5, function() _loadBtn.Text = "📂 " .. _L.loadCfg; _loadBtn.BackgroundColor3 = _Cfg.Theme.TabInactive; _loadBtn.TextColor3 = _Cfg.Theme.TextPrimary end)
    else
        _loadBtn.Text = "❌ SIN ARCHIVO"; _loadBtn.BackgroundColor3 = _Cfg.Theme.BtnOff
        task.delay(1.5, function() _loadBtn.Text = "📂 " .. _L.loadCfg; _loadBtn.BackgroundColor3 = _Cfg.Theme.TabInactive end)
    end
end)

local function _getSkelColor(plr)
    if _Cfg.SkeletonStyle == "Oro" then return _Cfg.Theme.Gold end
    if _Cfg.SkeletonStyle == "Blanco" then return Color3.fromRGB(255, 255, 255) end
    if _Cfg.SkeletonStyle == "Equipo" then return _St.teamPlayers[plr.Name] and _Cfg.Theme.EspTeam or _Cfg.Theme.Stroke end
    return Color3.fromRGB(255, 255, 255)
end

local function _createLine()
    if not _hasDrawing then return nil end
    local ok, l = pcall(_Drawing.new, "Line")
    if ok and l then
        l.Thickness = 1.5; l.Transparency = 1; l.Visible = false
        return l
    end
    return nil
end

local function _getSkel(plr)
    local name = plr.Name
    if not _SkelCache[name] then
        _SkelCache[name] = {
            Head_Spine = _createLine(), Spine_LeftArm = _createLine(), Spine_RightArm = _createLine(),
            LeftArm_Hand = _createLine(), RightArm_Hand = _createLine(), Spine_LeftLeg = _createLine(),
            Spine_RightLeg = _createLine(), LeftLeg_Foot = _createLine(), RightLeg_Foot = _createLine()
        }
    end
    return _SkelCache[name]
end

local function _hideSkel(plr)
    local sk = _SkelCache[plr.Name]
    if sk then
        for _, l in pairs(sk) do if l then pcall(function() l.Visible = false end) end end
    end
end

local function _updateSkelEsp(plr, char)
    if not _St.espEnabled or _Cfg.SkeletonStyle == "Off" or not _hasDrawing then _hideSkel(plr); return end
    local sk = _getSkel(plr)
    local col = _getSkelColor(plr)

    local function connJ(line, p1, p2)
        if not line then return end
        if p1 and p2 then
            local v1, vis1 = _Cam:WorldToViewportPoint(p1.Position)
            local v2, vis2 = _Cam:WorldToViewportPoint(p2.Position)
            if vis1 or vis2 then
                pcall(function() line.From = Vector2.new(v1.X, v1.Y); line.To = Vector2.new(v2.X, v2.Y); line.Color = col; line.Visible = true end)
                return
            end
        end
        pcall(function() line.Visible = false end)
    end

    if char:FindFirstChild("UpperTorso") then
        connJ(sk.Head_Spine, char:FindFirstChild("Head"), char:FindFirstChild("UpperTorso"))
        connJ(sk.Spine_LeftArm, char:FindFirstChild("UpperTorso"), char:FindFirstChild("LeftUpperArm"))
        connJ(sk.Spine_RightArm, char:FindFirstChild("UpperTorso"), char:FindFirstChild("RightUpperArm"))
        connJ(sk.LeftArm_Hand, char:FindFirstChild("LeftUpperArm"), char:FindFirstChild("LeftHand"))
        connJ(sk.RightArm_Hand, char:FindFirstChild("RightUpperArm"), char:FindFirstChild("RightHand"))
        connJ(sk.Spine_LeftLeg, char:FindFirstChild("LowerTorso"), char:FindFirstChild("LeftUpperLeg"))
        connJ(sk.Spine_RightLeg, char:FindFirstChild("LowerTorso"), char:FindFirstChild("RightUpperLeg"))
        connJ(sk.LeftLeg_Foot, char:FindFirstChild("LeftUpperLeg"), char:FindFirstChild("LeftFoot"))
        connJ(sk.RightLeg_Foot, char:FindFirstChild("RightUpperLeg"), char:FindFirstChild("RightFoot"))
    elseif char:FindFirstChild("Torso") then
        connJ(sk.Head_Spine, char:FindFirstChild("Head"), char:FindFirstChild("Torso"))
        connJ(sk.Spine_LeftArm, char:FindFirstChild("Torso"), char:FindFirstChild("Left Arm"))
        connJ(sk.Spine_RightArm, char:FindFirstChild("Torso"), char:FindFirstChild("Right Arm"))
        connJ(sk.Spine_LeftLeg, char:FindFirstChild("Torso"), char:FindFirstChild("Left Leg"))
        connJ(sk.Spine_RightLeg, char:FindFirstChild("Torso"), char:FindFirstChild("Right Leg"))
    else
        _hideSkel(plr)
    end
end

local function _getMyPos()
    local char = _LP.Character
    if char then
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum and hum.SeatPart then return hum.SeatPart.Position end
        local root = char:FindFirstChild("HumanoidRootPart")
        if root then return root.Position end
    end
    return _Cam.CFrame.Position
end

local function _renderPlrList()
    local activeP, pList = {}, {}
    for _, p in ipairs(_Plrs:GetPlayers()) do 
        if p ~= _LP then activeP[p.Name] = true; table.insert(pList, p) end 
    end
    for name, f in pairs(_RowCache) do 
        if not activeP[name] then f:Destroy(); _RowCache[name] = nil end 
    end

    table.sort(pList, function(a, b)
        local aPin = _St.pinnedPlayers[a.Name] and 1 or 0
        local bPin = _St.pinnedPlayers[b.Name] and 1 or 0
        if aPin ~= bPin then return aPin > bPin end
        return a.Name < b.Name
    end)

    for ord, p in ipairs(pList) do
        local isPin, isTeam = _St.pinnedPlayers[p.Name], _St.teamPlayers[p.Name]
        local row = _RowCache[p.Name]
        
        if not row then
            row = Instance.new("Frame")
            row.Size = UDim2.new(1, -6, 0, 38)
            
            local rc = Instance.new("UICorner")
            rc.CornerRadius = UDim.new(0, 6)
            rc.Parent = row
            
            local uBtn = Instance.new("TextLabel")
            uBtn.Name = "UserBtn"
            uBtn.Size = UDim2.new(1, -110, 1, 0)
            uBtn.Position = UDim2.new(0, 8, 0, 0)
            uBtn.BackgroundTransparency = 1
            uBtn.Font = Enum.Font.GothamBold
            uBtn.TextSize = 11
            uBtn.TextXAlignment = Enum.TextXAlignment.Left
            uBtn.Parent = row

            local tBtn = Instance.new("TextButton")
            tBtn.Name = "TeamBtn"
            tBtn.Size = UDim2.new(0, 45, 0, 22)
            tBtn.Position = UDim2.new(1, -95, 0.5, -11)
            tBtn.Font = Enum.Font.GothamBold
            tBtn.TextSize = 9
            tBtn.TextColor3 = _Cfg.Theme.TextPrimary
            
            local tc = Instance.new("UICorner")
            tc.CornerRadius = UDim.new(0, 4)
            tc.Parent = tBtn
            tBtn.Parent = row

            local pBtn = Instance.new("TextButton")
            pBtn.Name = "PinBtn"
            pBtn.Size = UDim2.new(0, 40, 0, 22)
            pBtn.Position = UDim2.new(1, -45, 0.5, -11)
            pBtn.Font = Enum.Font.GothamBold
            pBtn.TextSize = 9
            pBtn.TextColor3 = _Cfg.Theme.TextPrimary
            
            local pc = Instance.new("UICorner")
            pc.CornerRadius = UDim.new(0, 5)
            pc.Parent = pBtn
            pBtn.Parent = row

            tBtn.MouseButton1Click:Connect(function() 
                _St.teamPlayers[p.Name] = not _St.teamPlayers[p.Name] or nil
                _renderPlrList()
                _saveConfig() 
            end)
            pBtn.MouseButton1Click:Connect(function() 
                if _St.pinnedPlayers[p.Name] then 
                    _St.pinnedPlayers[p.Name] = nil
                    _St.autoPinned[p.Name] = nil 
                else 
                    _St.pinnedPlayers[p.Name] = true 
                end
                _renderPlrList()
                _saveConfig()
            end)
            
            _RowCache[p.Name] = row
            row.Parent = _scroll
        end

        row.LayoutOrder = ord
        row.BackgroundColor3 = isPin and _Cfg.Theme.PlayerRowPinned or _Cfg.Theme.PlayerRow
        
        local uBtn = row:FindFirstChild("UserBtn")
        local tBtn = row:FindFirstChild("TeamBtn")
        local pBtn = row:FindFirstChild("PinBtn")
        
        if uBtn then 
            uBtn.TextColor3 = isTeam and _Cfg.Theme.EspTeam or (isPin and _Cfg.Theme.EspPinned or _Cfg.Theme.TextPrimary)
            uBtn.Text = (isTeam and "[ALIADO] " or (isPin and "[TARGET] " or "")) .. p.DisplayName 
        end
        if tBtn then 
            tBtn.BackgroundColor3 = isTeam and _Cfg.Theme.TeamActive or _Cfg.Theme.PinInactive
            tBtn.Text = isTeam and "No Team" or "Team"
            tBtn.TextColor3 = isTeam and Color3.fromRGB(10,10,20) or _Cfg.Theme.TextPrimary
        end
        if pBtn then 
            pBtn.BackgroundColor3 = isPin and _Cfg.Theme.PinActive or _Cfg.Theme.PinInactive
            pBtn.Text = isPin and "Unpin" or "Pin"
            pBtn.TextColor3 = isPin and Color3.fromRGB(10,10,20) or _Cfg.Theme.TextPrimary
        end
    end
end

local function _getRarityColor(r)
    local cols = {Common = Color3.fromRGB(0, 255, 100), Rare = Color3.fromRGB(0, 150, 255), Epic = Color3.fromRGB(180, 50, 255), Legendary = Color3.fromRGB(255, 200, 0)}
    return cols[r] or Color3.fromRGB(255, 255, 255)
end

local function _matchTool(tool)
    if not tool then return "Unknown" end
    local name = tool.Name
    if _ToolCache[name] then return _ToolCache[name] end
    local handle = tool:FindFirstChild("Handle")
    if not handle then _ToolCache[name] = name; return name end
    local names = {}
    for _, ch in ipairs(handle:GetChildren()) do names[ch.Name] = true end
    for _, src in ipairs({_RepS:FindFirstChild("Items"), _StkP}) do
        if src then
            for _, item in ipairs(src:GetDescendants()) do
                if item:IsA("Tool") and item:FindFirstChild("Handle") then
                    local match = true
                    for cName in pairs(names) do if not item.Handle:FindFirstChild(cName) then match = false; break end end
                    if match then _ToolCache[name] = item.Name; return item.Name end
                end
            end
        end
    end
    _ToolCache[name] = name; return name
end

local function _getPlayerTools(plr)
    local now = tick()
    if _LastScan[plr.Name] and (now - _LastScan[plr.Name].time < 1.5) then
        return _LastScan[plr.Name].tools
    end

    local tools = {}
    if not plr then return tools end
    local hasLeg = false
    local bp = plr:FindFirstChildOfClass("Backpack")
    local char = plr.Character
    
    local function scan(cont)
        if not cont then return end
        for _, tool in ipairs(cont:GetChildren()) do
            if tool:IsA("Tool") then
                local rName = _matchTool(tool)
                local rarity = tool:GetAttribute("RarityName") or "Common"
                if rarity == "Legendary" then hasLeg = true end
                table.insert(tools, {name = rName, rarity = rarity, equipped = (cont == char)})
            end
        end
    end
    scan(bp); scan(char)
    
    if hasLeg then
        if not _St.pinnedPlayers[plr.Name] then 
            _St.pinnedPlayers[plr.Name] = true 
            _St.autoPinned[plr.Name] = true 
            task.spawn(_renderPlrList) 
        end
    else
        if _St.autoPinned[plr.Name] then 
            _St.pinnedPlayers[plr.Name] = nil 
            _St.autoPinned[plr.Name] = nil 
            task.spawn(_renderPlrList) 
        end
    end

    _LastScan[plr.Name] = {time = now, tools = tools}
    return tools
end

local function _getOrCreateMasterEsp(plr)
    if _MasterObj[plr.Name] then return _MasterObj[plr.Name] end
    local char = plr.Character
    if not char then return nil end
    local head = char:FindFirstChild("Head")
    if not head then return nil end
    
    local bb = Instance.new("BillboardGui")
    bb.Name = "BsMasterEsp"
    bb.Size = UDim2.new(0, 180, 0, 180)
    bb.StudsOffset = Vector3.new(0, 3.5, 0)
    bb.AlwaysOnTop = true
    bb.Parent = head

    local mainF = Instance.new("Frame")
    mainF.Size = UDim2.new(1, 0, 1, 0)
    mainF.BackgroundTransparency = 1
    mainF.Parent = bb
    
    local ll = Instance.new("UIListLayout")
    ll.FillDirection = Enum.FillDirection.Vertical
    ll.SortOrder = Enum.SortOrder.LayoutOrder
    ll.Padding = UDim.new(0, 4)
    ll.HorizontalAlignment = Enum.HorizontalAlignment.Center
    ll.Parent = mainF

    local espLbl = Instance.new("TextLabel")
    espLbl.Name = "EspLabel"
    espLbl.Size = UDim2.new(1, 0, 0, 38)
    espLbl.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    espLbl.BackgroundTransparency = 0.65
    espLbl.Font = Enum.Font.GothamBold
    espLbl.TextStrokeTransparency = 0.4
    espLbl.LayoutOrder = 1
    
    local lc = Instance.new("UICorner")
    lc.CornerRadius = UDim.new(0, 5)
    lc.Parent = espLbl
    espLbl.Parent = mainF

    local invC = Instance.new("Frame")
    invC.Name = "InvContainer"
    invC.Size = UDim2.new(1, 0, 0, 120)
    invC.BackgroundTransparency = 1
    invC.LayoutOrder = 2
    invC.Parent = mainF
    
    local il = Instance.new("UIListLayout")
    il.FillDirection = Enum.FillDirection.Vertical
    il.SortOrder = Enum.SortOrder.LayoutOrder
    il.Padding = UDim.new(0, 2)
    il.HorizontalAlignment = Enum.HorizontalAlignment.Center
    il.Parent = invC

    _MasterObj[plr.Name] = {Gui = bb, EspLabel = espLbl, InvContainer = invC}
    return _MasterObj[plr.Name]
end

local function _removeMasterEsp(plr)
    local m = _MasterObj[plr.Name]
    if m then
        if m.Gui then m.Gui:Destroy() end
        _MasterObj[plr.Name] = nil
        _LastInvState[plr] = nil
    end
    _hideSkel(plr)
end

local function _updateVisuals()
    if not _St.alive then return end
    local myPos = _getMyPos()

    for _, plr in ipairs(_Plrs:GetPlayers()) do
        if plr ~= _LP then
            local char = plr.Character
            if char then
                local head, root, hum = char:FindFirstChild("Head"), char:FindFirstChild("HumanoidRootPart"), char:FindFirstChildOfClass("Humanoid")
                if head and root and hum then
                    local isPin, isTeam = _St.pinnedPlayers[plr.Name], _St.teamPlayers[plr.Name]
                    local dist = math.floor((root.Position - myPos).Magnitude)
                    local maxDist = (isPin or isTeam) and _Cfg.MaxSpecialDistance or _Cfg.MaxNormalDistance

                    if hum.Health > 0 and dist <= maxDist then
                        _updateSkelEsp(plr, char)
                        local m = _getOrCreateMasterEsp(plr)
                        if m and m.Gui and m.Gui.Parent == head then
                            m.Gui.Enabled = true
                            local tScale = math.clamp(12 - (dist / 400), 7.5, 11.5)

                            if _St.espEnabled then
                                m.EspLabel.Visible = true
                                m.EspLabel.TextColor3 = isTeam and _Cfg.Theme.EspTeam or (isPin and _Cfg.Theme.EspPinned or _Cfg.Theme.EspNormal)
                                m.EspLabel.TextSize = tScale
                                local prefix = isTeam and "[ALIADO]\n" or (isPin and "[TARGET]\n" or "")
                                m.EspLabel.Text = string.format("%s%s\n%d studs | %d HP", prefix, plr.DisplayName, dist, math.floor(hum.Health))
                            else
                                m.EspLabel.Visible = false
                            end

                            if _St.invViewEnabled then
                                m.InvContainer.Visible = true
                                local tools = _getPlayerTools(plr)
                                local invStr = ""
                                for _, td in ipairs(tools) do invStr = invStr .. td.name .. td.rarity .. tostring(td.equipped) end
                                
                                if _LastInvState[plr] ~= invStr then
                                    _LastInvState[plr] = invStr
                                    for _, ch in ipairs(m.InvContainer:GetChildren()) do if ch:IsA("TextLabel") then ch:Destroy() end end
                                    for i, td in ipairs(tools) do
                                        local line = Instance.new("TextLabel")
                                        line.Size = UDim2.new(0, 145, 0, 14)
                                        line.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
                                        line.BackgroundTransparency = 0.7
                                        line.Font = Enum.Font.GothamBold
                                        line.TextStrokeTransparency = 0.5
                                        line.Text = " " .. td.name .. " "
                                        line.TextColor3 = _getRarityColor(td.rarity)
                                        line.LayoutOrder = i
                                        
                                        local lCorner = Instance.new("UICorner")
                                        lCorner.CornerRadius = UDim.new(0, 4)
                                        lCorner.Parent = line
                                        
                                        if td.equipped then line.Text = "👉 " .. td.name; line.BackgroundColor3 = Color3.fromRGB(25, 15, 35) end
                                        line.Parent = m.InvContainer
                                    end
                                end
                                for _, ch in ipairs(m.InvContainer:GetChildren()) do if ch:IsA("TextLabel") then ch.TextSize = tScale end end
                            else
                                m.InvContainer.Visible = false
                            end
                        else
                            _removeMasterEsp(plr)
                        end

                        if isTeam or isPin then
                            local hl = char:FindFirstChild("BsAura")
                            if not hl then 
                                hl = Instance.new("Highlight")
                                hl.Name = "BsAura"
                                hl.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                                hl.OutlineColor = _Cfg.Theme.AuraOutline
                                hl.Parent = char 
                            end
                            hl.FillColor = isTeam and _Cfg.Theme.AuraTeamFill or _Cfg.Theme.AuraFill
                            hl.FillTransparency = 0.65 + math.sin(tick() * 4) * 0.08
                        else
                            local hl = char:FindFirstChild("BsAura")
                            if hl then hl:Destroy() end
                        end
                    else
                        _removeMasterEsp(plr)
                        local hl = char:FindFirstChild("BsAura")
                        if hl then hl:Destroy() end
                    end
                else
                    _removeMasterEsp(plr)
                end
            else
                _removeMasterEsp(plr)
            end
        end
    end
end

local _FOVCircle = nil
if _hasDrawing then
    pcall(function()
        _FOVCircle = Drawing.new("Circle")
        _FOVCircle.Thickness = 1.5; _FOVCircle.NumSides = 60; _FOVCircle.Filled = false; _FOVCircle.Transparency = 1
    end)
end

local function _getPartName(tMode, char)
    if not char then return nil end
    local head, torso = char:FindFirstChild("Head"), char:FindFirstChild("UpperTorso") or char:FindFirstChild("Torso")
    if tMode == "Cabeza" then return head and "Head" or nil
    elseif tMode == "Pecho" then return torso and torso.Name or nil
    elseif tMode == "Mixto" then 
        local hum = char:FindFirstChildOfClass("Humanoid")
        return (hum and hum.Health > 30) and (head and "Head" or (torso and torso.Name or nil)) or (torso and torso.Name or (head and "Head" or nil))
    end
    return "Head"
end

local function _getClosest()
    if _Cfg.AimMode == "FOV" then
        local closest, minDist = nil, _Cfg.AimFOV
        local center = _Cam.ViewportSize / 2
        local current = _St.lockedTarget
        local currentDist = math.huge

        for _, plr in ipairs(_Plrs:GetPlayers()) do
            if plr ~= _LP and not _St.teamPlayers[plr.Name] then
                local char = plr.Character
                if char then
                    local hum = char:FindFirstChildOfClass("Humanoid")
                    if hum and hum.Health > 0 then
                        local pName = _getPartName(_Cfg.AimTarget, char)
                        local part = pName and char:FindFirstChild(pName)
                        if part and part:IsA("BasePart") then
                            local pos, onScr = _Cam:WorldToViewportPoint(part.Position)
                            if onScr then
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
            if _St.teamPlayers[current.Name] or not char or not hum or hum.Health <= 0 or currentDist > _Cfg.AimFOV then
                _St.lockedTarget = nil
                current = nil
            end
        end

        if closest then
            if not current then
                _St.lockedTarget = closest
            elseif closest ~= current and minDist < (currentDist * 0.72) then
                _St.lockedTarget = closest
            end
        else
            _St.lockedTarget = nil
        end
        return _St.lockedTarget
    end

    local locked = _St.lockedTarget
    if locked then
        local char = locked.Character
        local hum = char and char:FindFirstChildOfClass("Humanoid")
        if _St.teamPlayers[locked.Name] or not char or not hum or hum.Health <= 0 then
            _St.lockedTarget = nil
            locked = nil
        end
    end
    if locked then return locked end

    local closest, minDist = nil, _Cfg.AimFOV
    local center = _Cam.ViewportSize / 2

    for _, plr in ipairs(_Plrs:GetPlayers()) do
        if plr ~= _LP and not _St.teamPlayers[plr.Name] then
            local char = plr.Character
            if char then
                local hum = char:FindFirstChildOfClass("Humanoid")
                if hum and hum.Health > 0 then
                    local pName = _getPartName(_Cfg.AimTarget, char)
                    local part = pName and char:FindFirstChild(pName)
                    if part and part:IsA("BasePart") then
                        local pos, onScr = _Cam:WorldToViewportPoint(part.Position)
                        if onScr then
                            local dist = (Vector2.new(pos.X, pos.Y) - center).Magnitude
                            if dist < minDist then minDist = dist; closest = plr end
                        end
                    end
                end
            end
        end
    end
    _St.lockedTarget = closest
    return closest
end

task.spawn(function()
    while _St.alive do
        _updateVisuals()
        task.wait(0.033) 
    end
end)

_safeConn(_RunS.RenderStepped, function()
    if _FOVCircle then
        pcall(function()
            _FOVCircle.Visible = _Cfg.ShowFOV
            _FOVCircle.Radius = _Cfg.AimFOV
            _FOVCircle.Position = Vector2.new(_Cam.ViewportSize.X / 2, _Cam.ViewportSize.Y / 2)
            _FOVCircle.Color = _St.lockedTarget and _Cfg.Theme.FOVLocked or _Cfg.Theme.FOVNormal
        end)
    end
end)

_RunS:BindToRenderStep("BlockSpinAimbot", Enum.RenderPriority.Camera.Value + 1, function(dt)
    if not _St.alive then return end
    local shouldAim = false
    if _Cfg.AimMode == "Toggle" then shouldAim = _St.aimEnabled
    elseif _Cfg.AimMode == "FOV" then shouldAim = _St.holdingAimTrigger or _St.aimEnabled
    elseif _Cfg.AimMode == "Hold" then shouldAim = _St.holdingAimTrigger end
    if not shouldAim then return end

    local target = _getClosest()
    if target and target.Character then
        local pName = _getPartName(_Cfg.AimTarget, target.Character)
        local part = pName and target.Character:FindFirstChild(pName)
        if part and part:IsA("BasePart") then
            local camPos = _Cam.CFrame.Position
            local targetPos = part.Position
            if (targetPos - camPos).Magnitude < 0.5 then return end
            local desired = CFrame.new(camPos, targetPos)
            local ok, x, y = pcall(function()
                local a, b = desired:ToEulerAnglesYXZ()
                return a, b
            end)
            if ok then
                x = math.clamp(x, math.rad(-80), math.rad(80))
                desired = CFrame.new(camPos) * CFrame.fromEulerAnglesYXZ(x, y, 0)
            end
            local hardLock = (_Cfg.AimMode == "Toggle") or (_Cfg.AimMode == "Hold") or (_Cfg.AimSmooth == "Bajo")
            if hardLock then
                _Cam.CFrame = desired
            else
                local alpha = 1
                if _Cfg.AimSmooth == "Medio" then alpha = 1 - math.exp(-22 * dt)
                else alpha = 1 - math.exp(-10 * dt) end
                _Cam.CFrame = _Cam.CFrame:Lerp(desired, math.clamp(alpha, 0, 1))
            end
        end
    end
end)

_safeConn(_Uis.InputBegan, function(input, gpe)
    if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == _Cfg.Binds.GamepadAim then _St.holdingAimTrigger = true end
    if _St.isBinding then
        if input.UserInputType == Enum.UserInputType.Keyboard then
            local act = _St.isBinding
            _Cfg.Binds[act] = input.KeyCode; _St.isBinding = nil; _syncUi()
            _saveConfig() 
        end
        return
    end
    if gpe then return end
    if input.KeyCode == _Cfg.Binds.ToggleMenu then _MainF.Visible = not _MainF.Visible
    elseif input.KeyCode == _Cfg.Binds.Aimbot or input.KeyCode == _Cfg.Binds.GamepadToggle then
        _St.aimEnabled = not _St.aimEnabled
        if not _St.aimEnabled then _St.lockedTarget = nil end
        _updateMainBtns()
        _saveConfig()
    elseif input.KeyCode == _Cfg.Binds.InvView then 
        _St.invViewEnabled = not _St.invViewEnabled
        _updateMainBtns()
        _saveConfig() 
    end
end)

_safeConn(_Uis.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == _Cfg.Binds.GamepadAim then _St.holdingAimTrigger = false; _St.lockedTarget = nil end
end)

local _dragging, _dStart, _sPos
_Hdr.InputBegan:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then
        _dragging = true; _dStart = i.Position; _sPos = _MainF.Position
    end
end)

_safeConn(_Uis.InputChanged, function(i)
    if _dragging and (i.UserInputType == Enum.UserInputType.MouseMovement or i.UserInputType == Enum.UserInputType.Touch) then
        local delta = i.Position - _dStart
        _MainF.Position = UDim2.new(_sPos.X.Scale, _sPos.X.Offset + delta.X, _sPos.Y.Scale, _sPos.Y.Offset + delta.Y)
    end
end)

_safeConn(_Uis.InputEnded, function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then _dragging = false end
end)

local function _cleanup()
    _St.alive = false
    pcall(function() _RunS:UnbindFromRenderStep("BlockSpinAimbot") end)
    for _, conn in ipairs(_St.connections) do pcall(function() conn:Disconnect() end) end
    if _FOVCircle then pcall(function() _FOVCircle:Remove() end) end
    
    for _, p in ipairs(_Plrs:GetPlayers()) do
        _removeMasterEsp(p)
        if p.Character then 
            local h1 = p.Character:FindFirstChild("BsAura")
            if h1 then h1:Destroy() end 
        end
    end
    
    for _, lines in pairs(_SkelCache) do 
        for _, l in pairs(lines) do if l then pcall(function() l:Remove() end) end end 
    end
end

_ClsBtn.MouseButton1Click:Connect(function() _cleanup(); _gui:Destroy() end)
_safeConn(_Plrs.PlayerAdded, function(p) _autoTeam(p); _renderPlrList() end)
_safeConn(_Plrs.PlayerRemoving, function(plr)
    _removeMasterEsp(plr)
    local sk = _SkelCache[plr.Name]
    if sk then for _, l in pairs(sk) do if l then pcall(function() l:Remove() end) end end; _SkelCache[plr.Name] = nil end
    _St.teamPlayers[plr.Name] = nil; _St.pinnedPlayers[plr.Name] = nil; _St.autoPinned[plr.Name] = nil
    local row = _RowCache[plr.Name]; if row then row:Destroy(); _RowCache[plr.Name] = nil end
    _renderPlrList()
end)

for _, p in ipairs(_Plrs:GetPlayers()) do if p ~= _LP then _autoTeam(p) end end
_renderPlrList()
task.spawn(_loadConfig)
print("[Hermanos CP] v5.4 cargado completamente libre y modificado de forma segura.")
