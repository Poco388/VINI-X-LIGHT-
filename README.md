local Players = game:GetService("Players")
local player = Players.LocalPlayer
local pgui = player:WaitForChild("PlayerGui")

if pgui:FindFirstChild("KeyCheckGUI") then pgui.KeyCheckGUI:Destroy() end

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KeyCheckGUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = pgui

local background = Instance.new("Frame")
background.Size = UDim2.new(1, 0, 1, 0)
background.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
background.BackgroundTransparency = 0.5
background.Parent = screenGui

local centralFrame = Instance.new("Frame")
centralFrame.Size = UDim2.new(0, 300, 0, 180)
centralFrame.Position = UDim2.new(0.5, -150, 0.5, -90)
centralFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
centralFrame.BackgroundTransparency = 0
centralFrame.BorderSizePixel = 0
centralFrame.Parent = background

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 10)
corner.Parent = centralFrame

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.Position = UDim2.new(0, 0, 0, 0)
title.BackgroundTransparency = 1
title.Text = "INSIRA A KEY"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.GothamBold
title.TextSize = 18
title.Parent = centralFrame

local textBox = Instance.new("TextBox")
textBox.Size = UDim2.new(0.8, 0, 0, 45)
textBox.Position = UDim2.new(0.1, 0, 0, 50)
textBox.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
textBox.TextColor3 = Color3.fromRGB(255, 255, 255)
textBox.Font = Enum.Font.Gotham
textBox.TextSize = 14
textBox.PlaceholderText = "Digite a key aqui..."
textBox.Text = ""
textBox.Parent = centralFrame

local textBoxCorner = Instance.new("UICorner")
textBoxCorner.CornerRadius = UDim.new(0, 5)
textBoxCorner.Parent = textBox

local applyButton = Instance.new("TextButton")
applyButton.Size = UDim2.new(0.5, 0, 0, 45)
applyButton.Position = UDim2.new(0.25, 0, 0, 110)
applyButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
applyButton.Text = "APLICAR KEY"
applyButton.TextColor3 = Color3.fromRGB(0, 0, 0)
applyButton.Font = Enum.Font.GothamBold
applyButton.TextSize = 14
applyButton.Parent = centralFrame

local buttonCorner = Instance.new("UICorner")
buttonCorner.CornerRadius = UDim.new(0, 5)
buttonCorner.Parent = applyButton

local feedback = Instance.new("TextLabel")
feedback.Size = UDim2.new(1, 0, 0, 25)
feedback.Position = UDim2.new(0, 0, 0, 160)
feedback.BackgroundTransparency = 1
feedback.Text = ""
feedback.TextColor3 = Color3.fromRGB(255, 100, 100)
feedback.Font = Enum.Font.Gotham
feedback.TextSize = 12
feedback.Parent = centralFrame

