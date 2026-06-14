-- [[ MO HUB INTRO SCRIPT FOR DELTA ]] --

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local CoreGui = game:GetService("CoreGui")
local TargetParent = CoreGui or LocalPlayer:WaitForChild("PlayerGui")

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MO_HUB_IntroGui"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.DisplayOrder = 2147483647
ScreenGui.Parent = TargetParent

local Background = Instance.new("Frame")
Background.Size = UDim2.new(1, 0, 1, 0)
Background.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Background.BorderSizePixel = 0
Background.Parent = ScreenGui

local IntroSound = Instance.new("Sound")
IntroSound.SoundId = "rbxassetid://1841683877"
IntroSound.TimePosition = 0
IntroSound.Volume = 1
IntroSound.Parent = ScreenGui

local ImageLabel = Instance.new("ImageLabel")
ImageLabel.Size = UDim2.new(0, 200, 0, 200)
ImageLabel.Position = UDim2.new(0.5, -100, 0.5, -100)
ImageLabel.BackgroundTransparency = 1
ImageLabel.Image = "rbxassetid://96306504246987"
ImageLabel.ImageTransparency = 1
ImageLabel.Parent = Background

local FlashFrame = Instance.new("Frame")
FlashFrame.Size = UDim2.new(1, 0, 1, 0)
FlashFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
FlashFrame.BackgroundTransparency = 1
FlashFrame.BorderSizePixel = 0
FlashFrame.ZIndex = 2
FlashFrame.Parent = Background

local TextLabel = Instance.new("TextLabel")
TextLabel.Size = UDim2.new(1, 0, 0, 100)
TextLabel.Position = UDim2.new(0, 0, 0.5, -50)
TextLabel.BackgroundTransparency = 1
TextLabel.Text = "MO TOP 1"
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.TextSize = 50
TextLabel.Font = Enum.Font.Code
TextLabel.TextTransparency = 1
TextLabel.Parent = Background

local SkipHintLabel = Instance.new("TextLabel")
SkipHintLabel.Size = UDim2.new(1, 0, 0, 50)
SkipHintLabel.Position = UDim2.new(0, 0, 1, -60)
SkipHintLabel.BackgroundTransparency = 1
SkipHintLabel.Text = "اضغط مرتين لتخطي الإنترو"
SkipHintLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
SkipHintLabel.TextSize = 16
SkipHintLabel.Font = Enum.Font.Code
SkipHintLabel.TextTransparency = 0.4
SkipHintLabel.ZIndex = 11
SkipHintLabel.Parent = Background

local GlitchFrame = Instance.new("Frame")
GlitchFrame.Size = UDim2.new(1, 0, 1, 0)
GlitchFrame.BackgroundTransparency = 1
GlitchFrame.BorderSizePixel = 0
GlitchFrame.Parent = Background

local SkipButton = Instance.new("TextButton")
SkipButton.Size = UDim2.new(1, 0, 1, 0)
SkipButton.BackgroundTransparency = 1
SkipButton.Text = ""
SkipButton.ZIndex = 10
SkipButton.Parent = Background

