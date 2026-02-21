-- ╔══════════════════════════════════════════╗
-- ║         BRAINROT HUB  •  v5.0            ║
-- ║     Mobile + PC  •  Bugs corrigidos      ║
-- ╚══════════════════════════════════════════╝

local Players          = game:GetService("Players")
local TweenService     = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local RunService       = game:GetService("RunService")
local Workspace        = game:GetService("Workspace")

local player = Players.LocalPlayer

-- ══════════════════════════════════════════════
-- CORES
-- ══════════════════════════════════════════════
local C = {
    BG        = Color3.fromRGB(8,   8,  16),
    PANEL     = Color3.fromRGB(13,  13, 26),
    ITEM      = Color3.fromRGB(18,  18, 36),
    HOVER     = Color3.fromRGB(25,  25, 50),
    BORDER    = Color3.fromRGB(40,  40, 75),
    ACCENT    = Color3.fromRGB(105, 90, 255),
    ACCENT2   = Color3.fromRGB(170, 90, 255),
    GREEN     = Color3.fromRGB(60,  220, 140),
    GOLD      = Color3.fromRGB(255, 195, 60),
    RED       = Color3.fromRGB(255, 60,  85),
    TEXT      = Color3.fromRGB(230, 230, 255),
    TEXTSUB   = Color3.fromRGB(120, 120, 170),
    CELESTIAL = Color3.fromRGB(90,  160, 255),
    SECRET    = Color3.fromRGB(255, 100, 220),
    MYTHIC    = Color3.fromRGB(255, 175, 50),
}

-- ══════════════════════════════════════════════
-- HELPERS
-- ══════════════════════════════════════════════
local function tw(obj, props, t, style)
    TweenService:Create(obj,
        TweenInfo.new(t or 0.18, style or Enum.EasingStyle.Quart, Enum.EasingDirection.Out),
        props):Play()
end

local function corner(p, r)
    local u = Instance.new("UICorner")
    u.CornerRadius = UDim.new(0, r or 8)
    u.Parent = p
    return u
end

local function stroke(p, col, th)
    local s = Instance.new("UIStroke")
    s.Color = col or C.BORDER
    s.Thickness = th or 1
    s.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    s.Parent = p
    return s
end

local function pad(p, l, r, t, b)
    local u = Instance.new("UIPadding")
    u.PaddingLeft   = UDim.new(0, l or 0)
    u.PaddingRight  = UDim.new(0, r or 0)
    u.PaddingTop    = UDim.new(0, t or 0)
    u.PaddingBottom = UDim.new(0, b or 0)
    u.Parent = p
end

local function vlist(p, sp)
    local u = Instance.new("UIListLayout")
    u.Padding = UDim.new(0, sp or 6)
    u.SortOrder = Enum.SortOrder.LayoutOrder
    u.Parent = p
    return u
end

local function lbl(parent, txt, size, col, font, xalign)
    local l = Instance.new("TextLabel", parent)
    l.Text = txt
    l.BackgroundTransparency = 1
    l.TextColor3 = col or C.TEXT
    l.TextSize = size or 11
    l.Font = font or Enum.Font.GothamBold
    l.TextXAlignment = xalign or Enum.TextXAlignment.Left
    l.Size = UDim2.new(1, 0, 1, 0)
    return l
end

-- ══════════════════════════════════════════════
-- SCREEN GUI
-- ══════════════════════════════════════════════
local sg = Instance.new("ScreenGui")
sg.Name           = "BrainrotHub"
sg.ResetOnSpawn   = false
sg.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
sg.IgnoreGuiInset = true
sg.Parent         = player.PlayerGui

-- ══════════════════════════════════════════════
-- JANELA
-- ══════════════════════════════════════════════
local WIN_W    = 255
local WIN_H    = 380
local TOPBAR_H = 38

local win = Instance.new("Frame")
win.Name              = "Window"
win.Size              = UDim2.new(0, WIN_W, 0, WIN_H)
win.Position          = UDim2.new(0, 10, 0, 36)
win.BackgroundColor3  = C.BG
win.BorderSizePixel   = 0
win.ClipsDescendants  = true
win.Parent            = sg
corner(win, 11)
stroke(win, C.BORDER, 1.5)

-- ══════════════════════════════════════════════
-- TOP BAR
-- ══════════════════════════════════════════════
local topBar = Instance.new("Frame")
topBar.Size             = UDim2.new(1, 0, 0, TOPBAR_H)
topBar.BackgroundColor3 = C.PANEL
topBar.BorderSizePixel  = 0
topBar.ZIndex           = 3
topBar.Parent           = win
corner(topBar, 11)

-- cobre cantos inferiores do topBar
local tbc = Instance.new("Frame", topBar)
tbc.Size = UDim2.new(1, 0, 0, 11)
tbc.Position = UDim2.new(0, 0, 1, -11)
tbc.BackgroundColor3 = C.PANEL
tbc.BorderSizePixel  = 0
tbc.ZIndex = 3

