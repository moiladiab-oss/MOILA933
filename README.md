-- [[ MO SPAM ]] --

local TweenService = game:GetService("TweenService")
local UIS          = game:GetService("UserInputService")
local Players      = game:GetService("Players")
local RS           = game:GetService("ReplicatedStorage")
local LocalPlayer  = Players.LocalPlayer

local LGREEN = Color3.fromRGB(100, 255, 120)  -- أخضر فاتح للحواف
local GREEN  = Color3.fromRGB(0, 210, 80)
local RED    = Color3.fromRGB(220, 40, 40)
local BLACK  = Color3.fromRGB(0, 0, 0)
local WHITE  = Color3.fromRGB(255, 255, 255)

local spamming  = false
local spamDelay = 0.0
local spamConn  = nil

-- ======= إرسال الرسالة =======
local function sendMsg(msg)
        -- طريقة 1: HD Admin Remote (الريموت المطلوب)
        local hdOk = pcall(function()
                local hd = RS:FindFirstChild("HDAdminHDClient")
                if not hd then error("no hd") end
                local sig = hd:FindFirstChild("Signals")
                if not sig then error("no sig") end
                local rem = sig:FindFirstChild("RequestCommandModification")
                if not rem then error("no rem") end
                rem:InvokeServer(msg)
        end)
        if hdOk then return end
        -- طريقة 2: نظام الشات الجديد
        local ok2 = pcall(function()
                local tcs = game:GetService("TextChatService")
                local ch  = tcs.TextChannels:FindFirstChild("RBXGeneral")
                if not ch then error("no ch") end
                ch:SendAsync(msg)
        end)
        if ok2 then return end
        -- طريقة 3: نظام الشات القديم
        pcall(function()
                RS:WaitForChild("DefaultChatSystemChatEvents", 2)
                  :WaitForChild("SayMessageRequest", 2)
                  :FireServer(msg, "All")
        end)
end

local function corner(p, r)
        Instance.new("UICorner", p).CornerRadius = UDim.new(0, r or 10)
end

local function makeDraggable(frame)
        local dragging, dragInput, dragStart, startPos
        frame.InputBegan:Connect(function(inp)
                if inp.UserInputType == Enum.UserInputType.MouseButton1 or
                   inp.UserInputType == Enum.UserInputType.Touch then
                        dragging = true; dragStart = inp.Position; startPos = frame.Position
                        inp.Changed:Connect(function()
                                if inp.UserInputState == Enum.UserInputState.End then dragging = false end
                        end)
                end
        end)
        frame.InputChanged:Connect(function(inp)
                if inp.UserInputType == Enum.UserInputType.MouseMovement or
                   inp.UserInputType == Enum.UserInputType.Touch then dragInput = inp end
        end)
        UIS.InputChanged:Connect(function(inp)
                if inp == dragInput and dragging then
                        local d = inp.Position - dragStart
                        frame.Position = UDim2.new(
                                startPos.X.Scale, startPos.X.Offset + d.X,
                                startPos.Y.Scale, startPos.Y.Offset + d.Y)
                end
        end)
end

-- ======= الواجهة =======
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MO_SPAM"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 310, 0, 280)
MainFrame.Position = UDim2.new(0.5, -155, 0.5, -140)
MainFrame.BackgroundColor3 = BLACK
MainFrame.BackgroundTransparency = 0
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Parent = ScreenGui
corner(MainFrame, 18)
makeDraggable(MainFrame)

-- حواف خضراء فاتحة متوهجة
local mainStroke = Instance.new("UIStroke", MainFrame)
mainStroke.Color = LGREEN
mainStroke.Thickness = 2.5
mainStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
task.spawn(function()
        while MainFrame and MainFrame.Parent do
                local p = (math.sin(tick() * 2) + 1) / 2
                mainStroke.Transparency = p * 0.45
                mainStroke.Thickness = 2 + p * 1.5
                task.wait(0.03)
        end
end)