local function createGlitchLine()
	if not GlitchFrame or not GlitchFrame.Parent then return end
	local line = Instance.new("Frame")
	line.Size = UDim2.new(1, 0, 0, math.random(5, 20))
	line.Position = UDim2.new(0, 0, math.random(0, 90)/100, 0)
	local colors = {Color3.fromRGB(255,0,0), Color3.fromRGB(0,255,0), Color3.fromRGB(0,0,255), Color3.fromRGB(255,0,255)}
	line.BackgroundColor3 = colors[math.random(1, #colors)]
	line.BorderSizePixel = 0
	line.Parent = GlitchFrame
	game:GetService("Debris"):AddItem(line, 0.1)
end

local isSkipped = false
local lastClick = 0

local function skipIntro()
	if isSkipped then return end
	isSkipped = true
	if ImageLabel then ImageLabel:Destroy() end
	if FlashFrame then FlashFrame:Destroy() end
	if TextLabel then TextLabel:Destroy() end
	if SkipHintLabel then SkipHintLabel:Destroy() end
	if GlitchFrame then GlitchFrame:Destroy() end
	if SkipButton then SkipButton:Destroy() end
	TweenService:Create(IntroSound, TweenInfo.new(0.5), {Volume = 0}):Play()
	TweenService:Create(Background, TweenInfo.new(0.5), {BackgroundTransparency = 1}):Play()
	task.wait(0.5)
	IntroSound:Stop()
	ScreenGui:Destroy()
end

SkipButton.MouseButton1Click:Connect(function()
	local currentTime = os.clock()
	if currentTime - lastClick < 0.4 then
		skipIntro()
	end
	lastClick = currentTime
end)

task.wait(1)
if isSkipped then return end

IntroSound:Play()
TweenService:Create(ImageLabel, TweenInfo.new(1), {ImageTransparency = 0}):Play()

local startTime = os.time()
local flashColors = {Color3.fromRGB(255,0,0), Color3.fromRGB(0,255,0), Color3.fromRGB(0,0,255), Color3.fromRGB(255,255,0), Color3.fromRGB(255,0,255), Color3.fromRGB(0,255,255)}

while os.time() - startTime < 6 and not isSkipped do
	if ImageLabel and ImageLabel.Parent then
		ImageLabel:TweenSize(UDim2.new(0, 230, 0, 230), "Out", "Quad", 0.15, true)
	end
	if FlashFrame and FlashFrame.Parent then
		FlashFrame.BackgroundColor3 = flashColors[math.random(1, #flashColors)]
		FlashFrame.BackgroundTransparency = 0.65
	end
	task.wait(0.1)
	if FlashFrame and FlashFrame.Parent then
		FlashFrame.BackgroundTransparency = 1
	end
	if ImageLabel and ImageLabel.Parent then
		ImageLabel:TweenSize(UDim2.new(0, 200, 0, 200), "In", "Quad", 0.15, true)
	end
	task.wait(0.4)
end

if isSkipped then return end

if ImageLabel then ImageLabel:Destroy() end
if FlashFrame then FlashFrame:Destroy() end

TweenService:Create(TextLabel, TweenInfo.new(0.5), {TextTransparency = 0}):Play()

local textWait = os.clock()
while os.clock() - textWait < 2 and not isSkipped do task.wait(0.1) end

if isSkipped then return end

local glitchTime = os.time()
while os.time() - glitchTime < 2 and not isSkipped do
	createGlitchLine()
	if TextLabel and TextLabel.Parent then
		TextLabel.Position = UDim2.new(0, math.random(-10, 10), 0.5, math.random(-55, -45))
		TextLabel.TextColor3 = Color3.fromRGB(math.random(0,255), math.random(0,255), math.random(0,255))
	end
	task.wait(0.05)
end

if isSkipped then return end

if TextLabel then TextLabel:Destroy() end
if SkipHintLabel then SkipHintLabel:Destroy() end
if GlitchFrame then GlitchFrame:Destroy() end
if SkipButton then SkipButton:Destroy() end

Background.BackgroundColor3 = Color3.fromRGB(5, 10, 25)
task.wait(0.5)

if isSkipped then return end

TweenService:Create(IntroSound, TweenInfo.new(1), {Volume = 0}):Play()
TweenService:Create(Background, TweenInfo.new(1), {BackgroundTransparency = 1}):Play()
task.wait(1)

IntroSound:Stop()
ScreenGui:Destroy()


-- [[ ULTRA BLUE GLASSMORPHISM - MOILA HUBBB TOTAL SYSTEM ]] --

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")
local StarterGui = game:GetService("StarterGui")
local UIS = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer
local player = LocalPlayer

local spamming = false
local selectedTarget = "الكل"

-- ====== BLUE & BLACK PULSING COLOR PALETTE ======
local BLUE_A  = Color3.fromRGB(30, 100, 255)
local BLUE_B  = Color3.fromRGB(10, 40, 160)
local DARK    = Color3.fromRGB(3, 5, 22)
local WHITE   = Color3.fromRGB(255, 255, 255)

local soundPalette = {
	{Color3.fromRGB(20, 70, 200), Color3.fromRGB(10, 40, 130)},
	{Color3.fromRGB(30, 90, 230), Color3.fromRGB(15, 50, 150)},
	{Color3.fromRGB(15, 60, 180), Color3.fromRGB(8, 35, 120)},
	{Color3.fromRGB(40, 110, 255), Color3.fromRGB(20, 60, 170)},
}

local function getSoundRemote()
	local gui = LocalPlayer.PlayerGui:FindFirstChild("MountedGui")
	if gui then
		for _, v in pairs(gui:GetDescendants()) do
			if v.Name == "Remote" and v:IsA("RemoteEvent") then
				return v
			end
		end
	end
end

local function fireSoundRemote(target, code)
	local r = getSoundRemote()
	if not r then return end
	if target == "الكل" then
		for _, p in pairs(Players:GetPlayers()) do
			r:FireServer(p, code)
		end
	else
		local p = Players:FindFirstChild(target)
		if p then r:FireServer(p, code) end
	end
end

local FoodRemote = ReplicatedStorage:WaitForChild("RemoteEvents", 5):WaitForChild("food", 5)
local HDAdminRemote = ReplicatedStorage:WaitForChild("HDAdminHDClient", 5):WaitForChild("Signals", 5):WaitForChild("RequestCommandModification", 5)
local TitleRemote = ReplicatedStorage:WaitForChild("ApplyTitle", 5)
local DataServiceRemote = ReplicatedStorage:WaitForChild("RemoteEvents", 5):WaitForChild("DataService", 5)

local function fireTextPayload(msg)
	if msg == "" then return end
	local args = {[1] = msg}
	if DataServiceRemote and DataServiceRemote:IsA("RemoteEvent") then
		DataServiceRemote:FireServer(unpack(args))
	end
	if FoodRemote and FoodRemote:IsA("RemoteEvent") then
		FoodRemote:FireServer(unpack(args))
	end
	if HDAdminRemote and (HDAdminRemote:IsA("RemoteEvent") or HDAdminRemote:IsA("RemoteFunction")) then
		task.spawn(function()
			if HDAdminRemote:IsA("RemoteFunction") then
				HDAdminRemote:InvokeServer(unpack(args))
			else
				HDAdminRemote:FireServer(unpack(args))
			end
		end)
	end
end

local chatEvent = nil
local remoteEvents = ReplicatedStorage:FindFirstChild("RemoteEvents")
if remoteEvents then
	chatEvent = remoteEvents:FindFirstChild("ChatEvent")
end
if not chatEvent then
	for _, v in pairs(ReplicatedStorage:GetDescendants()) do
		if v.Name == "ChatEvent" and v:IsA("RemoteEvent") then
			chatEvent = v
			break
		end
	end
end

local execSignal = nil
local hdClient = ReplicatedStorage:FindFirstChild("HDAdminHDClient")
if hdClient and hdClient:FindFirstChild("Signals") then
	execSignal = hdClient.Signals:FindFirstChild("RequestCommandModification")
end

local function deleteNightVision()
	local hd = ReplicatedStorage:FindFirstChild("HDAdminHDClient")
	if hd then
		local assets = hd:FindFirstChild("Assets")
		if assets then
			local nightVision = assets:FindFirstChild("NightVision")
			if nightVision then nightVision:Destroy(); return true end
		end
	end
	return false
end

local function deleteHDInterface()
	local playerGui = player:FindFirstChild("PlayerGui")
	if playerGui then
		local hdInterface = playerGui:FindFirstChild("HDAdminInterface")
		if hdInterface then hdInterface:Destroy(); return true end
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
	s.Color = col
	s.Thickness = t or 1
	s.Transparency = trans or 0
	s.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	return s
end

local function whiteText(lbl)
	lbl.TextColor3 = WHITE
	lbl.TextStrokeColor3 = Color3.fromRGB(0, 0, 0)
	lbl.TextStrokeTransparency = 0.55
end

local function hoverScale(btn)
	local baseSize = btn.Size
	btn.MouseEnter:Connect(function()
		TweenService:Create(btn, TweenInfo.new(0.18, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
			{Size = UDim2.new(baseSize.X.Scale, baseSize.X.Offset, baseSize.Y.Scale, baseSize.Y.Offset + 2)}):Play()
	end)
	btn.MouseLeave:Connect(function()
		TweenService:Create(btn, TweenInfo.new(0.18, Enum.EasingStyle.Quad), {Size = baseSize}):Play()
	end)
	btn.MouseButton1Down:Connect(function()
		TweenService:Create(btn, TweenInfo.new(0.08), {Size = UDim2.new(baseSize.X.Scale, baseSize.X.Offset - 2, baseSize.Y.Scale, baseSize.Y.Offset - 2)}):Play()
	end)
	btn.MouseButton1Up:Connect(function()
		TweenService:Create(btn, TweenInfo.new(0.18, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {Size = baseSize}):Play()
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
		rip.AnchorPoint = Vector2.new(0.5, 0.5)
		rip.Position = UDim2.new(0, m.X - abs.X, 0, m.Y - abs.Y)
		rip.Size = UDim2.new(0, 0, 0, 0)
		corner(rip, 999)
		local size = math.max(btn.AbsoluteSize.X, btn.AbsoluteSize.Y) * 2
		TweenService:Create(rip, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
			{Size = UDim2.new(0, size, 0, size), BackgroundTransparency = 1}):Play()
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
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = input.Position
			startPos = frame.Position
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then dragging = false end
			end)
		end
	end)
	dragHandle.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)
	UIS.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			local delta = input.Position - dragStart
			frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
		end
	end)
end

-- ====== TOGGLE BUTTON ======
local ToggleButton = Instance.new("TextButton")
ToggleButton.Name = "MO_Toggle"
ToggleButton.Size = UDim2.new(0, 55, 0, 55)
ToggleButton.Position = UDim2.new(0, 20, 0.5, -27)
ToggleButton.BackgroundColor3 = BLUE_A
ToggleButton.BackgroundTransparency = 0.2
ToggleButton.Text = "MO"
ToggleButton.TextColor3 = WHITE
ToggleButton.TextSize = 20
ToggleButton.Font = Enum.Font.GothamBold
ToggleButton.Active = true
ToggleButton.Parent = ScreenGui

local ToggleCorner = Instance.new("UICorner")
ToggleCorner.CornerRadius = UDim.new(1, 0)
ToggleCorner.Parent = ToggleButton

local ToggleStroke = Instance.new("UIStroke")
ToggleStroke.Thickness = 3
ToggleStroke.Color = BLUE_A
ToggleStroke.Parent = ToggleButton

makeDraggable(ToggleButton)

task.spawn(function()
	while true do
		local t = tick()
		local pulse = (math.sin(t * 2.5) + 1) / 2
		local r = math.floor(10 + pulse * 20)
		local g = math.floor(60 + pulse * 80)
		local b = math.floor(180 + pulse * 75)
		local blueColor = Color3.fromRGB(r, g, b)
		ToggleButton.BackgroundColor3 = blueColor
		ToggleStroke.Color = blueColor
		local whitePulse = (math.sin(t * 2.5 + 1) + 1) / 2
		local wVal = math.floor(180 + whitePulse * 75)
		ToggleButton.TextColor3 = Color3.fromRGB(wVal, wVal, wVal)
		RunService.Heartbeat:Wait()
	end
end)

-- ====== MAIN FRAME (مكبّرة) ======
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 640, 0, 430)
MainFrame.Position = UDim2.new(0.5, -320, 0.5, -215)
MainFrame.BackgroundColor3 = DARK
MainFrame.BackgroundTransparency = 0.15
MainFrame.BorderSizePixel = 0
MainFrame.Visible = false
MainFrame.Active = true
MainFrame.Parent = ScreenGui

corner(MainFrame, 16)

local MainStroke = Instance.new("UIStroke")
MainStroke.Color = WHITE
MainStroke.Thickness = 2
MainStroke.Transparency = 0.3
MainStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
MainStroke.Parent = MainFrame

task.spawn(function()
	while true do
		local t = tick()
		local pulse = (math.sin(t * 2) + 1) / 2
		MainStroke.Transparency = 0.1 + pulse * 0.7
		task.wait(0.03)
	end
end)

makeDraggable(MainFrame)

-- عنوان الواجهة
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -50, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "☢️ MOILA933 Script maker ☢️"
Title.TextColor3 = Color3.fromRGB(80, 160, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 15
Title.Parent = MainFrame

-- ====== زر الإغلاق (X) على يمين الواجهة ======
local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 32, 0, 32)
CloseButton.Position = UDim2.new(1, -38, 0, 4)
CloseButton.BackgroundColor3 = Color3.fromRGB(180, 30, 30)
CloseButton.Text = "✕"
CloseButton.TextColor3 = WHITE
CloseButton.TextSize = 16
CloseButton.Font = Enum.Font.GothamBold
CloseButton.AutoButtonColor = false
CloseButton.BorderSizePixel = 0
CloseButton.ZIndex = 10
CloseButton.Parent = MainFrame
corner(CloseButton, 8)
stroke(CloseButton, WHITE, 1, 0.5)

-- تأثير hover على زر الإغلاق
CloseButton.MouseEnter:Connect(function()
	TweenService:Create(CloseButton, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(220, 50, 50)}):Play()
end)
CloseButton.MouseLeave:Connect(function()
	TweenService:Create(CloseButton, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(180, 30, 30)}):Play()
end)
CloseButton.MouseButton1Click:Connect(function()
	TweenService:Create(MainFrame, TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.In),
		{Size = UDim2.new(0, 0, 0, 0), Position = UDim2.new(0.5, 0, 0.5, 0)}):Play()
	task.wait(0.3)
	ScreenGui:Destroy()
