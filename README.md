local a=game:GetService("Players")local b=game:GetService("CoreGui")local c=game:GetService("TweenService")local d=game:GetService("UserInputService")local e=a.LocalPlayer local f=workspace.CurrentCamera
if b:FindFirstChild("HermanosCPLoader_Premium")then return end
if e:FindFirstChild("PlayerGui")and e.PlayerGui:FindFirstChild("HermanosCPLoader_Premium")then return end
local g=(e.LocaleId and e.LocaleId:lower())or"es"local h=not g:match("^es")
local function i()return(f and f.ViewportSize.X)or 800 end
local function j()return i()<700 end
local function k(l)if l or j()then return math.clamp(math.floor(i()*0.88),280,360)end return 390 end
local function m(l)if l or j()then return 270 end return 300 end
local n={es={choose="Elige tu dispositivo:",pc="PC / COMPUTADORA",pcD="Menu completo en pantalla.",mob="CELULAR / MOVIL",mobD="Bolita flotante para abrir el menu.",sub="Elija la optimizacion para su sistema:",norm="VERSION FULL / NORMAL",normD="Optimizado para alto rendimiento con carga completa.",light="VERSION ULTRA LIGHT",lightD="Menos consumo y mas FPS.",requesting="[Hermanos CP] Cargando ",kickLoad="Hermanos CP // Error al cargar el script",protected="Protected | Offline Combined"},en={choose="Choose your device:",pc="PC / COMPUTER",pcD="Full on-screen menu.",mob="PHONE / MOBILE",mobD="Floating ball to open the menu.",sub="Choose the optimization for your system:",norm="FULL / NORMAL VERSION",normD="Optimized for high performance with full load.",light="ULTRA LIGHT VERSION",lightD="Lower usage and more FPS.",requesting="[Hermanos CP] Loading ",kickLoad="Hermanos CP // Error loading script",protected="Protected | Offline Combined"}}
local function o()return h and n.en or n.es end
local function p()local q,r=pcall(function()return(type(cloneref)=="function"and cloneref(b))or b end)if q and r then return r end return e:WaitForChild("PlayerGui",5)end

