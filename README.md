-- [[ واجهة ايقاف مؤقت ]] --

local Players      = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local LocalPlayer  = Players.LocalPlayer

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MO_PAUSED_GUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.DisplayOrder = 999
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

-- خلفية شفافة داكنة
local Overlay = Instance.new("Frame")
Overlay.Size = UDim2.new(1, 0, 1, 0)
Overlay.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Overlay.BackgroundTransparency = 0.45
Overlay.BorderSizePixel = 0
Overlay.Parent = ScreenGui

-- الإطار الرئيسي
local Main = Instance.new("Frame")
Main.Size = UDim2.new(0, 320, 0, 370)
Main.Position = UDim2.new(0.5, -160, 0.5, -185)
Main.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Main.BackgroundTransparency = 0.05
Main.BorderSizePixel = 0
Main.Parent = ScreenGui
local mc = Instance.new("UICorner", Main)
mc.CornerRadius = UDim.new(0, 20)

-- حافة خضراء متوهجة
local mainStroke = Instance.new("UIStroke", Main)
mainStroke.Color = Color3.fromRGB(100, 255, 120)
mainStroke.Thickness = 2.5
mainStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
task.spawn(function()
        while Main and Main.Parent do
                local p = (math.sin(tick() * 2) + 1) / 2
                mainStroke.Transparency = p * 0.5
                mainStroke.Thickness = 2 + p * 1.5
                task.wait(0.03)
        end
end)

-- انيميشن ظهور
Main.AnchorPoint = Vector2.new(0.5, 0.5)
Main.Position = UDim2.new(0.5, 0, 0.5, 0)
Main.Size = UDim2.new(0, 0, 0, 0)
TweenService:Create(Main, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
        {Size = UDim2.new(0, 320, 0, 370)}):Play()

-- العنوان
local TitleLbl = Instance.new("TextLabel")
TitleLbl.Size = UDim2.new(1, 0, 0, 44)
TitleLbl.Position = UDim2.new(0, 0, 0, 8)
TitleLbl.BackgroundTransparency = 1
TitleLbl.Text = "☢️ MO HUB ☢️"
TitleLbl.TextColor3 = Color3.fromRGB(100, 255, 120)
TitleLbl.Font = Enum.Font.GothamBold
TitleLbl.TextSize = 18
TitleLbl.Parent = Main
task.spawn(function()
        while TitleLbl and TitleLbl.Parent do
                local p = (math.sin(tick() * 2.5) + 1) / 2
                TitleLbl.TextColor3 = Color3.fromRGB(
                        math.floor(70 + p * 60),
                        math.floor(210 + p * 45),
                        math.floor(100 + p * 55))
                task.wait(0.04)
        end
end)

-- إطار الصورة
local AvatarFrame = Instance.new("Frame")
AvatarFrame.Size = UDim2.new(0, 150, 0, 150)
AvatarFrame.Position = UDim2.new(0.5, -75, 0, 58)
AvatarFrame.BackgroundColor3 = Color3.fromRGB(10, 30, 10)
AvatarFrame.BorderSizePixel = 0
AvatarFrame.Parent = Main
local afc = Instance.new("UICorner", AvatarFrame)
afc.CornerRadius = UDim.new(1, 0)
local afStroke = Instance.new("UIStroke", AvatarFrame)
afStroke.Color = Color3.fromRGB(100, 255, 120)
afStroke.Thickness = 3
afStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
task.spawn(function()
        while AvatarFrame and AvatarFrame.Parent do
                local p = (math.sin(tick() * 2 + 1) + 1) / 2
                afStroke.Transparency = p * 0.4
                task.wait(0.03)
        end
end)

-- صورة اللاعب moila933
local AvatarImg = Instance.new("ImageLabel")
AvatarImg.Size = UDim2.new(1, -8, 1, -8)
AvatarImg.Position = UDim2.new(0, 4, 0, 4)
AvatarImg.BackgroundTransparency = 1
AvatarImg.Image = ""
AvatarImg.Parent = AvatarFrame
local imgc = Instance.new("UICorner", AvatarImg)
imgc.CornerRadius = UDim.new(1, 0)