local tdiv = Instance.new("Frame", topBar)
tdiv.Size = UDim2.new(1, 0, 0, 1)
tdiv.Position = UDim2.new(0, 0, 1, -1)
tdiv.BackgroundColor3 = C.BORDER
tdiv.BorderSizePixel  = 0
tdiv.ZIndex = 4

-- Badge ✦
local badge = Instance.new("Frame", topBar)
badge.Size             = UDim2.new(0, 22, 0, 22)
badge.Position         = UDim2.new(0, 8, 0.5, -11)
badge.BackgroundColor3 = C.ACCENT
badge.BorderSizePixel  = 0
badge.ZIndex           = 5
corner(badge, 6)
local bt = Instance.new("TextLabel", badge)
bt.Text = "✦" bt.Size = UDim2.new(1,0,1,0) bt.BackgroundTransparency = 1
bt.TextColor3 = Color3.new(1,1,1) bt.TextSize = 11 bt.Font = Enum.Font.GothamBold bt.ZIndex = 6
bt.TextXAlignment = Enum.TextXAlignment.Center bt.TextYAlignment = Enum.TextYAlignment.Center

local titleL = Instance.new("TextLabel", topBar)
titleL.Text = "DN Hub - Auto Brainrots"
titleL.Size = UDim2.new(1, -90, 1, 0)
titleL.Position = UDim2.new(0, 36, 0, 0)
titleL.BackgroundTransparency = 1
titleL.TextColor3 = C.TEXT
titleL.TextSize = 11
titleL.Font = Enum.Font.GothamBold
titleL.TextXAlignment = Enum.TextXAlignment.Left
titleL.ZIndex = 5

-- Botões fechar / minimizar
local function mkCtrl(xOff, bg, txt)
    local b = Instance.new("TextButton", topBar)
    b.Size = UDim2.new(0, 18, 0, 18)
    b.Position = UDim2.new(1, -xOff, 0.5, -9)
    b.BackgroundColor3 = bg
    b.Text = txt
    b.TextColor3 = Color3.fromRGB(10, 10, 10)
    b.TextSize = 9
    b.Font = Enum.Font.GothamBold
    b.BorderSizePixel = 0
    b.AutoButtonColor = false
    b.ZIndex = 6
    corner(b, 50)
    return b
end
local closeBtn    = mkCtrl(24, C.RED,  "✕")
local minimizeBtn = mkCtrl(46, C.GOLD, "−")

-- ══════════════════════════════════════════════
-- DRAG — Mouse + Touch
-- ══════════════════════════════════════════════
local isDragging   = false
local dragStart    = Vector2.new()
local winStartOff  = Vector2.new()

topBar.InputBegan:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1
    or i.UserInputType == Enum.UserInputType.Touch then
        isDragging  = true
        dragStart   = Vector2.new(i.Position.X, i.Position.Y)
        winStartOff = Vector2.new(win.Position.X.Offset, win.Position.Y.Offset)
    end
end)

topBar.InputChanged:Connect(function(i)
    if not isDragging then return end
    if i.UserInputType == Enum.UserInputType.MouseMovement
    or i.UserInputType == Enum.UserInputType.Touch then
        local d = Vector2.new(i.Position.X, i.Position.Y) - dragStart
        local sx, sy = sg.AbsoluteSize.X, sg.AbsoluteSize.Y
        win.Position = UDim2.new(0,
            math.clamp(winStartOff.X + d.X, 0, sx - WIN_W), 0,
            math.clamp(winStartOff.Y + d.Y, 0, sy - TOPBAR_H))
    end
end)

-- Mouse move vem pelo UIS, Touch move vem pelo topBar.InputChanged acima
UserInputService.InputChanged:Connect(function(i)
    if not isDragging then return end
    if i.UserInputType == Enum.UserInputType.MouseMovement then
        local d = Vector2.new(i.Position.X, i.Position.Y) - dragStart
        local sx, sy = sg.AbsoluteSize.X, sg.AbsoluteSize.Y
        win.Position = UDim2.new(0,
            math.clamp(winStartOff.X + d.X, 0, sx - WIN_W), 0,
            math.clamp(winStartOff.Y + d.Y, 0, sy - TOPBAR_H))
    end
end)

UserInputService.InputEnded:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1
    or i.UserInputType == Enum.UserInputType.Touch then
        isDragging = false
    end
end)

-- ══════════════════════════════════════════════
-- SCROLL CONTENT
-- ══════════════════════════════════════════════
local scroll = Instance.new("ScrollingFrame")
scroll.Size                = UDim2.new(1, 0, 1, -TOPBAR_H)
scroll.Position            = UDim2.new(0, 0, 0, TOPBAR_H)
scroll.BackgroundTransparency = 1
scroll.BorderSizePixel     = 0
scroll.ScrollBarThickness  = 2
scroll.ScrollBarImageColor3= C.ACCENT
scroll.CanvasSize          = UDim2.new(0, 0, 0, 0)
scroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
scroll.ClipsDescendants    = true
scroll.Parent              = win
vlist(scroll, 7)
pad(scroll, 8, 8, 8, 10)