local NORMAL_SCRIPT = [==========[
local _Gms = game
local _Wsp = workspace
local _Plrs = _Gms:GetService("Players")
local _RepS = _Gms:GetService("ReplicatedStorage")
local _StkP = _Gms:GetService("StarterPack")
local _RunS = _Gms:GetService("RunService")
local _Uis = _Gms:GetService("UserInputService")
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
local _Cgs = _Gms:GetService("CoreGui")
local _Tws = _Gms:GetService("TweenService")
local _Hts = _Gms:GetService("HttpService")
local function _gE(name)
    local g = (type(getgenv) == "function" and getgenv()) or {}
    local f = (type(getfenv) == "function" and getfenv()) or {}
    local ok, val = pcall(function() return g[name] or f[name] or _G[name] end)
    return ok and val or nil
end
local _cloneref = _gE("cloneref")
local _Drawing = _gE("Drawing")
local _writefile = _gE("writefile")
local _readfile = _gE("readfile")
local _isfile = _gE("isfile")
while not _Plrs.LocalPlayer do
    task.wait(0.1)
end
local _LP = _Plrs.LocalPlayer
local _Cam = _Wsp.CurrentCamera or _Wsp:WaitForChild("Camera")
local _CfgFile = "HermanosCP_v54_Config.json"
local _sCfg
local _lCfg
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
local function _sC(signal, cb)
    local conn = signal:Connect(cb)
    table.insert(_St.connections, conn)
    return conn
end
local _cnt = 0
local function _gN()
    _cnt = _cnt + 1
    return string.char(math.random(65, 90)) .. string.char(math.random(97, 122)) .. tostring(math.random(100, 999)) .. tostring(_cnt)
end
local _hasDrawing = (type(_Drawing) == "table" and type(_Drawing.new) == "function")
local function _gSP()
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
_sC(_Wsp:GetPropertyChangedSignal("CurrentCamera"), function()
    _Cam = _Wsp.CurrentCamera or _Cam
end)
local function _fC()
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
_sC(_Cam:GetPropertyChangedSignal("CameraSubject"), function() task.spawn(_fC) end)
_sC(_Cam:GetPropertyChangedSignal("CameraType"), function() task.spawn(_fC) end)
local _humConn
local function _cH(hum)
    if _humConn then _humConn:Disconnect() end
    _humConn = hum:GetPropertyChangedSignal("CameraOffset"):Connect(function()
        if _Cfg.VehicleCameraFix and hum.CameraOffset ~= Vector3.zero then
            hum.CameraOffset = Vector3.zero
        end
    end)
    table.insert(_St.connections, _humConn)
end
_sC(_LP.CharacterAdded, function(char)
    local hum = char:WaitForChild("Humanoid", 5)
    if hum then _cH(hum) end
    task.spawn(_fC)
end)
if _LP.Character then
    local hum = _LP.Character:FindFirstChildOfClass("Humanoid")
    if hum then _cH(hum) end
end
local function _aT(plr)
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
_gui.Name = _gN()
_gui.IgnoreGuiInset = true
_gui.ResetOnSpawn = false
_gui.Parent = _gSP()

-- NATIVO CÍRCULO FOV (COMPATIBLE CON LUAMOR / CELULARES)
local _FovFrame = Instance.new("Frame")
_FovFrame.Name = "HCP_FOV_CircleUI"
_FovFrame.AnchorPoint = Vector2.new(0.5, 0.5)
_FovFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
_FovFrame.BackgroundTransparency = 1
_FovFrame.Visible = false
_FovFrame.Parent = _gui

local _FovCorner = Instance.new("UICorner")
_FovCorner.CornerRadius = UDim.new(1, 0)
_FovCorner.Parent = _FovFrame

local _FovStroke = Instance.new("UIStroke")
_FovStroke.Thickness = 1.5
_FovStroke.Color = _Cfg.Theme.FOVNormal
_FovStroke.Transparency = 0
_FovStroke.Parent = _FovFrame

local function _sN(msg, col)
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
local function _uMB()
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
_uMB()
_AimBtn.MouseButton1Click:Connect(function()
    _St.aimEnabled = not _St.aimEnabled
    if not _St.aimEnabled then _St.lockedTarget = nil end
    _uMB()
    _sCfg()
end)
_EspBtn.MouseButton1Click:Connect(function()
    _St.espEnabled = not _St.espEnabled
    _uMB()
    _sCfg()
end)
_InvBtn.MouseButton1Click:Connect(function()
    _St.invViewEnabled = not _St.invViewEnabled
    _uMB()
    _sCfg()
end)
local _cfgLayout = Instance.new("UIListLayout")
_cfgLayout.SortOrder = Enum.SortOrder.LayoutOrder
_cfgLayout.Padding = UDim.new(0, 14)
_cfgLayout.Parent = _ContCfg
local function _cCS(tText, bData, cb)
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
            _sCfg()
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
local _aimModeBtns = _cCS(_L.aimMode, {
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
local function _aFA(alpha)
    alpha = math.clamp(alpha, 0, 1)
    local val = math.floor(_FOV_MIN + alpha * (_FOV_MAX - _FOV_MIN) + 0.5)
    _Cfg.AimFOV = val
    _fovFill.Size = UDim2.new(alpha, 0, 1, 0)
    _fovKnob.Position = UDim2.new(alpha, 0, 0.5, 0)
    _fovValLbl.Text = tostring(val)
end
local function _uFS()
    local alpha = math.clamp((_Cfg.AimFOV - _FOV_MIN) / (_FOV_MAX - _FOV_MIN), 0, 1)
    _fovFill.Size = UDim2.new(alpha, 0, 1, 0)
    _fovKnob.Position = UDim2.new(alpha, 0, 0.5, 0)
    _fovValLbl.Text = tostring(_Cfg.AimFOV)
end
local _fovDragging = false
local function _fFI(input)
    local absPos = _fovTrack.AbsolutePosition.X
    local absSize = _fovTrack.AbsoluteSize.X
    if absSize <= 0 then return end
    _aFA((input.Position.X - absPos) / absSize)
end
_fovTrack.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        _fovDragging = true
        _fFI(input)
    end
end)
_fovKnob.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        _fovDragging = true
    end
end)
_sC(_Uis.InputChanged, function(input)
    if not _fovDragging then return end
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        _fFI(input)
    end
end)
_sC(_Uis.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        if _fovDragging then
            _fovDragging = false
            _sCfg()
        end
    end
end)
local _fovInput = nil
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
_sC(_Uis.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        if _sliderDrag then
            _sliderDrag = false
            _sCfg()
        end
    end
end)
_sC(_Uis.InputChanged, function(input)
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
local _skelBtns = _cCS(_L.skel, {
    {Label = "❌ " .. _L.off, Value = "Off"}, {Label = "🟡 " .. _L.gold, Value = "Oro"}, {Label = "⚪ " .. _L.white, Value = "Blanco"}, {Label = "🔵 " .. _L.cyan, Value = "Equipo"}
}, function(val) _Cfg.SkeletonStyle = val end)
local _targetBtns = _cCS(_L.target, {
    {Label = "👤 " .. _L.head, Value = "Cabeza"}, {Label = _L.chest, Value = "Pecho"}, {Label = "🔀 " .. _L.mixed, Value = "Mixto"}
}, function(val) _Cfg.AimTarget = val; _St.lockedTarget = nil end)
local _smoothBtns = _cCS(_L.smooth, {
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
local function _sUi()
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
    if _uFS then
        _uFS()
    end
end
_sCfg = function()
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
_lCfg = function()
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
    _sUi()
    _uMB()
    return true
end
_sUi()
_saveBtn.MouseButton1Click:Connect(function()
    if _sCfg() then
        _saveBtn.Text = "✅ ¡GUARDADO!"; _saveBtn.BackgroundColor3 = _Cfg.Theme.TeamActive; _saveBtn.TextColor3 = Color3.fromRGB(10, 10, 20)
        task.delay(1.5, function() _saveBtn.Text = "💾 " .. _L.saveCfg; _saveBtn.BackgroundColor3 = _Cfg.Theme.TabInactive; _saveBtn.TextColor3 = _Cfg.Theme.TextPrimary end)
    else
        _saveBtn.Text = "❌ ERROR"; _saveBtn.BackgroundColor3 = _Cfg.Theme.BtnOff
        task.delay(1.5, function() _saveBtn.Text = "💾 " .. _L.saveCfg; _saveBtn.BackgroundColor3 = _Cfg.Theme.TabInactive end)
    end
end)
_loadBtn.MouseButton1Click:Connect(function()
    if _lCfg() then
        _loadBtn.Text = "✅ ¡CARGADO!"; _loadBtn.BackgroundColor3 = _Cfg.Theme.TeamActive; _loadBtn.TextColor3 = Color3.fromRGB(10, 10, 20)
        task.delay(1.5, function() _loadBtn.Text = "📂 " .. _L.loadCfg; _loadBtn.BackgroundColor3 = _Cfg.Theme.TabInactive; _loadBtn.TextColor3 = _Cfg.Theme.TextPrimary end)
    else
        _loadBtn.Text = "❌ SIN ARCHIVO"; _loadBtn.BackgroundColor3 = _Cfg.Theme.BtnOff
        task.delay(1.5, function() _loadBtn.Text = "📂 " .. _L.loadCfg; _loadBtn.BackgroundColor3 = _Cfg.Theme.TabInactive end)
    end
end)
local function _gSC(plr)
    if _Cfg.SkeletonStyle == "Oro" then return _Cfg.Theme.Gold end
    if _Cfg.SkeletonStyle == "Blanco" then return Color3.fromRGB(255, 255, 255) end
    if _Cfg.SkeletonStyle == "Equipo" then return _St.teamPlayers[plr.Name] and _Cfg.Theme.EspTeam or _Cfg.Theme.Stroke end
    return Color3.fromRGB(255, 255, 255)
end
local function _cL()
    if not _hasDrawing then return nil end
    local ok, l = pcall(_Drawing.new, "Line")
    if ok and l then
        l.Thickness = 1.5; l.Transparency = 1; l.Visible = false
        return l
    end
    return nil
end
local function _gSk(plr)
    local name = plr.Name
    if not _SkelCache[name] then
        _SkelCache[name] = {
            Head_Spine = _cL(), Spine_LeftArm = _cL(), Spine_RightArm = _cL(),
            LeftArm_Hand = _cL(), RightArm_Hand = _cL(), Spine_LeftLeg = _cL(),
            Spine_RightLeg = _cL(), LeftLeg_Foot = _cL(), RightLeg_Foot = _cL()
        }
    end
    return _SkelCache[name]
end
local function _hSk(plr)
    local sk = _SkelCache[plr.Name]
    if sk then
        for _, l in pairs(sk) do if l then pcall(function() l.Visible = false end) end end
    end
end
local function _uSE(plr, char)
    if not _St.espEnabled or _Cfg.SkeletonStyle == "Off" or not _hasDrawing then _hSk(plr); return end
    local sk = _gSk(plr)
    local col = _gSC(plr)
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
        _hSk(plr)
    end
end
local function _gMP()
    local char = _LP.Character
    if char then
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum and hum.SeatPart then return hum.SeatPart.Position end
        local root = char:FindFirstChild("HumanoidRootPart")
        if root then return root.Position end
    end
    return _Cam.CFrame.Position
end
local function _rPL()
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
                _rPL()
                _sCfg()
            end)
            pBtn.MouseButton1Click:Connect(function()
                if _St.pinnedPlayers[p.Name] then
                    _St.pinnedPlayers[p.Name] = nil
                    _St.autoPinned[p.Name] = nil
                else
                    _St.pinnedPlayers[p.Name] = true
                end
                _rPL()
                _sCfg()
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
local function _gRC(r)
    local cols = {Common = Color3.fromRGB(0, 255, 100), Rare = Color3.fromRGB(0, 150, 255), Epic = Color3.fromRGB(180, 50, 255), Legendary = Color3.fromRGB(255, 200, 0)}
    return cols[r] or Color3.fromRGB(255, 255, 255)
end
local function _mT(tool)
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
local function _gPT(plr)
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
                local rName = _mT(tool)
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
            task.spawn(_rPL)
        end
    else
        if _St.autoPinned[plr.Name] then
            _St.pinnedPlayers[plr.Name] = nil
            _St.autoPinned[plr.Name] = nil
            task.spawn(_rPL)
        end
    end
    _LastScan[plr.Name] = {time = now, tools = tools}
    return tools
end
local function _gOME(plr)
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
local function _rME(plr)
    local m = _MasterObj[plr.Name]
    if m then
        if m.Gui then m.Gui:Destroy() end
        _MasterObj[plr.Name] = nil
        _LastInvState[plr] = nil
    end
    _hSk(plr)
end
local function _uV()
    if not _St.alive then return end
    local myPos = _gMP()
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
                        _uSE(plr, char)
                        local m = _gOME(plr)
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
                                local tools = _gPT(plr)
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
                                        line.TextColor3 = _gRC(td.rarity)
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
                            _rME(plr)
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
                        _rME(plr)
                        local hl = char:FindFirstChild("BsAura")
                        if hl then hl:Destroy() end
                    end
                else
                    _rME(plr)
                end
            else
                _rME(plr)
            end
        end
    end
end

local function _gPN(tMode, char)
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
local function _gC()
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
                        local pName = _gPN(_Cfg.AimTarget, char)
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
                    local pName = _gPN(_Cfg.AimTarget, char)
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
        _uV()
        task.wait(0.033)
    end
end)

_sC(_RunS.RenderStepped, function()
    local isVis = (_Cfg.ShowFOV and _Cfg.AimMode == "FOV")
    _FovFrame.Visible = isVis
    if isVis then
        local d = _Cfg.AimFOV * 2
        _FovFrame.Size = UDim2.new(0, d, 0, d)
        _FovStroke.Color = _St.lockedTarget and _Cfg.Theme.FOVLocked or _Cfg.Theme.FOVNormal
    end
end)

_RunS:BindToRenderStep("BlockSpinAimbot", Enum.RenderPriority.Camera.Value + 1, function(dt)
    if not _St.alive then return end
    local shouldAim = false
    if _Cfg.AimMode == "Toggle" then shouldAim = _St.aimEnabled
    elseif _Cfg.AimMode == "FOV" then shouldAim = _St.holdingAimTrigger or _St.aimEnabled
    elseif _Cfg.AimMode == "Hold" then shouldAim = _St.holdingAimTrigger end
    if not shouldAim then return end
    local target = _gC()
    if target and target.Character then
        local pName = _gPN(_Cfg.AimTarget, target.Character)
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
_sC(_Uis.InputBegan, function(input, gpe)
    if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == _Cfg.Binds.GamepadAim then _St.holdingAimTrigger = true end
    if _St.isBinding then
        if input.UserInputType == Enum.UserInputType.Keyboard then
            local act = _St.isBinding
            _Cfg.Binds[act] = input.KeyCode; _St.isBinding = nil; _sUi()
            _sCfg()
        end
        return
    end
    if gpe then return end
    if input.KeyCode == _Cfg.Binds.ToggleMenu then _MainF.Visible = not _MainF.Visible
    elseif input.KeyCode == _Cfg.Binds.Aimbot or input.KeyCode == _Cfg.Binds.GamepadToggle then
        _St.aimEnabled = not _St.aimEnabled
        if not _St.aimEnabled then _St.lockedTarget = nil end
        _uMB()
        _sCfg()
    elseif input.KeyCode == _Cfg.Binds.InvView then
        _St.invViewEnabled = not _St.invViewEnabled
        _uMB()
        _sCfg()
    end
end)
_sC(_Uis.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == _Cfg.Binds.GamepadAim then _St.holdingAimTrigger = false; _St.lockedTarget = nil end
end)
local _dragging, _dStart, _sPos
_Hdr.InputBegan:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then
        _dragging = true; _dStart = i.Position; _sPos = _MainF.Position
    end
end)
_sC(_Uis.InputChanged, function(i)
    if _dragging and (i.UserInputType == Enum.UserInputType.MouseMovement or i.UserInputType == Enum.UserInputType.Touch) then
        local delta = i.Position - _dStart
        _MainF.Position = UDim2.new(_sPos.X.Scale, _sPos.X.Offset + delta.X, _sPos.Y.Scale, _sPos.Y.Offset + delta.Y)
    end
end)
_sC(_Uis.InputEnded, function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then _dragging = false end
end)
local function _cln()
    _St.alive = false
    pcall(function() _RunS:UnbindFromRenderStep("BlockSpinAimbot") end)
    for _, conn in ipairs(_St.connections) do pcall(function() conn:Disconnect() end) end
    if _FovFrame then pcall(function() _FovFrame:Destroy() end) end
    for _, p in ipairs(_Plrs:GetPlayers()) do
        _rME(p)
        if p.Character then
            local h1 = p.Character:FindFirstChild("BsAura")
            if h1 then h1:Destroy() end
        end
    end
    for _, lines in pairs(_SkelCache) do
        for _, l in pairs(lines) do if l then pcall(function() l:Remove() end) end end
    end
end
_ClsBtn.MouseButton1Click:Connect(function() _cln(); _gui:Destroy() end)
_sC(_Plrs.PlayerAdded, function(p) _aT(p); _rPL() end)
_sC(_Plrs.PlayerRemoving, function(plr)
    _rME(plr)
    local sk = _SkelCache[plr.Name]
    if sk then for _, l in pairs(sk) do if l then pcall(function() l:Remove() end) end end; _SkelCache[plr.Name] = nil end
    _St.teamPlayers[plr.Name] = nil; _St.pinnedPlayers[plr.Name] = nil; _St.autoPinned[plr.Name] = nil
    local row = _RowCache[plr.Name]; if row then row:Destroy(); _RowCache[plr.Name] = nil end
    _rPL()
end)
for _, p in ipairs(_Plrs:GetPlayers()) do if p ~= _LP then _aT(p) end end
_rPL()
task.spawn(_lCfg)
print("[Hermanos CP] v5.4 cargado completamente libre y modificado de forma segura.")
]==========]

local LIGHT_SCRIPT = [==========[
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
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local StarterPack = game:GetService("StarterPack")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
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
local CoreGuiService = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local HttpService = game:GetService("HttpService")
local function gEG(name)
    local genv = (type(getgenv) == "function" and getgenv()) or {}
    local fenv = (type(getfenv) == "function" and getfenv()) or {}
    local success, val = pcall(function()
        return genv[name] or fenv[name] or _G[name]
    end)
    return success and val or nil
end
local cloneref = gEG("cloneref")
local Drawing = gEG("Drawing")
local writefile = gEG("writefile")
local readfile = gEG("readfile")
local isfile = gEG("isfile")
while not Players.LocalPlayer do
    task.wait(0.1)
end
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera or workspace:WaitForChild("Camera")
local CONFIG_FILE = "HermanosCP_Clean_Config.json"
local sCfg
local lCfg
local targetController
local smoothController
local modeController
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
local function sC(signal, callback)
    local conn = signal:Connect(callback)
    table.insert(State.connections, conn)
    return conn
end
local nameCounter = 0
local function gN()
    nameCounter = nameCounter + 1
    return string.char(math.random(65, 90)) .. string.char(math.random(97, 122)) .. tostring(math.random(100, 999)) .. tostring(nameCounter)
end
local HasDrawing = (type(Drawing) == "table" and type(Drawing.new) == "function")
local function gSGP()
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
sC(workspace:GetPropertyChangedSignal("CurrentCamera"), function()
    Camera = workspace.CurrentCamera or Camera
end)
local function fCAO()
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
sC(Camera:GetPropertyChangedSignal("CameraSubject"), function() task.spawn(fCAO) end)
sC(Camera:GetPropertyChangedSignal("CameraType"), function() task.spawn(fCAO) end)
local humanoidConnection
local function cH(hum)
    if humanoidConnection then humanoidConnection:Disconnect() end
    humanoidConnection = hum:GetPropertyChangedSignal("CameraOffset"):Connect(function()
        if Config.VehicleCameraFix and hum.CameraOffset ~= Vector3.zero then
            hum.CameraOffset = Vector3.zero
        end
    end)
    table.insert(State.connections, humanoidConnection)
end
sC(LocalPlayer.CharacterAdded, function(char)
    local hum = char:WaitForChild("Humanoid", 5)
    if hum then cH(hum) end
    task.spawn(fCAO)
end)
if LocalPlayer.Character then
    local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if hum then cH(hum) end
end
local function cAAT(player)
    if player == LocalPlayer then return end
    task.spawn(function()
        local success, isFriend = pcall(function() return LocalPlayer:IsFriendsWith(player.UserId) end)
        if success and isFriend then
            State.teamPlayers[player.Name] = true
            if State.lockedTarget == player then State.lockedTarget = nil end
        end
    end)
end
local gui = Instance.new("ScreenGui")
gui.Name = gN()
gui.IgnoreGuiInset = true
gui.ResetOnSpawn = false
gui.Parent = gSGP()

-- NATIVO CÍRCULO FOV (LIGHT - COMPATIBLE CON LUAMOR / CELULARES)
local FovGuiFrame = Instance.new("Frame")
FovGuiFrame.Name = "HCP_FOV_CircleUI"
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
sC(UserInputService.InputChanged, function(input)
    if ballDrag and (input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseMovement) then
        local d = input.Position - ballStart
        openBall.Position = UDim2.new(ballPos.X.Scale, ballPos.X.Offset + d.X, ballPos.Y.Scale, ballPos.Y.Offset + d.Y)
    end
end)
sC(UserInputService.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
        ballDrag = false
    end
end)
openBall.MouseButton1Click:Connect(function()
    MainFrame.Visible = true
    openBall.Visible = false
end)
minBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
    openBall.Visible = true
end)
local TabBar = Instance.new("Frame")
TabBar.Size = UDim2.new(1, -20, 0, 34)
TabBar.Position = UDim2.new(0, 10, 0, 55)
TabBar.BackgroundTransparency = 1
TabBar.Parent = MainFrame
local tabLayout = Instance.new("UIListLayout")
tabLayout.FillDirection = Enum.FillDirection.Horizontal
tabLayout.Padding = UDim.new(0, 8)
tabLayout.Parent = TabBar
local function cTB(text, parent)
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
local TabPrincipalBtn, tabPStroke = cTB(_L.tabMain, TabBar)
local TabConfigBtn, tabCStroke = cTB("⚙️ " .. _L.tabCfg, TabBar)
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
local function sT(tabName)
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
sT("Principal")
local function aTH(btn, stroke, tabName)
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
aTH(TabPrincipalBtn, tabPStroke, "Principal")
aTH(TabConfigBtn, tabCStroke, "Config")
TabPrincipalBtn.MouseButton1Click:Connect(function() sT("Principal") end)
TabConfigBtn.MouseButton1Click:Connect(function() sT("Config") end)
local TogglePanel = Instance.new("Frame")
TogglePanel.Size = UDim2.new(1, 0, 0, 35)
TogglePanel.Position = UDim2.new(0, 0, 0, 0)
TogglePanel.BackgroundTransparency = 1
TogglePanel.Parent = ContentPrincipal
local grid = Instance.new("UIGridLayout")
grid.CellSize = UDim2.new(0.32, 0, 0, 32)
grid.CellPadding = UDim2.new(0, 6, 0, 6)
grid.Parent = TogglePanel
local function cTog(parent, text)
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
local AimToggleBtn = cTog(TogglePanel, _L.aimbot)
local EspToggleBtn = cTog(TogglePanel, "ESP VISUALS")
local InvToggleBtn = cTog(TogglePanel, "INV VIEW")
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
local function uMB()
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
uMB()
AimToggleBtn.MouseButton1Click:Connect(function()
    State.aimEnabled = not State.aimEnabled
    if not State.aimEnabled then State.lockedTarget = nil end
    uMB()
    sCfg()
end)
EspToggleBtn.MouseButton1Click:Connect(function()
    State.espEnabled = not State.espEnabled
    uMB()
    sCfg()
end)
InvToggleBtn.MouseButton1Click:Connect(function()
    State.invViewEnabled = not State.invViewEnabled
    uMB()
    sCfg()
end)
local function cCCS(titleText, buttonsData, callback)
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
        sCfg()
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
local function aFFA(alpha)
    alpha = math.clamp(alpha, 0, 1)
    local val = math.floor(FOV_MIN + alpha * (FOV_MAX - FOV_MIN) + 0.5)
    Config.AimFOV = val
    fovFill.Size = UDim2.new(alpha, 0, 1, 0)
    fovKnob.Position = UDim2.new(alpha, 0, 0.5, 0)
    fovValueLbl.Text = tostring(val)
end
local function uFSU()
    local alpha = math.clamp((Config.AimFOV - FOV_MIN) / (FOV_MAX - FOV_MIN), 0, 1)
    fovFill.Size = UDim2.new(alpha, 0, 1, 0)
    fovKnob.Position = UDim2.new(alpha, 0, 0.5, 0)
    fovValueLbl.Text = tostring(Config.AimFOV)
end
local fovDragging = false
local function fFI(input)
    local absPos = fovTrack.AbsolutePosition.X
    local absSize = fovTrack.AbsoluteSize.X
    if absSize <= 0 then return end
    local alpha = (input.Position.X - absPos) / absSize
    aFFA(alpha)
end
fovTrack.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        fovDragging = true
        fFI(input)
    end
end)
fovKnob.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        fovDragging = true
    end
end)
sC(UserInputService.InputChanged, function(input)
    if not fovDragging then return end
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        fFI(input)
    end
end)
sC(UserInputService.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        if fovDragging then
            fovDragging = false
            sCfg()
        end
    end
end)
local fovInput = nil
targetController = cCCS(_L.target, {
    {Label = "👤 " .. _L.head, Value = "Cabeza"}, {Label = "👕 " .. _L.chest, Value = "Pecho"}, {Label = "🔀 " .. _L.mixed, Value = "Mixto"}
}, function(value) Config.AimTarget = value; State.lockedTarget = nil end)
smoothController = cCCS(_L.smooth, {
    {Label = "⚡ " .. _L.low, Value = "Bajo"}, {Label = "🛡️ " .. _L.mid, Value = "Medio"}, {Label = "🍃 " .. _L.high, Value = "Alto"}
}, function(value) Config.AimSmooth = value end)
modeController = cCCS(_L.aimMode, {
    {Label = _L.modeToggle, Value = "Toggle"},
    {Label = _L.modeFov, Value = "FOV"},
    {Label = _L.modeHold, Value = "Hold"}
}, function(value) Config.AimMode = value end)
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
local function uBUT()
    for action, btn in pairs(bindButtons) do
        if State.isBinding ~= action then
            btn.Text = bindLabels[action] .. ": [" .. Config.Binds[action].Name .. "]"
            btn.BackgroundColor3 = Config.Theme.TabInactive
            btn.TextColor3 = Config.Theme.TextPrimary
        end
    end
end
local function sCU()
    if targetController then targetController.setValue(Config.AimTarget) end
    if smoothController then smoothController.setValue(Config.AimSmooth) end
    if modeController then modeController.setValue(Config.AimMode) end
    uBUT()
    if uFSU then
        uFSU()
    end
end
sCfg = function()
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
lCfg = function()
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
    sCU()
    uMB()
    return true
end
sCU()
saveBtn.MouseButton1Click:Connect(function()
    if sCfg() then
        saveBtn.Text = "✅ GUARDADO"; saveBtn.BackgroundColor3 = Config.Theme.TeamActive; saveBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
        task.delay(1.5, function() saveBtn.Text = "💾 " .. _L.saveCfg; saveBtn.BackgroundColor3 = Config.Theme.TabInactive; saveBtn.TextColor3 = Config.Theme.TextPrimary end)
    else
        saveBtn.Text = "❌ ERROR"; saveBtn.BackgroundColor3 = Config.Theme.BtnOff
        task.delay(1.5, function() saveBtn.Text = "💾 " .. _L.saveCfg; saveBtn.BackgroundColor3 = Config.Theme.TabInactive end)
    end
end)
loadBtn.MouseButton1Click:Connect(function()
    if lCfg() then
        loadBtn.Text = "✅ CARGADO"; loadBtn.BackgroundColor3 = Config.Theme.TeamActive; loadBtn.TextColor3 = Color3.fromRGB(10, 10, 18)
        task.delay(1.5, function() loadBtn.Text = "📂 " .. _L.loadCfg; loadBtn.BackgroundColor3 = Config.Theme.TabInactive; loadBtn.TextColor3 = Config.Theme.TextPrimary end)
    else
        loadBtn.Text = "❌ VACÍO"; loadBtn.BackgroundColor3 = Config.Theme.BtnOff
        task.delay(1.5, function() loadBtn.Text = "📂 " .. _L.loadCfg; loadBtn.BackgroundColor3 = Config.Theme.TabInactive end)
    end
end)
local function gMRP()
    local char = LocalPlayer.Character
    if char then
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum and hum.SeatPart then return hum.SeatPart.Position end
        local root = char:FindFirstChild("HumanoidRootPart")
        if root then return root.Position end
    end
    return Camera.CFrame.Position
end
local function rPL()
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
            teamBtn.MouseButton1Click:Connect(function() State.teamPlayers[player.Name] = not State.teamPlayers[player.Name] or nil; rPL(); sCfg() end)
            pinBtn.MouseButton1Click:Connect(function()
                if State.pinnedPlayers[player.Name] then State.pinnedPlayers[player.Name] = nil; State.autoPinned[player.Name] = nil else State.pinnedPlayers[player.Name] = true end
                rPL(); sCfg()
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
local function gRC(rarity)
    local colors = {Common = Color3.fromRGB(0, 255, 100), Rare = Color3.fromRGB(0, 150, 255), Epic = Color3.fromRGB(180, 50, 255), Legendary = Color3.fromRGB(255, 200, 0)}
    return colors[rarity] or Color3.fromRGB(255, 255, 255)
end
local function mTN(tool)
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
local function gPT(player)
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
                local realName = mTN(tool)
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
            task.spawn(rPL)
        end
    else
        if State.autoPinned[player.Name] then
            State.pinnedPlayers[player.Name] = nil
            State.autoPinned[player.Name] = nil
            task.spawn(rPL)
        end
    end
    LastToolScan[player.Name] = {time = now, tools = tools}
    return tools
end
local function gOME(player)
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
local function rME(player)
    local master = MasterObjects[player.Name]
    if master then
        if master.Gui then master.Gui:Destroy() end
        MasterObjects[player.Name] = nil; LastInventoryState[player] = nil
    end
end
local function uV()
    if not State.alive then return end
    local myPosition = gMRP()
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            local char = player.Character
            if char then
                local head, root, hum = char:FindFirstChild("Head"), char:FindFirstChild("HumanoidRootPart"), char:FindFirstChildOfClass("Humanoid")
                if head and root and hum then
                    local isPinned, isTeam = State.pinnedPlayers[player.Name], State.teamPlayers[player.Name]
                    if hum.Health > 0 then
                        local master = gOME(player)
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
                                local tools = gPT(player)
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
                                        line.TextColor3 = gRC(toolData.rarity)
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
                            rME(player)
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
                        rME(player)
                        local hl = char:FindFirstChild("BsAura")
                        if hl then hl:Destroy() end
                    end
                else
                    rME(player)
                end
            else
                rME(player)
            end
        end
    end
end

local function gIPN(targetMode, char)
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
local function gCT()
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
                        local partName = gIPN(Config.AimTarget, char)
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
                    local partName = gIPN(Config.AimTarget, char)
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
task.spawn(function()
    while State.alive do
        uV()
        task.wait(0.03)
    end
end)

sC(RunService.RenderStepped, function(dt)
    local isVis = (Config.ShowFOV and Config.AimMode == "FOV")
    FovGuiFrame.Visible = isVis
    if isVis then
        local d = Config.AimFOV * 2
        FovGuiFrame.Size = UDim2.new(0, d, 0, d)
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
    local target = gCT()
    if target and target.Character then
        local partName = gIPN(Config.AimTarget, target.Character)
        local part = partName and target.Character:FindFirstChild(partName)
        if part and part:IsA("BasePart") then
            local camPos = Camera.CFrame.Position
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
            local hardLock = (Config.AimMode == "Toggle") or (Config.AimMode == "Hold") or (Config.AimSmooth == "Bajo")
            if hardLock then
                Camera.CFrame = desired
            else
                local lerpAlpha = 1
                if Config.AimSmooth == "Medio" then
                    lerpAlpha = 1 - math.exp(-22 * dt)
                else
                    lerpAlpha = 1 - math.exp(-10 * dt)
                end
                Camera.CFrame = Camera.CFrame:Lerp(desired, math.clamp(lerpAlpha, 0, 1))
            end
        end
    end
end)
sC(UserInputService.InputBegan, function(input, gpe)
    if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == Config.Binds.GamepadAim then State.holdingAimTrigger = true end
    if State.isBinding then
        if input.UserInputType == Enum.UserInputType.Keyboard then
            local action = State.isBinding
            Config.Binds[action] = input.KeyCode; State.isBinding = nil; sCU()
            sCfg()
        end
        return
    end
    if gpe then return end
    if input.KeyCode == Config.Binds.ToggleMenu then
        MainFrame.Visible = not MainFrame.Visible
    elseif input.KeyCode == Config.Binds.Aimbot or input.KeyCode == Config.Binds.GamepadToggle then
        State.aimEnabled = not State.aimEnabled; if not State.aimEnabled then State.lockedTarget = nil end; uMB(); sCfg()
    elseif input.KeyCode == Config.Binds.InvView then State.invViewEnabled = not State.invViewEnabled; uMB(); sCfg() end
end)
sC(UserInputService.InputEnded, function(input, gpe)
    if input.UserInputType == Enum.UserInputType.MouseButton2 or input.KeyCode == Config.Binds.GamepadAim then State.holdingAimTrigger = false; State.lockedTarget = nil end
end)
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
sC(UserInputService.InputChanged, function(input)
    if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)
sC(UserInputService.InputEnded, function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = false
    end
end)
local function cln()
    State.alive = false
    pcall(function()
        RunService:UnbindFromRenderStep("BlockSpinAimbot")
    end)
    if FovGuiFrame then pcall(function() FovGuiFrame:Destroy() end) end
    for _, conn in ipairs(State.connections) do
        pcall(function() conn:Disconnect() end)
    end
    for _, p in ipairs(Players:GetPlayers()) do
        rME(p)
        if p.Character then
            local h1 = p.Character:FindFirstChild("BsAura")
            if h1 then h1:Destroy() end
        end
    end
end
closeBtn.MouseButton1Click:Connect(function() cln(); gui:Destroy() end)
sC(Players.PlayerAdded, function(p) cAAT(p); rPL() end)
sC(Players.PlayerRemoving, function(player)
    rME(player)
    State.teamPlayers[player.Name] = nil; State.pinnedPlayers[player.Name] = nil; State.autoPinned[player.Name] = nil
    local row = PlayerRowCache[player.Name]; if row then row:Destroy(); PlayerRowCache[player.Name] = nil end
    rPL()
end)
for _, p in ipairs(Players:GetPlayers()) do if p ~= LocalPlayer then cAAT(p) end end
rPL()
task.spawn(lCfg)
print("[Hermanos CP] Modificación aplicada de manera segura: Versión libre de restricciones cargada con éxito.")
]==========]

