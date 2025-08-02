--// Create Text \\
local function Text(target, title, color, fontsize, name)
local Billboard = Instance.new("BillboardGui", target)
local TextLabel = Instance.new("TextLabel", Billboard)
local UIStroke = Instance.new("UIStroke", TextLabel)
--// Billboard \\
Billboard.AlwaysOnTop = true
Billboard.Size = UDim2.new(0,400,0,100)
Billboard.Name = name
Billboard.Active = true
--// TextLabel \\
TextLabel.AnchorPoint = Vector2.new(0.5,0.5)
TextLabel.BackgroundTransparency = 1
TextLabel.BackgroundColor3 = Color3.new(0,0,0)
TextLabel.TextColor3 = color
TextLabel.Font = "RobotoMono"
TextLabel.TextSize = fontsize
TextLabel.TextTransparency = 0
TextLabel.Visible = true
TextLabel.Text = title
TextLabel.Size = UDim2.new(1,0,0,0)
TextLabel.Position = UDim2.new(0.5,0,0.7,-35)
--// UIStroke \\
UIStroke.Thickness = 1
UIStroke.Color = Color3.new()
UIStroke.Transparency = 0
end
--// Create Highlight \\
local function Highlight(target, color, name)
task.wait(0.25)
local Highlight = Instance.new('Highlight', target)
--// Highlight \\
Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
Highlight.FillColor = color
Highlight.OutlineColor = color
Highlight.FillTransparency = 1
Highlight.OutlineTransparency =  0
Highlight.Name = name
end
--// Disable Text & Highlight \\
local function Disable(name)
for _,v in ipairs(workspace:GetDescendants()) do
if v.Name == name then
v:Destroy()
end
end
end
--// Library \\
local repo = 'https://raw.githubusercontent.com/mstudio45/LinoriaLib/main/'
local Library = loadstring(game:HttpGet(repo .. 'Library.lua'))()
local ThemeManager = loadstring(game:HttpGet(repo .. 'addons/ThemeManager.lua'))()
local SaveManager = loadstring(game:HttpGet(repo .. 'addons/SaveManager.lua'))()

local Options = Library.Options
local Toggles = Library.Toggles

Library.ShowToggleFrameInKeybinds = true
Library.ShowCustomCursor = true
Library.NotifySide = "Left"

--// Create Window \\
local Window = Library:CreateWindow({
	Title = 'sao chép hub | Forsaken',
	Center = true,
	AutoShow = true,
	Resizable = true,
	ShowCustomCursor = true,
	NotifySide = "Right",
	TabPadding = 8,
	MenuFadeTime = 0
})
--// Create Tab \\
local Tabs = {
	Main = Window:AddTab('Main'),
	Settings = Window:AddTab('Setting')
}
--// Code \\

local Generator = Tabs.Main:AddRightGroupbox('Generator')