-- ══════════════════════════════════════════════
-- COMPONENTES BASE
-- ══════════════════════════════════════════════

-- Cartão simples dentro do scroll
local function mkCard(lo)
    local f = Instance.new("Frame")
    f.Size              = UDim2.new(1, 0, 0, 0)
    f.AutomaticSize     = Enum.AutomaticSize.Y
    f.BackgroundColor3  = C.PANEL
    f.BorderSizePixel   = 0
    f.LayoutOrder       = lo
    f.ClipsDescendants  = false   -- IMPORTANTE: não clipar, senão a lista some!
    f.Parent            = scroll
    corner(f, 8)
    stroke(f, C.BORDER)
    pad(f, 8, 8, 7, 8)
    vlist(f, 5)
    return f
end

-- Header do cartão (barra colorida + ícone + título)
local function mkHeader(p, ico, title, col)
    local h = Instance.new("Frame", p)
    h.Size               = UDim2.new(1, 0, 0, 20)
    h.BackgroundTransparency = 1
    h.LayoutOrder        = 0

    local bar = Instance.new("Frame", h)
    bar.Size = UDim2.new(0, 3, 1, 0)
    bar.BackgroundColor3 = col or C.ACCENT
    bar.BorderSizePixel  = 0
    corner(bar, 3)

    local icoL = Instance.new("TextLabel", h)
    icoL.Text = ico
    icoL.Size = UDim2.new(0, 18, 1, 0)
    icoL.Position = UDim2.new(0, 8, 0, 0)
    icoL.BackgroundTransparency = 1
    icoL.TextColor3 = col or C.ACCENT
    icoL.TextSize = 12
    icoL.Font = Enum.Font.GothamBold

    local tL = Instance.new("TextLabel", h)
    tL.Text = title
    tL.Size = UDim2.new(1, -30, 1, 0)
    tL.Position = UDim2.new(0, 26, 0, 0)
    tL.BackgroundTransparency = 1
    tL.TextColor3 = col or C.ACCENT
    tL.TextSize = 10
    tL.Font = Enum.Font.GothamBold
    tL.TextXAlignment = Enum.TextXAlignment.Left
end

-- Botão toggle (expande/recolhe lista)
local function mkToggleBtn(p, lo, ico, label, col)
    local b = Instance.new("TextButton", p)
    b.Size             = UDim2.new(1, 0, 0, 30)
    b.BackgroundColor3 = C.ITEM
    b.Text             = ""
    b.BorderSizePixel  = 0
    b.AutoButtonColor  = false
    b.LayoutOrder      = lo
    corner(b, 6)
    stroke(b, C.BORDER)

    local icoL = Instance.new("TextLabel", b)
    icoL.Text = ico
    icoL.Size = UDim2.new(0, 20, 1, 0)
    icoL.Position = UDim2.new(0, 6, 0, 0)
    icoL.BackgroundTransparency = 1
    icoL.TextColor3 = col or C.ACCENT
    icoL.TextSize   = 12
    icoL.Font       = Enum.Font.GothamBold

    local tL = Instance.new("TextLabel", b)
    tL.Text = label
    tL.Size = UDim2.new(1, -52, 1, 0)
    tL.Position = UDim2.new(0, 28, 0, 0)
    tL.BackgroundTransparency = 1
    tL.TextColor3 = C.TEXT
    tL.TextSize   = 11
    tL.Font       = Enum.Font.GothamBold
    tL.TextXAlignment = Enum.TextXAlignment.Left

    local arr = Instance.new("TextLabel", b)
    arr.Text = "▾"
    arr.Size = UDim2.new(0, 18, 1, 0)
    arr.Position = UDim2.new(1, -20, 0, 0)
    arr.BackgroundTransparency = 1
    arr.TextColor3 = C.TEXTSUB
    arr.TextSize   = 12
    arr.Font       = Enum.Font.GothamBold

    b.MouseEnter:Connect(function() tw(b, {BackgroundColor3=C.HOVER}, 0.1) end)
    b.MouseLeave:Connect(function() tw(b, {BackgroundColor3=C.ITEM},  0.1) end)
    return b, arr
end

-- Label de status
local function mkStatus(p, lo)
    local l = Instance.new("TextLabel", p)
    l.Size               = UDim2.new(1, 0, 0, 14)
    l.BackgroundTransparency = 1
    l.TextColor3         = C.TEXTSUB
    l.TextSize           = 9
    l.Font               = Enum.Font.Gotham
    l.TextXAlignment     = Enum.TextXAlignment.Left
    l.LayoutOrder        = lo
    l.Text               = ""
    return l
end

local function setStatus(l, msg, col)
    l.Text       = "  " .. msg
    l.TextColor3 = col or C.TEXTSUB
    if col then
        task.delay(3, function()
            if l and l.Parent then tw(l, {TextColor3=C.TEXTSUB}, 0.5) end
        end)
    end