local function s(t)
_G.HCP_LANG=h and"en"or"es"
print(o().requesting..t.."...")
local u=(t=="normal")and NORMAL_SCRIPT or LIGHT_SCRIPT
if not u or #u<100 then e:Kick(o().kickLoad)return end
local v,w=loadstring(u)
if not v then warn("[HCP] loadstring error: "..tostring(w))e:Kick(o().kickLoad)return end
local x,y=pcall(v)
if not x then warn("[HCP] runtime error: "..tostring(y))end
end

local z=Instance.new("ScreenGui")
z.Name="HermanosCPLoader_Premium"
z.IgnoreGuiInset=true
z.ResetOnSpawn=false
z.ZIndexBehavior=Enum.ZIndexBehavior.Sibling
z.Parent=p()

local function A(B,C)
if C then B.BackgroundColor3=Color3.fromRGB(0,140,220)B.TextColor3=Color3.fromRGB(255,255,255)
else B.BackgroundColor3=Color3.fromRGB(28,28,40)B.TextColor3=Color3.fromRGB(160,165,180)end
end

local function D(E,F)
local G=Instance.new("Frame")
G.Size=UDim2.new(0,E,0,F)
G.Position=UDim2.new(0.5,-math.floor(E/2),0.5,-math.floor(F/2))
G.BackgroundColor3=Color3.fromRGB(10,10,15)
G.BorderSizePixel=0
G.ClipsDescendants=true
G.Parent=z
Instance.new("UICorner",G).CornerRadius=UDim.new(0,12)
local H=Instance.new("UIStroke")
H.Color=Color3.fromRGB(0,180,255)
H.Thickness=1.5
H.Transparency=0.2
H.Parent=G
local I=Instance.new("UIGradient")
I.Color=ColorSequence.new({ColorSequenceKeypoint.new(0,Color3.fromRGB(15,12,28)),ColorSequenceKeypoint.new(0.5,Color3.fromRGB(8,8,12)),ColorSequenceKeypoint.new(1,Color3.fromRGB(5,15,20))})
I.Rotation=45
I.Parent=G
return G,H
end