Generator:AddDropdown('Sữa máy', {
	Values = {'rất nhanh', 'nhanh', 'bình thường'},
	Default = 3,
	Multi = false,
	Text = 'Delay',
	Searchable = false,
        Callback = function(v)
_G.FixMode = v or "Normal"
end})
Generator:AddToggle("AutoGenerator",{
Text = "Always fix generator",
Default = false,
Callback = function(v)
_G.AutoGen = v
pcall(function()
task.spawn(function()
while _G.AutoGen do
if _G.FixMode == "rất nhanh" and game:GetService("Players").LocalPlayer.PlayerGui:FindFirstChild("PuzzleUI") then
wait(1.7)
for _,v in ipairs(workspace["Map"]["Ingame"]["Map"]:GetChildren()) do
if v.Name == "Generator" then
v.Remotes.RE:FireServer()
end
end
elseif _G.FixMode == "nhanh" and game:GetService("Players").LocalPlayer.PlayerGui:FindFirstChild("PuzzleUI") then
wait(3.4)
for _,v in ipairs(workspace["Map"]["Ingame"]["Map"]:GetChildren()) do
if v.Name == "Generator" then
v.Remotes.RE:FireServer()
end
end
elseif _G.FixMode == "bình thường" and game:GetService("Players").LocalPlayer.PlayerGui:FindFirstChild("PuzzleUI") then
wait(4.8)
for _,v in ipairs(workspace["Map"]["Ingame"]["Map"]:GetChildren()) do
if v.Name == "Generator" then
v.Remotes.RE:FireServer()
end
end
end
wait()
end
end)
end)
end})
Generator:AddToggle("fram tiền",{
Text = "Framing from generator",
Default = false,
Callback = function(v)
_G.AutoFarm = v
pcall(function()
task.spawn(function()
while _G.AutoFarm == true do
for _,v in ipairs(workspace.Map.Ingame.Map:GetChildren()) do
if v.Name == "Generator" and game.Players.LocalPlayer.Character:FindFirstChild("CollisionHitbox") then
if v.Progress.Value < 100 and not game.Players.LocalPlayer.PlayerGui:FindFirstChild("PuzzleUI") then
game.Players.LocalPlayer.Character.HumanoidRootPart.Position = v:FindFirstChild("Main").Position
game.Players.LocalPlayer.Character:FindFirstChild("CollisionHitbox").Position = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
fireproximityprompt(v:FindFirstChild("Main").Prompt)
end
end
end
wait(1)
end
end)
end)
end})
Generator:AddToggle("AutoFarm",{
Text = "Always unshow fix ui",
Default = false,
Callback = function(v)
_G.UnshowFixUi = v
game:GetService("RunService").RenderStepped:Connect(function()
game:GetService("Players").LocalPlayer.PlayerGui:FindFirstChild("PuzzleUI").Enabled = not _G.UnshowFixUi
end)
end})
Generator:AddButton("Teleport to generator",function()
_G.TTG = true
task.spawn(function()
while _G.TTG do
for _,v in ipairs(workspace.Map.Ingame.Map:GetChildren()) do
if v.Name == "Generator" and game.Players.LocalPlayer.Character:FindFirstChild("CollisionHitbox") then
if v.Progress.Value < 100 and not game.Players.LocalPlayer.PlayerGui:FindFirstChild("PuzzleUI") then
game.Players.LocalPlayer.Character.HumanoidRootPart.Position = v:FindFirstChild("Main").Position
game.Players.LocalPlayer.Character:FindFirstChild("CollisionHitbox").Position = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
end
end
end
wait()
end
end)
wait(0.5)
_G.TTG = false
end)
local Misc = Tabs.Main:AddLeftGroupbox('Miscellaneous')

Misc:AddSlider("HealthEatPizza",{
Text = "Health",
Min = 1,
Default = 50,
Max = 50,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.HealthEatPizza = v
end})
Misc:AddSlider("DistanceEatPizza",{
Text = "Distance",
Min = 10,
Default = 10,
Max = 50,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.DistanceEatPizza = v
end})

_G.HealthEatPizza = 50
_G.DistanceEatPizza = 10