end)

-- ====== TAB BAR (8 تابات بعد حذف التاسع) ======
local TabBar = Instance.new("Frame")
TabBar.Size = UDim2.new(1, -16, 0, 30)
TabBar.Position = UDim2.new(0, 8, 0, 42)
TabBar.BackgroundTransparency = 1
TabBar.Parent = MainFrame

-- عرض كل تاب = 1/8 = 0.125
local function createTabBtn(text, posPercent)
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(0.125, -2, 1, 0)
	btn.Position = UDim2.new(posPercent, 0, 0, 0)
	btn.BackgroundColor3 = Color3.fromRGB(5, 10, 35)
	btn.Text = text
	btn.TextColor3 = Color3.fromRGB(80, 140, 220)
	btn.Font = Enum.Font.GothamBold
	btn.TextSize = 8
	btn.Parent = TabBar
	corner(btn, 6)
	local tabStroke = Instance.new("UIStroke")
	tabStroke.Color = WHITE
	tabStroke.Thickness = 1
	tabStroke.Transparency = 0.7
	tabStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	tabStroke.Parent = btn
	task.spawn(function()
		while btn and btn.Parent do
			local t = tick()
			local pulse = (math.sin(t * 2.5 + posPercent * 6) + 1) / 2
			tabStroke.Transparency = 0.4 + pulse * 0.55
			task.wait(0.04)
		end
	end)
	return btn
end

local Tab1Button = createTabBtn("الوصف✨", 0.000)
Tab1Button.BackgroundColor3 = Color3.fromRGB(10, 25, 70)
Tab1Button.TextColor3 = WHITE

local Tab2Button = createTabBtn("نسخ تحديث📋", 0.125)
local Tab3Button = createTabBtn("سكنات👤", 0.250)
local Tab4Button = createTabBtn("حماية logs🛡️", 0.375)
local Tab5Button = createTabBtn("الاسم✨", 0.500)
local Tab6Button = createTabBtn("سبام مخفي✍️", 0.625)
local Tab7Button = createTabBtn("حماية nv🛡️", 0.750)
local Tab8Button = createTabBtn("الراديو🎧", 0.875)

local function createContainerFrame()
	local f = Instance.new("Frame")
	f.Size = UDim2.new(1, -24, 1, -88)
	f.Position = UDim2.new(0, 12, 0, 78)
	f.BackgroundTransparency = 1
	f.Visible = false
	f.Parent = MainFrame
	return f
end

local function makeTabContainer(parent)
	local f = Instance.new("Frame")
	f.Size = UDim2.new(1, 0, 1, 0)
	f.BackgroundColor3 = DARK
	f.BackgroundTransparency = 0.5
	f.Parent = parent
	corner(f, 10)
	local cs = Instance.new("UIStroke")
	cs.Color = WHITE
	cs.Thickness = 1.5
	cs.Transparency = 0.5
	cs.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	cs.Parent = f
	local bg = Instance.new("UIGradient")
	bg.Color = ColorSequence.new(Color3.fromRGB(5, 10, 40), Color3.fromRGB(3, 5, 20))
	bg.Rotation = 135
	bg.Parent = f
	task.spawn(function()
		while f and f.Parent do
			local t = tick()
			local pulse = (math.sin(t * 1.8) + 1) / 2
			cs.Transparency = 0.2 + pulse * 0.65
			f.BackgroundColor3 = Color3.fromRGB(
				math.floor(3 + pulse * 8),
				math.floor(5 + pulse * 15),
				math.floor(20 + pulse * 30)
			)
			task.wait(0.04)
		end
	end)
	return f
end

-- ====== TAB 1 - الوصف (مُحدث مع الأزرار) ======
local Tab1Frame = createContainerFrame()
Tab1Frame.Visible = true
local Tab1Container = makeTabContainer(Tab1Frame)

-- إطار للأزرار على اليسار
local ButtonsFrame = Instance.new("Frame")
ButtonsFrame.Size = UDim2.new(0, 140, 1, -10)
ButtonsFrame.Position = UDim2.new(0, 5, 0, 5)
ButtonsFrame.BackgroundTransparency = 1
ButtonsFrame.Parent = Tab1Container

local UIListLayout_Btns = Instance.new("UIListLayout", ButtonsFrame)
UIListLayout_Btns.Padding = UDim.new(0, 10)
UIListLayout_Btns.HorizontalAlignment = Enum.HorizontalAlignment.Center

-- دالة إنشاء زر للتاب الأول
local function createTab1Btn(text, link)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, 0, 0, 40)
    btn.Text = text
    styleButton(btn, Color3.fromRGB(15, 60, 180), Color3.fromRGB(10, 40, 130))
    btn.Parent = ButtonsFrame
    btn.MouseButton1Click:Connect(function()
        loadstring(game:HttpGet(link))()
    end)
end

createTab1Btn("تايتل🔅", "https://raw.githubusercontent.com/moiladiab-oss/MOILA933-.../main/README.md")
createTab1Btn("سكنات🔅", "https://raw.githubusercontent.com/moiladiab-oss/MO-LAE/main/README.md")
createTab1Btn("فزعة لخويك🔅", "https://raw.githubusercontent.com/moiladiab-oss/To-ARB/main/README.md")

-- تعديل الوصف ليكون بجانب الأزرار
local DescScroll = Instance.new("ScrollingFrame")
DescScroll.Size = UDim2.new(1, -155, 1, -10)
DescScroll.Position = UDim2.new(0, 150, 0, 5)
DescScroll.BackgroundTransparency = 1
DescScroll.ScrollBarThickness = 3
DescScroll.ScrollBarImageColor3 = BLUE_A
DescScroll.BorderSizePixel = 0
DescScroll.CanvasSize = UDim2.new()
DescScroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
DescScroll.Parent = Tab1Container