local function J(K,L,M,N,O)
local P=Instance.new("Frame")
P.Size=UDim2.new(1,0,0,44)
P.BackgroundColor3=Color3.fromRGB(14,14,22)
P.BorderSizePixel=0
P.Parent=K
Instance.new("UICorner",P).CornerRadius=UDim.new(0,12)
local Q=Instance.new("Frame")
Q.Size=UDim2.new(1,0,0,12)
Q.Position=UDim2.new(0,0,1,-12)
Q.BackgroundColor3=Color3.fromRGB(14,14,22)
Q.BorderSizePixel=0
Q.Parent=P
local R=Instance.new("TextLabel")
R.Font=Enum.Font.Michroma
R.TextSize=10
R.TextColor3=Color3.fromRGB(255,255,255)
R.Size=UDim2.new(0,120,1,0)
R.Position=UDim2.new(0,12,0,0)
R.BackgroundTransparency=1
R.Text=L
R.TextXAlignment=Enum.TextXAlignment.Left
R.Parent=P
local S=O and 140 or 108
local T=Instance.new("TextButton")
T.Size=UDim2.new(0,30,0,22)
T.Position=UDim2.new(1,-S,0.5,-11)
T.Text="ES"
T.Font=Enum.Font.GothamBold
T.TextSize=10
T.Parent=P
Instance.new("UICorner",T).CornerRadius=UDim.new(0,5)
local U=Instance.new("TextButton")
U.Size=UDim2.new(0,30,0,22)
U.Position=UDim2.new(1,-(S-34),0.5,-11)
U.Text="EN"
U.Font=Enum.Font.GothamBold
U.TextSize=10
U.Parent=P
Instance.new("UICorner",U).CornerRadius=UDim.new(0,5)
A(T,not h)A(U,h)
if O then
local V=Instance.new("TextButton")
V.Size=UDim2.new(0,26,0,26)
V.Position=UDim2.new(1,-64,0.5,-13)
V.Text="−"
V.TextSize=18
V.Font=Enum.Font.GothamBold
V.TextColor3=Color3.fromRGB(255,210,80)
V.BackgroundColor3=Color3.fromRGB(40,35,18)
V.Parent=P
Instance.new("UICorner",V).CornerRadius=UDim.new(0,6)
V.MouseButton1Click:Connect(function()if M then M()end end)
end
local W=Instance.new("TextButton")
W.Size=UDim2.new(0,26,0,26)
W.Position=UDim2.new(1,-34,0.5,-13)
W.Text="X"
W.TextSize=14
W.Font=Enum.Font.GothamBold
W.TextColor3=Color3.fromRGB(255,90,110)
W.BackgroundColor3=Color3.fromRGB(28,16,22)
W.Parent=P
Instance.new("UICorner",W).CornerRadius=UDim.new(0,6)
W.MouseButton1Click:Connect(N)
return P,T,U
end