end

-- ══════════════════════════════════════════════
-- LISTA DE MODELOS
-- FIX: o panel fica SEMPRE no DOM, só Visible muda.
-- O card precisa de ClipsDescendants=false.
-- ══════════════════════════════════════════════
local function buildModelPanel(parentCard, folderGetter, accentColor, insertOrder)
    local panel = Instance.new("Frame", parentCard)
    panel.Name             = "ModelPanel"
    panel.Size             = UDim2.new(1, 0, 0, 0)
    panel.AutomaticSize    = Enum.AutomaticSize.Y
    panel.BackgroundTransparency = 1
    panel.BorderSizePixel  = 0
    panel.LayoutOrder      = insertOrder
    panel.Visible          = false
    panel.ClipsDescendants = false
    vlist(panel, 3)

    local statusLbl = mkStatus(panel, 0)

    local function refresh()
        -- limpa filhos que não são o status
        for _, c in ipairs(panel:GetChildren()) do
            if c ~= statusLbl and (c:IsA("TextButton") or c:IsA("Frame")) then
                c:Destroy()
            end
        end

        local folder = folderGetter()
        if not folder then
            setStatus(statusLbl, "⚠ Pasta não encontrada.", C.RED)
            return
        end

        local models = folder:GetChildren()
        if #models == 0 then
            setStatus(statusLbl, "⚠ Pasta vazia.", C.GOLD)
            return
        end

        setStatus(statusLbl, #models .. " modelo(s) disponível(is)")

        for i, model in ipairs(models) do
            local row = Instance.new("TextButton", panel)
            row.Size             = UDim2.new(1, 0, 0, 28)
            row.BackgroundColor3 = C.ITEM
            row.Text             = ""
            row.BorderSizePixel  = 0
            row.AutoButtonColor  = false
            row.LayoutOrder      = i
            corner(row, 5)
            stroke(row, C.BORDER)

            local dot = Instance.new("Frame", row)
            dot.Size             = UDim2.new(0, 5, 0, 5)
            dot.Position         = UDim2.new(0, 7, 0.5, -2.5)
            dot.BackgroundColor3 = accentColor
            dot.BorderSizePixel  = 0
            corner(dot, 50)

            local nL = Instance.new("TextLabel", row)
            nL.Text             = model.Name
            nL.Size             = UDim2.new(1, -56, 1, 0)
            nL.Position         = UDim2.new(0, 18, 0, 0)
            nL.BackgroundTransparency = 1
            nL.TextColor3       = C.TEXT
            nL.TextSize         = 10
            nL.Font             = Enum.Font.Gotham
            nL.TextXAlignment   = Enum.TextXAlignment.Left
            nL.TextTruncate     = Enum.TextTruncate.AtEnd

            local tpB = Instance.new("TextButton", row)
            tpB.Size             = UDim2.new(0, 38, 0, 18)
            tpB.Position         = UDim2.new(1, -44, 0.5, -9)
            tpB.BackgroundColor3 = accentColor
            tpB.Text             = "IR"
            tpB.TextColor3       = Color3.fromRGB(8, 8, 16)
            tpB.TextSize         = 9
            tpB.Font             = Enum.Font.GothamBold
            tpB.BorderSizePixel  = 0
            tpB.AutoButtonColor  = false
            corner(tpB, 4)

            row.MouseEnter:Connect(function() tw(row, {BackgroundColor3=C.HOVER}, 0.1) end)
            row.MouseLeave:Connect(function() tw(row, {BackgroundColor3=C.ITEM},  0.1) end)

            local function doTP()
                local c    = player.Character
                local root = c and c:FindFirstChild("HumanoidRootPart")
                if not root then setStatus(statusLbl, "⚠ Sem personagem.", C.RED) return end

                local f = folderGetter()
                local m = f and f:FindFirstChild(model.Name)
                if not m then setStatus(statusLbl, "⚠ Modelo sumiu.", C.RED) return end

                local part = m.PrimaryPart or m:FindFirstChildWhichIsA("BasePart")
                if part then
                    root.CFrame = part.CFrame + Vector3.new(0, 5, 0)
                    setStatus(statusLbl, "✓ → " .. model.Name, C.GREEN)
                else
                    setStatus(statusLbl, "⚠ Modelo sem BasePart.", C.GOLD)
                end
            end

            tpB.MouseButton1Click:Connect(doTP)
            row.MouseButton1Click:Connect(doTP)
        end
    end

    return panel, refresh
end

local function bindToggle(btn, arr, panel, refreshFn)
    local open = false
    local function toggle()
        open = not open
        if open then refreshFn() end
        panel.Visible = open
        arr.Text = open and "▴" or "▾"
    end
    -- Usa APENAS MouseButton1Click para PC e Activated para Mobile
    -- Não conectar os dois no mesmo botão (dispara 2x no PC com touch emulado)
    btn.MouseButton1Click:Connect(toggle)
end

-- ══════════════════════════════════════════════
-- CARTÕES: CELESTIAL / SECRET / MYTHIC
-- ══════════════════════════════════════════════
local function mkBrainrotCard(lo, ico, title, col, folderName)
    local card = mkCard(lo)
    mkHeader(card, ico, title, col)
    local btn, arr = mkToggleBtn(card, 1, ico, title, col)
    local panel, refresh = buildModelPanel(card, function()
        local gf = Workspace:FindFirstChild("GameFolder")
        local br = gf and gf:FindFirstChild("Brainrots")
        return br and br:FindFirstChild(folderName)
    end, col, 2)
    bindToggle(btn, arr, panel, refresh)
end

mkBrainrotCard(1, "🌌", "AUTO CELESTIAL", C.CELESTIAL, "Celestial")
mkBrainrotCard(2, "🔮", "AUTO SECRET",    C.SECRET,    "Secret")
mkBrainrotCard(3, "🔥", "AUTO MYTHIC",    C.MYTHIC,    "Mythic")

-- ══════════════════════════════════════════════
-- TP TO BASE
-- FIX: Baseplace é um Model, não tem .CFrame.
-- Pega PrimaryPart ou primeira BasePart recursiva.
-- ══════════════════════════════════════════════
local baseCard = mkCard(4)
mkHeader(baseCard, "🏠", "TELEPORTE", C.GREEN)

local tpBtn = Instance.new("TextButton", baseCard)
tpBtn.Size             = UDim2.new(1, 0, 0, 30)
tpBtn.BackgroundColor3 = C.GREEN
tpBtn.Text             = "🏠  TP To Base"
tpBtn.TextColor3       = Color3.fromRGB(8, 8, 16)
tpBtn.TextSize         = 11
tpBtn.Font             = Enum.Font.GothamBold
tpBtn.BorderSizePixel  = 0
tpBtn.AutoButtonColor  = false
tpBtn.LayoutOrder      = 1
corner(tpBtn, 6)
tpBtn.MouseEnter:Connect(function() tw(tpBtn, {BackgroundTransparency=0.2}, 0.1) end)
tpBtn.MouseLeave:Connect(function() tw(tpBtn, {BackgroundTransparency=0},   0.1) end)

local tpStatus = mkStatus(baseCard, 2)

tpBtn.MouseButton1Click:Connect(function()
    local c    = player.Character
    local root = c and c:FindFirstChild("HumanoidRootPart")
    if not root then setStatus(tpStatus, "⚠ Sem personagem.", C.RED) return end

    local gf       = Workspace:FindFirstChild("GameFolder")
    local baseplate = gf and gf:FindFirstChild("Baseplate")

    if baseplate and baseplate:IsA("BasePart") then
        root.CFrame = baseplate.CFrame + Vector3.new(0, 6, 0)
        setStatus(tpStatus, "✓ Teleportado para a Base!", C.GREEN)
    else
        setStatus(tpStatus, "⚠ Baseplate não encontrado.", C.RED)
    end
end)

-- ══════════════════════════════════════════════
-- PLAYER CARD
-- ══════════════════════════════════════════════
local playerCard = mkCard(5)
mkHeader(playerCard, "⚙", "PLAYER", C.ACCENT)

-- ── FLY ──────────────────────────────────────
-- FIX: flySwitch era TextButton filho de Frame dentro do scroll.
-- O problema era que Activated disparava 2x (Mouse+Touch).
-- Agora usa APENAS MouseButton1Click + um debounce.
local flyActive  = false
local flyConn, flyBV, flyBG

-- Direções pressionadas por toque mobile
local flyTouch = { f=false, b=false, l=false, r=false, u=false, d=false }

-- ── Row: toggle switch ────────────────────────
local flyRow = Instance.new("Frame", playerCard)
flyRow.Size             = UDim2.new(1, 0, 0, 30)
flyRow.BackgroundColor3 = C.ITEM
flyRow.BorderSizePixel  = 0
flyRow.LayoutOrder      = 1
corner(flyRow, 6)
stroke(flyRow, C.BORDER)

local flyIco = Instance.new("TextLabel", flyRow)
flyIco.Text = "🦋" flyIco.Size = UDim2.new(0,22,1,0) flyIco.Position = UDim2.new(0,6,0,0)
flyIco.BackgroundTransparency=1 flyIco.TextColor3=C.ACCENT flyIco.TextSize=12 flyIco.Font=Enum.Font.GothamBold

local flyLbl = Instance.new("TextLabel", flyRow)
flyLbl.Text="Fly (Em Manutenção)" flyLbl.Size=UDim2.new(1,-82,1,0) flyLbl.Position=UDim2.new(0,28,0,0)
flyLbl.BackgroundTransparency=1 flyLbl.TextColor3=C.TEXT flyLbl.TextSize=10
flyLbl.Font=Enum.Font.GothamBold flyLbl.TextXAlignment=Enum.TextXAlignment.Left

local flySwitch = Instance.new("Frame", flyRow)
flySwitch.Size=UDim2.new(0,40,0,20) flySwitch.Position=UDim2.new(1,-46,0.5,-10)
flySwitch.BackgroundColor3=C.BORDER flySwitch.BorderSizePixel=0 corner(flySwitch,10)

local flyKnob = Instance.new("Frame", flySwitch)
flyKnob.Size=UDim2.new(0,14,0,14) flyKnob.Position=UDim2.new(0,3,0.5,-7)
flyKnob.BackgroundColor3=C.TEXT flyKnob.BorderSizePixel=0 corner(flyKnob,50)

local flyClickArea = Instance.new("TextButton", flyRow)
flyClickArea.Size=UDim2.new(1,0,1,0) flyClickArea.BackgroundTransparency=1
flyClickArea.Text="" flyClickArea.BorderSizePixel=0 flyClickArea.AutoButtonColor=false flyClickArea.ZIndex=5

-- ── Botões Mobile (aparecem só com fly ligado) ─
local flyBtnsFrame = Instance.new("Frame", playerCard)
flyBtnsFrame.Size=UDim2.new(1,0,0,80) flyBtnsFrame.BackgroundTransparency=1
flyBtnsFrame.BorderSizePixel=0 flyBtnsFrame.LayoutOrder=2 flyBtnsFrame.Visible=false

local function mkFlyBtn(parent, txt, x, y, w, h, dirKey)
    local b = Instance.new("TextButton", parent)
    b.Size=UDim2.new(0,w or 36,0,h or 28) b.Position=UDim2.new(0,x,0,y)
    b.BackgroundColor3=C.ITEM b.Text=txt b.TextColor3=C.ACCENT
    b.TextSize=13 b.Font=Enum.Font.GothamBold b.BorderSizePixel=0 b.AutoButtonColor=false
    corner(b,6) stroke(b,C.BORDER)

    b.InputBegan:Connect(function(i)
        if i.UserInputType==Enum.UserInputType.Touch
        or i.UserInputType==Enum.UserInputType.MouseButton1 then
            flyTouch[dirKey]=true
            tw(b,{BackgroundColor3=C.ACCENT},0.08)
        end
    end)
    b.InputEnded:Connect(function(i)
        if i.UserInputType==Enum.UserInputType.Touch
        or i.UserInputType==Enum.UserInputType.MouseButton1 then
            flyTouch[dirKey]=false
            tw(b,{BackgroundColor3=C.ITEM},0.08)
        end
    end)
    -- segurança: se o dedo sair da tela
    UserInputService.InputEnded:Connect(function(i)
        if i.UserInputType==Enum.UserInputType.Touch then flyTouch[dirKey]=false end
    end)
    return b
end

-- Layout dos botões (estilo direcional)
--   [  ▲  ]  [UP] [DN]
-- [◀][  ▼  ][▶]
local BW, BH = 44, 30
local col1 = 0
mkFlyBtn(flyBtnsFrame, "◀", col1,        26, BW, BH, "l")
mkFlyBtn(flyBtnsFrame, "▲", col1+BW+2,    0, BW, BH, "f")
mkFlyBtn(flyBtnsFrame, "▼", col1+BW+2,   32, BW, BH, "b")
mkFlyBtn(flyBtnsFrame, "▶", col1+BW*2+4, 26, BW, BH, "r")
mkFlyBtn(flyBtnsFrame, "⬆", col1+BW*3+10, 0, BW, BH, "u")
mkFlyBtn(flyBtnsFrame, "⬇", col1+BW*3+10,32, BW, BH, "d")

local function setFlyVisual(on)
    if on then
        tw(flySwitch,{BackgroundColor3=C.ACCENT},0.18)
        tw(flyKnob,{Position=UDim2.new(1,-17,0.5,-7)},0.18)
    else
        tw(flySwitch,{BackgroundColor3=C.BORDER},0.18)
        tw(flyKnob,{Position=UDim2.new(0,3,0.5,-7)},0.18)
    end
end

local function stopFly()
    flyActive = false
    setFlyVisual(false)
    flyBtnsFrame.Visible = false
    for k in pairs(flyTouch) do flyTouch[k]=false end
    if flyConn then flyConn:Disconnect() flyConn=nil end
    if flyBV and flyBV.Parent then flyBV:Destroy() end
    if flyBG and flyBG.Parent then flyBG:Destroy() end
    flyBV,flyBG=nil,nil
    local ch=player.Character
    local hum=ch and ch:FindFirstChildOfClass("Humanoid")
    if hum then hum.PlatformStand=false end
end

local function startFly()
    local ch   = player.Character
    local root = ch and ch:FindFirstChild("HumanoidRootPart")
    local hum  = ch and ch:FindFirstChildOfClass("Humanoid")
    if not root or not hum then return end

    flyActive = true
    setFlyVisual(true)
    flyBtnsFrame.Visible = true
    hum.PlatformStand = true

    flyBV = Instance.new("BodyVelocity", root)
    flyBV.MaxForce = Vector3.new(1e5,1e5,1e5) flyBV.Velocity = Vector3.zero

    flyBG = Instance.new("BodyGyro", root)
    flyBG.MaxTorque=Vector3.new(1e5,1e5,1e5) flyBG.P=1e4 flyBG.CFrame=root.CFrame

    flyConn = RunService.Heartbeat:Connect(function()
        if not flyActive then return end
        local r=player.Character and player.Character:FindFirstChild("HumanoidRootPart")
        if not r then stopFly() return end
        local cam=Workspace.CurrentCamera
        local spd=55
        local vel=Vector3.zero

        -- Teclado (PC)
        if UserInputService:IsKeyDown(Enum.KeyCode.W)         then vel+=cam.CFrame.LookVector*spd end
        if UserInputService:IsKeyDown(Enum.KeyCode.S)         then vel-=cam.CFrame.LookVector*spd end
        if UserInputService:IsKeyDown(Enum.KeyCode.A)         then vel-=cam.CFrame.RightVector*spd end
        if UserInputService:IsKeyDown(Enum.KeyCode.D)         then vel+=cam.CFrame.RightVector*spd end
        if UserInputService:IsKeyDown(Enum.KeyCode.Space)     then vel+=Vector3.new(0,spd,0) end
        if UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) then vel+=Vector3.new(0,-spd,0) end

        -- Botões mobile
        if flyTouch.f then vel+=cam.CFrame.LookVector*spd end
        if flyTouch.b then vel-=cam.CFrame.LookVector*spd end
        if flyTouch.l then vel-=cam.CFrame.RightVector*spd end
        if flyTouch.r then vel+=cam.CFrame.RightVector*spd end
        if flyTouch.u then vel+=Vector3.new(0,spd,0) end
        if flyTouch.d then vel+=Vector3.new(0,-spd,0) end

        flyBV.Velocity=vel
        flyBG.CFrame=CFrame.new(r.Position,r.Position+cam.CFrame.LookVector)
    end)
