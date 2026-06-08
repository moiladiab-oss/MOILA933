-- [[ ULTRA RED GLASSMORPHISM - TURBO SPAM & RADIO EDITION BY MOILA933 ]] --

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

-- ريموتات الماب الرسمية المستخرجة
local FoodRemote = ReplicatedStorage:WaitForChild("RemoteEvents", 5):WaitForChild("food", 5)
local HDAdminRemote = ReplicatedStorage:WaitForChild("HDAdminHDClient", 5):WaitForChild("Signals", 5):WaitForChild("RequestCommandModification", 5)
local TitleRemote = ReplicatedStorage:WaitForChild("ApplyTitle", 5)
local RadioRemote = ReplicatedStorage:WaitForChild("RemoteEvents", 5):WaitForChild("PlaySong", 5) or ReplicatedStorage:WaitForChild("RemoteEvents", 5):WaitForChild("Radio", 5)

-- 1. إنشاء الواجهة الأساسية (ScreenGui)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MOILA933_Mini_System"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

-- 2. زر التشغيل الدائري المطور الملون (RGB Glowing Button)
local ToggleButton = Instance.new("TextButton")
ToggleButton.Name = "MO_Toggle"
ToggleButton.Size = UDim2.new(0, 55, 0, 55) 
ToggleButton.Position = UDim2.new(0, 20, 0.5, -27)
ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
ToggleButton.BackgroundTransparency = 0.2
ToggleButton.Text = "MO"
ToggleButton.TextColor3 = Color3.fromRGB(255, 20, 20)
ToggleButton.TextSize = 20
ToggleButton.Font = Enum.Font.GothamBold
ToggleButton.Active = true
ToggleButton.Draggable = true
ToggleButton.Parent = ScreenGui

local ToggleCorner = Instance.new("UICorner")
ToggleCorner.CornerRadius = UDim.new(1, 0)
ToggleCorner.Parent = ToggleButton

local ToggleStroke = Instance.new("UIStroke")
ToggleStroke.Thickness = 3
ToggleStroke.Color = Color3.fromRGB(255, 0, 0)
ToggleStroke.Parent = ToggleButton

task.spawn(function()
	local speed = 0.4
	while true do
		local hue = (tick() * speed) % 1
		local rgbColor = Color3.fromHSV(hue, 0.8, 0.8)
		ToggleButton.BackgroundColor3 = rgbColor
		ToggleStroke.Color = rgbColor
		local glowIntensity = 0.7 + (math.sin(tick() * 5) * 0.3)
		ToggleButton.TextColor3 = Color3.fromRGB(255 * glowIntensity, 0, 0)
		RunService.Heartbeat:Wait()
	end
end)

-- 3. الإطار الرئيسي الزجاجي المصغر (Mini Main Frame)
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 520, 0, 340)
MainFrame.Position = UDim2.new(0.5, -260, 0.5, -170)
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 3, 3)
MainFrame.BackgroundTransparency = 0.2
MainFrame.BorderSizePixel = 0
MainFrame.Visible = false
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 16)
MainCorner.Parent = MainFrame

local MainStroke = Instance.new("UIStroke")
MainStroke.Thickness = 2
MainStroke.Color = Color3.fromRGB(255, 30, 30)
MainStroke.Transparency = 0.3
MainStroke.Parent = MainFrame

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "☢️ MOILA933 Script maker ☢️"
Title.TextColor3 = Color3.fromRGB(255, 50, 50)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 15
Title.Parent = MainFrame

--- [ نظام الأزرار للتنقل بين الواجهات المحدث لـ 7 أقسام ]
local TabBar = Instance.new("Frame")
TabBar.Size = UDim2.new(1, -16, 0, 30)
TabBar.Position = UDim2.new(0, 8, 0, 40)
TabBar.BackgroundTransparency = 1
TabBar.Parent = MainFrame

local function createTabBtn(text, posPercent)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.135, -2, 1, 0)
    btn.Position = UDim2.new(posPercent, 0, 0, 0)
    btn.BackgroundColor3 = Color3.fromRGB(30, 5, 5)
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(180, 100, 100)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 8
    btn.Parent = TabBar
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 5)
    return btn
end

local Tab1Button = createTabBtn("الوصف✨️", 0.0)
Tab1Button.BackgroundColor3 = Color3.fromRGB(60, 10, 10)
Tab1Button.TextColor3 = Color3.fromRGB(255, 255, 255)

local Tab2Button = createTabBtn("سبام💥", 0.14)
local Tab3Button = createTabBtn("👤 سكنات✨", 0.28)
local Tab4Button = createTabBtn("🛡️ حماية", 0.42)
local Tab5Button = createTabBtn("التايتل✨️", 0.56)
local Tab6Button = createTabBtn("✍️ سبام خاص", 0.70)
local Tab7Button = createTabBtn("📻 الراديو🎵", 0.84) -- زر الراديو الجديد!