local function X(Y,Z,aa,ab,ac,ad)
local ae=Instance.new("TextButton")
ae.Size=UDim2.new(1,-24,0,62)
ae.Position=UDim2.new(0,12,0,Z)
ae.BackgroundColor3=Color3.fromRGB(16,16,26)
ae.Text=""
ae.Parent=Y
Instance.new("UICorner",ae).CornerRadius=UDim.new(0,8)
local af=Instance.new("UIStroke")
af.Thickness=1.2
af.Color=Color3.fromRGB(32,32,48)
af.Transparency=0.4
af.Parent=ae
local ag=Instance.new("TextLabel")
ag.Font=Enum.Font.GothamBold
ag.TextSize=12
ag.TextColor3=Color3.fromRGB(245,245,250)
ag.Size=UDim2.new(1,-32,0,18)
ag.Position=UDim2.new(0,12,0,8)
ag.BackgroundTransparency=1
ag.TextXAlignment=Enum.TextXAlignment.Left
ag.Text=aa
ag.Parent=ae
local ah=Instance.new("TextLabel")
ah.Font=Enum.Font.Ubuntu
ah.TextSize=10
ah.TextColor3=Color3.fromRGB(130,140,160)
ah.Size=UDim2.new(1,-32,0,28)
ah.Position=UDim2.new(0,12,0,28)
ah.BackgroundTransparency=1
ah.TextXAlignment=Enum.TextXAlignment.Left
ah.TextWrapped=true
ah.Text=ab
ah.Parent=ae
local ai=Instance.new("TextLabel")
ai.Font=Enum.Font.GothamBold
ai.TextSize=13
ai.TextColor3=Color3.fromRGB(60,60,80)
ai.Size=UDim2.new(0,16,1,0)
ai.Position=UDim2.new(1,-20,0,0)
ai.BackgroundTransparency=1
ai.Text=">"
ai.Parent=ae
ae.MouseEnter:Connect(function()
c:Create(ae,TweenInfo.new(0.15),{BackgroundColor3=Color3.fromRGB(22,22,38)}):Play()
c:Create(af,TweenInfo.new(0.15),{Color=ac,Transparency=0}):Play()
c:Create(ag,TweenInfo.new(0.15),{TextColor3=ac}):Play()
c:Create(ai,TweenInfo.new(0.15),{TextColor3=ac}):Play()
end)
ae.MouseLeave:Connect(function()
c:Create(ae,TweenInfo.new(0.15),{BackgroundColor3=Color3.fromRGB(16,16,26)}):Play()
c:Create(af,TweenInfo.new(0.15),{Color=Color3.fromRGB(32,32,48),Transparency=0.4}):Play()
c:Create(ag,TweenInfo.new(0.15),{TextColor3=Color3.fromRGB(245,245,250)}):Play()
c:Create(ai,TweenInfo.new(0.15),{TextColor3=Color3.fromRGB(60,60,80)}):Play()
end)
ae.MouseButton1Click:Connect(ad)
return ag,ah
end