local DescLabel = Instance.new("TextLabel")
DescLabel.Size = UDim2.new(1, -10, 0, 0)
DescLabel.AutomaticSize = Enum.AutomaticSize.Y
DescLabel.Position = UDim2.new(0, 5, 0, 5)
DescLabel.BackgroundTransparency = 1
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
DescLabel.TextColor3 = Color3.fromRGB(180, 215, 255)
DescLabel.Font = Enum.Font.GothamSemibold
DescLabel.TextSize = 13
DescLabel.TextWrapped = true
DescLabel.TextXAlignment = Enum.TextXAlignment.Right
DescLabel.Parent = DescScroll

-- ====== TAB 2 - نسخ تحديث الجديد (مع قائمة لاعبين + تمرير) ======
local Tab2Frame = createContainerFrame()
local Tab2Container = makeTabContainer(Tab2Frame)

local selectedTab2Target = "الكل"

-- عنوان المستهدف
local tab2TargetLabel = Instance.new("TextLabel")
tab2TargetLabel.Size = UDim2.new(1, -12, 0, 22)
tab2TargetLabel.Position = UDim2.new(0, 6, 0, 4)
tab2TargetLabel.BackgroundColor3 = Color3.fromRGB(8, 20, 60)
tab2TargetLabel.BackgroundTransparency = 0.2
tab2TargetLabel.Text = "🎯 المستهدف: الكل"
tab2TargetLabel.TextColor3 = Color3.fromRGB(180, 220, 255)
tab2TargetLabel.Font = Enum.Font.GothamBold
tab2TargetLabel.TextSize = 11
tab2TargetLabel.BorderSizePixel = 0
tab2TargetLabel.Parent = Tab2Container
corner(tab2TargetLabel, 6)
gradient(tab2TargetLabel, Color3.fromRGB(10, 30, 90), Color3.fromRGB(5, 15, 50), 90)
local t2LblStroke = Instance.new("UIStroke")
t2LblStroke.Color = WHITE
t2LblStroke.Thickness = 1
t2LblStroke.Transparency = 0.5
t2LblStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
t2LblStroke.Parent = tab2TargetLabel
task.spawn(function()
	while tab2TargetLabel and tab2TargetLabel.Parent do
		local t = tick()
		local p = (math.sin(t * 2.5) + 1) / 2
		t2LblStroke.Transparency = 0.2 + p * 0.65
		task.wait(0.04)
	end
end)

-- قائمة اللاعبين (أفقية)
local playerScrollTab2 = Instance.new("ScrollingFrame")
playerScrollTab2.Size = UDim2.new(1, -12, 0, 32)
playerScrollTab2.Position = UDim2.new(0, 6, 0, 28)
playerScrollTab2.BackgroundColor3 = Color3.fromRGB(3, 8, 28)
playerScrollTab2.BackgroundTransparency = 0.3
playerScrollTab2.ScrollBarThickness = 3
playerScrollTab2.ScrollBarImageColor3 = BLUE_A
playerScrollTab2.BorderSizePixel = 0
playerScrollTab2.CanvasSize = UDim2.new()
playerScrollTab2.AutomaticCanvasSize = Enum.AutomaticSize.X
playerScrollTab2.ScrollingDirection = Enum.ScrollingDirection.X
playerScrollTab2.Parent = Tab2Container
corner(playerScrollTab2, 6)
stroke(playerScrollTab2, BLUE_A, 1, 0.5)

local playerListLayoutT2 = Instance.new("UIListLayout")
playerListLayoutT2.FillDirection = Enum.FillDirection.Horizontal
playerListLayoutT2.Padding = UDim.new(0, 4)
playerListLayoutT2.SortOrder = Enum.SortOrder.LayoutOrder
playerListLayoutT2.VerticalAlignment = Enum.VerticalAlignment.Center
playerListLayoutT2.Parent = playerScrollTab2

local playerListPadT2 = Instance.new("UIPadding")
playerListPadT2.PaddingLeft = UDim.new(0, 4)
playerListPadT2.PaddingRight = UDim.new(0, 4)
playerListPadT2.PaddingTop = UDim.new(0, 3)
playerListPadT2.PaddingBottom = UDim.new(0, 3)
playerListPadT2.Parent = playerScrollTab2

-- منطقة التمرير الرأسية
local tab2ScrollContent = Instance.new("ScrollingFrame")
tab2ScrollContent.Size = UDim2.new(1, -12, 1, -66)
tab2ScrollContent.Position = UDim2.new(0, 6, 0, 64)
tab2ScrollContent.BackgroundTransparency = 1
tab2ScrollContent.ScrollBarThickness = 4
tab2ScrollContent.ScrollBarImageColor3 = BLUE_A
tab2ScrollContent.BorderSizePixel = 0
tab2ScrollContent.CanvasSize = UDim2.new()
tab2ScrollContent.AutomaticCanvasSize = Enum.AutomaticSize.Y
tab2ScrollContent.Parent = Tab2Container

local tab2ContentLayout = Instance.new("UIListLayout")
tab2ContentLayout.Padding = UDim.new(0, 8)
tab2ContentLayout.SortOrder = Enum.SortOrder.LayoutOrder
tab2ContentLayout.Parent = tab2ScrollContent

local tab2ContentPad = Instance.new("UIPadding")
tab2ContentPad.PaddingTop = UDim.new(0, 4)
tab2ContentPad.PaddingBottom = UDim.new(0, 6)
tab2ContentPad.PaddingLeft = UDim.new(0, 2)
tab2ContentPad.PaddingRight = UDim.new(0, 2)
tab2ContentPad.Parent = tab2ScrollContent

-- صف دالة الأمر
local prefixRow = Instance.new("Frame")
prefixRow.Size = UDim2.new(1, 0, 0, 32)
prefixRow.BackgroundTransparency = 1
prefixRow.LayoutOrder = 0
prefixRow.Parent = tab2ScrollContent

local prefixLabel = Instance.new("TextLabel")
prefixLabel.Size = UDim2.new(0.7, 0, 1, 0)
prefixLabel.BackgroundTransparency = 1
prefixLabel.Text = "🔧 دالة الأمر:"
prefixLabel.TextColor3 = Color3.fromRGB(180, 210, 255)
prefixLabel.Font = Enum.Font.GothamBold
prefixLabel.TextSize = 12
prefixLabel.TextXAlignment = Enum.TextXAlignment.Left
prefixLabel.Parent = prefixRow

local prefixBox = Instance.new("TextBox")
prefixBox.Size = UDim2.new(0, 48, 0, 26)
prefixBox.Position = UDim2.new(1, -50, 0.5, -13)
prefixBox.Text = ";"
prefixBox.BackgroundColor3 = Color3.fromRGB(5, 12, 40)
prefixBox.Font = Enum.Font.GothamBold
prefixBox.TextSize = 15
prefixBox.TextColor3 = Color3.fromRGB(80, 160, 255)
prefixBox.BorderSizePixel = 0
prefixBox.ClearTextOnFocus = false
prefixBox.Parent = prefixRow
corner(prefixBox, 6)
stroke(prefixBox, WHITE, 1, 0.3)

-- الأقسام الثلاثة
local spamSectionActive = {false, false, false}
local spamSectionCmds = {
	-- النسخ العادي
	"/logs /re /nv /clogs /logs /re /nv /clogs /logs /re /nv /clogs /logs /re /nv /clogs /logs /re /nv /clogs /logs /re /nv /clogs /logs /re /nv /clogs /logs /re /nv /clogs",
	-- سبام قوي
	";jump;ice;res;nv;jail;logs;cmdbar;jump;ice;res;nv",
	-- النسخ الغامض
	"/explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re /explode /res /nv /warp /logs /re",
}
local spamSectionInfo = {
	{label = "⚡ سبام عادي",  hdr1 = Color3.fromRGB(20, 80, 200),  hdr2 = Color3.fromRGB(10, 45, 130)},
	{label = "💥 سبام قوي",   hdr1 = Color3.fromRGB(160, 50, 20),  hdr2 = Color3.fromRGB(100, 25, 10)},
	{label = "👻 سبام غامض",  hdr1 = Color3.fromRGB(80, 20, 160),  hdr2 = Color3.fromRGB(50, 10, 110)},
}