-- [ دالة الإرسال المباشر للسبام التوربو السريع ]
local function fireGiantPayload(giantMessage)
    if giantMessage == "" then return end
    local args = {[1] = giantMessage}
    
    -- إرسال مكرر مضاعف بنفس اللحظة لتفجير السرعة
    if FoodRemote and FoodRemote:IsA("RemoteEvent") then
        FoodRemote:FireServer(unpack(args))
        FoodRemote:FireServer(unpack(args))
    end
    if HDAdminRemote and HDAdminRemote:IsA("RemoteFunction") then
        task.spawn(function() HDAdminRemote:InvokeServer(unpack(args)) end)
        task.spawn(function() HDAdminRemote:InvokeServer(unpack(args)) end)
    end
end

-- [ الواجهة 3: السكنات ]
local Tab3Frame = Instance.new("Frame")
Tab3Frame.Size = UDim2.new(1, -24, 1, -85)
Tab3Frame.Position = UDim2.new(0, 12, 0, 75)
Tab3Frame.BackgroundTransparency = 1
Tab3Frame.Visible = false
Tab3Frame.Parent = MainFrame

local SkinsContainer = Instance.new("Frame")
SkinsContainer.Size = UDim2.new(1, 0, 1, 0)
SkinsContainer.BackgroundColor3 = Color3.fromRGB(10, 2, 2)
SkinsContainer.BackgroundTransparency = 0.6
SkinsContainer.Parent = Tab3Frame
Instance.new("UICorner", SkinsContainer).CornerRadius = UDim.new(0, 10)

local ButtonsGridFrame = Instance.new("Frame")
ButtonsGridFrame.Size = UDim2.new(1, -16, 1, -16)
ButtonsGridFrame.Position = UDim2.new(0, 8, 0, 8)
ButtonsGridFrame.BackgroundTransparency = 1
ButtonsGridFrame.Parent = SkinsContainer

local UIGridLayout = Instance.new("UIGridLayout")
UIGridLayout.CellSize = UDim2.new(0, 110, 0, 30)
UIGridLayout.CellPadding = UDim2.new(0, 6, 0, 6)
UIGridLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
UIGridLayout.VerticalAlignment = Enum.VerticalAlignment.Center
UIGridLayout.Parent = ButtonsGridFrame

local HiddenSkinData = {
	{Alias = "👦 سكن أولاد 1", Command = ";char me coreddddd_core"},
	{Alias = "👦 سكن أولاد 2", Command = ";char me xx_tr22"},
	{Alias = "👦 سكن أولاد 3", Command = ";char me Ahmad_00435A"},
	{Alias = "👦 سكن أولاد 4", Command = ";char me fh_556"},
	{Alias = "👧 سكن بنات 5", Command = ";char me Layanmunahi"},
	{Alias = "👧 سكن بنات 6", Command = ";char me malal_816"},
	{Alias = "👦 سكن أولاد 5", Command = ";char me lr_2e"},
	{Alias = "👦 سكن أولاد 6", Command = ";char me pa_989"},
	{Alias = "سكن shhode320", Command = ";char me shhode320"},
	{Alias = "سكن كرنج🎭", Command = ";char me lolo_yota1"},
	{Alias = "سكن بنات 1", Command = ";char me rrily7"},
	{Alias = "سكن اولاد 7", Command = ";char me omare3leloo"},
	{Alias = "بسة😂", Command = ";char me 3wwaass"},
	{Alias = "سكن رول1", Command = ";char me xd_99121"},
    {Alias = "R6 سكن لولد", Command = ";char me MR_MAHADA5678"},
    {Alias = "سكن أولاد", Command = ";char me saaaaa9924"},
    {Alias = "سكن بنات2", Command = ";char me alyazya366"},
    {Alias = "سكن بنات3", Command = ";char me youry754"}
}

for i = 1, #HiddenSkinData do
	local data = HiddenSkinData[i]
	local SkinButton = Instance.new("TextButton")
	SkinButton.BackgroundColor3 = Color3.fromRGB(45, 8, 8)
	SkinButton.Font = Enum.Font.GothamBold
	SkinButton.Text = data.Alias
	SkinButton.TextColor3 = Color3.fromRGB(255, 180, 180)
	SkinButton.TextSize = 10
	SkinButton.Parent = ButtonsGridFrame
	Instance.new("UICorner", SkinButton).CornerRadius = UDim.new(0, 6)
	
	SkinButton.MouseButton1Click:Connect(function()
		local command = data.Command
		task.spawn(function()
			pcall(function()
				game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("DataService"):FireServer(command)
			end)
		end)
		task.spawn(function()
			pcall(function()
				game:GetService("ReplicatedStorage"):WaitForChild("HDAdminHDClient"):WaitForChild("Signals"):WaitForChild("RequestCommandModification"):InvokeServer(command)
			end)
		end)
	end)
end