local function aj(ak,al)
local am,an,ao
ak.InputBegan:Connect(function(ap)
if ap.UserInputType==Enum.UserInputType.MouseButton1 or ap.UserInputType==Enum.UserInputType.Touch then
am=true an=ap.Position ao=al.Position
end
end)
d.InputChanged:Connect(function(ap)
if am and(ap.UserInputType==Enum.UserInputType.MouseMovement or ap.UserInputType==Enum.UserInputType.Touch)then
local aq=ap.Position-an
al.Position=UDim2.new(ao.X.Scale,ao.X.Offset+aq.X,ao.Y.Scale,ao.Y.Offset+aq.Y)
end
end)
d.InputEnded:Connect(function(ap)
if ap.UserInputType==Enum.UserInputType.MouseButton1 or ap.UserInputType==Enum.UserInputType.Touch then am=false end
end)
end

local function ar(as,at,au,av)
c:Create(at,TweenInfo.new(0.12),{Transparency=1}):Play()
local aw=c:Create(as,TweenInfo.new(0.18,Enum.EasingStyle.Quad,Enum.EasingDirection.In),{Size=UDim2.new(0,au,0,0),Position=UDim2.new(0.5,-math.floor(au/2),0.5,0)})
aw:Play()
aw.Completed:Connect(function()as:Destroy()if av then av()end end)
end