for i = 1, 3 do
	local sectionFrame = Instance.new("Frame")
	sectionFrame.Size = UDim2.new(1, 0, 0, 76)
	sectionFrame.BackgroundTransparency = 1
	sectionFrame.LayoutOrder = i
	sectionFrame.Parent = tab2ScrollContent

	local hdr = Instance.new("TextLabel")
	hdr.Size = UDim2.new(1, 0, 0, 26)
	hdr.Position = UDim2.new(0, 0, 0, 0)
	hdr.BackgroundTransparency = 0.2
	hdr.Text = spamSectionInfo[i].label
	hdr.TextColor3 = WHITE
	hdr.Font = Enum.Font.GothamBlack
	hdr.TextSize = 12
	hdr.BorderSizePixel = 0
	hdr.Parent = sectionFrame
	corner(hdr, 7)
	gradient(hdr, spamSectionInfo[i].hdr1, spamSectionInfo[i].hdr2, 90)
	local hdrStroke = Instance.new("UIStroke")
	hdrStroke.Color = WHITE
	hdrStroke.Thickness = 1
	hdrStroke.Transparency = 0.4
	hdrStroke.Parent = hdr
	task.spawn(function()
		while hdr and hdr.Parent do
			local t = tick()
			local p = (math.sin(t * 2 + i * 1.2) + 1) / 2
			hdrStroke.Transparency = 0.2 + p * 0.7
			task.wait(0.04)
		end
	end)

	local startBtn = Instance.new("TextButton")
	startBtn.Size = UDim2.new(0.47, -4, 0, 34)
	startBtn.Position = UDim2.new(0, 0, 0, 32)
	startBtn.Text = "▶ تشغيل"
	startBtn.Parent = sectionFrame
	styleButton(startBtn, Color3.fromRGB(10, 120, 35), Color3.fromRGB(5, 70, 18))

	local stopBtn = Instance.new("TextButton")
	stopBtn.Size = UDim2.new(0.47, -4, 0, 34)
	stopBtn.Position = UDim2.new(0.5, 4, 0, 32)
	stopBtn.Text = "⏹ إيقاف"
	stopBtn.Parent = sectionFrame
	styleButton(stopBtn, Color3.fromRGB(160, 30, 30), Color3.fromRGB(100, 15, 15))

	local idx = i
	startBtn.MouseButton1Click:Connect(function()
		if not spamSectionActive[idx] then
			spamSectionActive[idx] = true
			startBtn.Text = "⏳ يعمل..."
			task.spawn(function()
				while spamSectionActive[idx] do
					local prefix = prefixBox.Text ~= "" and prefixBox.Text or ";"
					local raw = spamSectionCmds[idx]
					local target = selectedTab2Target
					local finalCmd = ""
					for cmd in string.gmatch(raw, "[^/]+") do
						local c = cmd:match("^%s*(.-)%s*$")
						if c ~= "" then
							if target == "الكل" then
								finalCmd = finalCmd .. "/" .. c .. " "
							else
								finalCmd = finalCmd .. "/" .. c .. " " .. target .. " "
							end
						end
					end
					fireTextPayload(finalCmd)
					task.wait(0.3)
				end
				startBtn.Text = "▶ تشغيل"
			end)
		end
	end)

	stopBtn.MouseButton1Click:Connect(function()
		spamSectionActive[idx] = false
		startBtn.Text = "▶ تشغيل"
	end)
end