end

flyClickArea.MouseButton1Click:Connect(function()
    if flyActive then stopFly() else startFly() end
end)
flyClickArea.Activated:Connect(function()
    if flyActive then stopFly() else startFly() end
end)

player.CharacterAdded:Connect(function()
    if flyActive then stopFly() task.wait(1) startFly() end
end)

-- ── SLIDERS ──────────────────────────────────
local function mkSlider(p, lo, ico, labelTxt, col, minV, maxV, defV, onChange)
    local card = Instance.new("Frame", p)
    card.Size             = UDim2.new(1, 0, 0, 54)
    card.BackgroundColor3 = C.ITEM
    card.BorderSizePixel  = 0
    card.LayoutOrder      = lo
    corner(card, 6)
    stroke(card, C.BORDER)

    local icoL = Instance.new("TextLabel", card)
    icoL.Text = ico
    icoL.Size = UDim2.new(0, 20, 0, 22)
    icoL.Position = UDim2.new(0, 6, 0, 3)
    icoL.BackgroundTransparency = 1
    icoL.TextColor3 = col
    icoL.TextSize   = 11
    icoL.Font       = Enum.Font.GothamBold

    local lblL = Instance.new("TextLabel", card)
    lblL.Text = labelTxt
    lblL.Size = UDim2.new(1, -76, 0, 22)
    lblL.Position = UDim2.new(0, 26, 0, 3)
    lblL.BackgroundTransparency = 1
    lblL.TextColor3 = C.TEXT
    lblL.TextSize   = 10
    lblL.Font       = Enum.Font.GothamBold
    lblL.TextXAlignment = Enum.TextXAlignment.Left

    local inputBox = Instance.new("TextBox", card)
    inputBox.Size             = UDim2.new(0, 40, 0, 20)
    inputBox.Position         = UDim2.new(1, -46, 0, 4)
    inputBox.BackgroundColor3 = C.BG
    inputBox.BorderSizePixel  = 0
    inputBox.TextColor3       = col
    inputBox.TextSize         = 11
    inputBox.Font             = Enum.Font.GothamBold
    inputBox.Text             = tostring(defV)
    inputBox.ClearTextOnFocus = false
    corner(inputBox, 4)
    stroke(inputBox, C.BORDER)

    local track = Instance.new("Frame", card)
    track.Size             = UDim2.new(1, -12, 0, 6)
    track.Position         = UDim2.new(0, 6, 0, 34)
    track.BackgroundColor3 = C.BORDER
    track.BorderSizePixel  = 0
    corner(track, 4)

    local fill = Instance.new("Frame", track)
    fill.Size             = UDim2.new((defV-minV)/(maxV-minV), 0, 1, 0)
    fill.BackgroundColor3 = col
    fill.BorderSizePixel  = 0
    corner(fill, 4)

    local knob = Instance.new("Frame", track)
    knob.Size             = UDim2.new(0, 14, 0, 14)
    knob.AnchorPoint      = Vector2.new(0.5, 0.5)
    knob.Position         = UDim2.new((defV-minV)/(maxV-minV), 0, 0.5, 0)
    knob.BackgroundColor3 = Color3.new(1, 1, 1)
    knob.BorderSizePixel  = 0
    corner(knob, 50)

    local curVal = defV

    local function applyVal(v)
        v = math.clamp(math.floor(v + 0.5), minV, maxV)
        curVal = v
        local pct = (v - minV) / (maxV - minV)
        fill.Size     = UDim2.new(pct, 0, 1, 0)
        knob.Position = UDim2.new(pct, 0, 0.5, 0)
        inputBox.Text = tostring(v)
        onChange(v)
    end

    inputBox.FocusLost:Connect(function()
        local n = tonumber(inputBox.Text)
        if n then applyVal(n) else inputBox.Text = tostring(curVal) end
    end)

    local function pctFromX(absX)
        local tw2 = track.AbsoluteSize.X
        if tw2 == 0 then return 0 end
        return math.clamp((absX - track.AbsolutePosition.X) / tw2, 0, 1)
    end

    local sliderDrag = false

    track.InputBegan:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1
        or i.UserInputType == Enum.UserInputType.Touch then
            sliderDrag = true
            applyVal(minV + pctFromX(i.Position.X) * (maxV - minV))
        end
    end)
    knob.InputBegan:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1
        or i.UserInputType == Enum.UserInputType.Touch then
            sliderDrag = true
        end
    end)

    -- Movimento (mouse via UIS, touch via track.InputChanged)
    UserInputService.InputChanged:Connect(function(i)
        if sliderDrag and i.UserInputType == Enum.UserInputType.MouseMovement then
            applyVal(minV + pctFromX(i.Position.X) * (maxV - minV))
        end
    end)
    track.InputChanged:Connect(function(i)
        if sliderDrag and i.UserInputType == Enum.UserInputType.Touch then
            applyVal(minV + pctFromX(i.Position.X) * (maxV - minV))
        end
    end)

    UserInputService.InputEnded:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1
        or i.UserInputType == Enum.UserInputType.Touch then
            sliderDrag = false
        end
    end)