-- جلب صورة اللاعب
task.spawn(function()
        local ok, userId = pcall(function()
                return Players:GetUserIdFromNameAsync("moila933")
        end)
        if ok and userId then
                local ok2, img = pcall(function()
                        return Players:GetUserThumbnailAsync(
                                userId,
                                Enum.ThumbnailType.AvatarBust,
                                Enum.ThumbnailSize.Size420x420)
                end)
                if ok2 and img then
                        AvatarImg.Image = img
                end
        end
end)

-- اسم اللاعب
local NameLbl = Instance.new("TextLabel")
NameLbl.Size = UDim2.new(1, -20, 0, 30)
NameLbl.Position = UDim2.new(0, 10, 0, 215)
NameLbl.BackgroundTransparency = 1
NameLbl.Text = "moila933"
NameLbl.TextColor3 = Color3.fromRGB(100, 255, 120)
NameLbl.Font = Enum.Font.GothamBold
NameLbl.TextSize = 18
NameLbl.Parent = Main

-- خط فاصل
local Line = Instance.new("Frame")
Line.Size = UDim2.new(0.8, 0, 0, 1)
Line.Position = UDim2.new(0.1, 0, 0, 252)
Line.BackgroundColor3 = Color3.fromRGB(100, 255, 120)
Line.BackgroundTransparency = 0.5
Line.BorderSizePixel = 0
Line.Parent = Main

-- نص الإيقاف
local PausedLbl = Instance.new("TextLabel")
PausedLbl.Size = UDim2.new(1, -20, 0, 50)
PausedLbl.Position = UDim2.new(0, 10, 0, 260)
PausedLbl.BackgroundTransparency = 1
PausedLbl.Text = "رح ينزل اليوم حماية من jail و ice"
PausedLbl.TextColor3 = Color3.fromRGB(255, 255, 255)
PausedLbl.Font = Enum.Font.GothamBold
PausedLbl.TextSize = 15
PausedLbl.TextWrapped = true
PausedLbl.Parent = Main
task.spawn(function()
        while PausedLbl and PausedLbl.Parent do
                local p = (math.sin(tick() * 3) + 1) / 2
                PausedLbl.TextTransparency = p * 0.5
                task.wait(0.04)
        end
end)

-- زر الإغلاق
local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0.7, 0, 0, 40)
CloseBtn.Position = UDim2.new(0.15, 0, 0, 318)
CloseBtn.BackgroundColor3 = Color3.fromRGB(20, 80, 20)
CloseBtn.Text = "✖ إغلاق"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.TextSize = 14
CloseBtn.AutoButtonColor = false
CloseBtn.Parent = Main
local cc = Instance.new("UICorner", CloseBtn)
cc.CornerRadius = UDim.new(0, 10)
local cs = Instance.new("UIStroke", CloseBtn)
cs.Color = Color3.fromRGB(100, 255, 120); cs.Thickness = 1.5
cs.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
CloseBtn.MouseEnter:Connect(function()
        TweenService:Create(CloseBtn, TweenInfo.new(0.15),
                {BackgroundColor3 = Color3.fromRGB(30, 120, 30)}):Play()
end)
CloseBtn.MouseLeave:Connect(function()
        TweenService:Create(CloseBtn, TweenInfo.new(0.15),
                {BackgroundColor3 = Color3.fromRGB(20, 80, 20)}):Play()
end)
CloseBtn.MouseButton1Click:Connect(function()
        TweenService:Create(Main, TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.In),
                {Size = UDim2.new(0, 0, 0, 0)}):Play()
        task.wait(0.3)
        ScreenGui:Destroy()
end)
-- [[ MO HUB — FIXED VERSION ]] --

local TweenService = game:GetService("TweenService")
local Players      = game:GetService("Players")
local StarterGui   = game:GetService("StarterGui")
local LocalPlayer  = Players.LocalPlayer

local function notify(title, msg)
        pcall(function()
                StarterGui:SetCore("SendNotification", {Title=title, Text=msg, Duration=6})
        end)
end