-- العنوان
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 44)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "☢️ MO SPAM ☢️"
Title.TextColor3 = LGREEN
Title.Font = Enum.Font.GothamBold
Title.TextSize = 17
Title.Parent = MainFrame
task.spawn(function()
        while Title and Title.Parent do
                local p = (math.sin(tick() * 2.5) + 1) / 2
                Title.TextColor3 = Color3.fromRGB(
                        math.floor(80 + p * 80),
                        math.floor(220 + p * 35),
                        math.floor(100 + p * 50))
                task.wait(0.04)
        end
end)

-- ======= دائرة التشغيل/الإيقاف =======
local CircleBtn = Instance.new("TextButton")
CircleBtn.Size = UDim2.new(0, 38, 0, 38)
CircleBtn.Position = UDim2.new(1, -48, 0, 3)
CircleBtn.BackgroundColor3 = RED
CircleBtn.Text = "▶"
CircleBtn.TextColor3 = WHITE
CircleBtn.TextSize = 16
CircleBtn.Font = Enum.Font.GothamBold
CircleBtn.AutoButtonColor = false
CircleBtn.ZIndex = 10
CircleBtn.Parent = MainFrame
corner(CircleBtn, 999)
local circleStroke = Instance.new("UIStroke", CircleBtn)
circleStroke.Color = WHITE; circleStroke.Thickness = 2
circleStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

-- توهج الدائرة
task.spawn(function()
        while CircleBtn and CircleBtn.Parent do
                local p = (math.sin(tick() * 3) + 1) / 2
                if spamming then
                        CircleBtn.BackgroundColor3 = Color3.fromRGB(0, math.floor(170 + p * 40), math.floor(60 + p * 20))
                        circleStroke.Color = LGREEN
                else
                        CircleBtn.BackgroundColor3 = Color3.fromRGB(math.floor(170 + p * 50), 0, 0)
                        circleStroke.Color = WHITE
                end
                task.wait(0.04)
        end
end)

-- تسمية الرسالة
local MsgLabel = Instance.new("TextLabel")
MsgLabel.Size = UDim2.new(1, -20, 0, 22)
MsgLabel.Position = UDim2.new(0, 10, 0, 52)
MsgLabel.BackgroundTransparency = 1
MsgLabel.Text = "📝 الرسالة:"
MsgLabel.TextColor3 = LGREEN
MsgLabel.Font = Enum.Font.GothamBold
MsgLabel.TextSize = 13
MsgLabel.TextXAlignment = Enum.TextXAlignment.Right
MsgLabel.Parent = MainFrame

-- صندوق الرسالة
local MsgBox = Instance.new("TextBox")
MsgBox.Size = UDim2.new(1, -20, 0, 50)
MsgBox.Position = UDim2.new(0, 10, 0, 76)
MsgBox.BackgroundColor3 = Color3.fromRGB(8, 18, 8)
MsgBox.BackgroundTransparency = 0
MsgBox.PlaceholderText = "اكتب رسالة السبام..."
MsgBox.PlaceholderColor3 = Color3.fromRGB(70, 130, 70)
MsgBox.Text = ""
MsgBox.TextColor3 = WHITE
MsgBox.Font = Enum.Font.GothamBold
MsgBox.TextSize = 13
MsgBox.ClearTextOnFocus = false
MsgBox.TextXAlignment = Enum.TextXAlignment.Right
MsgBox.MultiLine = false
MsgBox.Parent = MainFrame
corner(MsgBox, 10)
local mStroke = Instance.new("UIStroke", MsgBox)
mStroke.Color = LGREEN; mStroke.Thickness = 1.5
mStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

-- تسمية السرعة
local SpeedLabel = Instance.new("TextLabel")
SpeedLabel.Size = UDim2.new(1, -20, 0, 22)
SpeedLabel.Position = UDim2.new(0, 10, 0, 140)
SpeedLabel.BackgroundTransparency = 1
SpeedLabel.Text = "⚡ السرعة (ثانية) — 0 = أسرع ما يمكن:"
SpeedLabel.TextColor3 = LGREEN
SpeedLabel.Font = Enum.Font.GothamBold
SpeedLabel.TextSize = 12
SpeedLabel.TextXAlignment = Enum.TextXAlignment.Right
SpeedLabel.Parent = MainFrame

