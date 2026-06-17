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
PausedLbl.Text = "⏸️ تم إيقاف السكربت مؤقتاً"
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