-- تحديث قائمة اللاعبين في التاب 2
local function refreshTab2Players()
	for _, v in pairs(playerScrollTab2:GetChildren()) do
		if v:IsA("TextButton") then v:Destroy() end
	end
	local allBtn = Instance.new("TextButton")
	allBtn.Size = UDim2.new(0, 55, 0, 24)
	allBtn.Text = "🌐 الكل"
	allBtn.LayoutOrder = 0
	allBtn.Parent = playerScrollTab2
	styleButton(allBtn, BLUE_A, BLUE_B)
	allBtn.MouseButton1Click:Connect(function()
		selectedTab2Target = "الكل"
		tab2TargetLabel.Text = "🎯 المستهدف: الكل"
		TweenService:Create(tab2TargetLabel, TweenInfo.new(0.12), {BackgroundColor3 = WHITE}):Play()
		task.delay(0.2, function()
			TweenService:Create(tab2TargetLabel, TweenInfo.new(0.25), {BackgroundColor3 = Color3.fromRGB(8, 20, 60)}):Play()
		end)
	end)
	for i, p in ipairs(Players:GetPlayers()) do
		local b = Instance.new("TextButton")
		local nameLen = math.max(60, #p.Name * 7 + 20)
		b.Size = UDim2.new(0, nameLen, 0, 24)
		b.Text = "👤 " .. p.Name
		b.LayoutOrder = i
		b.Parent = playerScrollTab2
		styleButton(b, Color3.fromRGB(8, 20, 60), Color3.fromRGB(5, 12, 40))
		b.MouseButton1Click:Connect(function()
			selectedTab2Target = p.Name
			tab2TargetLabel.Text = "🎯 المستهدف: " .. p.Name
			TweenService:Create(tab2TargetLabel, TweenInfo.new(0.12), {BackgroundColor3 = Color3.fromRGB(20, 80, 200)}):Play()
			task.delay(0.2, function()
				TweenService:Create(tab2TargetLabel, TweenInfo.new(0.25), {BackgroundColor3 = Color3.fromRGB(8, 20, 60)}):Play()
			end)
		end)
	end
end

refreshTab2Players()
Players.PlayerAdded:Connect(refreshTab2Players)
Players.PlayerRemoving:Connect(refreshTab2Players)

-- ====== TAB 3 - السكربت الإضافي (معدل) ======
local Tab3Frame = createContainerFrame()
local Tab3Container = makeTabContainer(Tab3Frame)

-- زر التشغيل النابض
local ExecuteButton = Instance.new("TextButton")
ExecuteButton.Size = UDim2.new(0.8, 0, 0, 60)
ExecuteButton.Position = UDim2.new(0.1, 0, 0.4, 0)
ExecuteButton.Text = "🚀 تشغيل السكربت الإضافي"
ExecuteButton.Font = Enum.Font.GothamBold
ExecuteButton.TextSize = 14
ExecuteButton.TextColor3 = WHITE
ExecuteButton.AutoButtonColor = false
ExecuteButton.Parent = Tab3Container

-- تصميم الزر
corner(ExecuteButton, 12)
gradient(ExecuteButton, BLUE_A, BLUE_B, 90)
stroke(ExecuteButton, WHITE, 2, 0)

-- تأثير النبض للزر
task.spawn(function()
	while ExecuteButton and ExecuteButton.Parent do
		local t = tick()
		local pulse = (math.sin(t * 3) + 1) / 2 -- سرعة النبض
		local sizeOffset = pulse * 4
		ExecuteButton.Size = UDim2.new(0.8, 0, 0, 60 + sizeOffset)
		ExecuteButton.Position = UDim2.new(0.1, 0, 0.4 - (sizeOffset/200), 0)
		task.wait(0.03)
	end
end)

-- وظيفة الزر
ExecuteButton.MouseButton1Click:Connect(function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/moiladiab-oss/MO-S/main/README.md"))()
	ExecuteButton.Text = "✅ تم التنفيذ!"
	task.wait(2)
	ExecuteButton.Text = "🚀 تشغيل السكربت الإضافي"
end)


-- ====== TAB 4 - حماية من logs و clogs ======
local Tab4Frame = createContainerFrame()
local Tab4Container = makeTabContainer(Tab4Frame)

local CleanerDescLabel = Instance.new("TextLabel")
CleanerDescLabel.Size = UDim2.new(1, -30, 0, 90)
CleanerDescLabel.Position = UDim2.new(0, 15, 0, 15)
CleanerDescLabel.BackgroundTransparency = 1
CleanerDescLabel.Text = "logs و clogs اذا ضغطت على الزر الي تحت رح تجيك حماية من"
CleanerDescLabel.TextColor3 = Color3.fromRGB(180, 230, 255)
CleanerDescLabel.Font = Enum.Font.GothamBold
CleanerDescLabel.TextSize = 13
CleanerDescLabel.TextWrapped = true
CleanerDescLabel.Parent = Tab4Container

local StartCleanerButton = Instance.new("TextButton")
StartCleanerButton.Size = UDim2.new(0.8, 0, 0, 45)
StartCleanerButton.Position = UDim2.new(0.1, 0, 0.65, 0)
StartCleanerButton.BackgroundColor3 = Color3.fromRGB(10, 50, 150)
StartCleanerButton.Font = Enum.Font.GothamBold
StartCleanerButton.Text = "🛡️ ACTIVATE STEALTH MODE"
StartCleanerButton.TextColor3 = Color3.fromRGB(200, 230, 255)
StartCleanerButton.TextSize = 12
StartCleanerButton.Parent = Tab4Container
corner(StartCleanerButton, 10)

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

-- ====== TAB 5 - الاسم ======
local Tab5Frame = createContainerFrame()
local Tab5Container = makeTabContainer(Tab5Frame)

local TitleDescLabel = Instance.new("TextLabel")
TitleDescLabel.Size = UDim2.new(1, -30, 0, 45)
TitleDescLabel.Position = UDim2.new(0, 15, 0, 10)
TitleDescLabel.BackgroundTransparency = 1
TitleDescLabel.Text = "ملاحظة مهمة: ترا اذا كتبت سب رح يطلع حتى لو طويل لان هي خاصيته وشكراً🫡"
TitleDescLabel.TextColor3 = Color3.fromRGB(150, 200, 255)
TitleDescLabel.Font = Enum.Font.GothamBold
TitleDescLabel.TextSize = 12
TitleDescLabel.TextWrapped = true
TitleDescLabel.Parent = Tab5Container

local TitleInput = Instance.new("TextBox")
TitleInput.Size = UDim2.new(0.85, 0, 0, 38)
TitleInput.Position = UDim2.new(0.075, 0, 0.4, 0)
TitleInput.BackgroundColor3 = Color3.fromRGB(5, 12, 40)
TitleInput.BackgroundTransparency = 0.5
TitleInput.Font = Enum.Font.Gotham
TitleInput.PlaceholderText = "اكتب اللقب هنا..."
TitleInput.Text = ""
TitleInput.TextColor3 = WHITE
TitleInput.PlaceholderColor3 = Color3.fromRGB(100, 150, 220)
TitleInput.TextSize = 13
TitleInput.Parent = Tab5Container
corner(TitleInput, 6)

local ApplyButton = Instance.new("TextButton")
ApplyButton.Size = UDim2.new(0.85, 0, 0, 42)
ApplyButton.Position = UDim2.new(0.075, 0, 0.72, 0)
ApplyButton.BackgroundColor3 = Color3.fromRGB(20, 70, 200)
ApplyButton.Font = Enum.Font.GothamBold
ApplyButton.Text = "اضغط هنا لتفعيل الاسم💥"
ApplyButton.TextColor3 = WHITE
ApplyButton.TextSize = 13
ApplyButton.Parent = Tab5Container
corner(ApplyButton, 6)

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

-- ====== TAB 6 - سبام مخفي ======
local Tab6Frame = createContainerFrame()
local Tab6Container = makeTabContainer(Tab6Frame)

local CustomInput = Instance.new("TextBox")
CustomInput.Size = UDim2.new(0.9, 0, 0, 50)
CustomInput.Position = UDim2.new(0.05, 0, 0.1, 0)
CustomInput.BackgroundColor3 = Color3.fromRGB(5, 12, 40)
CustomInput.BackgroundTransparency = 0.3
CustomInput.PlaceholderText = "أكتب هنا الي بدك ياه🫡"
CustomInput.Text = ""
CustomInput.TextColor3 = WHITE
CustomInput.Font = Enum.Font.Gotham
CustomInput.TextSize = 14
CustomInput.Parent = Tab6Container
corner(CustomInput, 8)

local CustomActionButton = Instance.new("TextButton")
CustomActionButton.Size = UDim2.new(0.9, 0, 0, 45)
CustomActionButton.Position = UDim2.new(0.05, 0, 0.55, 0)
CustomActionButton.BackgroundColor3 = Color3.fromRGB(15, 60, 180)
CustomActionButton.Text = "هاد سبام انت بتكتب نسخك🫡💥"
CustomActionButton.TextColor3 = WHITE
CustomActionButton.Font = Enum.Font.GothamBold
CustomActionButton.TextSize = 13
CustomActionButton.Parent = Tab6Container
corner(CustomActionButton, 8)

local isCustomSpamming = false
CustomActionButton.MouseButton1Click:Connect(function()
	isCustomSpamming = not isCustomSpamming
	if isCustomSpamming then
		CustomActionButton.Text = "🛑 إيقاف"
		task.spawn(function()
			while isCustomSpamming do
				if HDAdminRemote and HDAdminRemote:IsA("RemoteFunction") then
					HDAdminRemote:InvokeServer(CustomInput.Text)
				elseif HDAdminRemote and HDAdminRemote:IsA("RemoteEvent") then
					HDAdminRemote:FireServer(CustomInput.Text)
				end
				task.wait()
			end
		end)
	else
		CustomActionButton.Text = "هاد سبام انت بتكتب نسخك🫡💥"
	end
end)

-- ====== TAB 7 - حماية من nv و re ======
local Tab7Frame = createContainerFrame()
local Tab7Container = makeTabContainer(Tab7Frame)

local ProDescLabel = Instance.new("TextLabel")
ProDescLabel.Size = UDim2.new(1, -30, 0, 60)
ProDescLabel.Position = UDim2.new(0, 15, 0, 15)
ProDescLabel.BackgroundTransparency = 1
ProDescLabel.Text = "نظام حماية MOILA HUBBB المتقدم لتدمير واجهة HD Admin و NightVision وحذف الأصول الضارة بالسيرفر."
ProDescLabel.TextColor3 = Color3.fromRGB(160, 210, 255)
ProDescLabel.Font = Enum.Font.GothamBold
ProDescLabel.TextSize = 12
ProDescLabel.TextWrapped = true
ProDescLabel.Parent = Tab7Container

local StatusLabel = Instance.new("TextLabel")
StatusLabel.Size = UDim2.new(1, -30, 0, 30)
StatusLabel.Position = UDim2.new(0, 15, 0, 80)
StatusLabel.BackgroundTransparency = 1
StatusLabel.Text = "حالة الحماية: لم يتم التفعيل بعد 🚫"
StatusLabel.TextColor3 = Color3.fromRGB(180, 180, 180)
StatusLabel.Font = Enum.Font.GothamSemibold
StatusLabel.TextSize = 11
StatusLabel.Parent = Tab7Container

local StartProButton = Instance.new("TextButton")
StartProButton.Size = UDim2.new(0.8, 0, 0, 45)
StartProButton.Position = UDim2.new(0.1, 0, 0.65, 0)
StartProButton.BackgroundColor3 = Color3.fromRGB(15, 55, 160)
StartProButton.Font = Enum.Font.GothamBold
StartProButton.Text = "🛡️ تفعيل حماية MOILA HUBBB"
StartProButton.TextColor3 = Color3.fromRGB(210, 230, 255)
StartProButton.TextSize = 13
StartProButton.Parent = Tab7Container
corner(StartProButton, 10)

StartProButton.MouseButton1Click:Connect(function()
	local d1 = deleteNightVision()
	local d2 = deleteHDInterface()
	local msg = "تم تفعيل الحماية MOILA HUBBB"
	sendMsg(msg)
	if execSignal then execCmd(msg) end
	StatusLabel.Text = "NightVision: " .. tostring(d1) .. " | HDInterface: " .. tostring(d2)
	StatusLabel.TextColor3 = Color3.fromRGB(50, 255, 50)
	StartProButton.Text = "✅ تم تشغيل الحماية بنجاح"
	StartProButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
end)

-- ====== TAB 8 - خاصية الراديو ======
local Tab8Frame = createContainerFrame()

local soundPlayerList = Instance.new("ScrollingFrame", Tab8Frame)
soundPlayerList.Size = UDim2.new(0, 130, 1, 0)
soundPlayerList.Position = UDim2.new(0, 0, 0, 0)
soundPlayerList.BackgroundColor3 = Color3.fromRGB(3, 8, 28)
soundPlayerList.BackgroundTransparency = 0.3
soundPlayerList.ScrollBarThickness = 3
soundPlayerList.ScrollBarImageColor3 = BLUE_A
soundPlayerList.BorderSizePixel = 0
soundPlayerList.CanvasSize = UDim2.new()
soundPlayerList.AutomaticCanvasSize = Enum.AutomaticSize.Y
corner(soundPlayerList, 10)
local sndListStroke = Instance.new("UIStroke")
sndListStroke.Color = WHITE
sndListStroke.Thickness = 1
sndListStroke.Transparency = 0.6
sndListStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
sndListStroke.Parent = soundPlayerList
task.spawn(function()
	while soundPlayerList and soundPlayerList.Parent do
		local t = tick()
		local p = (math.sin(t * 2.3 + 1) + 1) / 2
		sndListStroke.Transparency = 0.3 + p * 0.6
		task.wait(0.04)
	end
end)

local sPad = Instance.new("UIPadding", soundPlayerList)
sPad.PaddingTop = UDim.new(0, 5)
sPad.PaddingLeft = UDim.new(0, 4)
sPad.PaddingRight = UDim.new(0, 4)

local sLayout = Instance.new("UIListLayout", soundPlayerList)
sLayout.Padding = UDim.new(0, 5)
sLayout.SortOrder = Enum.SortOrder.LayoutOrder

local soundSide = Instance.new("Frame", Tab8Frame)
soundSide.Position = UDim2.new(0, 140, 0, 0)
soundSide.Size = UDim2.new(1, -140, 1, 0)
soundSide.BackgroundTransparency = 1

local soundLabel = Instance.new("TextLabel", soundSide)
soundLabel.Size = UDim2.new(1, 0, 0, 26)
soundLabel.Text = "🎯 المستهدف: الكل"
soundLabel.BackgroundColor3 = Color3.fromRGB(8, 20, 60)
soundLabel.Font = Enum.Font.GothamBold
soundLabel.TextSize = 11
soundLabel.BorderSizePixel = 0
whiteText(soundLabel)
corner(soundLabel, 8)
gradient(soundLabel, Color3.fromRGB(15, 40, 100), Color3.fromRGB(5, 15, 50), 90)
local sLabelStroke = Instance.new("UIStroke")
sLabelStroke.Color = WHITE
sLabelStroke.Thickness = 1
sLabelStroke.Transparency = 0.5
sLabelStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
sLabelStroke.Parent = soundLabel
task.spawn(function()
	while soundLabel and soundLabel.Parent do
		local t = tick()
		local p = (math.sin(t * 2.8 + 2) + 1) / 2
		sLabelStroke.Transparency = 0.2 + p * 0.65
		task.wait(0.04)
	end
end)

local soundBox = Instance.new("TextBox", soundSide)
soundBox.Size = UDim2.new(1, 0, 0, 28)
soundBox.Position = UDim2.new(0, 0, 0, 32)
soundBox.Text = ""
soundBox.PlaceholderText = "Sound ID..."
soundBox.PlaceholderColor3 = Color3.fromRGB(120, 160, 220)
soundBox.BackgroundColor3 = Color3.fromRGB(5, 12, 40)
soundBox.Font = Enum.Font.GothamMedium
soundBox.TextSize = 12
soundBox.BorderSizePixel = 0
soundBox.ClearTextOnFocus = false
whiteText(soundBox)
corner(soundBox, 8)
stroke(soundBox, BLUE_A, 1, 0.5)

local actualSoundId = ""
soundBox:GetPropertyChangedSignal("Text"):Connect(function()
	if #soundBox.Text > #actualSoundId then
		actualSoundId = actualSoundId .. string.sub(soundBox.Text, #soundBox.Text, #soundBox.Text)
		soundBox.Text = string.rep("*", #actualSoundId)
	elseif #soundBox.Text < #actualSoundId then
		actualSoundId = string.sub(actualSoundId, 1, #soundBox.Text)
	end
end)

local soundBoxPad = Instance.new("UIPadding", soundBox)
soundBoxPad.PaddingLeft = UDim.new(0, 8)
soundBoxPad.PaddingRight = UDim.new(0, 8)

local playSoundBtn = Instance.new("TextButton", soundSide)
playSoundBtn.Size = UDim2.new(0.48, 0, 0, 28)
playSoundBtn.Position = UDim2.new(0, 0, 0, 66)
playSoundBtn.Text = "▶ تشغيل"
styleButton(playSoundBtn, Color3.fromRGB(20, 80, 200), Color3.fromRGB(10, 45, 130))

local spamSoundBtn = Instance.new("TextButton", soundSide)
spamSoundBtn.Size = UDim2.new(0.48, 0, 0, 28)
spamSoundBtn.Position = UDim2.new(0.52, 0, 0, 66)
spamSoundBtn.Text = "🚀 سبام"
styleButton(spamSoundBtn, Color3.fromRGB(30, 90, 220), Color3.fromRGB(15, 50, 140))

local libraryTitle = Instance.new("TextLabel", soundSide)
libraryTitle.Size = UDim2.new(1, 0, 0, 18)
libraryTitle.Position = UDim2.new(0, 4, 0, 100)
libraryTitle.BackgroundTransparency = 1
libraryTitle.Text = "🎶 مكتبة محمد ✨"
libraryTitle.Font = Enum.Font.GothamBlack
libraryTitle.TextSize = 12
libraryTitle.TextXAlignment = Enum.TextXAlignment.Left
whiteText(libraryTitle)

local songsFrame = Instance.new("ScrollingFrame", soundSide)
songsFrame.Size = UDim2.new(1, 0, 1, -122)
songsFrame.Position = UDim2.new(0, 0, 0, 122)
songsFrame.BackgroundColor3 = Color3.fromRGB(3, 8, 28)
songsFrame.BackgroundTransparency = 0.3
songsFrame.ScrollBarThickness = 3
songsFrame.ScrollBarImageColor3 = BLUE_A
songsFrame.BorderSizePixel = 0
songsFrame.CanvasSize = UDim2.new()
songsFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
corner(songsFrame, 10)
stroke(songsFrame, BLUE_A, 1, 0.6)

local songsPad = Instance.new("UIPadding", songsFrame)
songsPad.PaddingTop = UDim.new(0, 5)
songsPad.PaddingLeft = UDim.new(0, 5)
songsPad.PaddingRight = UDim.new(0, 5)

local sl = Instance.new("UIListLayout", songsFrame)
sl.Padding = UDim.new(0, 4)
sl.SortOrder = Enum.SortOrder.LayoutOrder

local songs = {
	{"ريمكس1",  "74697049223758"}, {"ريمكس2",  "97279560249940"},
	{"ريمكس3",  "136552935669331"}, {"ريمكس4",  "83585067879048"},
	{"ريمكس5",  "139930083180432"}, {"ريمكس6",  "75299605058609"},
	{"ريمكس7",  "97729048791539"}, {"ريمكس8",  "92373674574435"},
	{"Golden brown ✨️", "78317236576153"},
	{"ريمكس9",  "74697049223758"}, {"ريمكس10", "91044846005468"},
	{"ريمكس11", "88378283536818"}, {"ريمكس12", "80197259053353"},
	{"ريمكس13", "80028794437152"}, {"ريمكس14", "106708864246193"},
	{"ريمكس15", "116864099044494"}, {"ريمكس16", "82470542018740"},
	{"ريمكس17", "102054539492265"}, {"ريمكس18", "88363245864725"},
	{"ريمكس19", "105848553383746"}, {"ريمكس20", "100991657598498"},
	{"ريمكس21", "90521568613709"}, {"ريمكس22", "80442979651569"},
	{"ريمكس23", "78334848065356"},
	-- الأغاني الجديدة المضافة:
	{"ريمكس 24", "125636136707501"}, {"ريمكس 25", "114714620814172"},
	{"ريمكس 26", "135018311294635"}, {"ريمكس 27", "83768816338009"},
	{"ريمكس 28", "82746224492420"}, {"ريمكس 29", "133239998424394"},
	{"ريمكس 30", "139882660636026"}, {"ريمكس 31", "133391717164163"},
	{"ريمكس 32", "84375012001991"}, {"ريمكس 33", "95211090341684"},
	{"ريمكس34", "139401685458361"}, {"ريمكس 35", "13337902185139"},
	{"ريمكس 36", "136290865487468"}, {"ريمكس 37", "97317379646997"},
	{"ريمكس 38", "119439195710921"}, {"ريمكس 39", "106251060487387"},
	{"ريمكس 40", "139202008782317"}, {"ريمكس 41", "100472207006460"},
	{"ريمكس 42", "80442979651569"}
}


for i, s in ipairs(songs) do
	local n, id = s[1], s[2]
	local b = Instance.new("TextButton", songsFrame)
	b.Size = UDim2.new(1, -8, 0, 24)
	b.Text = "  " .. n
	b.TextXAlignment = Enum.TextXAlignment.Left
	b.LayoutOrder = i
	local p = soundPalette[((i - 1) % #soundPalette) + 1]
	styleButton(b, p[1], p[2])
	b.MouseButton1Click:Connect(function()
		actualSoundId = id
		soundBox.Text = string.rep("*", #id)
		fireSoundRemote(selectedTarget, id)
		local original = soundLabel.BackgroundColor3
		TweenService:Create(soundLabel, TweenInfo.new(0.15), {BackgroundColor3 = WHITE}):Play()
		task.delay(0.25, function()
			TweenService:Create(soundLabel, TweenInfo.new(0.3), {BackgroundColor3 = original}):Play()
		end)
	end)
end

playSoundBtn.MouseButton1Click:Connect(function()
	fireSoundRemote(selectedTarget, actualSoundId)
end)

spamSoundBtn.MouseButton1Click:Connect(function()
	spamming = not spamming
	if spamming then
		spamSoundBtn.Text = "🛑 إيقاف"
		local g = spamSoundBtn:FindFirstChildOfClass("UIGradient")
		if g then g.Color = ColorSequence.new(Color3.fromRGB(255, 255, 255), Color3.fromRGB(180, 180, 180)) end
	else
		spamSoundBtn.Text = "🚀 سبام"
		local g = spamSoundBtn:FindFirstChildOfClass("UIGradient")
		if g then g.Color = ColorSequence.new(Color3.fromRGB(30, 90, 220), Color3.fromRGB(15, 50, 140)) end
	end
	task.spawn(function()
		while spamming do
			fireSoundRemote(selectedTarget, actualSoundId)
			task.wait(0.5)
		end
	end)
end)

local function refreshSoundPlayers()
	for _, v in pairs(soundPlayerList:GetChildren()) do
		if v:IsA("TextButton") then v:Destroy() end
	end
	local all = Instance.new("TextButton", soundPlayerList)
	all.Size = UDim2.new(1, -8, 0, 24)
	all.Text = "🌐 الكل"
	all.LayoutOrder = 0
	styleButton(all, BLUE_A, BLUE_B)
	all.MouseButton1Click:Connect(function()
		selectedTarget = "الكل"
		soundLabel.Text = "🎯 المستهدف: الكل"
	end)
	for i, p in ipairs(Players:GetPlayers()) do
		local b = Instance.new("TextButton", soundPlayerList)
		b.Size = UDim2.new(1, -8, 0, 24)
		b.Text = "👤 " .. p.Name
		b.LayoutOrder = i
		styleButton(b, Color3.fromRGB(8, 20, 60), Color3.fromRGB(5, 12, 40))
		b.MouseButton1Click:Connect(function()
			selectedTarget = p.Name
			soundLabel.Text = "🎯 المستهدف: " .. p.Name
		end)
	end
end

refreshSoundPlayers()
Players.PlayerAdded:Connect(refreshSoundPlayers)
Players.PlayerRemoving:Connect(refreshSoundPlayers)

-- ====== TAB SWITCHING (8 تابات) ======
local function resetTabs()
	Tab1Frame.Visible = false; Tab2Frame.Visible = false; Tab3Frame.Visible = false
	Tab4Frame.Visible = false; Tab5Frame.Visible = false; Tab6Frame.Visible = false
	Tab7Frame.Visible = false; Tab8Frame.Visible = false
	local btns = {Tab1Button, Tab2Button, Tab3Button, Tab4Button, Tab5Button, Tab6Button, Tab7Button, Tab8Button}
	for _, btn in pairs(btns) do
		btn.BackgroundColor3 = Color3.fromRGB(5, 10, 35)
		btn.TextColor3 = Color3.fromRGB(80, 140, 220)
	end
end

Tab1Button.MouseButton1Click:Connect(function() resetTabs(); Tab1Frame.Visible = true; Tab1Button.BackgroundColor3 = Color3.fromRGB(10, 25, 70); Tab1Button.TextColor3 = WHITE end)
Tab2Button.MouseButton1Click:Connect(function() resetTabs(); Tab2Frame.Visible = true; Tab2Button.BackgroundColor3 = Color3.fromRGB(10, 25, 70); Tab2Button.TextColor3 = WHITE end)
Tab3Button.MouseButton1Click:Connect(function() resetTabs(); Tab3Frame.Visible = true; Tab3Button.BackgroundColor3 = Color3.fromRGB(10, 25, 70); Tab3Button.TextColor3 = WHITE end)
Tab4Button.MouseButton1Click:Connect(function() resetTabs(); Tab4Frame.Visible = true; Tab4Button.BackgroundColor3 = Color3.fromRGB(10, 25, 70); Tab4Button.TextColor3 = WHITE end)
Tab5Button.MouseButton1Click:Connect(function() resetTabs(); Tab5Frame.Visible = true; Tab5Button.BackgroundColor3 = Color3.fromRGB(10, 25, 70); Tab5Button.TextColor3 = WHITE end)
Tab6Button.MouseButton1Click:Connect(function() resetTabs(); Tab6Frame.Visible = true; Tab6Button.BackgroundColor3 = Color3.fromRGB(10, 25, 70); Tab6Button.TextColor3 = WHITE end)
Tab7Button.MouseButton1Click:Connect(function() resetTabs(); Tab7Frame.Visible = true; Tab7Button.BackgroundColor3 = Color3.fromRGB(10, 25, 70); Tab7Button.TextColor3 = WHITE end)
Tab8Button.MouseButton1Click:Connect(function() resetTabs(); Tab8Frame.Visible = true; Tab8Button.BackgroundColor3 = Color3.fromRGB(10, 25, 70); Tab8Button.TextColor3 = WHITE end)

ToggleButton.MouseButton1Click:Connect(function() MainFrame.Visible = not MainFrame.Visible end)