-- ===================== INTRO =====================
local function runIntro(onDone)
        local TargetParent = LocalPlayer:WaitForChild("PlayerGui")
        pcall(function()
                local cg = game:GetService("CoreGui")
                if cg then TargetParent = cg end
        end)

        local IntroGui = Instance.new("ScreenGui")
        IntroGui.Name = "MO_HUB_IntroGui"
        IntroGui.ResetOnSpawn = false
        IntroGui.IgnoreGuiInset = true
        IntroGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
        IntroGui.DisplayOrder = 2147483647
        IntroGui.Parent = TargetParent

        local Background = Instance.new("Frame")
        Background.Size = UDim2.new(1,0,1,0)
        Background.BackgroundColor3 = Color3.fromRGB(0,0,0)
        Background.BorderSizePixel = 0
        Background.Parent = IntroGui

        local IntroSound = Instance.new("Sound")
        IntroSound.SoundId = "rbxassetid://1841683877"
        IntroSound.Volume = 1
        IntroSound.Parent = IntroGui

        local ImageLabel = Instance.new("ImageLabel")
        ImageLabel.Size = UDim2.new(0,200,0,200)
        ImageLabel.Position = UDim2.new(0.5,-100,0.5,-100)
        ImageLabel.BackgroundTransparency = 1
        ImageLabel.Image = "rbxassetid://96306504246987"
        ImageLabel.ImageTransparency = 1
        ImageLabel.Parent = Background

        local FlashFrame = Instance.new("Frame")
        FlashFrame.Size = UDim2.new(1,0,1,0)
        FlashFrame.BackgroundColor3 = Color3.fromRGB(255,255,255)
        FlashFrame.BackgroundTransparency = 1
        FlashFrame.BorderSizePixel = 0
        FlashFrame.ZIndex = 2
        FlashFrame.Parent = Background

        local TextLabel = Instance.new("TextLabel")
        TextLabel.Size = UDim2.new(1,0,0,100)
        TextLabel.Position = UDim2.new(0,0,0.5,-50)
        TextLabel.BackgroundTransparency = 1
        TextLabel.Text = "MO TOP 1"
        TextLabel.TextColor3 = Color3.fromRGB(255,255,255)
        TextLabel.TextSize = 50
        TextLabel.Font = Enum.Font.Code
        TextLabel.TextTransparency = 1
        TextLabel.Parent = Background

        local SkipHintLabel = Instance.new("TextLabel")
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

        local GlitchFrame = Instance.new("Frame")
        GlitchFrame.Size = UDim2.new(1,0,1,0)
        GlitchFrame.BackgroundTransparency = 1
        GlitchFrame.BorderSizePixel = 0
        GlitchFrame.Parent = Background

        local SkipButton = Instance.new("TextButton")
        SkipButton.Size = UDim2.new(1,0,1,0)
        SkipButton.BackgroundTransparency = 1
        SkipButton.Text = ""
        SkipButton.ZIndex = 10
        SkipButton.Parent = Background

        local function createGlitchLine()
                if not GlitchFrame or not GlitchFrame.Parent then return end
                local line = Instance.new("Frame")
                line.Size = UDim2.new(1,0,0,math.random(5,20))
                line.Position = UDim2.new(0,0,math.random(0,90)/100,0)
                local colors = {Color3.fromRGB(255,0,0),Color3.fromRGB(0,255,0),Color3.fromRGB(0,0,255),Color3.fromRGB(255,0,255)}
                line.BackgroundColor3 = colors[math.random(1,#colors)]
                line.BorderSizePixel = 0
                line.Parent = GlitchFrame
                game:GetService("Debris"):AddItem(line, 0.1)
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
                        if ImageLabel and ImageLabel.Parent then ImageLabel:TweenSize(UDim2.new(0,230,0,230),"Out","Quad",0.15,true) end
                        if FlashFrame and FlashFrame.Parent then
                                FlashFrame.BackgroundColor3 = flashColors[math.random(1,#flashColors)]
                                FlashFrame.BackgroundTransparency = 0.65
                        end
                        task.wait(0.1)
                        if FlashFrame and FlashFrame.Parent then FlashFrame.BackgroundTransparency = 1 end
                        if ImageLabel and ImageLabel.Parent then ImageLabel:TweenSize(UDim2.new(0,200,0,200),"In","Quad",0.15,true) end
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
        local RunService  = game:GetService("RunService")
        local StarterGui  = game:GetService("StarterGui")
        local UIS         = game:GetService("UserInputService")
        local RS          = game:GetService("ReplicatedStorage")
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
                local gui = LocalPlayer.PlayerGui:FindFirstChild("MountedGui")
                if gui then
                        for _, v in pairs(gui:GetDescendants()) do
                                if v.Name == "Remote" and v:IsA("RemoteEvent") then return v end
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
                local re = RS:WaitForChild("RemoteEvents", 3)
                if re then chatEvent = re:FindFirstChild("ChatEvent") end
        end)
        if not chatEvent then
                for _, v in pairs(RS:GetDescendants()) do
                        if v.Name == "ChatEvent" and v:IsA("RemoteEvent") then chatEvent = v; break end
                end
        end
        pcall(function()
                local hdc = RS:FindFirstChild("HDAdminHDClient")
                if hdc and hdc:FindFirstChild("Signals") then
                        execSignal = hdc.Signals:FindFirstChild("RequestCommandModification")
                end
        end)

        local function deleteNightVision()
                local hd = RS:FindFirstChild("HDAdminHDClient")
                if hd then
                        local assets = hd:FindFirstChild("Assets")
                        if assets then
                                local nv = assets:FindFirstChild("NightVision")
                                if nv then nv:Destroy(); return true end
                        end
                end
                return false
        end

        local function deleteHDInterface()
                local pg = player:FindFirstChild("PlayerGui")
                if pg then
                        local hdi = pg:FindFirstChild("HDAdminInterface")
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

        local ScreenGui = Instance.new("ScreenGui")
        ScreenGui.Name = "MOILA933_Mini_System"
        ScreenGui.ResetOnSpawn = false
        ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

        -- ===== HELPERS =====
        local function corner(p, r)
                local c = Instance.new("UICorner", p)
                c.CornerRadius = UDim.new(0, r or 12)
                return c
        end
        local function gradient(p, c1, c2, rot)
                local g = Instance.new("UIGradient", p)
                g.Color = ColorSequence.new(c1, c2)
                g.Rotation = rot or 90
                return g
        end
        local function stroke(p, col, t, trans)
                local s = Instance.new("UIStroke", p)
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
                        local rip = Instance.new("Frame", btn)
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
        local ToggleButton = Instance.new("TextButton")
        ToggleButton.Size = UDim2.new(0,55,0,55)
        ToggleButton.Position = UDim2.new(0,20,0.5,-27)
        ToggleButton.BackgroundColor3 = BLUE_A
        ToggleButton.BackgroundTransparency = 0.2
        ToggleButton.Text = "MO"
        ToggleButton.TextColor3 = WHITE
        ToggleButton.TextSize = 20
        ToggleButton.Font = Enum.Font.GothamBold
        ToggleButton.Active = true
        ToggleButton.Parent = ScreenGui
        local tc = Instance.new("UICorner"); tc.CornerRadius = UDim.new(1,0); tc.Parent = ToggleButton
        local ts = Instance.new("UIStroke"); ts.Thickness = 3; ts.Color = BLUE_A; ts.Parent = ToggleButton
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
        local MainFrame = Instance.new("Frame")
        MainFrame.Size = UDim2.new(0,640,0,430)
        MainFrame.Position = UDim2.new(0.5,-320,0.5,-215)
        MainFrame.BackgroundColor3 = DARK
        MainFrame.BackgroundTransparency = 0.15
        MainFrame.BorderSizePixel = 0
        MainFrame.Visible = false
        MainFrame.Active = true
        MainFrame.Parent = ScreenGui
        corner(MainFrame, 16)
        local MainStroke = Instance.new("UIStroke")
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

        local Title = Instance.new("TextLabel")
        Title.Size = UDim2.new(1,-50,0,40); Title.BackgroundTransparency = 1
        Title.Text = "☢️ MOILA933 Script maker ☢️"
        Title.TextColor3 = Color3.fromRGB(80,160,255)
        Title.Font = Enum.Font.GothamBold; Title.TextSize = 15; Title.Parent = MainFrame

        local CloseButton = Instance.new("TextButton")
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
        local TabBar = Instance.new("Frame")
        TabBar.Size = UDim2.new(1,-16,0,30); TabBar.Position = UDim2.new(0,8,0,42)
        TabBar.BackgroundTransparency = 1; TabBar.Parent = MainFrame

        local TAB_W = 0.1666
        local function createTabBtn(text, posPercent)
                local btn = Instance.new("TextButton")
                btn.Size = UDim2.new(TAB_W,-2,1,0)
                btn.Position = UDim2.new(posPercent,0,0,0)
                btn.BackgroundColor3 = Color3.fromRGB(5,10,35)
                btn.Text = text
                btn.TextColor3 = Color3.fromRGB(80,140,220)
                btn.Font = Enum.Font.GothamBold
                btn.TextSize = 8
                btn.Parent = TabBar
                corner(btn, 6)
                local tabStroke = Instance.new("UIStroke")
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

        local Tab1Button = createTabBtn("أدوات",    0.0)
        Tab1Button.BackgroundColor3 = Color3.fromRGB(10,25,70); Tab1Button.TextColor3 = WHITE
        local Tab2Button = createTabBtn("نسخ تحديث📋",  TAB_W*1)
        local Tab3Button = createTabBtn("حماية logs🛡️", TAB_W*2)
        local Tab4Button = createTabBtn("حماية nv🛡️",  TAB_W*3)
        local Tab5Button = createTabBtn("الراديو🎧",    TAB_W*4)
        local Tab6Button = createTabBtn("الوصف",       TAB_W*5)

        local function createContainerFrame()
                local f = Instance.new("Frame")
                f.Size = UDim2.new(1,-24,1,-88); f.Position = UDim2.new(0,12,0,78)
                f.BackgroundTransparency = 1; f.Visible = false; f.Parent = MainFrame
                return f
        end

        local function makeTabContainer(parent)
                local f = Instance.new("Frame")
                f.Size = UDim2.new(1,0,1,0)
                f.BackgroundColor3 = DARK
                f.BackgroundTransparency = 0.5
                f.Parent = parent
                corner(f, 10)
                local cs = Instance.new("UIStroke")
                cs.Color = WHITE; cs.Thickness = 1.5; cs.Transparency = 0.5
                cs.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; cs.Parent = f
                local bg = Instance.new("UIGradient")
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
                local f = Instance.new("Frame")
                f.Size = UDim2.new(1,0,1,0)
                f.BackgroundColor3 = Color3.fromRGB(18,45,110)
                f.BackgroundTransparency = 0.1
                f.Parent = parent
                corner(f, 10)
                local cs = Instance.new("UIStroke")
                cs.Color = Color3.fromRGB(100,180,255); cs.Thickness = 2; cs.Transparency = 0.2
                cs.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; cs.Parent = f
                local bg = Instance.new("UIGradient")
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
                local btn = Instance.new("TextButton")
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

                local btnStroke = Instance.new("UIStroke", btn)
                btnStroke.Color = WHITE
                btnStroke.Thickness = 2.5
                btnStroke.Transparency = 0
                btnStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

                local btnGrad = Instance.new("UIGradient", btn)
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

        local t2Desc = Instance.new("TextLabel")
        t2Desc.Size = UDim2.new(1,-30,0,50); t2Desc.Position = UDim2.new(0,15,0,20)
        t2Desc.BackgroundTransparency = 1
        t2Desc.Text = "اضغط على الزر أدناه لتحميل وتشغيل أحدث نسخة من سكربت MO HUT 🚀"
        t2Desc.TextColor3 = Color3.fromRGB(160,210,255); t2Desc.Font = Enum.Font.GothamBold
        t2Desc.TextSize = 13; t2Desc.TextWrapped = true
        t2Desc.TextXAlignment = Enum.TextXAlignment.Right; t2Desc.Parent = Tab2Container

        local LoadBtn = Instance.new("TextButton")
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

        local CleanerDesc = Instance.new("TextLabel")
        CleanerDesc.Size = UDim2.new(1,-30,0,90); CleanerDesc.Position = UDim2.new(0,15,0,15)
        CleanerDesc.BackgroundTransparency = 1
        CleanerDesc.Text = "logs و clogs اذا ضغطت على الزر الي تحت رح تجيك حماية من"
        CleanerDesc.TextColor3 = Color3.fromRGB(180,230,255); CleanerDesc.Font = Enum.Font.GothamBold
        CleanerDesc.TextSize = 13; CleanerDesc.TextWrapped = true; CleanerDesc.Parent = Tab3Container

        local StartCleaner = Instance.new("TextButton")
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
                local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")
                local Keywords = {"admin","cmd","log","console","terminal","adoni","kohl"}
                local function cleanUI(g)
                        local n = g.Name:lower()
                        for _, k in ipairs(Keywords) do
                                if n:find(k) and not n:find("shop") and not n:find("menu") then
                                        g:Destroy(); break
                                end
                        end
                end
                for _, c in ipairs(PlayerGui:GetChildren()) do cleanUI(c) end
                PlayerGui.ChildAdded:Connect(cleanUI)
                task.spawn(function()
                        while task.wait(1) do
                                pcall(function() StarterGui:SetCore("DevConsoleVisible", false) end)
                        end
                end)
        end)

        -- ===================================================
        -- TAB 4 — حماية nv
        -- ===================================================
        local Tab4Frame = createContainerFrame()
        local Tab4Container = makeTabContainer(Tab4Frame)

        local ProDesc = Instance.new("TextLabel")
        ProDesc.Size = UDim2.new(1,-30,0,60); ProDesc.Position = UDim2.new(0,15,0,15)
        ProDesc.BackgroundTransparency = 1
        ProDesc.Text = "نظام حماية MOILA HUBBB المتقدم لتدمير واجهة HD Admin و NightVision وحذف الأصول الضارة بالسيرفر."
        ProDesc.TextColor3 = Color3.fromRGB(160,210,255); ProDesc.Font = Enum.Font.GothamBold
        ProDesc.TextSize = 12; ProDesc.TextWrapped = true; ProDesc.Parent = Tab4Container

        local StatusLabel = Instance.new("TextLabel")
        StatusLabel.Size = UDim2.new(1,-30,0,30); StatusLabel.Position = UDim2.new(0,15,0,80)
        StatusLabel.BackgroundTransparency = 1; StatusLabel.Text = "حالة الحماية: لم يتم التفعيل بعد 🚫"
        StatusLabel.TextColor3 = Color3.fromRGB(180,180,180); StatusLabel.Font = Enum.Font.GothamSemibold
        StatusLabel.TextSize = 11; StatusLabel.Parent = Tab4Container

        local StartPro = Instance.new("TextButton")
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
                StatusLabel.Text = "NightVision: "..tostring(d1).." | HDInterface: "..tostring(d2)
                StatusLabel.TextColor3 = Color3.fromRGB(50,255,50)
                StartPro.Text = "✅ تم تشغيل الحماية بنجاح"
                StartPro.BackgroundColor3 = Color3.fromRGB(40,40,40)
        end)

        -- ===================================================
        -- TAB 5 — الراديو
        -- ===================================================
        local Tab5Frame = createContainerFrame()

        local soundPlayerList = Instance.new("ScrollingFrame", Tab5Frame)
        soundPlayerList.Size = UDim2.new(0,130,1,0); soundPlayerList.BackgroundColor3 = Color3.fromRGB(3,8,28)
        soundPlayerList.BackgroundTransparency = 0.3; soundPlayerList.ScrollBarThickness = 3
        soundPlayerList.ScrollBarImageColor3 = BLUE_A; soundPlayerList.BorderSizePixel = 0
        soundPlayerList.CanvasSize = UDim2.new(); soundPlayerList.AutomaticCanvasSize = Enum.AutomaticSize.Y
        corner(soundPlayerList, 10)
        local sndListStroke = Instance.new("UIStroke")
        sndListStroke.Color = WHITE; sndListStroke.Thickness = 1; sndListStroke.Transparency = 0.6
        sndListStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; sndListStroke.Parent = soundPlayerList
        task.spawn(function()
                while soundPlayerList and soundPlayerList.Parent do
                        local p = (math.sin(tick()*2.3+1)+1)/2
                        sndListStroke.Transparency = 0.3+p*0.6; task.wait(0.04)
                end
        end)
        local sPad = Instance.new("UIPadding", soundPlayerList)
        sPad.PaddingTop = UDim.new(0,5); sPad.PaddingLeft = UDim.new(0,4); sPad.PaddingRight = UDim.new(0,4)
        local sLayout = Instance.new("UIListLayout", soundPlayerList)
        sLayout.Padding = UDim.new(0,5); sLayout.SortOrder = Enum.SortOrder.LayoutOrder

        local soundSide = Instance.new("Frame", Tab5Frame)
        soundSide.Position = UDim2.new(0,140,0,0); soundSide.Size = UDim2.new(1,-140,1,0)
        soundSide.BackgroundTransparency = 1

        local soundLabel = Instance.new("TextLabel", soundSide)
        soundLabel.Size = UDim2.new(1,0,0,26); soundLabel.Text = "🎯 المستهدف: الكل"
        soundLabel.BackgroundColor3 = Color3.fromRGB(8,20,60); soundLabel.Font = Enum.Font.GothamBold
        soundLabel.TextSize = 11; soundLabel.BorderSizePixel = 0; whiteText(soundLabel)
        corner(soundLabel, 8); gradient(soundLabel, Color3.fromRGB(15,40,100), Color3.fromRGB(5,15,50), 90)
        local sLabelStroke = Instance.new("UIStroke")
        sLabelStroke.Color = WHITE; sLabelStroke.Thickness = 1; sLabelStroke.Transparency = 0.5
        sLabelStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; sLabelStroke.Parent = soundLabel
        task.spawn(function()
                while soundLabel and soundLabel.Parent do
                        local p = (math.sin(tick()*2.8+2)+1)/2
                        sLabelStroke.Transparency = 0.2+p*0.65; task.wait(0.04)
                end
        end)

        local soundBox = Instance.new("TextBox", soundSide)
        soundBox.Size = UDim2.new(1,0,0,28); soundBox.Position = UDim2.new(0,0,0,32)
        soundBox.Text = ""; soundBox.PlaceholderText = "Sound ID..."
        soundBox.PlaceholderColor3 = Color3.fromRGB(120,160,220)
        soundBox.BackgroundColor3 = Color3.fromRGB(5,12,40)
        soundBox.Font = Enum.Font.GothamMedium; soundBox.TextSize = 12
        soundBox.BorderSizePixel = 0; soundBox.ClearTextOnFocus = false
        whiteText(soundBox); corner(soundBox, 8); stroke(soundBox, BLUE_A, 1, 0.5)
        local actualSoundId = ""
        soundBox:GetPropertyChangedSignal("Text"):Connect(function()
                if #soundBox.Text > #actualSoundId then
                        actualSoundId = actualSoundId .. string.sub(soundBox.Text, #soundBox.Text, #soundBox.Text)
                        soundBox.Text = string.rep("*", #actualSoundId)
                elseif #soundBox.Text < #actualSoundId then
                        actualSoundId = string.sub(actualSoundId, 1, #soundBox.Text)
                end
        end)
        local sbPad = Instance.new("UIPadding", soundBox)
        sbPad.PaddingLeft = UDim.new(0,8); sbPad.PaddingRight = UDim.new(0,8)

        local playSoundBtn = Instance.new("TextButton", soundSide)
        playSoundBtn.Size = UDim2.new(0.48,0,0,28); playSoundBtn.Position = UDim2.new(0,0,0,66)
        playSoundBtn.Text = "▶ تشغيل"
        styleButton(playSoundBtn, Color3.fromRGB(20,80,200), Color3.fromRGB(10,45,130))

        local spamSoundBtn = Instance.new("TextButton", soundSide)
        spamSoundBtn.Size = UDim2.new(0.48,0,0,28); spamSoundBtn.Position = UDim2.new(0.52,0,0,66)
        spamSoundBtn.Text = "🚀 سبام"
        styleButton(spamSoundBtn, Color3.fromRGB(30,90,220), Color3.fromRGB(15,50,140))

        local libraryTitle = Instance.new("TextLabel", soundSide)
        libraryTitle.Size = UDim2.new(1,0,0,18); libraryTitle.Position = UDim2.new(0,4,0,100)
        libraryTitle.BackgroundTransparency = 1; libraryTitle.Text = "🎶 مكتبة محمد ✨"
        libraryTitle.Font = Enum.Font.GothamBlack; libraryTitle.TextSize = 12
        libraryTitle.TextXAlignment = Enum.TextXAlignment.Left; whiteText(libraryTitle)

        local songsFrame = Instance.new("ScrollingFrame", soundSide)
        songsFrame.Size = UDim2.new(1,0,1,-122); songsFrame.Position = UDim2.new(0,0,0,122)
        songsFrame.BackgroundColor3 = Color3.fromRGB(3,8,28); songsFrame.BackgroundTransparency = 0.3
        songsFrame.ScrollBarThickness = 3; songsFrame.ScrollBarImageColor3 = BLUE_A
        songsFrame.BorderSizePixel = 0; songsFrame.CanvasSize = UDim2.new()
        songsFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
        corner(songsFrame, 10); stroke(songsFrame, BLUE_A, 1, 0.6)
        local songsPad = Instance.new("UIPadding", songsFrame)
        songsPad.PaddingTop = UDim.new(0,5); songsPad.PaddingLeft = UDim.new(0,5); songsPad.PaddingRight = UDim.new(0,5)
        local sl = Instance.new("UIListLayout", songsFrame)
        sl.Padding = UDim.new(0,4); sl.SortOrder = Enum.SortOrder.LayoutOrder

        local songs = {
                {"ريمكس1","74697049223758"},{"ريمكس2","97279560249940"},{"ريمكس3","136552935669331"},
                {"ريمكس4","83585067879048"},{"ريمكس5","139930083180432"},{"ريمكس6","75299605058609"},
                {"ريمكس7","97729048791539"},{"ريمكس8","92373674574435"},{"Golden brown ✨️","78317236576153"},
                {"ريمكس9","74697049223758"},{"ريمكس10","91044846005468"},{"ريمكس11","88378283536818"},
                {"ريمكس12","80197259053353"},{"ريمكس13","80028794437152"},{"ريمكس14","106708864246193"},
                {"ريمكس15","116864099044494"},{"ريمكس16","82470542018740"},{"ريمكس17","102054539492265"},
                {"ريمكس18","88363245864725"},{"ريمكس19","105848553383746"},{"ريمكس20","100991657598498"},
                {"ريمكس21","90521568613709"},{"ريمكس22","80442979651569"},{"ريمكس23","78334848065356"},
                {"ريمكس 24","125636136707501"},{"ريمكس 25","114714620814172"},{"ريمكس 26","135018311294635"},
                {"ريمكس 27","83768816338009"},{"ريمكس 28","82746224492420"},{"ريمكس 29","133239998424394"},
                {"ريمكس 30","139882660636026"},{"ريمكس 31","133391717164163"},{"ريمكس 32","84375012001991"},
                {"ريمكس 33","95211090341684"},{"ريمكس34","139401685458361"},{"ريمكس 35","13337902185139"},
                {"ريمكس 36","136290865487468"},{"ريمكس 37","97317379646997"},{"ريمكس 38","119439195710921"},
                {"ريمكس 39","106251060487387"},{"ريمكس 40","139202008782317"},{"ريمكس 41","100472207006460"},
                {"ريمكس 42","80442979651569"},
        }
        for i, s in ipairs(songs) do
                local n, id = s[1], s[2]
                local b = Instance.new("TextButton", songsFrame)
                b.Size = UDim2.new(1,-8,0,24); b.Text = "  "..n
                b.TextXAlignment = Enum.TextXAlignment.Left; b.LayoutOrder = i
                local p = soundPalette[((i-1)%#soundPalette)+1]
                styleButton(b, p[1], p[2])
                b.MouseButton1Click:Connect(function()
                        actualSoundId = id; soundBox.Text = string.rep("*",#id)
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
                        local g = spamSoundBtn:FindFirstChildOfClass("UIGradient")
                        if g then g.Color = ColorSequence.new(Color3.fromRGB(255,255,255), Color3.fromRGB(180,180,180)) end
                else
                        spamSoundBtn.Text = "🚀 سبام"
                        local g = spamSoundBtn:FindFirstChildOfClass("UIGradient")
                        if g then g.Color = ColorSequence.new(Color3.fromRGB(30,90,220), Color3.fromRGB(15,50,140)) end
                end
                task.spawn(function()
                        while spamming do fireSoundRemote(selectedTarget, actualSoundId); task.wait(0.5) end
                end)
        end)

        local function refreshSoundPlayers()
                for _, v in pairs(soundPlayerList:GetChildren()) do
                        if v:IsA("TextButton") then v:Destroy() end
                end
                local all = Instance.new("TextButton", soundPlayerList)
                all.Size = UDim2.new(1,-8,0,24); all.Text = "🌐 الكل"; all.LayoutOrder = 0
                styleButton(all, BLUE_A, BLUE_B)
                all.MouseButton1Click:Connect(function()
                        selectedTarget = "الكل"; soundLabel.Text = "🎯 المستهدف: الكل"
                end)
                for i, p in ipairs(Players:GetPlayers()) do
                        local b = Instance.new("TextButton", soundPlayerList)
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

        local DescScroll = Instance.new("ScrollingFrame")
        DescScroll.Size = UDim2.new(1,-10,1,-10); DescScroll.Position = UDim2.new(0,5,0,5)
        DescScroll.BackgroundTransparency = 1; DescScroll.ScrollBarThickness = 3
        DescScroll.ScrollBarImageColor3 = BLUE_A; DescScroll.BorderSizePixel = 0
        DescScroll.CanvasSize = UDim2.new(); DescScroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
        DescScroll.Parent = Tab6Container

        local DescLabel = Instance.new("TextLabel")
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