-- [ الواجهة 1: الوصف ]
local Tab1Frame = Instance.new("Frame")
Tab1Frame.Size = UDim2.new(1, -24, 1, -85)
Tab1Frame.Position = UDim2.new(0, 12, 0, 75)
Tab1Frame.BackgroundTransparency = 1
Tab1Frame.Visible = true
Tab1Frame.Parent = MainFrame

local DescLabel = Instance.new("TextLabel")
DescLabel.Size = UDim2.new(1, 0, 1, 0)
DescLabel.BackgroundTransparency = 0.6
DescLabel.BackgroundColor3 = Color3.fromRGB(10, 2, 2)
DescLabel.Text = "✨ بسم الله الرحمن الرحيم ✨\n\n👑 MOILA933 👑\n\nالسكربت تم تحديثه رسمياً لتسريع السبام لأقصى حد وإضافة خاصية الراديو الحصرية!\n\nوبس شكراً على استخدامكم المستمر للسكربت وعطونا رايكم بالتحديث السريع!✨️🫡"
DescLabel.TextColor3 = Color3.fromRGB(255, 200, 200)
DescLabel.Font = Enum.Font.GothamSemibold
DescLabel.TextSize = 12
DescLabel.TextWrapped = true
DescLabel.Parent = Tab1Frame
Instance.new("UICorner", DescLabel).CornerRadius = UDim.new(0, 10)

-- [ الواجهة 2: سبام الأوامر التوربو السريع ]
local Tab2Frame = Instance.new("Frame")
Tab2Frame.Size = UDim2.new(1, -24, 1, -85)
Tab2Frame.Position = UDim2.new(0, 12, 0, 75)
Tab2Frame.BackgroundTransparency = 1
Tab2Frame.Visible = false
Tab2Frame.Parent = MainFrame

local PlayersScroll = Instance.new("ScrollingFrame")
PlayersScroll.Size = UDim2.new(1, 0, 0, 45)
PlayersScroll.Position = UDim2.new(0, 0, 0, 0)
PlayersScroll.BackgroundTransparency = 0.85
PlayersScroll.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
PlayersScroll.BorderSizePixel = 0
PlayersScroll.CanvasSize = UDim2.new(3, 0, 0, 0)
PlayersScroll.ScrollBarThickness = 4
PlayersScroll.ScrollBarImageColor3 = Color3.fromRGB(255, 0, 0)
PlayersScroll.Parent = Tab2Frame

local ListLayout = Instance.new("UIListLayout")
ListLayout.FillDirection = Enum.FillDirection.Horizontal
ListLayout.SortOrder = Enum.SortOrder.Name
ListLayout.Padding = UDim.new(0, 8)
ListLayout.VerticalAlignment = Enum.VerticalAlignment.Center
ListLayout.Parent = PlayersScroll

local NameInput = Instance.new("TextBox")
NameInput.Size = UDim2.new(1, 0, 0, 38)
NameInput.Position = UDim2.new(0, 0, 0, 55)
NameInput.BackgroundColor3 = Color3.fromRGB(15, 3, 3)
NameInput.BackgroundTransparency = 0.4
NameInput.Text = ""
NameInput.PlaceholderText = "🎯 Select or Type Target Name..."
NameInput.TextColor3 = Color3.fromRGB(255, 255, 255)
NameInput.PlaceholderColor3 = Color3.fromRGB(180, 100, 100)
NameInput.Font = Enum.Font.GothamSemibold
NameInput.TextSize = 12
NameInput.Parent = Tab2Frame
Instance.new("UICorner", NameInput).CornerRadius = UDim.new(0, 10)

local ActionButton = Instance.new("TextButton")
ActionButton.Size = UDim2.new(1, 0, 0, 45)
ActionButton.Position = UDim2.new(0, 0, 0, 105)
ActionButton.BackgroundColor3 = Color3.fromRGB(140, 0, 0)
ActionButton.Font = Enum.Font.GothamBold
ActionButton.Text = "⚡ LAUNCH TURBO MOILA933 SYSTEM ⚡"
ActionButton.TextColor3 = Color3.fromRGB(255, 220, 220)
ActionButton.TextSize = 13
ActionButton.Parent = Tab2Frame
Instance.new("UICorner", ActionButton).CornerRadius = UDim.new(0, 12)

local isQuickSpamming = false
ActionButton.MouseButton1Click:Connect(function()
    local targetPlayer = NameInput.Text
    if targetPlayer == "" then return end
    isQuickSpamming = not isQuickSpamming
    if isQuickSpamming then
        ActionButton.Text = "🛑 إيقاف السبام السريع..."
        ActionButton.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
        task.spawn(function()
            local cmds = ";re ;nv ;res ;logs ;clogs ;kill ;re ;nv ;res ;logs ;clogs ;kill"
            local cmdList = {}
            for command in cmds:gmatch("%S+") do
                table.insert(cmdList, command .. " " .. targetPlayer)
            end
            local payload = table.concat(cmdList, " ")
            while isQuickSpamming do
                fireGiantPayload(payload)
                task.wait() -- تم تعديل السرعة لأقصى حد بدون تأخير غشيم!
            end
        end)
    else
        ActionButton.Text = "⚡ LAUNCH TURBO MOILA933 SYSTEM ⚡"
        ActionButton.BackgroundColor3 = Color3.fromRGB(140, 0, 0)
    end
end)

