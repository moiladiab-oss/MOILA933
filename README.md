-- [[ ULTRA RED GLASSMORPHISM - MINI COMPACT VERSION WITH RGB TOGGLE BY MOILA933 ]] --

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")
local StarterGui = game:GetService("StarterGui")
local LocalPlayer = Players.LocalPlayer

-- [ واجهة البداية (Intro) ]
local IntroGui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
IntroGui.IgnoreGuiInset = true
local IntroFrame = Instance.new("Frame", IntroGui)
IntroFrame.Size = UDim2.new(1, 0, 1, 0)
IntroFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)

local DevLabel = Instance.new("TextLabel", IntroFrame)
DevLabel.Size = UDim2.new(0, 300, 0, 50)
DevLabel.Position = UDim2.new(0.5, -150, 0.5, -25)
DevLabel.BackgroundTransparency = 1
DevLabel.Text = "مطور السكربت: MOILA933 👑"
DevLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
DevLabel.Font = Enum.Font.GothamBold
DevLabel.TextSize = 25

local HintLabel = Instance.new("TextLabel", IntroFrame)
HintLabel.Size = UDim2.new(1, 0, 0, 30)
HintLabel.Position = UDim2.new(0, 0, 0.9, 0)
HintLabel.BackgroundTransparency = 1
HintLabel.Text = "انقر مرتين لإزالة الألترو"
HintLabel.TextColor3 = Color3.fromRGB(150, 150, 150)
HintLabel.Font = Enum.Font.Gotham
HintLabel.TextSize = 14

-- تحريك النص عشوائياً
task.spawn(function()
    while IntroGui and IntroGui.Parent do
        local randomX = math.random(0, 700) / 1000
        local randomY = math.random(0, 800) / 1000
        TweenService:Create(DevLabel, TweenInfo.new(2, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {Position = UDim2.new(randomX, -150, randomY, -25)}):Play()
        task.wait(2)
    end
end)

local clicks = 0
IntroFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        clicks = clicks + 1
        if clicks >= 2 then
            TweenService:Create(IntroFrame, TweenInfo.new(0.5), {BackgroundTransparency = 1}):Play()
            TweenService:Create(DevLabel, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
            TweenService:Create(HintLabel, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
            task.wait(0.5)
            IntroGui:Destroy()
        end
    end
end)

-- (باقي السكربت الأصلي يبدأ من هنا...)
local FoodRemote = ReplicatedStorage:WaitForChild("RemoteEvents", 5):WaitForChild("food", 5)
local HDAdminRemote = ReplicatedStorage:WaitForChild("HDAdminHDClient", 5):WaitForChild("Signals", 5):WaitForChild("RequestCommandModification", 5)
local TitleRemote = ReplicatedStorage:WaitForChild("ApplyTitle", 5)

-- 1. إنشاء الواجهة الأساسية (ScreenGui)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MOILA933_Mini_System"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

-- ... (تم الاحتفاظ بباقي الأكواد كما هي في طلبك السابق لتجنب أي أخطاء)
-- (ملاحظة: يمكنك لصق بقية الكود الخاص بك من هنا للأسفل)