end

mkSlider(playerCard, 2, "🏃", "WalkSpeed", C.ACCENT,  1, 200,  16, function(v)
    local hum = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if hum then hum.WalkSpeed = v end
end)

mkSlider(playerCard, 3, "⬆",  "JumpPower", C.ACCENT2, 1, 300,  50, function(v)
    local hum = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if hum then hum.JumpPower = v end
end)

-- ══════════════════════════════════════════════
-- FECHAR / MINIMIZAR
-- ══════════════════════════════════════════════
local reopenBtn = Instance.new("TextButton", sg)
reopenBtn.Size             = UDim2.new(0, 38, 0, 38)
reopenBtn.Position         = UDim2.new(0, 10, 0, 40)
reopenBtn.BackgroundColor3 = C.ACCENT
reopenBtn.Text             = "✦"
reopenBtn.TextColor3       = Color3.new(1, 1, 1)
reopenBtn.TextSize         = 16
reopenBtn.Font             = Enum.Font.GothamBold
reopenBtn.BorderSizePixel  = 0
reopenBtn.AutoButtonColor  = false
reopenBtn.Visible          = false
corner(reopenBtn, 9)
stroke(reopenBtn, C.BORDER)

local minimized = false

minimizeBtn.MouseButton1Click:Connect(function()
    minimized = not minimized
    if minimized then
        scroll.Visible = false
        tw(win, {Size=UDim2.new(0, WIN_W, 0, TOPBAR_H)}, 0.18, Enum.EasingStyle.Back)
        minimizeBtn.Text = "+"
    else
        scroll.Visible = true
        tw(win, {Size=UDim2.new(0, WIN_W, 0, WIN_H)}, 0.22, Enum.EasingStyle.Back)
        minimizeBtn.Text = "−"
    end
end)

closeBtn.MouseButton1Click:Connect(function()
    tw(win, {Size=UDim2.new(0, WIN_W, 0, 0)}, 0.18)
    task.wait(0.2)
    win.Visible      = false
    reopenBtn.Visible = true
end)

reopenBtn.MouseButton1Click:Connect(function()
    win.Visible      = true
    win.Size         = UDim2.new(0, WIN_W, 0, 0)
    reopenBtn.Visible = false
    minimized         = false
    scroll.Visible    = true
    minimizeBtn.Text  = "−"
    tw(win, {Size=UDim2.new(0, WIN_W, 0, WIN_H)}, 0.22, Enum.EasingStyle.Back)
end)

-- ══════════════════════════════════════════════
-- ANIMAÇÃO DE ENTRADA
-- ══════════════════════════════════════════════
win.Size = UDim2.new(0, WIN_W, 0, 0)
tw(win, {Size=UDim2.new(0, WIN_W, 0, WIN_H)}, 0.38, Enum.EasingStyle.Back)

print("[BrainrotHub v5.0] Carregado!")