local SecondSpamButton = Instance.new("TextButton")
SecondSpamButton.Size = UDim2.new(1, 0, 0, 40)
SecondSpamButton.Position = UDim2.new(0, 0, 0, 155)
SecondSpamButton.BackgroundColor3 = Color3.fromRGB(80, 0, 0)
SecondSpamButton.Font = Enum.Font.GothamBold
SecondSpamButton.Text = "سبام الأوامر 2 السريع 🎭"
SecondSpamButton.TextColor3 = Color3.fromRGB(255, 200, 200)
SecondSpamButton.TextSize = 11
SecondSpamButton.Parent = Tab2Frame
Instance.new("UICorner", SecondSpamButton).CornerRadius = UDim.new(0, 8)

local isSecondSpamming = false
SecondSpamButton.MouseButton1Click:Connect(function()
    local targetPlayer = NameInput.Text
    if targetPlayer == "" then return end
    isSecondSpamming = not isSecondSpamming
    if isSecondSpamming then
        SecondSpamButton.Text = "🛑 إيقاف"
        task.spawn(function()
            local cmds = ";jump ;res ;char miri ;ice ;dog ;logs"
            local cmdList = {}
            for command in cmds:gmatch("%S+") do
                table.insert(cmdList, command .. " " .. targetPlayer)
            end
            local payload = table.concat(cmdList, " ")
            while isSecondSpamming do
                fireGiantPayload(payload)
                task.wait() -- سرعة قصوى
            end
        end)
    else
        SecondSpamButton.Text = "سبام الأوامر 2 السريع 🎭"
    end
end)

local function updatePlayerList()
	for _, child in pairs(PlayersScroll:GetChildren()) do if child:IsA("TextButton") then child:Destroy() end end
	for _, player in pairs(Players:GetPlayers()) do
		local pButton = Instance.new("TextButton")
		pButton.Size = UDim2.new(0, 95, 0, 30)
		pButton.BackgroundColor3 = Color3.fromRGB(60, 10, 10)
		pButton.Text = player.Name
		pButton.Font = Enum.Font.GothamSemibold
		pButton.TextSize = 10
		Instance.new("UICorner", pButton).CornerRadius = UDim.new(0, 6)
		pButton.MouseButton1Click:Connect(function() NameInput.Text = player.Name end)
		pButton.Parent = PlayersScroll
        
        task.spawn(function()
            while pButton and pButton.Parent do
                local hue = (tick() * 0.5) % 1
                pButton.TextColor3 = Color3.fromHSV(hue, 1, 1)
                task.wait(0.1)
            end
        end)
	end
end
Players.PlayerAdded:Connect(updatePlayerList)
Players.PlayerRemoving:Connect(updatePlayerList)
updatePlayerList()

-- [ الواجهة 4: الحماية ]
local Tab4Frame = Instance.new("Frame")
Tab4Frame.Size = UDim2.new(1, -24, 1, -85)
Tab4Frame.Position = UDim2.new(0, 12, 0, 75)
Tab4Frame.BackgroundTransparency = 1
Tab4Frame.Visible = false
Tab4Frame.Parent = MainFrame

local CleanerContainer = Instance.new("Frame")
CleanerContainer.Size = UDim2.new(1, 0, 1, 0)
CleanerContainer.BackgroundColor3 = Color3.fromRGB(10, 2, 2)
CleanerContainer.BackgroundTransparency = 0.6
CleanerContainer.Parent = Tab4Frame
Instance.new("UICorner", CleanerContainer).CornerRadius = UDim.new(0, 10)

local CleanerDescLabel = Instance.new("TextLabel")
CleanerDescLabel.Size = UDim2.new(1, -30, 0, 90)
CleanerDescLabel.Position = UDim2.new(0, 15, 0, 15)
CleanerDescLabel.BackgroundTransparency = 1
CleanerDescLabel.Text = "logs و clogs اذا ضغطت على الزر الي تحت رح تجيك حماية من"
CleanerDescLabel.TextColor3 = Color3.fromRGB(200, 255, 200)
CleanerDescLabel.Font = Enum.Font.GothamBold
CleanerDescLabel.TextSize = 13
CleanerDescLabel.TextWrapped = true
CleanerDescLabel.Parent = CleanerContainer

local StartCleanerButton = Instance.new("TextButton")
StartCleanerButton.Size = UDim2.new(0.8, 0, 0, 45)
StartCleanerButton.Position = UDim2.new(0.1, 0, 0.65, 0)
StartCleanerButton.BackgroundColor3 = Color3.fromRGB(15, 80, 15)
StartCleanerButton.Font = Enum.Font.GothamBold
StartCleanerButton.Text = "🛡️ ACTIVATE STEALTH MODE"
StartCleanerButton.TextColor3 = Color3.fromRGB(200, 255, 200)
StartCleanerButton.TextSize = 12
StartCleanerButton.Parent = CleanerContainer
Instance.new("UICorner", StartCleanerButton).CornerRadius = UDim.new(0, 10)