game:GetService("RunService").RenderStepped:Connect(function()
if _G.AlwaysEatPizza and workspace.Map.Ingame:FindFirstChild("Pizza") then
if game.Players.LocalPlayer.Character.Humanoid.Health < _G.HealthEatPizza and (workspace.Map:FindFirstChild("Ingame"):FindFirstChild("Pizza").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < _G.DistanceEatPizza then
workspace.Map.Ingame:FindFirstChild("Pizza").Position = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
end
end
end)
Misc:AddToggle("AlwaysEatPizza",{
Text = "Always eat pizza",
Default = false,
Callback = function(v)
_G.AlwaysEatPizza = v
end})
Misc:AddDivider()
Misc:AddToggle("AlwaysCoinFlip",{
Text = "Auto Flip Coin",
Default = false,
Callback = function(v)
_G.AutoFlipCoins = v or false
game:GetService("RunService").RenderStepped:Connect(function()
if _G.AutoFlipCoins then
game:GetService("ReplicatedStorage"):WaitForChild("Modules"):WaitForChild("Network"):WaitForChild("RemoteEvent"):FireServer("UseActorAbility", "CoinFlip")
end
end)
end})
game:GetService("RunService").RenderStepped:Connect(function()
game.Players.LocalPlayer.PlayerGui:FindFirstChild("TemporaryUI"):FindFirstChild("PlayerInfo").CurrentSurvivors.Visible = not _G.HideBar
end)
Misc:AddToggle("AlwaysHideBar",{
Text = "Hide Survivors Bar",
Default = false,
Callback = function(v)
_G.HideBar = v or false
end})
Misc:AddDivider()
Misc:AddSlider("SizeHeart",{
Text = "Size shiftlock",
Min = 10,
Default = 10,
Max = 50,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.SizeHeart = v or 10
end})
Misc:AddToggle("EnabledHeart",{
Text = "Enabled",
Default = false,
Callback = function(v)
_G.Heart = v or false
game:GetService("RunService").RenderStepped:Connect(function()
if _G.Heart then
game:GetService("Players").LocalPlayer.PlayerGui.MainUI:FindFirstChild("MobileUI").Crosshair.Size = UDim2.new(0.05,_G.SizeHeart,0.05,_G.SizeHeart)
else
game:GetService("Players").LocalPlayer.PlayerGui.MainUI:FindFirstChild("MobileUI").Crosshair.Size = UDim2.new(0.05,0,0.05,0)
end
end)
end})
Misc:AddDivider()
Misc:AddSlider("HitboxTransparency",{
Text = "Transparency",
Min = 0.1,
Default = 0.1,
Max = 0.9,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.HitboxTransparency = v or 0.1
end})
Misc:AddToggle("EnabledHitbox",{
Text = "Hitbox Transparency",
Default = false,
Callback = function(v)
if v then
for _,v in pairs(workspace.Hitboxes:GetChildren()) do
if v.Parent.Name == "Hitboxes" then
v.Transparency = _G.HitboxTransparency or 0.1
end
end
HitboxTran = workspace.Hitboxes.DescendantAdded:Connect(function(v)
if v.Parent.Name == "Hitboxes" then
v.Transparency = _G.HitboxTransparency or 0.1
end
end)
else
HitboxTran:Disconnect()
for _,v in pairs(workspace.Hitboxes:GetChildren()) do
if v.Parent.Name == "Hitboxes" then
v.Transparency = 0
end
end
end
end})




local Players = Tabs.Main:AddRightGroupbox('Player')

Players:AddDropdown('SpeedBoostValue', {
	Values = {'1', '2', '3', '4', '5'},
	Default = 2,
	Multi = false,
	Text = 'Tpwalk',
	Searchable = false,
        Callback = function(v)
_G.SpeedBoostValue = v or '2'
end})

Players:AddToggle("SpeedBoost",{
Text = "Enabled tpwalk",
Default = false,
Callback = function(v)
_G.SpeedBoost = v
while _G.SpeedBoost do
if _G.SpeedBoostValue == '1' then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame += game.Players.LocalPlayer.Character.Humanoid.MoveDirection * 0.1
game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = true
elseif _G.SpeedBoostValue == '2' then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame += game.Players.LocalPlayer.Character.Humanoid.MoveDirection * 0.2
game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = true
elseif _G.SpeedBoostValue == '3' then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame += game.Players.LocalPlayer.Character.Humanoid.MoveDirection * 0.3
game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = true
elseif _G.SpeedBoostValue == '4' then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame += game.Players.LocalPlayer.Character.Humanoid.MoveDirection * 0.4
game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = true
elseif _G.SpeedBoostValue == '5' then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame += game.Players.LocalPlayer.Character.Humanoid.MoveDirection * 0.5
game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = true
end
wait()
end
end})
Players:AddDivider()
StaminaScript = require(game:GetService("ReplicatedStorage").Systems.Character.Game.Sprinting)
game:GetService("RunService").RenderStepped:Connect(function()
for _,v in pairs(workspace.Players.Survivors:GetChildren()) do
if v.Parent.Name == "Survivors" and v:GetAttribute("Username") == game.Players.LocalPlayer.Name then
StaminaScript.MaxStamina = _G.MaxStaminaS or 100
StaminaScript.StaminaGain = _G.StaminaGainS or 30
StaminaScript.StaminaLoss = _G.StaminaLossS or 10
StaminaScript.SprintSpeed = _G.SpeedSprintS or 24
end
end
end)
Players:AddLabel("Exclusively for your survivor")
Players:AddSlider("MaxStamina",{
Text = "Max Stamina",
Min = 100,
Default = 100,
Max = 400,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.MaxStaminaS = v
end})
Players:AddSlider("StaminaGain",{
Text = "Stamina Gain",
Min = 30,
Default = 30,
Max = 50,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.StaminaGainS = v
end})
Players:AddSlider("StaminaLoss",{
Text = "Stamina Loss",
Min = 1,
Default = 10,
Max = 15,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.StaminaLossS = v
end})
Players:AddSlider("StaminaSprint",{
Text = "Sprint Speed",
Min = 24,
Default = 28,
Max = 32,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.SpeedSprintS = v
end})
Players:AddDivider()
game:GetService("RunService").RenderStepped:Connect(function()
for _,v in pairs(workspace.Players.Killers:GetChildren()) do
if v.Parent.Name == "Killers" and v:GetAttribute("Username") == game.Players.LocalPlayer.Name then
StaminaScript.MaxStamina = _G.MaxStaminaK or 110
StaminaScript.StaminaGain = _G.StaminaGainK or 30
StaminaScript.StaminaLoss = _G.StaminaLossK or 10
StaminaScript.SprintSpeed = _G.SpeedSprintK or 28
end
end
end)
Players:AddLabel("Exclusively for your killer")
Players:AddSlider("MaxStamina",{
Text = "Max Stamina",
Min = 110,
Default = 110,
Max = 400,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.MaxStaminaK = v
end})
Players:AddSlider("StaminaGain",{
Text = "Stamina Gain",
Min = 30,
Default = 30,
Max = 50,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.StaminaGainK = v
end})
Players:AddSlider("StaminaLoss",{
Text = "Stamina Loss",
Min = 1,
Default = 10,
Max = 15,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.StaminaLossK = v
end})
Players:AddSlider("StaminaSprint",{
Text = "Sprint Speed",
Min = 28,
Default = 28,
Max = 32,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.SpeedSprintK = v
end})
Players:AddDivider()
Players:AddToggle("InfStamina",{
Text = "No Loss Stamina",
Default = false,
Callback = function(v)
_G.InfinityStamina = v
InfStamina = game:GetService("RunService").RenderStepped:Connect(function()
if not _G.InfinityStamina then
InfStamina:Disconnect()
StaminaScript.StaminaLossDisabled = nil
return
end
StaminaScript.StaminaLossDisabled = function() 
end
end)
end})
game:GetService("RunService").RenderStepped:Connect(function()
if _G.Invisible and game.Players.LocalPlayer.Character.Parent ~= workspace.Players.Spectating then
local Animation = Instance.new("Animation")
Animation.Name = "Invisible_Animation"
Animation.AnimationId = "rbxassetid://75804462760596"
local Load = game.Players.LocalPlayer.Character.Humanoid:LoadAnimation(Animation)
Load:Play(0,1,1)
Load:AdjustSpeed(0)
else
for i,v in next, game.Players.LocalPlayer.Character.Humanoid:GetPlayingAnimationTracks() do
if v.Animation.Name == "Invisible_Animation" then
v:Stop()
end
end
end
end)
Players:AddToggle("Invisible",{
Text = "Invisible",
Default = false,
Callback = function(v)
_G.Invisible = v
end}):AddKeyPicker("AutoInteractKeybind", {
   Default = "G",
   Text = "Invisible",
   Mode = Library.IsMobile and "Toggle" or "Hold",
   SyncToggleState = Library.IsMobile
})
Players:AddToggle("SpamFootstepFE",{
Text = "Spam Footstep (FE)",
Default = false,
Callback = function(v)
_G.SpamFootstep = v
game:GetService("RunService").RenderStepped:Connect(function()
if _G.SpamFootstep then
game:GetService("ReplicatedStorage"):WaitForChild("Modules"):WaitForChild("Network"):WaitForChild("UnreliableRemoteEvent"):FireServer("FootstepPlayed", 9)
end
end)
end}):AddKeyPicker("AutoInteractKeybind", {
   Default = "F",
   Text = "Spam Footstep",
   Mode = Library.IsMobile and "Toggle" or "Hold",
   SyncToggleState = Library.IsMobile
})

Players:AddButton("No Blindness", function()
game:GetService("ReplicatedStorage").Modules.StatusEffects.Blindness:Destroy()
end)
Players:AddButton("No Slowspeed", function()
game:GetService("ReplicatedStorage").Modules.StatusEffects.Slowness:Destroy()
end)

local Camera = Tabs.Main:AddLeftGroupbox('Camera Offical')

Camera:AddSlider("FieldOfViewValue",{
Text = "Field Of View",
Min = 80,
Default = 80,
Max = 120,
Rounding = 1,
Compact = true,
Callback = function(v)
_G.FieldOfViewValue = v
end})
Camera:AddToggle("FOV",{
Text = "Enabled",
Default = false,
Callback = function(v)
_G.FieldOfView = v
game:GetService("RunService").RenderStepped:Connect(function()
if _G.FieldOfView then
workspace.Camera.FieldOfView = _G.FieldOfViewValue or 80
end
end)
end})
Camera:AddDivider()
Camera:AddToggle("NoFog",{
Text = "Removal Fog",
Default = false,
Callback = function(v)
_G.NoFog = v
game:GetService("RunService").RenderStepped:Connect(function()
if not game.Lighting:GetAttribute("FogStart") then game.Lighting:SetAttribute("FogStart", game.Lighting.FogStart) end
if not game.Lighting:GetAttribute("FogEnd") then game.Lighting:SetAttribute("FogEnd", game.Lighting.FogEnd) end
game.Lighting.FogStart = _G.NoFog and 0 or game.Lighting:GetAttribute("FogStart")
game.Lighting.FogEnd = _G.NoFog and math.huge or game.Lighting:GetAttribute("FogEnd")
local fog = game.Lighting:FindFirstChildOfClass("Atmosphere")
if fog then
if not fog:GetAttribute("Density") then fog:SetAttribute("Density", fog.Density) end
fog.Density = _G.NoFog and 0 or fog:GetAttribute("Density")
end
end)
end})
Camera:AddToggle("Fullbright",{
Text = "Always Light Corver",
Default = false,
Callback = function(v)
_G.Fullbright = v
game:GetService("RunService").RenderStepped:Connect(function()
if _G.Fullbright then
game.Lighting.OutdoorAmbient = Color3.fromRGB(255,255,255)
game.Lighting.Brightness = 1.5
game.Lighting.GlobalShadows = false
else
game.Lighting.OutdoorAmbient = Color3.fromRGB(55,55,55)
game.Lighting.Brightness = 1.5
game.Lighting.GlobalShadows = true
end
end)
end})

local ESP = Tabs.Main:AddLeftGroupbox('ESP')

ESP:AddToggle("KE",{
Text = "Killers ESP",
Default = false,
Callback = function(v)
if v then
for _, v in pairs(workspace.Players.Killers:GetChildren()) do
if v:IsA("Model") and v.Parent.Name == "Killers" then
Text(v.HumanoidRootPart, v.Name .. "\n\nSkin : " .. v:GetAttribute("SkinNameDisplay"), Color3.new(1), 14, "Killer_ESP")
Highlight(v, Color3.new(1), "Killer_ESP")
elseif v.Parent.Name == "Killers" and v:GetAttribute("Username") == game.Players.LocalPlayer.Name then
v:FindFirstChild("Killer_ESP"):Destroy()
end
end
KillerESP = workspace.Players.DescendantAdded:Connect(function(v)
wait(2)
if v:IsA("Model") and v.Parent.Name == "Killers" then
Text(v.HumanoidRootPart, v.Name .. "\n\nSkin : " .. v:GetAttribute("SkinNameDisplay"), Color3.new(1), 14, "Killer_ESP")
Highlight(v, Color3.new(1), "Killer_ESP")
elseif v.Parent.Name == "Killers" and v:GetAttribute("Username") == game.Players.LocalPlayer.Name then
v:FindFirstChild("Killer_ESP"):Destroy()
end
end)
else
KillerESP:Disconnect()
Disable("Killer_ESP")
end
end})
ESP:AddToggle("SE",{
Text = "Survivor ESP",
Default = false,
Callback = function(v)
if v then
for _, v in ipairs(workspace.Players.Survivors:GetChildren()) do
if v:IsA("Model") and v.Parent.Name == "Survivors" then
Text(v.HumanoidRootPart, v.Name, Color3.new(0,1), 14, "Survivor_ESP")
Highlight(v, Color3.new(0,1), "Survivor_ESP")
elseif v.Parent.Name == "Survivors" and v:GetAttribute("Username") == game.Players.LocalPlayer.Name then
v:FindFirstChild("Survivor_ESP"):Destroy()
end
end
SurvivalESP = workspace.Players.DescendantAdded:Connect(function(v)
wait(2)
if v:IsA("Model") and v.Parent.Name == "Survivors" then
Text(v.HumanoidRootPart, v.Name, Color3.new(0,1), 14, "Survivor_ESP")
Highlight(v, Color3.new(0,1), "Survivor_ESP")
elseif v.Parent.Name == "Survivors" and v:GetAttribute("Username") == game.Players.LocalPlayer.Name then
v:FindFirstChild("Survivor_ESP"):Destroy()
end
end)
else
SurvivalESP:Disconnect()
Disable("Survivor_ESP")
end
end})
ESP:AddToggle("IE",{
Text = "Support Items ESP",
Default = false,
Callback = function(v)
if v then
for _, v in ipairs(workspace:GetDescendants()) do
if v:IsA("Model") and v.Name == "BloxyCola" and not v:FindFirstChild("Items_ESP") then
Text(v, v.Name, Color3.new(1,1), 14, "Items_ESP")
Highlight(v, Color3.new(1,1), "Items_ESP")
elseif v:IsA("Model") and v.Name == "Medkit" and not v:FindFirstChild("Items_ESP") then
Text(v, v.Name, Color3.new(1), 14, "Items_ESP")
Highlight(v, Color3.new(1), "Items_ESP")
end
end
ItemsESP = workspace.Map.Ingame.DescendantAdded:Connect(function(v)
if v:IsA("Model") and v.Name == "BloxyCola" and not v:FindFirstChild("Items_ESP") then
Text(v, v.Name, Color3.new(1,1), 14, "Items_ESP")
Highlight(v, Color3.new(1,1), "Items_ESP")
elseif v:IsA("Model") and v.Name == "Medkit" and not v:FindFirstChild("Items_ESP") then
Text(v, v.Name, Color3.new(1), 14, "Items_ESP")
Highlight(v, Color3.new(1), "Items_ESP")
end
end)
else
ItemsESP:Disconnect()
Disable("Items_ESP")
end
end})
ESP:AddToggle("GE",{
Text = "Generator ESP",
Default = false,
Callback = function(v)
if v then
for _, v in ipairs(workspace:GetDescendants()) do
if v:IsA("Model") and v.Parent.Name == "Map" and v.Name == "Generator" and not v:FindFirstChild("Generator_ESP") then
Text(v, v.Name, Color3.new(0,0,1), 14, "Generator_ESP")
Highlight(v, Color3.new(0,0,1), "Generator_ESP")
end
end
GeneratorESP = workspace.Map.Ingame.DescendantAdded:Connect(function(v)
if v:IsA("Model") and v.Parent.Name == "Map" and v.Name == "Generator" and not v:FindFirstChild("Generator_ESP") then
Text(v, v.Name, Color3.new(0,0,1), 14, "Generator_ESP")
Highlight(v, Color3.new(0,0,1), "Generator_ESP")
end
end)
else
GeneratorESP:Disconnect()
Disable("Generator_ESP")
end
end})
ESP:AddToggle("SSTME",{
Text = "Subspace Tripmine ESP",
Default = false,
Callback = function(v)
if v then
for _, v in ipairs(workspace:GetDescendants()) do
if v:IsA("Model") and v.Name == "SubspaceTripmine" and not v:FindFirstChild("SubspaceTripmine_ESP") then
Text(v, v.Name, Color3.new(1,0,1), 14, "SSTM_ESP")
Highlight(v, Color3.new(1,0,1), "SSTM_ESP")
end
end
SubspaceTripmineESP = workspace.Map.Ingame.DescendantAdded:Connect(function(v)
wait(1)
if v:IsA("Model") and v.Name == "SubspaceTripmine" and not v:FindFirstChild("SubspaceTripmine_ESP") then
Text(v, v.Name, Color3.new(1,0,1), 14, "SSTm_ESP")
Highlight(v, Color3.new(1,0,1), "SSTM_ESP")
end
end)
else
SubspaceTripmineESP:Disconnect()
Disable("SSTM_ESP")
end
end})



Library:SetWatermarkVisibility(true)

local FrameTimer = tick()
local FrameCounter = 0;
local FPS = 60;

local WatermarkConnection = game:GetService('RunService').RenderStepped:Connect(function()
	FrameCounter += 1;

	if (tick() - FrameTimer) >= 1 then
		FPS = FrameCounter;
		FrameTimer = tick();
		FrameCounter = 0;
	end;

	Library:SetWatermark(('Forsaken | %s fps | %s ms'):format(
		math.floor(FPS),
		math.floor(game:GetService('Stats').Network.ServerStatsItem['Data Ping']:GetValue())
	))
end)

local MenuGroup = Tabs.Settings:AddLeftGroupbox("Menu")
local CreditsGroup = Tabs.Settings:AddRightGroupbox("Credits")

MenuGroup:AddToggle("KeybindMenuOpen", { Default = false, Text = "Open Keybind Menu", Callback = function(v) Library.KeybindFrame.Visible = v end})
MenuGroup:AddToggle("ShowCustomCursor", {Text = "Custom Cursor", Default = true, Callback = function(v) Library.ShowCustomCursor = v end})
MenuGroup:AddDivider()
MenuGroup:AddLabel("Keybind"):AddKeyPicker("MenuKeybind", { Default = "RightShift", NoUI = true, Text = "Menu keybind" })
MenuGroup:AddButton("Unload", function() Library:Unload() end)

CreditsGroup:AddLabel("Developers:")
CreditsGroup:AddLabel("Owner | rechedmcvn")
CreditsGroup:AddLabel("Reviewer:")
CreditsGroup:AddLabel("Not Found.")

ThemeManager:SetLibrary(Library)
SaveManager:SetLibrary(Library)

SaveManager:IgnoreThemeSettings()

ThemeManager:SetFolder("MyScriptHub")
SaveManager:SetFolder("MyScriptHub/specific-game")
SaveManager:SetSubFolder("specific-place") 

SaveManager:BuildConfigSection(Tabs.Settings)

ThemeManager:ApplyToTab(Tabs.Settings)