local function ax(ay)
local az,aA=k(ay),m(ay)
local aB,aC=D(az,aA)
aB.Name="VersionMenu"
local function aD()ar(aB,aC,az)end
local aE,aF,aG=J(aB,"HERMANOS CP",aD,function()if ay then aD()else z:Destroy()end end,ay)
aj(aE,aB)
local aH=Instance.new("TextLabel")
aH.Font=Enum.Font.Ubuntu aH.TextSize=11 aH.TextColor3=Color3.fromRGB(150,160,185)
aH.Size=UDim2.new(1,-24,0,18)aH.Position=UDim2.new(0,12,0,50)aH.BackgroundTransparency=1
aH.TextXAlignment=Enum.TextXAlignment.Left aH.Text=o().sub aH.Parent=aB
local aI,aJ=X(aB,76,o().norm,o().normD,Color3.fromRGB(0,210,255),function()
ar(aB,aC,az,function()z:Destroy()s("normal")end)
end)
local aK,aL=X(aB,146,o().light,o().lightD,Color3.fromRGB(0,255,140),function()
ar(aB,aC,az,function()z:Destroy()s("light")end)
end)
local aM=Instance.new("TextLabel")
aM.Size=UDim2.new(1,-24,0,16)aM.Position=UDim2.new(0,12,1,-24)aM.BackgroundTransparency=1
aM.Font=Enum.Font.Ubuntu aM.TextSize=10 aM.TextColor3=Color3.fromRGB(120,130,150)
aM.TextXAlignment=Enum.TextXAlignment.Left aM.Text=o().protected aM.Parent=aB
local function aN()
local aO=o()
aH.Text=aO.sub aI.Text=aO.norm aJ.Text=aO.normD aK.Text=aO.light aL.Text=aO.lightD aM.Text=aO.protected
A(aF,not h)A(aG,h)
end
aF.MouseButton1Click:Connect(function()h=false aN()end)
aG.MouseButton1Click:Connect(function()h=true aN()end)
return aB
end