local cleanerActivated = false
StartCleanerButton.MouseButton1Click:Connect(function()
	if cleanerActivated then return end
	cleanerActivated = true
	StartCleanerButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
	StartCleanerButton.Text = "✅ STEALTH MODE IS RUNNING"
	StartCleanerButton.TextColor3 = Color3.fromRGB(150, 150, 150)
	local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")
	local TargetKeywords = {"admin", "cmd", "log", "console", "terminal", "adoni", "kohl"}
	local function cleanUI(guiObject)
		local name = guiObject.Name:lower()
		for _, keyword in ipairs(TargetKeywords) do
			if name:find(keyword) then
				if not name:find("shop") and not name:find("menu") then
					guiObject:Destroy()
					break
				end
			end
		end
	end
	for _, child in ipairs(PlayerGui:GetChildren()) do cleanUI(child) end
	PlayerGui.ChildAdded:Connect(cleanUI)
	task.spawn(function()
		while task.wait(1) do
			pcall(function() StarterGui:SetCore("DevConsoleVisible", false) end)
		end
	end)
end)

-- [ الواجهة 5: التايتل ]
local Tab5Frame = Instance.new("Frame")
Tab5Frame.Size = UDim2.new(1, -24, 1, -85)
Tab5Frame.Position = UDim2.new(0, 12, 0, 75)
Tab5Frame.BackgroundTransparency = 1
Tab5Frame.Visible = false
Tab5Frame.Parent = MainFrame

local TitleContainer = Instance.new("Frame")
TitleContainer.Size = UDim2.new(1, 0, 1, 0)
TitleContainer.BackgroundColor3 = Color3.fromRGB(10, 2, 2)
TitleContainer.BackgroundTransparency = 0.6
TitleContainer.Parent = Tab5Frame
Instance.new("UICorner", TitleContainer).CornerRadius = UDim.new(0, 10)

local TitleDescLabel = Instance.new("TextLabel")
TitleDescLabel.Size = UDim2.new(1, -30, 0, 45)
TitleDescLabel.Position = UDim2.new(0, 15, 0, 10)
TitleDescLabel.BackgroundTransparency = 1
TitleDescLabel.Text = "ملاحظة مهمة: ترا اذا كتبت سب رح يطلع حتى لو طويل لان هي خاصيته وشكراً🫡"
TitleDescLabel.TextColor3 = Color3.fromRGB(255, 100, 100)
TitleDescLabel.Font = Enum.Font.GothamBold
TitleDescLabel.TextSize = 12
TitleDescLabel.TextWrapped = true
TitleDescLabel.Parent = TitleContainer

local TitleInput = Instance.new("TextBox")
TitleInput.Size = UDim2.new(0.85, 0, 0, 38)
TitleInput.Position = UDim2.new(0.075, 0, 0.4, 0)
TitleInput.BackgroundColor3 = Color3.fromRGB(40, 0, 5)
TitleInput.BackgroundTransparency = 0.5
TitleInput.Font = Enum.Font.Gotham
TitleInput.PlaceholderText = "اكتب اللقب هنا..."
TitleInput.Text = ""
TitleInput.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleInput.PlaceholderColor3 = Color3.fromRGB(150, 100, 100)
TitleInput.TextSize = 13
TitleInput.Parent = TitleContainer
Instance.new("UICorner", TitleInput).CornerRadius = UDim.new(0, 6)

local ApplyButton = Instance.new("TextButton")
ApplyButton.Size = UDim2.new(0.85, 0, 0, 42)
ApplyButton.Position = UDim2.new(0.075, 0, 0.72, 0)
ApplyButton.BackgroundColor3 = Color3.fromRGB(180, 0, 30)
ApplyButton.Font = Enum.Font.GothamBold
ApplyButton.Text = "اضغط هنا لتفعيل الاسم💥"
ApplyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ApplyButton.TextSize = 13
ApplyButton.Parent = TitleContainer
Instance.new("UICorner", ApplyButton).CornerRadius = UDim.new(0, 6)

local rgbConnection = nil
local isRunning = false
ApplyButton.MouseButton1Click:Connect(function()
    local textToSend = TitleInput.Text
    if textToSend == "" then return end
    if rgbConnection then rgbConnection:Disconnect() end
    isRunning = true
    ApplyButton.Text = "تم التفعيل بنجاح! ⚡"
    task.delay(1.5, function() if isRunning then ApplyButton.Text = "تحديث اللقب" end end)
    local speed = 0.5 
    rgbConnection = RunService.Heartbeat:Connect(function()
        local hue = (tick() * speed) % 1
        local rgbColor = Color3.fromHSV(hue, 1, 1)
        local args = {[1] = textToSend, [2] = rgbColor}
        if TitleRemote then TitleRemote:FireServer(unpack(args)) end
    end)
end)