local function loadHub()
    local player = game:GetService("Players").LocalPlayer
    local playerName = player.DisplayName or player.Name
    local pgui = player:WaitForChild("PlayerGui")
    local UserInputService = game:GetService("UserInputService")
    local TweenService = game:GetService("TweenService")

    if pgui:FindFirstChild("VinihubLight") then pgui.VinihubLight:Destroy() end

    local VinihubUI = Instance.new("ScreenGui", pgui)
    VinihubUI.Name = "VinihubLight"
    VinihubUI.ResetOnSpawn = false

    _G.AutoLucky, _G.AutoYen, _G.AutoSkills = false, false, false
    local Remote = game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.7.0"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("SeasonService"):WaitForChild("RF"):WaitForChild("RequestRankedReward")

    local function makeDraggable(frame)
        local dragging, dragInput, dragStart, startPos
        frame.InputBegan:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
                dragging = true
                dragStart = input.Position
                startPos = frame.Position
                input.Changed:Connect(function()
                    if input.UserInputState == Enum.UserInputState.End then dragging = false end
                end)
            end
        end)
        frame.InputChanged:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then dragInput = input end
        end)
        UserInputService.InputChanged:Connect(function(input)
            if input == dragInput and dragging then
                local delta = input.Position - dragStart
                frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
            end
        end)
    end

    local function VinihubNotify(txt)
        local Notif = Instance.new("Frame", VinihubUI)
        Notif.Size = UDim2.new(0, 280, 0, 45)
        Notif.Position = UDim2.new(0.5, -140, -0.1, 0)
        Notif.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        Instance.new("UICorner", Notif).CornerRadius = UDim.new(0, 10)
        
        local Txt = Instance.new("TextLabel", Notif)
        Txt.Size = UDim2.new(1, 0, 1, 0)
        Txt.BackgroundTransparency = 1
        Txt.Text = "Vinihub x Light: " .. txt
        Txt.TextColor3 = Color3.fromRGB(0, 0, 0)
        Txt.Font = Enum.Font.GothamBold
        Txt.TextSize = 13
        
        Notif:TweenPosition(UDim2.new(0.5, -140, 0.05, 0), "Out", "Back", 0.5, true)
        task.wait(2.5)
        Notif:TweenPosition(UDim2.new(0.5, -140, -0.1, 0), "In", "Linear", 0.5, true)
        game:GetService("Debris"):AddItem(Notif, 0.6)
    end

    local VBtn = Instance.new("TextButton", VinihubUI)
    VBtn.Size = UDim2.new(0, 55, 0, 55)
    VBtn.Position = UDim2.new(0.05, 0, 0.15, 0)
    VBtn.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    VBtn.Text = "V"
    VBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    VBtn.Font = Enum.Font.GothamMedium
    VBtn.TextSize = 26
    Instance.new("UICorner", VBtn).CornerRadius = UDim.new(1, 0)
    local VStroke = Instance.new("UIStroke", VBtn)
    VStroke.Color = Color3.fromRGB(255, 255, 255)
    VStroke.Thickness = 2
    makeDraggable(VBtn)

    local Main = Instance.new("Frame", VinihubUI)
    Main.Size = UDim2.new(0, 230, 0, 300)
    Main.Position = UDim2.new(0.5, -115, 1.2, 0)
    Main.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    Main.ClipsDescendants = true
    Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 15)
    local MainStroke = Instance.new("UIStroke", Main)
    MainStroke.Color = Color3.fromRGB(255, 255, 255)
    MainStroke.Thickness = 1.5
    makeDraggable(Main)

    local Title = Instance.new("TextLabel", Main)
    Title.Size = UDim2.new(1, 0, 0, 50)
    Title.Text = "VINIHUB X LIGHT"
    Title.TextColor3 = Color3.fromRGB(255, 255, 255)
    Title.Font = Enum.Font.GothamBold
    Title.TextSize = 17
    Title.BackgroundTransparency = 1

    VBtn.MouseButton1Click:Connect(function()
        local isOpen = Main.Position.Y.Scale < 1
        local targetPos = isOpen and UDim2.new(0.5, -115, 1.2, 0) or UDim2.new(0.5, -115, 0.3, 0)
        Main:TweenPosition(targetPos, "Out", "Back", 0.5, true)
    end)

    local function CreateToggle(name, y, callback)
        local btn = Instance.new("TextButton", Main)
        btn.Size = UDim2.new(0.85, 0, 0, 45)
        btn.Position = UDim2.new(0.075, 0, 0, y)
        btn.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
        btn.Text = name
        btn.TextColor3 = Color3.fromRGB(255, 255, 255)
        btn.Font = Enum.Font.Gotham
        btn.TextSize = 12
        Instance.new("UICorner", btn)
        local bStroke = Instance.new("UIStroke", btn)
        bStroke.Color = Color3.fromRGB(255, 255, 255)
        bStroke.Transparency = 0.8
        
        local active = false
        btn.MouseButton1Click:Connect(function()
            active = not active
            local tween = TweenService:Create(btn, TweenInfo.new(0.3), {
                BackgroundColor3 = active and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(15, 15, 15),
                TextColor3 = active and Color3.fromRGB(0, 0, 0) or Color3.fromRGB(255, 255, 255)
            })
            tween:Play()
            if active then VinihubNotify(name .. " ATIVADO") end
            callback(active)
        end)
    end

    CreateToggle("Lucky Spin (Bronze 3)", 65, function(v) _G.AutoLucky = v end)
    CreateToggle("Yen (Cuidado!)", 125, function(v) _G.AutoYen = v end)
    CreateToggle("Habilidades (Silver 2)", 185, function(v) _G.AutoSkills = v end)

    task.spawn(function()
        while true do
            local waitTime = math.random(70, 200) / 100
            task.wait(waitTime)
            if _G.AutoLucky then pcall(function() Remote:InvokeServer(1) end) end
            if _G.AutoYen then pcall(function() Remote:InvokeServer(2) end) end
            if _G.AutoSkills then pcall(function() Remote:InvokeServer(4) end) end
        end
    end)

    VinihubNotify("Bem-vindo, " .. playerName .. "!")
end

local function applyKey()
    local inputKey = textBox.Text
    if inputKey == "LightVN" then
        feedback.Text = "Key válida! Acessando..."
        feedback.TextColor3 = Color3.fromRGB(100, 255, 100)
        task.wait(1)
        screenGui:Destroy()
        loadHub()
    else
        feedback.Text = "Key inválida! Tente novamente."
        feedback.TextColor3 = Color3.fromRGB(255, 100, 100)
        textBox.Text = ""
    end
end

applyButton.MouseButton1Click:Connect(applyKey)

textBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        applyKey()
    end
end)