local function aP()
local aQ=Instance.new("ImageButton")
aQ.Name="ToggleBall"aQ.Size=UDim2.new(0,52,0,52)aQ.Position=UDim2.new(1,-68,0.52,0)
aQ.BackgroundColor3=Color3.fromRGB(0,160,255)aQ.BorderSizePixel=0 aQ.AutoButtonColor=false aQ.Parent=z
Instance.new("UICorner",aQ).CornerRadius=UDim.new(1,0)
local aR=Instance.new("UIStroke")aR.Color=Color3.fromRGB(255,255,255)aR.Thickness=2 aR.Transparency=0.35 aR.Parent=aQ
local aS=Instance.new("TextLabel")aS.Size=UDim2.new(1,0,1,0)aS.BackgroundTransparency=1
aS.Font=Enum.Font.GothamBold aS.TextSize=13 aS.TextColor3=Color3.fromRGB(255,255,255)aS.Text="HCP"aS.Parent=aQ
local aT,aU,aV
aQ.InputBegan:Connect(function(aW)
if aW.UserInputType==Enum.UserInputType.Touch or aW.UserInputType==Enum.UserInputType.MouseButton1 then
aT=true aU=aW.Position aV=aQ.Position
end
end)
d.InputChanged:Connect(function(aW)
if aT and(aW.UserInputType==Enum.UserInputType.Touch or aW.UserInputType==Enum.UserInputType.MouseMovement)then
local aX=aW.Position-aU
aQ.Position=UDim2.new(aV.X.Scale,aV.X.Offset+aX.X,aV.Y.Scale,aV.Y.Offset+aX.Y)
end
end)
d.InputEnded:Connect(function(aW)
if aW.UserInputType==Enum.UserInputType.Touch or aW.UserInputType==Enum.UserInputType.MouseButton1 then aT=false end
end)
aQ.MouseButton1Click:Connect(function()
if z:FindFirstChild("VersionMenu")then z.VersionMenu:Destroy()else ax(true)end
end)
end

do
local aY,aZ=k(false),270
if j()then aY=k(true)aZ=260 end
local a_,aC2=D(aY,aZ)
a_.Name="DeviceSelect"
local b0,b1,b2=J(a_,"HERMANOS CP",nil,function()z:Destroy()end,false)
aj(b0,a_)
local b3=Instance.new("TextLabel")
b3.Font=Enum.Font.Ubuntu b3.TextSize=11 b3.TextColor3=Color3.fromRGB(150,160,185)
b3.Size=UDim2.new(1,-24,0,18)b3.Position=UDim2.new(0,12,0,50)b3.BackgroundTransparency=1
b3.TextXAlignment=Enum.TextXAlignment.Left b3.Text=o().choose b3.Parent=a_
local b6,b7=X(a_,76,o().pc,o().pcD,Color3.fromRGB(0,210,255),function()
ar(a_,aC2,aY,function()ax(false)end)
end)
local b8,b9=X(a_,146,o().mob,o().mobD,Color3.fromRGB(0,255,140),function()
ar(a_,aC2,aY,function()aP()end)
end)
local function ba()
local bb=o()
b3.Text=bb.choose b6.Text=bb.pc b7.Text=bb.pcD b8.Text=bb.mob b9.Text=bb.mobD
A(b1,not h)A(b2,h)
end
b1.MouseButton1Click:Connect(function()h=false ba()end)
b2.MouseButton1Click:Connect(function()h=true ba()end)
end

print("[Hermanos CP] Combined | Offline | UID "..e.UserId)