-- [ الواجهة 6: السبام الخاص التوربو ]
local Tab6Frame = Instance.new("Frame")
Tab6Frame.Size = UDim2.new(1, -24, 1, -85)
Tab6Frame.Position = UDim2.new(0, 12, 0, 75)
Tab6Frame.BackgroundTransparency = 1
Tab6Frame.Visible = false
Tab6Frame.Parent = MainFrame

local CustomSpamContainer = Instance.new("Frame")
CustomSpamContainer.Size = UDim2.new(1, 0, 1, 0)
CustomSpamContainer.BackgroundColor3 = Color3.fromRGB(10, 2, 2)
CustomSpamContainer.BackgroundTransparency = 0.6
CustomSpamContainer.Parent = Tab6Frame
Instance.new("UICorner", CustomSpamContainer).CornerRadius = UDim.new(0, 10)

local CustomInput = Instance.new("TextBox")
CustomInput.Size = UDim2.new(0.9, 0, 0, 50)
CustomInput.Position = UDim2.new(0.05, 0, 0.1, 0)
CustomInput.BackgroundColor3 = Color3.fromRGB(40, 0, 5)
CustomInput.BackgroundTransparency = 0.3
CustomInput.PlaceholderText = "أكتب هنا الي بدك ياه🫡"
CustomInput.Text = ""
CustomInput.TextColor3 = Color3.fromRGB(255, 255, 255)
CustomInput.Font = Enum.Font.Gotham
CustomInput.TextSize = 14
CustomInput.Parent = CustomSpamContainer
Instance.new("UICorner", CustomInput).CornerRadius = UDim.new(0, 8)

local CustomActionButton = Instance.new("TextButton")
CustomActionButton.Size = UDim2.new(0.9, 0, 0, 45)
CustomActionButton.Position = UDim2.new(0.05, 0, 0.55, 0)
CustomActionButton.BackgroundColor3 = Color3.fromRGB(140, 0, 0)
CustomActionButton.Text = "🚀 تفعيل السبام الخاص التوربو"
CustomActionButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CustomActionButton.Font = Enum.Font.GothamBold
CustomActionButton.Parent = CustomSpamContainer
Instance.new("UICorner", CustomActionButton).CornerRadius = UDim.new(0, 8)

local isCustomSpamming = false
CustomActionButton.MouseButton1Click:Connect(function()
    isCustomSpamming = not isCustomSpamming
    if isCustomSpamming then
        CustomActionButton.Text = "🛑 إيقاف"
        task.spawn(function()
            while isCustomSpamming do
                if HDAdminRemote and HDAdminRemote:IsA("RemoteFunction") then
                    local args = {[1] = CustomInput.Text}
                    HDAdminRemote:InvokeServer(unpack(args))
                end
                task.wait() -- سرعة فائقة جداً
            end
        end)
    else
        CustomActionButton.Text = "🚀 تفعيل السبام الخاص التوربو"
    end
end)

-- [ الواجهة 7: خاصية الراديو الجديدة بلمساتك واختيارك 📻 ]
local Tab7Frame = Instance.new("Frame")
Tab7Frame.Size = UDim2.new(1, -24, 1, -85)
Tab7Frame.Position = UDim2.new(0, 12, 0, 75)
Tab7Frame.BackgroundTransparency = 1
Tab7Frame.Visible = false
Tab7Frame.Parent = MainFrame

local RadioContainer = Instance.new("Frame")
RadioContainer.Size = UDim2.new(1, 0, 1, 0)
RadioContainer.BackgroundColor3 = Color3.fromRGB(10, 2, 2)
RadioContainer.BackgroundTransparency = 0.6
RadioContainer.Parent = Tab7Frame
Instance.new("UICorner", RadioContainer).CornerRadius = UDim.new(0, 10)

local RadioDescLabel = Instance.new("TextLabel")
RadioDescLabel.Size = UDim2.new(1, -30, 0, 40)
RadioDescLabel.Position = UDim2.new(0, 15, 0, 10)
RadioDescLabel.BackgroundTransparency = 1
RadioDescLabel.Text = "📻 نظام تشغيل راديو الماب - اكتب الـ ID وسَمّع السيرفر!"
RadioDescLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
RadioDescLabel.Font = Enum.Font.GothamBold
RadioDescLabel.TextSize = 12
RadioDescLabel.Parent = RadioContainer

local MusicInput = Instance.new("TextBox")
MusicInput.Size = UDim2.new(0.85, 0, 0, 38)
MusicInput.Position = UDim2.new(0.075, 0, 0.35, 0)
MusicInput.BackgroundColor3 = Color3.fromRGB(40, 0, 5)
MusicInput.BackgroundTransparency = 0.5
MusicInput.Font = Enum.Font.Gotham
MusicInput.PlaceholderText = "اكتب هنا ID الأغنية (مثال: 1837419)..."
MusicInput.Text = ""
MusicInput.TextColor3 = Color3.fromRGB(255, 255, 255)
MusicInput.PlaceholderColor3 = Color3.fromRGB(150, 100, 100)
MusicInput.TextSize = 13
MusicInput.Parent = RadioContainer
Instance.new("UICorner", MusicInput).CornerRadius = UDim.new(0, 6)

