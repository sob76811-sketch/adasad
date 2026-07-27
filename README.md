local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local LocalPlayer = Players.LocalPlayer
while not LocalPlayer do
    task.wait(0.1)
end

-- 1. OBTENCIÓN SEGURA DEL PARENT (Compatibilidad universal con Delta / Arceus X / Codex)
local function getGuiParent()
    local gH = (type(gethui) == "function" and gethui()) or (type(getgenv) == "function" and getgenv().gethui and getgenv().gethui())
    if gH then return gH end
    local ok, cg = pcall(function() return CoreGui end)
    if ok and cg then return cg end
    return LocalPlayer:WaitForChild("PlayerGui", 5)
end

-- Limpieza de ejecuciones previas
local parentGui = getGuiParent()
if parentGui:FindFirstChild("HCP_Mobile_UI") then
    parentGui.HCP_Mobile_UI:Destroy()
end

local Gui = Instance.new("ScreenGui")
Gui.Name = "HCP_Mobile_UI"
Gui.IgnoreGuiInset = true
Gui.ResetOnSpawn = false
Gui.Parent = parentGui

-- CONFIGURACIÓN DE AIMBOT Y FOV
local Config = {
    AimFOV = 220,
    ShowFOV = true,
    AimMode = "FOV",
    AimTarget = "Cabeza",
    AimSmooth = "Medio",
    FOVColorNormal = Color3.fromRGB(0, 210, 255),
    FOVColorLocked = Color3.fromRGB(255, 50, 80)
}

local State = {
    aimEnabled = true,
    lockedTarget = nil,
    holdingTrigger = false
}

-- 2. CÍRCULO FOV NATIVO (Parcheado para procesadores y shaders móviles)
local FovFrame = Instance.new("Frame")
FovFrame.Name = "FOVCircle"
FovFrame.AnchorPoint = Vector2.new(0.5, 0.5)
FovFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
FovFrame.BackgroundTransparency = 0.999 -- CRÍTICO: Evita que el shader de celular lo oculte
FovFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
FovFrame.Visible = false
FovFrame.Parent = Gui

local FovCorner = Instance.new("UICorner")
FovCorner.CornerRadius = UDim.new(1, 0)
FovCorner.Parent = FovFrame

local FovStroke = Instance.new("UIStroke")
FovStroke.Thickness = 2
FovStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
FovStroke.Color = Config.FOVColorNormal
FovStroke.Transparency = 0
FovStroke.Parent = FovFrame

-- BOTÓN FLOTANTE MÓVIL (Garantiza acceso si el menú se oculta)
local OpenBall = Instance.new("ImageButton")
OpenBall.Name = "HCP_OpenBall"
OpenBall.Size = UDim2.new(0, 45, 0, 45)
OpenBall.Position = UDim2.new(1, -60, 0.4, 0)
OpenBall.BackgroundColor3 = Color3.fromRGB(0, 160, 255)
OpenBall.Parent = Gui

local BallCorner = Instance.new("UICorner")
BallCorner.CornerRadius = UDim.new(1, 0)
BallCorner.Parent = OpenBall

local BallTxt = Instance.new("TextLabel")
BallTxt.Size = UDim2.new(1, 0, 1, 0)
BallTxt.BackgroundTransparency = 1
BallTxt.Font = Enum.Font.GothamBold
BallTxt.TextSize = 11
BallTxt.TextColor3 = Color3.fromRGB(255, 255, 255)
BallTxt.Text = "HCP"
BallTxt.Parent = OpenBall

-- LÓGICA DE ACTUALIZACIÓN DEL CÍRCULO Y AIMBOT
RunService.RenderStepped:Connect(function()
    local isVis = Config.ShowFOV and Config.AimMode == "FOV"
    FovFrame.Visible = isVis
    if isVis then
        local size = Config.AimFOV * 2
        FovFrame.Size = UDim2.new(0, size, 0, size)
        FovStroke.Color = State.lockedTarget and Config.FOVColorLocked or Config.FOVColorNormal
    end
end)

-- BÚSQUEDA DE OBJETIVO (Compatible con Mobile Touch)
local Camera = workspace.CurrentCamera
local function getClosestTarget()
    local closest, minDist = nil, Config.AimFOV
    local center = Camera.ViewportSize / 2
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer and plr.Character then
            local hum = plr.Character:FindFirstChildOfClass("Humanoid")
            local head = plr.Character:FindFirstChild("Head")
            if hum and hum.Health > 0 and head then
                local pos, onScr = Camera:WorldToViewportPoint(head.Position)
                if onScr then
                    local dist = (Vector2.new(pos.X, pos.Y) - center).Magnitude
                    if dist < minDist then
                        minDist = dist
                        closest = plr
                    end
                end
            end
        end
    end
    return closest
end

RunService:BindToRenderStep("HCP_AimbotLogic", Enum.RenderPriority.Camera.Value + 1, function(dt)
    if not State.aimEnabled then return end
    local target = getClosestTarget()
    State.lockedTarget = target
    if target and target.Character and target.Character:FindFirstChild("Head") then
        local camPos = Camera.CFrame.Position
        local targetPos = target.Character.Head.Position
        local desired = CFrame.new(camPos, targetPos)
        Camera.CFrame = Camera.CFrame:Lerp(desired, math.clamp(1 - math.exp(-18 * dt), 0, 1))
    end
end)

print("[Hermanos CP] Script cargado correctamente desde GitHub con parche nativo de móvil.")