-- صندوق السرعة
local SpeedBox = Instance.new("TextBox")
SpeedBox.Size = UDim2.new(1, -20, 0, 36)
SpeedBox.Position = UDim2.new(0, 10, 0, 164)
SpeedBox.BackgroundColor3 = Color3.fromRGB(8, 18, 8)
SpeedBox.BackgroundTransparency = 0
SpeedBox.PlaceholderText = "0.0"
SpeedBox.PlaceholderColor3 = Color3.fromRGB(70, 130, 70)
SpeedBox.Text = "0.0"
SpeedBox.TextColor3 = WHITE
SpeedBox.Font = Enum.Font.GothamBold
SpeedBox.TextSize = 14
SpeedBox.ClearTextOnFocus = false
SpeedBox.TextXAlignment = Enum.TextXAlignment.Center
SpeedBox.Parent = MainFrame
corner(SpeedBox, 10)
local sStroke = Instance.new("UIStroke", SpeedBox)
sStroke.Color = LGREEN; sStroke.Thickness = 1.5
sStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

SpeedBox.FocusLost:Connect(function()
        local val = tonumber(SpeedBox.Text)
        spamDelay = val and math.max(0, val) or spamDelay
        SpeedBox.Text = tostring(spamDelay)
end)

-- ======= زر السبام الكبير =======
local SpamBtn = Instance.new("TextButton")
SpamBtn.Size = UDim2.new(1, -20, 0, 48)
SpamBtn.Position = UDim2.new(0, 10, 0, 218)
SpamBtn.BackgroundColor3 = RED
SpamBtn.Text = "🔴  ابدأ السبام"
SpamBtn.TextColor3 = WHITE
SpamBtn.Font = Enum.Font.GothamBold
SpamBtn.TextSize = 15
SpamBtn.AutoButtonColor = false
SpamBtn.Parent = MainFrame
corner(SpamBtn, 12)
local sbStroke = Instance.new("UIStroke", SpamBtn)
sbStroke.Color = LGREEN; sbStroke.Thickness = 1.5
sbStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

SpamBtn.MouseButton1Down:Connect(function()
        TweenService:Create(SpamBtn, TweenInfo.new(0.07),
                {Size = UDim2.new(1,-24,0,44), Position = UDim2.new(0,12,0,222)}):Play()
end)
SpamBtn.MouseButton1Up:Connect(function()
        TweenService:Create(SpamBtn, TweenInfo.new(0.15, Enum.EasingStyle.Back),
                {Size = UDim2.new(1,-20,0,48), Position = UDim2.new(0,10,0,218)}):Play()
end)

-- توهج الزر الكبير
task.spawn(function()
        while SpamBtn and SpamBtn.Parent do
                local p = (math.sin(tick() * 3) + 1) / 2
                if spamming then
                        SpamBtn.BackgroundColor3 = Color3.fromRGB(0, math.floor(160+p*50), math.floor(50+p*30))
                else
                        SpamBtn.BackgroundColor3 = Color3.fromRGB(math.floor(160+p*60), 0, 0)
                end
                task.wait(0.04)
        end
end)

local function toggleSpam()
        if not spamming then
                local msg = MsgBox.Text
                if msg == "" then
                        SpamBtn.Text = "⚠️ اكتب رسالة أولاً!"
                        CircleBtn.Text = "!"
                        task.wait(1.5)
                        SpamBtn.Text = "🔴  ابدأ السبام"
                        CircleBtn.Text = "▶"
                        return
                end
                spamming = true
                SpamBtn.Text = "🟢  إيقاف السبام"
                CircleBtn.Text = "■"
                spamConn = task.spawn(function()
                        while spamming do
                                local m = MsgBox.Text
                                if m ~= "" then sendMsg(m) end
                                local d = math.max(0, spamDelay)
                                if d <= 0 then task.wait() else task.wait(d) end
                        end
                end)
        else
                spamming = false
                if spamConn then task.cancel(spamConn); spamConn = nil end
                SpamBtn.Text = "🔴  ابدأ السبام"
                CircleBtn.Text = "▶"
        end
end

SpamBtn.MouseButton1Click:Connect(toggleSpam)
CircleBtn.MouseButton1Click:Connect(toggleSpam)