local PlayMusicButton = Instance.new("TextButton")
PlayMusicButton.Size = UDim2.new(0.85, 0, 0, 42)
PlayMusicButton.Position = UDim2.new(0.075, 0, 0.68, 0)
PlayMusicButton.BackgroundColor3 = Color3.fromRGB(0, 120, 30)
PlayMusicButton.Font = Enum.Font.GothamBold
PlayMusicButton.Text = "🎵 تشغيل الصوت بالسيرفر"
PlayMusicButton.TextColor3 = Color3.fromRGB(255, 255, 255)
PlayMusicButton.TextSize = 13
PlayMusicButton.Parent = RadioContainer
Instance.new("UICorner", PlayMusicButton).CornerRadius = UDim.new(0, 6)

PlayMusicButton.MouseButton1Click:Connect(function()
    local songID = MusicInput.Text
    if songID == "" then return end
    pcall(function()
        if RadioRemote then
            RadioRemote:FireServer(tonumber(songID) or songID)
        else
            -- تجربة إرسال عبر الشات العادي كـ خيار احتياطي لو الريموت محمي
            game:GetService("ReplicatedStorage"):WaitForChild("DefaultChatSystemChatEvents"):WaitForChild("SayMessageRequest"):FireServer(";music " .. songID, "All")
        end
    end)
    PlayMusicButton.Text = "🔊 جاري التشغيل..."
    task.delay(1, function() PlayMusicButton.Text = "🎵 تشغيل الصوت بالسيرفر" end)
end)

-- [ منطق التنقل بين الواجهات السبعة ]
local function resetTabs()
	Tab1Frame.Visible = false; Tab2Frame.Visible = false; Tab3Frame.Visible = false; Tab4Frame.Visible = false; Tab5Frame.Visible = false; Tab6Frame.Visible = false; Tab7Frame.Visible = false
	local btns = {Tab1Button, Tab2Button, Tab3Button, Tab4Button, Tab5Button, Tab6Button, Tab7Button}
	for _, btn in pairs(btns) do
		btn.BackgroundColor3 = Color3.fromRGB(30, 5, 5)
		btn.TextColor3 = Color3.fromRGB(180, 100, 100)
	end
end

Tab1Button.MouseButton1Click:Connect(function() resetTabs(); Tab1Frame.Visible = true; Tab1Button.BackgroundColor3 = Color3.fromRGB(60, 10, 10); Tab1Button.TextColor3 = Color3.fromRGB(255, 255, 255) end)
Tab2Button.MouseButton1Click:Connect(function() resetTabs(); Tab2Frame.Visible = true; Tab2Button.BackgroundColor3 = Color3.fromRGB(60, 10, 10); Tab2Button.TextColor3 = Color3.fromRGB(255, 255, 255) end)
Tab3Button.MouseButton1Click:Connect(function() resetTabs(); Tab3Frame.Visible = true; Tab3Button.BackgroundColor3 = Color3.fromRGB(60, 10, 10); Tab3Button.TextColor3 = Color3.fromRGB(255, 255, 255) end)
Tab4Button.MouseButton1Click:Connect(function() resetTabs(); Tab4Frame.Visible = true; Tab4Button.BackgroundColor3 = Color3.fromRGB(60, 10, 10); Tab4Button.TextColor3 = Color3.fromRGB(255, 255, 255) end)
Tab5Button.MouseButton1Click:Connect(function() resetTabs(); Tab5Frame.Visible = true; Tab5Button.BackgroundColor3 = Color3.fromRGB(60, 10, 10); Tab5Button.TextColor3 = Color3.fromRGB(255, 255, 255) end)
Tab6Button.MouseButton1Click:Connect(function() resetTabs(); Tab6Frame.Visible = true; Tab6Button.BackgroundColor3 = Color3.fromRGB(60, 10, 10); Tab6Button.TextColor3 = Color3.fromRGB(255, 255, 255) end)
Tab7Button.MouseButton1Click:Connect(function() resetTabs(); Tab7Frame.Visible = true; Tab7Button.BackgroundColor3 = Color3.fromRGB(60, 10, 10); Tab7Button.TextColor3 = Color3.fromRGB(255, 255, 255) end)

ToggleButton.MouseButton1Click:Connect(function() MainFrame.Visible = not MainFrame.Visible end)

