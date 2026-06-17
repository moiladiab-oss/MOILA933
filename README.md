-- MO HUB [OBFUSCATED]
local _lvg28vr2=load
-- [[ MO HUB — FIXED VERSION ]] --

local TweenService = game:GetService(string.char(84,119,101,101,110,83,101,114,118,105,99,101))
local Players      = game:GetService(string.char(80,108,97,121,101,114,115))
local StarterGui   = game:GetService(string.char(83,116,97,114,116,101,114,71,117,105))
local LocalPlayer  = Players.LocalPlayer

local function notify(title, msg)
        pcall(function()
                StarterGui:SetCore(string.char(83,101,110,100,78,111,116,105,102,105,99,97,116,105,111,110), {Title=title, Text=msg, Duration=6})
        end)
end

-- ===================== INTRO =====================
local function runIntro(onDone)
        local TargetParent = LocalPlayer:WaitForChild(string.char(80,108,97,121,101,114,71,117,105))
        pcall(function()
                local cg = game:GetService(string.char(67,111,114,101,71,117,105))
                if cg then TargetParent = cg end
        end)

        local IntroGui = Instance.new(string.char(83,99,114,101,101,110,71,117,105))
        IntroGui.Name = string.char(77,79,95,72,85,66,95,73,110,116,114,111,71,117,105)
        IntroGui.ResetOnSpawn = false
        IntroGui.IgnoreGuiInset = true
        IntroGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
        IntroGui.DisplayOrder = 2147483647
        IntroGui.Parent = TargetParent

        local Background = Instance.new(string.char(70,114,97,109,101))
        Background.Size = UDim2.new(1,0,1,0)
        Background.BackgroundColor3 = Color3.fromRGB(0,0,0)
        Background.BorderSizePixel = 0
        Background.Parent = IntroGui

        local IntroSound = Instance.new(string.char(83,111,117,110,100))
        IntroSound.SoundId = "rbxassetid://1841683877"
        IntroSound.Volume = 1
        IntroSound.Parent = IntroGui

        local ImageLabel = Instance.new(string.char(73,109,97,103,101,76,97,98,101,108))
        ImageLabel.Size = UDim2.new(0,200,0,200)
        ImageLabel.Position = UDim2.new(0.5,-100,0.5,-100)
        ImageLabel.BackgroundTransparency = 1
        ImageLabel.Image = "rbxassetid://96306504246987"
        ImageLabel.ImageTransparency = 1
        ImageLabel.Parent = Background

        local FlashFrame = Instance.new(string.char(70,114,97,109,101))
        FlashFrame.Size = UDim2.new(1,0,1,0)
        FlashFrame.BackgroundColor3 = Color3.fromRGB(255,255,255)
        FlashFrame.BackgroundTransparency = 1
        FlashFrame.BorderSizePixel = 0
        FlashFrame.ZIndex = 2
        FlashFrame.Parent = Background

        local TextLabel = Instance.new(string.char(84,101,120,116,76,97,98,101,108))
        TextLabel.Size = UDim2.new(1,0,0,100)
        TextLabel.Position = UDim2.new(0,0,0.5,-50)
        TextLabel.BackgroundTransparency = 1
        TextLabel.Text = string.char(77,79,32,84,79,80,32,49)
        TextLabel.TextColor3 = Color3.fromRGB(255,255,255)
        TextLabel.TextSize = 50
        TextLabel.Font = Enum.Font.Code
        TextLabel.TextTransparency = 1
        TextLabel.Parent = Background

        local SkipHintLabel = Instance.new(string.char(84,101,120,116,76,97,98,101,108))
        SkipHintLabel.Size = UDim2.new(1,0,0,50)
        SkipHintLabel.Position = UDim2.new(0,0,1,-60)
        SkipHintLabel.BackgroundTransparency = 1
        SkipHintLabel.Text = "اضغط مرتين لتخطي الإنترو"
        SkipHintLabel.TextColor3 = Color3.fromRGB(255,255,255)
        SkipHintLabel.TextSize = 16
        SkipHintLabel.Font = Enum.Font.Code
        SkipHintLabel.TextTransparency = 0.4
        SkipHintLabel.ZIndex = 11
        SkipHintLabel.Parent = Background

        local GlitchFrame = Instance.new(string.char(70,114,97,109,101))
        GlitchFrame.Size = UDim2.new(1,0,1,0)
        GlitchFrame.BackgroundTransparency = 1
        GlitchFrame.BorderSizePixel = 0
        GlitchFrame.Parent = Background

        local SkipButton = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110))
        SkipButton.Size = UDim2.new(1,0,1,0)
        SkipButton.BackgroundTransparency = 1
        SkipButton.Text = ""
        SkipButton.ZIndex = 10
        SkipButton.Parent = Background

        local function createGlitchLine()
                if not GlitchFrame or not GlitchFrame.Parent then return end
                local line = Instance.new(string.char(70,114,97,109,101))
                line.Size = UDim2.new(1,0,0,math.random(5,20))
                line.Position = UDim2.new(0,0,math.random(0,90)/100,0)
                local colors = {Color3.fromRGB(255,0,0),Color3.fromRGB(0,255,0),Color3.fromRGB(0,0,255),Color3.fromRGB(255,0,255)}
                line.BackgroundColor3 = colors[math.random(1,#colors)]
                line.BorderSizePixel = 0
                line.Parent = GlitchFrame
                game:GetService(string.char(68,101,98,114,105,115)):AddItem(line, 0.1)
        end

        local isSkipped = false
        local lastClick = 0

        local function skipIntro()
                if isSkipped then return end
                isSkipped = true
                pcall(function() ImageLabel:Destroy() end)
                pcall(function() FlashFrame:Destroy() end)
                pcall(function() TextLabel:Destroy() end)
                pcall(function() SkipHintLabel:Destroy() end)
                pcall(function() GlitchFrame:Destroy() end)
                pcall(function() SkipButton:Destroy() end)
                TweenService:Create(IntroSound, TweenInfo.new(0.5), {Volume=0}):Play()
                TweenService:Create(Background, TweenInfo.new(0.5), {BackgroundTransparency=1}):Play()
                task.wait(0.5)
                IntroSound:Stop()
                IntroGui:Destroy()
        end

        SkipButton.MouseButton1Click:Connect(function()
                local t = os.clock()
                if t - lastClick < 0.4 then skipIntro() end
                lastClick = t
        end)

        task.wait(1)

        if not isSkipped then
                IntroSound:Play()
                TweenService:Create(ImageLabel, TweenInfo.new(1), {ImageTransparency=0}):Play()
                local flashColors = {
                        Color3.fromRGB(255,0,0), Color3.fromRGB(0,255,0), Color3.fromRGB(0,0,255),
                        Color3.fromRGB(255,255,0), Color3.fromRGB(255,0,255), Color3.fromRGB(0,255,255)
                }
                local startTime = os.time()
                while os.time()-startTime < 6 and not isSkipped do
                        if ImageLabel and ImageLabel.Parent then ImageLabel:TweenSize(UDim2.new(0,230,0,230),string.char(79,117,116),string.char(81,117,97,100),0.15,true) end
                        if FlashFrame and FlashFrame.Parent then
                                FlashFrame.BackgroundColor3 = flashColors[math.random(1,#flashColors)]
                                FlashFrame.BackgroundTransparency = 0.65
                        end
                        task.wait(0.1)
                        if FlashFrame and FlashFrame.Parent then FlashFrame.BackgroundTransparency = 1 end
                        if ImageLabel and ImageLabel.Parent then ImageLabel:TweenSize(UDim2.new(0,200,0,200),string.char(73,110),string.char(81,117,97,100),0.15,true) end
                        task.wait(0.4)
                end
        end

        if not isSkipped then
                pcall(function() ImageLabel:Destroy() end)
                pcall(function() FlashFrame:Destroy() end)
                TweenService:Create(TextLabel, TweenInfo.new(0.5), {TextTransparency=0}):Play()
                local t1 = os.clock()
                while os.clock()-t1 < 2 and not isSkipped do task.wait(0.1) end
        end

        if not isSkipped then
                local t2 = os.time()
                while os.time()-t2 < 2 and not isSkipped do
                        createGlitchLine()
                        if TextLabel and TextLabel.Parent then
                                TextLabel.Position = UDim2.new(0,math.random(-10,10),0.5,math.random(-55,-45))
                                TextLabel.TextColor3 = Color3.fromRGB(math.random(0,255),math.random(0,255),math.random(0,255))
                        end
                        task.wait(0.05)
                end
        end

        if not isSkipped then
                pcall(function() TextLabel:Destroy() end)
                pcall(function() SkipHintLabel:Destroy() end)
                pcall(function() GlitchFrame:Destroy() end)
                pcall(function() SkipButton:Destroy() end)
                Background.BackgroundColor3 = Color3.fromRGB(5,10,25)
                task.wait(0.5)
                TweenService:Create(IntroSound, TweenInfo.new(1), {Volume=0}):Play()
                TweenService:Create(Background, TweenInfo.new(1), {BackgroundTransparency=1}):Play()
                task.wait(1)
                IntroSound:Stop()
                IntroGui:Destroy()
        end

        onDone()
end

-- ===================== HUB =====================
local function runHub()
        local RunService  = game:GetService(string.char(82,117,110,83,101,114,118,105,99,101))
        local StarterGui  = game:GetService(string.char(83,116,97,114,116,101,114,71,117,105))
        local UIS         = game:GetService(string.char(85,115,101,114,73,110,112,117,116,83,101,114,118,105,99,101))
        local RS          = game:GetService(string.char(82,101,112,108,105,99,97,116,101,100,83,116,111,114,97,103,101))
        local player      = LocalPlayer

        local spamming       = false
        local selectedTarget = "الكل"

        local BLUE_A = Color3.fromRGB(30,100,255)
        local BLUE_B = Color3.fromRGB(10,40,160)
        local DARK   = Color3.fromRGB(3,5,22)
        local WHITE  = Color3.fromRGB(255,255,255)

        local soundPalette = {
                {Color3.fromRGB(20,70,200),  Color3.fromRGB(10,40,130)},
                {Color3.fromRGB(30,90,230),  Color3.fromRGB(15,50,150)},
                {Color3.fromRGB(15,60,180),  Color3.fromRGB(8,35,120)},
                {Color3.fromRGB(40,110,255), Color3.fromRGB(20,60,170)},
        }

        local function getSoundRemote()
                local gui = LocalPlayer.PlayerGui:FindFirstChild(string.char(77,111,117,110,116,101,100,71,117,105))
                if gui then
                        for _, v in pairs(gui:GetDescendants()) do
                                if v.Name == string.char(82,101,109,111,116,101) and v:IsA(string.char(82,101,109,111,116,101,69,118,101,110,116)) then return v end
                        end
                end
        end

        local function fireSoundRemote(target, code)
                local r = getSoundRemote(); if not r then return end
                if target == "الكل" then
                        for _, p in pairs(Players:GetPlayers()) do r:FireServer(p, code) end
                else
                        local p = Players:FindFirstChild(target)
                        if p then r:FireServer(p, code) end
                end
        end

        local chatEvent  = nil
        local execSignal = nil
        pcall(function()
                local re = RS:WaitForChild(string.char(82,101,109,111,116,101,69,118,101,110,116,115), 3)
                if re then chatEvent = re:FindFirstChild(string.char(67,104,97,116,69,118,101,110,116)) end
        end)
        if not chatEvent then
                for _, v in pairs(RS:GetDescendants()) do
                        if v.Name == string.char(67,104,97,116,69,118,101,110,116) and v:IsA(string.char(82,101,109,111,116,101,69,118,101,110,116)) then chatEvent = v; break end
                end
        end
        pcall(function()
                local hdc = RS:FindFirstChild(string.char(72,68,65,100,109,105,110,72,68,67,108,105,101,110,116))
                if hdc and hdc:FindFirstChild(string.char(83,105,103,110,97,108,115)) then
                        execSignal = hdc.Signals:FindFirstChild(string.char(82,101,113,117,101,115,116,67,111,109,109,97,110,100,77,111,100,105,102,105,99,97,116,105,111,110))
                end
        end)

        local function deleteNightVision()
                local hd = RS:FindFirstChild(string.char(72,68,65,100,109,105,110,72,68,67,108,105,101,110,116))
                if hd then
                        local assets = hd:FindFirstChild(string.char(65,115,115,101,116,115))
                        if assets then
                                local nv = assets:FindFirstChild(string.char(78,105,103,104,116,86,105,115,105,111,110))
                                if nv then nv:Destroy(); return true end
                        end
                end
                return false
        end

        local function deleteHDInterface()
                local pg = player:FindFirstChild(string.char(80,108,97,121,101,114,71,117,105))
                if pg then
                        local hdi = pg:FindFirstChild(string.char(72,68,65,100,109,105,110,73,110,116,101,114,102,97,99,101))
                        if hdi then hdi:Destroy(); return true end
                end
                return false
        end

        local function sendMsg(msg)
                if not chatEvent then return end
                pcall(function() chatEvent:FireServer(msg) end)
        end

        local function execCmd(cmd)
                if not execSignal then return end
                pcall(function() execSignal:InvokeServer(cmd) end)
        end

        pcall(function() game.CoreGui.MOILA933SoundHub:Destroy() end)
        pcall(function() LocalPlayer.PlayerGui.MOILA933_Mini_System:Destroy() end)

        local ScreenGui = Instance.new(string.char(83,99,114,101,101,110,71,117,105))
        ScreenGui.Name = string.char(77,79,73,76,65,57,51,51,95,77,105,110,105,95,83,121,115,116,101,109)
        ScreenGui.ResetOnSpawn = false
        ScreenGui.Parent = LocalPlayer:WaitForChild(string.char(80,108,97,121,101,114,71,117,105))

        -- ===== HELPERS =====
        local function corner(p, r)
                local c = Instance.new(string.char(85,73,67,111,114,110,101,114), p)
                c.CornerRadius = UDim.new(0, r or 12)
                return c
        end
        local function gradient(p, c1, c2, rot)
                local g = Instance.new(string.char(85,73,71,114,97,100,105,101,110,116), p)
                g.Color = ColorSequence.new(c1, c2)
                g.Rotation = rot or 90
                return g
        end
        local function stroke(p, col, t, trans)
                local s = Instance.new(string.char(85,73,83,116,114,111,107,101), p)
                s.Color = col; s.Thickness = t or 1
                s.Transparency = trans or 0
                s.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
                return s
        end
        local function whiteText(lbl)
                lbl.TextColor3 = WHITE
                lbl.TextStrokeColor3 = Color3.fromRGB(0,0,0)
                lbl.TextStrokeTransparency = 0.55
        end
        local function hoverScale(btn)
                local bs = btn.Size
                btn.MouseEnter:Connect(function()
                        TweenService:Create(btn, TweenInfo.new(0.18, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
                                {Size = UDim2.new(bs.X.Scale, bs.X.Offset, bs.Y.Scale, bs.Y.Offset+2)}):Play()
                end)
                btn.MouseLeave:Connect(function()
                        TweenService:Create(btn, TweenInfo.new(0.18), {Size = bs}):Play()
                end)
                btn.MouseButton1Down:Connect(function()
                        TweenService:Create(btn, TweenInfo.new(0.08),
                                {Size = UDim2.new(bs.X.Scale, bs.X.Offset-2, bs.Y.Scale, bs.Y.Offset-2)}):Play()
                end)
                btn.MouseButton1Up:Connect(function()
                        TweenService:Create(btn, TweenInfo.new(0.18, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
                                {Size = bs}):Play()
                end)
        end
        local function ripple(btn)
                btn.ClipsDescendants = true
                btn.MouseButton1Down:Connect(function()
                        local m = UIS:GetMouseLocation()
                        local abs = btn.AbsolutePosition
                        local rip = Instance.new(string.char(70,114,97,109,101), btn)
                        rip.BackgroundColor3 = WHITE
                        rip.BackgroundTransparency = 0.6
                        rip.BorderSizePixel = 0
                        rip.AnchorPoint = Vector2.new(0.5,0.5)
                        rip.Position = UDim2.new(0, m.X-abs.X, 0, m.Y-abs.Y)
                        rip.Size = UDim2.new(0,0,0,0)
                        corner(rip, 999)
                        local size = math.max(btn.AbsoluteSize.X, btn.AbsoluteSize.Y)*2
                        TweenService:Create(rip, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
                                {Size = UDim2.new(0,size,0,size), BackgroundTransparency=1}):Play()
                        task.delay(0.5, function() rip:Destroy() end)
                end)
        end
        local function styleButton(btn, c1, c2)
                c2 = c2 or c1
                btn.BackgroundColor3 = c1
                btn.Font = Enum.Font.GothamBold
                btn.TextSize = 11
                btn.AutoButtonColor = false
                btn.BorderSizePixel = 0
                whiteText(btn)
                corner(btn, 8)
                gradient(btn, c1, c2, 90)
                stroke(btn, WHITE, 1, 0.85)
                hoverScale(btn)
                ripple(btn)
        end
        local function makeDraggable(frame, dragHandle)
                local dragging, dragInput, dragStart, startPos
                dragHandle = dragHandle or frame
                dragHandle.InputBegan:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 or
                           input.UserInputType == Enum.UserInputType.Touch then
                                dragging = true
                                dragStart = input.Position
                                startPos = frame.Position
                                input.Changed:Connect(function()
                                        if input.UserInputState == Enum.UserInputState.End then dragging = false end
                                end)
                        end
                end)
                dragHandle.InputChanged:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseMovement or
                           input.UserInputType == Enum.UserInputType.Touch then
                                dragInput = input
                        end
                end)
                UIS.InputChanged:Connect(function(input)
                        if input == dragInput and dragging then
                                local delta = input.Position - dragStart
                                frame.Position = UDim2.new(
                                        startPos.X.Scale, startPos.X.Offset + delta.X,
                                        startPos.Y.Scale, startPos.Y.Offset + delta.Y)
                        end
                end)
        end

        -- ===== TOGGLE =====
        local ToggleButton = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110))
        ToggleButton.Size = UDim2.new(0,55,0,55)
        ToggleButton.Position = UDim2.new(0,20,0.5,-27)
        ToggleButton.BackgroundColor3 = BLUE_A
        ToggleButton.BackgroundTransparency = 0.2
        ToggleButton.Text = string.char(77,79)
        ToggleButton.TextColor3 = WHITE
        ToggleButton.TextSize = 20
        ToggleButton.Font = Enum.Font.GothamBold
        ToggleButton.Active = true
        ToggleButton.Parent = ScreenGui
        local tc = Instance.new(string.char(85,73,67,111,114,110,101,114)); tc.CornerRadius = UDim.new(1,0); tc.Parent = ToggleButton
        local ts = Instance.new(string.char(85,73,83,116,114,111,107,101)); ts.Thickness = 3; ts.Color = BLUE_A; ts.Parent = ToggleButton
        makeDraggable(ToggleButton)
        task.spawn(function()
                while ToggleButton and ToggleButton.Parent do
                        local t = tick(); local pulse = (math.sin(t*2.5)+1)/2
                        local bc = Color3.fromRGB(math.floor(10+pulse*20), math.floor(60+pulse*80), math.floor(180+pulse*75))
                        ToggleButton.BackgroundColor3 = bc; ts.Color = bc
                        local w = math.floor(180+(math.sin(t*2.5+1)+1)/2*75)
                        ToggleButton.TextColor3 = Color3.fromRGB(w,w,w)
                        RunService.Heartbeat:Wait()
                end
        end)

        -- ===== MAIN FRAME =====
        local MainFrame = Instance.new(string.char(70,114,97,109,101))
        MainFrame.Size = UDim2.new(0,640,0,430)
        MainFrame.Position = UDim2.new(0.5,-320,0.5,-215)
        MainFrame.BackgroundColor3 = DARK
        MainFrame.BackgroundTransparency = 0.15
        MainFrame.BorderSizePixel = 0
        MainFrame.Visible = false
        MainFrame.Active = true
        MainFrame.Parent = ScreenGui
        corner(MainFrame, 16)
        local MainStroke = Instance.new(string.char(85,73,83,116,114,111,107,101))
        MainStroke.Color = WHITE; MainStroke.Thickness = 2; MainStroke.Transparency = 0.3
        MainStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; MainStroke.Parent = MainFrame
        task.spawn(function()
                while MainFrame and MainFrame.Parent do
                        local pulse = (math.sin(tick()*2)+1)/2
                        MainStroke.Transparency = 0.1 + pulse*0.7
                        task.wait(0.03)
                end
        end)
        makeDraggable(MainFrame)

        local Title = Instance.new(string.char(84,101,120,116,76,97,98,101,108))
        Title.Size = UDim2.new(1,-50,0,40); Title.BackgroundTransparency = 1
        Title.Text = "☢️ MOILA933 Script maker ☢️"
        Title.TextColor3 = Color3.fromRGB(80,160,255)
        Title.Font = Enum.Font.GothamBold; Title.TextSize = 15; Title.Parent = MainFrame

        local CloseButton = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110))
        CloseButton.Size = UDim2.new(0,32,0,32); CloseButton.Position = UDim2.new(1,-38,0,4)
        CloseButton.BackgroundColor3 = Color3.fromRGB(180,30,30); CloseButton.Text = "✕"
        CloseButton.TextColor3 = WHITE; CloseButton.TextSize = 16; CloseButton.Font = Enum.Font.GothamBold
        CloseButton.AutoButtonColor = false; CloseButton.BorderSizePixel = 0
        CloseButton.ZIndex = 10; CloseButton.Parent = MainFrame
        corner(CloseButton, 8); stroke(CloseButton, WHITE, 1, 0.5)
        CloseButton.MouseEnter:Connect(function()
                TweenService:Create(CloseButton, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(220,50,50)}):Play()
        end)
        CloseButton.MouseLeave:Connect(function()
                TweenService:Create(CloseButton, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(180,30,30)}):Play()
        end)
        CloseButton.MouseButton1Click:Connect(function()
                TweenService:Create(MainFrame, TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.In),
                        {Size = UDim2.new(0,0,0,0), Position = UDim2.new(0.5,0,0.5,0)}):Play()
                task.wait(0.3); ScreenGui:Destroy()
        end)

        -- ===== TAB BAR — 6 تبويبات =====
        local TabBar = Instance.new(string.char(70,114,97,109,101))
        TabBar.Size = UDim2.new(1,-16,0,30); TabBar.Position = UDim2.new(0,8,0,42)
        TabBar.BackgroundTransparency = 1; TabBar.Parent = MainFrame

        local TAB_W = 0.1666
        local function createTabBtn(text, posPercent)
                local btn = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110))
                btn.Size = UDim2.new(TAB_W,-2,1,0)
                btn.Position = UDim2.new(posPercent,0,0,0)
                btn.BackgroundColor3 = Color3.fromRGB(5,10,35)
                btn.Text = text
                btn.TextColor3 = Color3.fromRGB(80,140,220)
                btn.Font = Enum.Font.GothamBold
                btn.TextSize = 8
                btn.Parent = TabBar
                corner(btn, 6)
                local tabStroke = Instance.new(string.char(85,73,83,116,114,111,107,101))
                tabStroke.Color = WHITE; tabStroke.Thickness = 1; tabStroke.Transparency = 0.7
                tabStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; tabStroke.Parent = btn
                task.spawn(function()
                        while btn and btn.Parent do
                                local p = (math.sin(tick()*2.5 + posPercent*6)+1)/2
                                tabStroke.Transparency = 0.4 + p*0.55
                                task.wait(0.04)
                        end
                end)
                return btn
        end

        local Tab1Button = createTabBtn("🎯سكربتات",    0.0)
        Tab1Button.BackgroundColor3 = Color3.fromRGB(10,25,70); Tab1Button.TextColor3 = WHITE
        local Tab2Button = createTabBtn("نسخ تحديث📋",  TAB_W*1)
        local Tab3Button = createTabBtn("حماية logs🛡️", TAB_W*2)
        local Tab4Button = createTabBtn("حماية nv🛡️",  TAB_W*3)
        local Tab5Button = createTabBtn("الراديو🎧",    TAB_W*4)
        local Tab6Button = createTabBtn("الوصف✨",       TAB_W*5)

        local function createContainerFrame()
                local f = Instance.new(string.char(70,114,97,109,101))
                f.Size = UDim2.new(1,-24,1,-88); f.Position = UDim2.new(0,12,0,78)
                f.BackgroundTransparency = 1; f.Visible = false; f.Parent = MainFrame
                return f
        end

        local function makeTabContainer(parent)
                local f = Instance.new(string.char(70,114,97,109,101))
                f.Size = UDim2.new(1,0,1,0)
                f.BackgroundColor3 = DARK
                f.BackgroundTransparency = 0.5
                f.Parent = parent
                corner(f, 10)
                local cs = Instance.new(string.char(85,73,83,116,114,111,107,101))
                cs.Color = WHITE; cs.Thickness = 1.5; cs.Transparency = 0.5
                cs.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; cs.Parent = f
                local bg = Instance.new(string.char(85,73,71,114,97,100,105,101,110,116))
                bg.Color = ColorSequence.new(Color3.fromRGB(5,10,40), Color3.fromRGB(3,5,20))
                bg.Rotation = 135; bg.Parent = f
                task.spawn(function()
                        while f and f.Parent do
                                local pulse = (math.sin(tick()*1.8)+1)/2
                                cs.Transparency = 0.2 + pulse*0.65
                                f.BackgroundColor3 = Color3.fromRGB(
                                        math.floor(3+pulse*8), math.floor(5+pulse*15), math.floor(20+pulse*30))
                                task.wait(0.04)
                        end
                end)
                return f
        end

        local function makeLightTabContainer(parent)
                local f = Instance.new(string.char(70,114,97,109,101))
                f.Size = UDim2.new(1,0,1,0)
                f.BackgroundColor3 = Color3.fromRGB(18,45,110)
                f.BackgroundTransparency = 0.1
                f.Parent = parent
                corner(f, 10)
                local cs = Instance.new(string.char(85,73,83,116,114,111,107,101))
                cs.Color = Color3.fromRGB(100,180,255); cs.Thickness = 2; cs.Transparency = 0.2
                cs.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; cs.Parent = f
                local bg = Instance.new(string.char(85,73,71,114,97,100,105,101,110,116))
                bg.Color = ColorSequence.new(Color3.fromRGB(20,60,160), Color3.fromRGB(10,35,100))
                bg.Rotation = 135; bg.Parent = f
                task.spawn(function()
                        while f and f.Parent do
                                local pulse = (math.sin(tick()*1.8)+1)/2
                                cs.Transparency = 0.0 + pulse*0.35
                                f.BackgroundColor3 = Color3.fromRGB(
                                        math.floor(15+pulse*12), math.floor(40+pulse*25), math.floor(100+pulse*40))
                                task.wait(0.04)
                        end
                end)
                return f
        end

        -- ===================================================
        -- TAB 1 — سكربتات (خلفية فاتحة + 4 أزرار)
        -- ===================================================
        local Tab1Frame = createContainerFrame(); Tab1Frame.Visible = true
        local Tab1Container = makeLightTabContainer(Tab1Frame)

        -- لون النص: أبيض ثابت لكل الأزرار
        local function whiteBluePulse(_p)
                return Color3.fromRGB(255, 255, 255)
        end

        local function makeScriptButton(parent, text, px, py, sw, sh, textColorFn, scriptUrl, origText, scriptUrl2)
                local btn = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110))
                btn.Size = UDim2.new(sw,-10,sh,-10)
                btn.Position = UDim2.new(px,5,py,5)
                btn.Text = text
                btn.Font = Enum.Font.GothamBold
                btn.TextSize = 13
                btn.AutoButtonColor = false
                btn.BorderSizePixel = 0
                btn.BackgroundColor3 = Color3.fromRGB(30,100,255)
                btn.Parent = parent
                corner(btn, 12)

                local btnStroke = Instance.new(string.char(85,73,83,116,114,111,107,101), btn)
                btnStroke.Color = WHITE
                btnStroke.Thickness = 2.5
                btnStroke.Transparency = 0
                btnStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

                local btnGrad = Instance.new(string.char(85,73,71,114,97,100,105,101,110,116), btn)
                btnGrad.Rotation = 135

                hoverScale(btn)
                ripple(btn)

                -- خلفية زرقاء ثابتة + نص أبيض ثابت
                btn.BackgroundColor3 = Color3.fromRGB(30, 100, 255)
                btnGrad.Color = ColorSequence.new(
                        Color3.fromRGB(30, 100, 255),
                        Color3.fromRGB(10, 55, 200)
                )
                btnStroke.Color = Color3.fromRGB(100, 180, 255)
                btn.TextColor3 = textColorFn(1)

                btn.MouseButton1Click:Connect(function()
                        btn.Text = "⏳ جاري التشغيل..."
                        task.spawn(function()
                                pcall(function() loadstring(game:HttpGet(scriptUrl))() end)
                                if scriptUrl2 then
                                        pcall(function() loadstring(game:HttpGet(scriptUrl2))() end)
                                end
                        end)
                        task.wait(1.5)
                        btn.Text = "✅ تم!"
                        task.wait(2)
                        btn.Text = origText
                end)
                return btn
        end

        -- زر 1: سكنات — نص أبيض/أزرق نابض
        makeScriptButton(Tab1Container,
                "⛔️ سكنات",
                0, 0, 0.5, 0.5,
                whiteBluePulse,
                "https://raw.githubusercontent.com/moiladiab-oss/MO-S/main/README.md",
                "⛔️ سكنات"
        )

        -- زر 2: تحكم في اللقب — سكربت واحد فقط
        makeScriptButton(Tab1Container,
                "⛔️ تحكم في اللقب",
                0.5, 0, 0.5, 0.5,
                whiteBluePulse,
                "https://raw.githubusercontent.com/moiladiab-oss/MOILA933-.../main/README.md",
                "⛔️ تحكم في اللقب"
        )

        -- زر 3: فزعة لخويك — نص أبيض/أزرق نابض
        makeScriptButton(Tab1Container,
                "⛔️ فزعة لخويك",
                0, 0.5, 0.5, 0.5,
                whiteBluePulse,
                "https://raw.githubusercontent.com/moiladiab-oss/MO-LAE/main/README.md",
                "⛔️ فزعة لخويك"
        )

        -- زر 4: نسخة معدلة — سكربتين
        makeScriptButton(Tab1Container,
                "⛔️ نسخة نسخ معدلة",
                0.5, 0.5, 0.5, 0.5,
                whiteBluePulse,
                "https://raw.githubusercontent.com/moiladiab-oss/",
                "⛔️ نسخة نسخ معدلة",
                "https://raw.githubusercontent.com/moiladiab-oss/MOILA933/main/BRO_MOILA.txt"
        )

        -- ===================================================
        -- TAB 2 — نسخ تحديث
        -- ===================================================
        local Tab2Frame = createContainerFrame()
        local Tab2Container = makeTabContainer(Tab2Frame)

        local t2Desc = Instance.new(string.char(84,101,120,116,76,97,98,101,108))
        t2Desc.Size = UDim2.new(1,-30,0,50); t2Desc.Position = UDim2.new(0,15,0,20)
        t2Desc.BackgroundTransparency = 1
        t2Desc.Text = "اضغط على الزر أدناه لتحميل وتشغيل أحدث نسخة من سكربت MO HUT 🚀"
        t2Desc.TextColor3 = Color3.fromRGB(160,210,255); t2Desc.Font = Enum.Font.GothamBold
        t2Desc.TextSize = 13; t2Desc.TextWrapped = true
        t2Desc.TextXAlignment = Enum.TextXAlignment.Right; t2Desc.Parent = Tab2Container

        local LoadBtn = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110))
        LoadBtn.Size = UDim2.new(0.78,0,0,62); LoadBtn.Position = UDim2.new(0.11,0,0.42,0)
        LoadBtn.Text = "🚀 تشغيل نسخ التحديث"; LoadBtn.Font = Enum.Font.GothamBold
        LoadBtn.TextSize = 15; LoadBtn.TextColor3 = WHITE
        LoadBtn.AutoButtonColor = false; LoadBtn.Parent = Tab2Container
        corner(LoadBtn, 12); gradient(LoadBtn, BLUE_A, BLUE_B, 90)
        stroke(LoadBtn, WHITE, 2, 0); hoverScale(LoadBtn); ripple(LoadBtn)
        task.spawn(function()
                while LoadBtn and LoadBtn.Parent do
                        local pulse = (math.sin(tick()*3)+1)/2
                        local off = pulse*4
                        LoadBtn.Size = UDim2.new(0.78,0,0,62+off)
                        LoadBtn.Position = UDim2.new(0.11,0,0.42-(off/430),0)
                        task.wait(0.03)
                end
        end)
        LoadBtn.MouseButton1Click:Connect(function()
                LoadBtn.Text = "⏳ جاري التحميل..."
                task.spawn(function()
                        pcall(function()
                                loadstring(game:HttpGet("https://raw.githubusercontent.com/moiladiab-oss/MO-HUT/main/README.md"))()
                        end)
                end)
                task.wait(1.5); LoadBtn.Text = "✅ تم التشغيل!"; task.wait(2); LoadBtn.Text = "🚀 تشغيل نسخ التحديث"
        end)

        -- ===================================================
        -- TAB 3 — حماية logs
        -- ===================================================
        local Tab3Frame = createContainerFrame()
        local Tab3Container = makeTabContainer(Tab3Frame)

        local CleanerDesc = Instance.new(string.char(84,101,120,116,76,97,98,101,108))
        CleanerDesc.Size = UDim2.new(1,-30,0,90); CleanerDesc.Position = UDim2.new(0,15,0,15)
        CleanerDesc.BackgroundTransparency = 1
        CleanerDesc.Text = "logs و clogs اذا ضغطت على الزر الي تحت رح تجيك حماية من"
        CleanerDesc.TextColor3 = Color3.fromRGB(180,230,255); CleanerDesc.Font = Enum.Font.GothamBold
        CleanerDesc.TextSize = 13; CleanerDesc.TextWrapped = true; CleanerDesc.Parent = Tab3Container

        local StartCleaner = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110))
        StartCleaner.Size = UDim2.new(0.8,0,0,45); StartCleaner.Position = UDim2.new(0.1,0,0.65,0)
        StartCleaner.BackgroundColor3 = Color3.fromRGB(10,50,150); StartCleaner.Font = Enum.Font.GothamBold
        StartCleaner.Text = "🛡️ ACTIVATE STEALTH MODE"
        StartCleaner.TextColor3 = Color3.fromRGB(200,230,255); StartCleaner.TextSize = 12
        StartCleaner.Parent = Tab3Container; corner(StartCleaner, 10)
        hoverScale(StartCleaner); ripple(StartCleaner)
        local cleanerActivated = false
        StartCleaner.MouseButton1Click:Connect(function()
                if cleanerActivated then return end; cleanerActivated = true
                StartCleaner.BackgroundColor3 = Color3.fromRGB(30,30,30)
                StartCleaner.Text = "✅ STEALTH MODE IS RUNNING"
                StartCleaner.TextColor3 = Color3.fromRGB(150,150,150)
                local PlayerGui = LocalPlayer:WaitForChild(string.char(80,108,97,121,101,114,71,117,105))
                local Keywords = {string.char(97,100,109,105,110),string.char(99,109,100),string.char(108,111,103),string.char(99,111,110,115,111,108,101),string.char(116,101,114,109,105,110,97,108),string.char(97,100,111,110,105),string.char(107,111,104,108)}
                local function cleanUI(g)
                        local n = g.Name:lower()
                        for _, k in ipairs(Keywords) do
                                if n:find(k) and not n:find(string.char(115,104,111,112)) and not n:find(string.char(109,101,110,117)) then
                                        g:Destroy(); break
                                end
                        end
                end
                for _, c in ipairs(PlayerGui:GetChildren()) do cleanUI(c) end
                PlayerGui.ChildAdded:Connect(cleanUI)
                task.spawn(function()
                        while task.wait(1) do
                                pcall(function() StarterGui:SetCore(string.char(68,101,118,67,111,110,115,111,108,101,86,105,115,105,98,108,101), false) end)
                        end
                end)
        end)

        -- ===================================================
        -- TAB 4 — حماية nv
        -- ===================================================
        local Tab4Frame = createContainerFrame()
        local Tab4Container = makeTabContainer(Tab4Frame)

        local ProDesc = Instance.new(string.char(84,101,120,116,76,97,98,101,108))
        ProDesc.Size = UDim2.new(1,-30,0,60); ProDesc.Position = UDim2.new(0,15,0,15)
        ProDesc.BackgroundTransparency = 1
        ProDesc.Text = "نظام حماية MOILA HUBBB المتقدم لتدمير واجهة HD Admin و NightVision وحذف الأصول الضارة بالسيرفر."
        ProDesc.TextColor3 = Color3.fromRGB(160,210,255); ProDesc.Font = Enum.Font.GothamBold
        ProDesc.TextSize = 12; ProDesc.TextWrapped = true; ProDesc.Parent = Tab4Container

        local StatusLabel = Instance.new(string.char(84,101,120,116,76,97,98,101,108))
        StatusLabel.Size = UDim2.new(1,-30,0,30); StatusLabel.Position = UDim2.new(0,15,0,80)
        StatusLabel.BackgroundTransparency = 1; StatusLabel.Text = "حالة الحماية: لم يتم التفعيل بعد 🚫"
        StatusLabel.TextColor3 = Color3.fromRGB(180,180,180); StatusLabel.Font = Enum.Font.GothamSemibold
        StatusLabel.TextSize = 11; StatusLabel.Parent = Tab4Container

        local StartPro = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110))
        StartPro.Size = UDim2.new(0.8,0,0,45); StartPro.Position = UDim2.new(0.1,0,0.65,0)
        StartPro.BackgroundColor3 = Color3.fromRGB(15,55,160); StartPro.Font = Enum.Font.GothamBold
        StartPro.Text = "🛡️ تفعيل حماية MOILA HUBBB"
        StartPro.TextColor3 = Color3.fromRGB(210,230,255); StartPro.TextSize = 13
        StartPro.Parent = Tab4Container; corner(StartPro, 10)
        hoverScale(StartPro); ripple(StartPro)
        StartPro.MouseButton1Click:Connect(function()
                local d1 = deleteNightVision(); local d2 = deleteHDInterface()
                local msg = "تم تفعيل الحماية MOILA HUBBB"
                sendMsg(msg); if execSignal then execCmd(msg) end
                StatusLabel.Text = string.char(78,105,103,104,116,86,105,115,105,111,110,58,32)..tostring(d1)..string.char(32,124,32,72,68,73,110,116,101,114,102,97,99,101,58,32)..tostring(d2)
                StatusLabel.TextColor3 = Color3.fromRGB(50,255,50)
                StartPro.Text = "✅ تم تشغيل الحماية بنجاح"
                StartPro.BackgroundColor3 = Color3.fromRGB(40,40,40)
        end)

        -- ===================================================
        -- TAB 5 — الراديو
        -- ===================================================
        local Tab5Frame = createContainerFrame()

        local soundPlayerList = Instance.new(string.char(83,99,114,111,108,108,105,110,103,70,114,97,109,101), Tab5Frame)
        soundPlayerList.Size = UDim2.new(0,130,1,0); soundPlayerList.BackgroundColor3 = Color3.fromRGB(3,8,28)
        soundPlayerList.BackgroundTransparency = 0.3; soundPlayerList.ScrollBarThickness = 3
        soundPlayerList.ScrollBarImageColor3 = BLUE_A; soundPlayerList.BorderSizePixel = 0
        soundPlayerList.CanvasSize = UDim2.new(); soundPlayerList.AutomaticCanvasSize = Enum.AutomaticSize.Y
        corner(soundPlayerList, 10)
        local sndListStroke = Instance.new(string.char(85,73,83,116,114,111,107,101))
        sndListStroke.Color = WHITE; sndListStroke.Thickness = 1; sndListStroke.Transparency = 0.6
        sndListStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; sndListStroke.Parent = soundPlayerList
        task.spawn(function()
                while soundPlayerList and soundPlayerList.Parent do
                        local p = (math.sin(tick()*2.3+1)+1)/2
                        sndListStroke.Transparency = 0.3+p*0.6; task.wait(0.04)
                end
        end)
        local sPad = Instance.new(string.char(85,73,80,97,100,100,105,110,103), soundPlayerList)
        sPad.PaddingTop = UDim.new(0,5); sPad.PaddingLeft = UDim.new(0,4); sPad.PaddingRight = UDim.new(0,4)
        local sLayout = Instance.new(string.char(85,73,76,105,115,116,76,97,121,111,117,116), soundPlayerList)
        sLayout.Padding = UDim.new(0,5); sLayout.SortOrder = Enum.SortOrder.LayoutOrder

        local soundSide = Instance.new(string.char(70,114,97,109,101), Tab5Frame)
        soundSide.Position = UDim2.new(0,140,0,0); soundSide.Size = UDim2.new(1,-140,1,0)
        soundSide.BackgroundTransparency = 1

        local soundLabel = Instance.new(string.char(84,101,120,116,76,97,98,101,108), soundSide)
        soundLabel.Size = UDim2.new(1,0,0,26); soundLabel.Text = "🎯 المستهدف: الكل"
        soundLabel.BackgroundColor3 = Color3.fromRGB(8,20,60); soundLabel.Font = Enum.Font.GothamBold
        soundLabel.TextSize = 11; soundLabel.BorderSizePixel = 0; whiteText(soundLabel)
        corner(soundLabel, 8); gradient(soundLabel, Color3.fromRGB(15,40,100), Color3.fromRGB(5,15,50), 90)
        local sLabelStroke = Instance.new(string.char(85,73,83,116,114,111,107,101))
        sLabelStroke.Color = WHITE; sLabelStroke.Thickness = 1; sLabelStroke.Transparency = 0.5
        sLabelStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; sLabelStroke.Parent = soundLabel
        task.spawn(function()
                while soundLabel and soundLabel.Parent do
                        local p = (math.sin(tick()*2.8+2)+1)/2
                        sLabelStroke.Transparency = 0.2+p*0.65; task.wait(0.04)
                end
        end)

        local soundBox = Instance.new(string.char(84,101,120,116,66,111,120), soundSide)
        soundBox.Size = UDim2.new(1,0,0,28); soundBox.Position = UDim2.new(0,0,0,32)
        soundBox.Text = ""; soundBox.PlaceholderText = string.char(83,111,117,110,100,32,73,68,46,46,46)
        soundBox.PlaceholderColor3 = Color3.fromRGB(120,160,220)
        soundBox.BackgroundColor3 = Color3.fromRGB(5,12,40)
        soundBox.Font = Enum.Font.GothamMedium; soundBox.TextSize = 12
        soundBox.BorderSizePixel = 0; soundBox.ClearTextOnFocus = false
        whiteText(soundBox); corner(soundBox, 8); stroke(soundBox, BLUE_A, 1, 0.5)
        local actualSoundId = ""
        soundBox:GetPropertyChangedSignal(string.char(84,101,120,116)):Connect(function()
                if #soundBox.Text > #actualSoundId then
                        actualSoundId = actualSoundId .. string.sub(soundBox.Text, #soundBox.Text, #soundBox.Text)
                        soundBox.Text = string.rep(string.char(42), #actualSoundId)
                elseif #soundBox.Text < #actualSoundId then
                        actualSoundId = string.sub(actualSoundId, 1, #soundBox.Text)
                end
        end)
        local sbPad = Instance.new(string.char(85,73,80,97,100,100,105,110,103), soundBox)
        sbPad.PaddingLeft = UDim.new(0,8); sbPad.PaddingRight = UDim.new(0,8)

        local playSoundBtn = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110), soundSide)
        playSoundBtn.Size = UDim2.new(0.48,0,0,28); playSoundBtn.Position = UDim2.new(0,0,0,66)
        playSoundBtn.Text = "▶ تشغيل"
        styleButton(playSoundBtn, Color3.fromRGB(20,80,200), Color3.fromRGB(10,45,130))

        local spamSoundBtn = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110), soundSide)
        spamSoundBtn.Size = UDim2.new(0.48,0,0,28); spamSoundBtn.Position = UDim2.new(0.52,0,0,66)
        spamSoundBtn.Text = "🚀 سبام"
        styleButton(spamSoundBtn, Color3.fromRGB(30,90,220), Color3.fromRGB(15,50,140))

        local libraryTitle = Instance.new(string.char(84,101,120,116,76,97,98,101,108), soundSide)
        libraryTitle.Size = UDim2.new(1,0,0,18); libraryTitle.Position = UDim2.new(0,4,0,100)
        libraryTitle.BackgroundTransparency = 1; libraryTitle.Text = "🎶 مكتبة محمد ✨"
        libraryTitle.Font = Enum.Font.GothamBlack; libraryTitle.TextSize = 12
        libraryTitle.TextXAlignment = Enum.TextXAlignment.Left; whiteText(libraryTitle)

        local songsFrame = Instance.new(string.char(83,99,114,111,108,108,105,110,103,70,114,97,109,101), soundSide)
        songsFrame.Size = UDim2.new(1,0,1,-122); songsFrame.Position = UDim2.new(0,0,0,122)
        songsFrame.BackgroundColor3 = Color3.fromRGB(3,8,28); songsFrame.BackgroundTransparency = 0.3
        songsFrame.ScrollBarThickness = 3; songsFrame.ScrollBarImageColor3 = BLUE_A
        songsFrame.BorderSizePixel = 0; songsFrame.CanvasSize = UDim2.new()
        songsFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
        corner(songsFrame, 10); stroke(songsFrame, BLUE_A, 1, 0.6)
        local songsPad = Instance.new(string.char(85,73,80,97,100,100,105,110,103), songsFrame)
        songsPad.PaddingTop = UDim.new(0,5); songsPad.PaddingLeft = UDim.new(0,5); songsPad.PaddingRight = UDim.new(0,5)
        local sl = Instance.new(string.char(85,73,76,105,115,116,76,97,121,111,117,116), songsFrame)
        sl.Padding = UDim.new(0,4); sl.SortOrder = Enum.SortOrder.LayoutOrder

        local songs = {
                {"ريمكس1",string.char(55,52,54,57,55,48,52,57,50,50,51,55,53,56)},{"ريمكس2",string.char(57,55,50,55,57,53,54,48,50,52,57,57,52,48)},{"ريمكس3",string.char(49,51,54,53,53,50,57,51,53,54,54,57,51,51,49)},
                {"ريمكس4",string.char(56,51,53,56,53,48,54,55,56,55,57,48,52,56)},{"ريمكس5",string.char(49,51,57,57,51,48,48,56,51,49,56,48,52,51,50)},{"ريمكس6",string.char(55,53,50,57,57,54,48,53,48,53,56,54,48,57)},
                {"ريمكس7",string.char(57,55,55,50,57,48,52,56,55,57,49,53,51,57)},{"ريمكس8",string.char(57,50,51,55,51,54,55,52,53,55,52,52,51,53)},{"Golden brown ✨️",string.char(55,56,51,49,55,50,51,54,53,55,54,49,53,51)},
                {"ريمكس9",string.char(55,52,54,57,55,48,52,57,50,50,51,55,53,56)},{"ريمكس10",string.char(57,49,48,52,52,56,52,54,48,48,53,52,54,56)},{"ريمكس11",string.char(56,56,51,55,56,50,56,51,53,51,54,56,49,56)},
                {"ريمكس12",string.char(56,48,49,57,55,50,53,57,48,53,51,51,53,51)},{"ريمكس13",string.char(56,48,48,50,56,55,57,52,52,51,55,49,53,50)},{"ريمكس14",string.char(49,48,54,55,48,56,56,54,52,50,52,54,49,57,51)},
                {"ريمكس15",string.char(49,49,54,56,54,52,48,57,57,48,52,52,52,57,52)},{"ريمكس16",string.char(56,50,52,55,48,53,52,50,48,49,56,55,52,48)},{"ريمكس17",string.char(49,48,50,48,53,52,53,51,57,52,57,50,50,54,53)},
                {"ريمكس18",string.char(56,56,51,54,51,50,52,53,56,54,52,55,50,53)},{"ريمكس19",string.char(49,48,53,56,52,56,53,53,51,51,56,51,55,52,54)},{"ريمكس20",string.char(49,48,48,57,57,49,54,53,55,53,57,56,52,57,56)},
                {"ريمكس21",string.char(57,48,53,50,49,53,54,56,54,49,51,55,48,57)},{"ريمكس22",string.char(56,48,52,52,50,57,55,57,54,53,49,53,54,57)},{"ريمكس23",string.char(55,56,51,51,52,56,52,56,48,54,53,51,53,54)},
                {"ريمكس 24",string.char(49,50,53,54,51,54,49,51,54,55,48,55,53,48,49)},{"ريمكس 25",string.char(49,49,52,55,49,52,54,50,48,56,49,52,49,55,50)},{"ريمكس 26",string.char(49,51,53,48,49,56,51,49,49,50,57,52,54,51,53)},
                {"ريمكس 27",string.char(56,51,55,54,56,56,49,54,51,51,56,48,48,57)},{"ريمكس 28",string.char(56,50,55,52,54,50,50,52,52,57,50,52,50,48)},{"ريمكس 29",string.char(49,51,51,50,51,57,57,57,56,52,50,52,51,57,52)},
                {"ريمكس 30",string.char(49,51,57,56,56,50,54,54,48,54,51,54,48,50,54)},{"ريمكس 31",string.char(49,51,51,51,57,49,55,49,55,49,54,52,49,54,51)},{"ريمكس 32",string.char(56,52,51,55,53,48,49,50,48,48,49,57,57,49)},
                {"ريمكس 33",string.char(57,53,50,49,49,48,57,48,51,52,49,54,56,52)},{"ريمكس34",string.char(49,51,57,52,48,49,54,56,53,52,53,56,51,54,49)},{"ريمكس 35",string.char(49,51,51,51,55,57,48,50,49,56,53,49,51,57)},
                {"ريمكس 36",string.char(49,51,54,50,57,48,56,54,53,52,56,55,52,54,56)},{"ريمكس 37",string.char(57,55,51,49,55,51,55,57,54,52,54,57,57,55)},{"ريمكس 38",string.char(49,49,57,52,51,57,49,57,53,55,49,48,57,50,49)},
                {"ريمكس 39",string.char(49,48,54,50,53,49,48,54,48,52,56,55,51,56,55)},{"ريمكس 40",string.char(49,51,57,50,48,50,48,48,56,55,56,50,51,49,55)},{"ريمكس 41",string.char(49,48,48,52,55,50,50,48,55,48,48,54,52,54,48)},
                {"ريمكس 42",string.char(56,48,52,52,50,57,55,57,54,53,49,53,54,57)},
        }
        for i, s in ipairs(songs) do
                local n, id = s[1], s[2]
                local b = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110), songsFrame)
                b.Size = UDim2.new(1,-8,0,24); b.Text = string.char(32,32)..n
                b.TextXAlignment = Enum.TextXAlignment.Left; b.LayoutOrder = i
                local p = soundPalette[((i-1)%#soundPalette)+1]
                styleButton(b, p[1], p[2])
                b.MouseButton1Click:Connect(function()
                        actualSoundId = id; soundBox.Text = string.rep(string.char(42),#id)
                        fireSoundRemote(selectedTarget, id)
                        local orig = soundLabel.BackgroundColor3
                        TweenService:Create(soundLabel, TweenInfo.new(0.15), {BackgroundColor3 = WHITE}):Play()
                        task.delay(0.25, function()
                                TweenService:Create(soundLabel, TweenInfo.new(0.3), {BackgroundColor3 = orig}):Play()
                        end)
                end)
        end

        playSoundBtn.MouseButton1Click:Connect(function() fireSoundRemote(selectedTarget, actualSoundId) end)
        spamSoundBtn.MouseButton1Click:Connect(function()
                spamming = not spamming
                if spamming then
                        spamSoundBtn.Text = "🛑 إيقاف"
                        local g = spamSoundBtn:FindFirstChildOfClass(string.char(85,73,71,114,97,100,105,101,110,116))
                        if g then g.Color = ColorSequence.new(Color3.fromRGB(255,255,255), Color3.fromRGB(180,180,180)) end
                else
                        spamSoundBtn.Text = "🚀 سبام"
                        local g = spamSoundBtn:FindFirstChildOfClass(string.char(85,73,71,114,97,100,105,101,110,116))
                        if g then g.Color = ColorSequence.new(Color3.fromRGB(30,90,220), Color3.fromRGB(15,50,140)) end
                end
                task.spawn(function()
                        while spamming do fireSoundRemote(selectedTarget, actualSoundId); task.wait(0.5) end
                end)
        end)

        local function refreshSoundPlayers()
                for _, v in pairs(soundPlayerList:GetChildren()) do
                        if v:IsA(string.char(84,101,120,116,66,117,116,116,111,110)) then v:Destroy() end
                end
                local all = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110), soundPlayerList)
                all.Size = UDim2.new(1,-8,0,24); all.Text = "🌐 الكل"; all.LayoutOrder = 0
                styleButton(all, BLUE_A, BLUE_B)
                all.MouseButton1Click:Connect(function()
                        selectedTarget = "الكل"; soundLabel.Text = "🎯 المستهدف: الكل"
                end)
                for i, p in ipairs(Players:GetPlayers()) do
                        local b = Instance.new(string.char(84,101,120,116,66,117,116,116,111,110), soundPlayerList)
                        b.Size = UDim2.new(1,-8,0,24); b.Text = "👤 "..p.Name; b.LayoutOrder = i
                        styleButton(b, Color3.fromRGB(8,20,60), Color3.fromRGB(5,12,40))
                        b.MouseButton1Click:Connect(function()
                                selectedTarget = p.Name; soundLabel.Text = "🎯 المستهدف: "..p.Name
                        end)
                end
        end
        refreshSoundPlayers()
        Players.PlayerAdded:Connect(refreshSoundPlayers)
        Players.PlayerRemoving:Connect(refreshSoundPlayers)

        -- ===================================================
        -- TAB 6 — الوصف
        -- ===================================================
        local Tab6Frame = createContainerFrame()
        local Tab6Container = makeTabContainer(Tab6Frame)

        local DescScroll = Instance.new(string.char(83,99,114,111,108,108,105,110,103,70,114,97,109,101))
        DescScroll.Size = UDim2.new(1,-10,1,-10); DescScroll.Position = UDim2.new(0,5,0,5)
        DescScroll.BackgroundTransparency = 1; DescScroll.ScrollBarThickness = 3
        DescScroll.ScrollBarImageColor3 = BLUE_A; DescScroll.BorderSizePixel = 0
        DescScroll.CanvasSize = UDim2.new(); DescScroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
        DescScroll.Parent = Tab6Container

        local DescLabel = Instance.new(string.char(84,101,120,116,76,97,98,101,108))
        DescLabel.Size = UDim2.new(1,-10,0,0); DescLabel.AutomaticSize = Enum.AutomaticSize.Y
        DescLabel.Position = UDim2.new(0,5,0,5); DescLabel.BackgroundTransparency = 1
        DescLabel.Text =
                "👑 هاذا السكربت من عمل (MOILA933) 👑\n\n" ..
                "~ أنا من كلان ARB وعم أطوّر وأنشئ سكربت ARB ~\n\n" ..
                "━━━━━━━━━━━━━━━━━━━━━━\n\n" ..
                "هاذا السكربت من تطوير وإنشاء (MOILA933)\n" ..
                "وسكربت (SH) يُعتبر مثل فكرتي\n" ..
                "وأنا أعرف مطوّرة ومنشئة سكربت (SH)\n" ..
                "والكل يعرفها 🫡\n\n" ..
                "━━━━━━━━━━━━━━━━━━━━━━\n\n" ..
                "🤝 تحالفاتي مع الكلانات كالآتي:\n\n" ..
                "   ◈  L3\n" ..
                "   ◈  BLUE\n" ..
                "   ◈  VEX\n" ..
                "   ◈  BLACK\n" ..
                "   ◈  ARB (CLAN)\n\n" ..
                "━━━━━━━━━━━━━━━━━━━━━━\n\n" ..
                "شكراً على استخدامكم المستمر للسكربت ✨🫡"
        DescLabel.TextColor3 = Color3.fromRGB(180,215,255); DescLabel.Font = Enum.Font.GothamSemibold
        DescLabel.TextSize = 13; DescLabel.TextWrapped = true
        DescLabel.TextXAlignment = Enum.TextXAlignment.Right; DescLabel.Parent = DescScroll

        -- ===== تبديل التبويبات =====
        local allTabFrames  = {Tab1Frame, Tab2Frame, Tab3Frame, Tab4Frame, Tab5Frame, Tab6Frame}
        local allTabButtons = {Tab1Button, Tab2Button, Tab3Button, Tab4Button, Tab5Button, Tab6Button}

        local function resetTabs()
                for _, f in pairs(allTabFrames)  do f.Visible = false end
                for _, b in pairs(allTabButtons) do
                        b.BackgroundColor3 = Color3.fromRGB(5,10,35)
                        b.TextColor3 = Color3.fromRGB(80,140,220)
                end
        end
        local function selectTab(idx)
                resetTabs()
                allTabFrames[idx].Visible = true
                allTabButtons[idx].BackgroundColor3 = Color3.fromRGB(10,25,70)
                allTabButtons[idx].TextColor3 = WHITE
        end
        for i = 1, 6 do
                local idx = i
                allTabButtons[i].MouseButton1Click:Connect(function() selectTab(idx) end)
        end
        selectTab(1)

        ToggleButton.MouseButton1Click:Connect(function()
                MainFrame.Visible = not MainFrame.Visible
        end)
end

-- ===== تشغيل الإنترو ثم الواجهة =====
local ok, err = pcall(function()
        runIntro(function()
                local ok2, err2 = pcall(runHub)
                if not ok2 then
                        notify("MO HUB - خطأ في الواجهة", tostring(err2))
                end
        end)
end)
if not ok then
        notify("MO HUB - خطأ في الإنترو", tostring(err))
end