-- [ الترحيب عند بداية التشغيل المحدث ]
local welcomeShown = false
ToggleButton.MouseButton1Click:Connect(function()
    if not welcomeShown then
        welcomeShown = true
        local WelcomeGui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
        local WelcomeFrame = Instance.new("Frame", WelcomeGui)
        WelcomeFrame.Size = UDim2.new(0, 300, 0, 250); WelcomeFrame.Position = UDim2.new(0.5, -150, -0.5, 0)
        WelcomeFrame.BackgroundColor3 = Color3.fromRGB(20, 3, 3); WelcomeFrame.BackgroundTransparency = 0.2; WelcomeFrame.BorderSizePixel = 0
        Instance.new("UICorner", WelcomeFrame).CornerRadius = UDim.new(0, 16); Instance.new("UIStroke", WelcomeFrame).Color = Color3.fromRGB(255, 30, 30)
        Instance.new("TextLabel", WelcomeFrame).Name = "Title"; local T = WelcomeFrame.Title; T.Size = UDim2.new(1, 0, 0, 40); T.BackgroundTransparency = 1; T.Text = "🔥 تم إطلاق التحديث 🔥"; T.TextColor3 = Color3.fromRGB(255, 50, 50); T.Font = Enum.Font.GothamBold; T.TextSize = 18
        Instance.new("TextLabel", WelcomeFrame).Name = "Desc"; local D = WelcomeFrame.Desc; D.Size = UDim2.new(0.9, 0, 0.5, 0); D.Position = UDim2.new(0.05, 0, 0.2, 0); D.BackgroundTransparency = 1; D.Text = "يا هلا خويي! تم تسريع السبام للتوربو الناري وإضافة ميزة تشغيل الراديو بنجاح! انشرو السكربت وادعمونا وشكراً من القلب❤️🫡"; D.TextColor3 = Color3.fromRGB(255, 200, 200); D.Font = Enum.Font.GothamSemibold; D.TextSize = 14; D.TextWrapped = true
        Instance.new("TextButton", WelcomeFrame).Name = "Close"; local C = WelcomeFrame.Close; C.Size = UDim2.new(0.6, 0, 0, 40); C.Position = UDim2.new(0.2, 0, 0.75, 0); C.BackgroundColor3 = Color3.fromRGB(140, 0, 0); C.Text = "كفوووو🫡🔥"; C.TextColor3 = Color3.fromRGB(255, 255, 255); C.Font = Enum.Font.GothamBold; Instance.new("UICorner", C).CornerRadius = UDim.new(0, 8)
        C.MouseButton1Click:Connect(function() WelcomeGui:Destroy() end)
        TweenService:Create(WelcomeFrame, TweenInfo.new(0.8, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out), {Position = UDim2.new(0.5, -150, 0.5, -125)}):Play()
    end
end)

-- [ نظام الإعلان الدوري - يظهر كل دقيقتين (120 ثانية) ]
task.spawn(function()
    task.wait(2) 
    while true do
        local NotifGui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
        local NotifFrame = Instance.new("Frame", NotifGui)
        NotifFrame.Size = UDim2.new(0, 350, 0, 120); NotifFrame.Position = UDim2.new(0.5, -175, 0.8, 0); NotifFrame.BackgroundColor3 = Color3.fromRGB(20, 3, 3); NotifFrame.BackgroundTransparency = 0.2
        Instance.new("UICorner", NotifFrame).CornerRadius = UDim.new(0, 12); Instance.new("UIStroke", NotifFrame).Color = Color3.fromRGB(255, 30, 30)
        
        local ImageContainer = Instance.new("ImageLabel", NotifFrame)
        ImageContainer.Size = UDim2.new(0, 90, 0, 90); ImageContainer.Position = UDim2.new(0.72, 0, 0.12, 0); ImageContainer.Image = "rbxassetid://123456789"; ImageContainer.BackgroundTransparency = 1
        Instance.new("UICorner", ImageContainer).CornerRadius = UDim.new(1, 0)
        
        local TextLabel = Instance.new("TextLabel", NotifFrame)
        TextLabel.Size = UDim2.new(0.65, 0, 1, 0); TextLabel.Position = UDim2.new(0.03, 0, 0, 0); TextLabel.BackgroundTransparency = 1; TextLabel.Text = "مصمم السكربت🫡💥\nتم إضافة نظام راديو متطور وتوربو سبام حارق.\nيلي بده السكربتات الجديدة يبعت طلب moila933 وبس شكراً🫡"; TextLabel.TextColor3 = Color3.new(1,1,1); TextLabel.Font = Enum.Font.GothamBold; TextLabel.TextSize = 12; TextLabel.TextWrapped = true
        
        NotifFrame.Position = UDim2.new(0.5, -175, 1.2, 0)
        TweenService:Create(NotifFrame, TweenInfo.new(0.5), {Position = UDim2.new(0.5, -175, 0.8, 0)}):Play()
        task.wait(5); TweenService:Create(NotifFrame, TweenInfo.new(0.5), {Position = UDim2.new(0.5, -175, 1.2, 0)}):Play(); task.wait(0.5); NotifGui:Destroy()
        
        task.wait(120) 
    end
end)
