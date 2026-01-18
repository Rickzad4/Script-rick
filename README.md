local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer
local character
local hrp
local hum

local function setupCharacter(char)
    character = char
    hrp = character:WaitForChild("HumanoidRootPart")
    hum = character:WaitForChild("Humanoid")
end

if player.Character then
    setupCharacter(player.Character)
end

player.CharacterAdded:Connect(setupCharacter)

local function create(class, props)
    local obj = Instance.new(class)
    for k, v in pairs(props) do
        if k ~= "Parent" then
            obj[k] = v
        end
    end
    if props.Parent then
        obj.Parent = props.Parent
    end
    return obj
end

local ScreenGui = create("ScreenGui", {
    Name = "LKZSpeedGui",
    ResetOnSpawn = false,
    ZIndexBehavior = Enum.ZIndexBehavior.Sibling,
    Parent = player:WaitForChild("PlayerGui")
})

local MainFrame = create("Frame", {
    Name = "MainFrame",
    Size = UDim2.new(0, 340, 0, 160),
    Position = UDim2.new(0.5, -170, 0.08, 0),
    BackgroundTransparency = 1,
    Active = true,
    Draggable = true,
    Parent = ScreenGui
})

local Background = create("Frame", {
    Size = UDim2.new(1, 0, 1, 0),
    BackgroundColor3 = Color3.fromRGB(12, 12, 16),
    BackgroundTransparency = 0.1,
    BorderSizePixel = 0,
    Parent = MainFrame
})

create("UICorner", {
    CornerRadius = UDim.new(0.15, 0),
    Parent = Background
})

local InnerGlow = create("Frame", {
    Size = UDim2.new(1, -8, 1, -8),
    Position = UDim2.new(0, 4, 0, 4),
    BackgroundColor3 = Color3.fromRGB(20, 20, 25),
    BackgroundTransparency = 0.5,
    BorderSizePixel = 0,
    Parent = MainFrame
})

create("UICorner", {
    CornerRadius = UDim.new(0.14, 0),
    Parent = InnerGlow
})

local Gradient = create("UIGradient", {
    Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(60, 0, 0)),
        ColorSequenceKeypoint.new(0.3, Color3.fromRGB(150, 10, 10)),
        ColorSequenceKeypoint.new(0.6, Color3.fromRGB(255, 60, 60)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 180, 180))
    }),
    Rotation = 0,
    Parent = Background
})

local Stroke = create("UIStroke", {
    Color = Color3.fromRGB(255, 255, 255),
    Thickness = 5,
    Transparency = 0,
    ApplyStrokeMode = Enum.ApplyStrokeMode.Border,
    Parent = Background
})

local StrokeGradient = create("UIGradient", {
    Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(100, 0, 0)),
        ColorSequenceKeypoint.new(0.3, Color3.fromRGB(255, 0, 0)),
        ColorSequenceKeypoint.new(0.6, Color3.fromRGB(255, 80, 80)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 255, 255))
    }),
    Rotation = 0,
    Parent = Stroke
})

local Title = create("TextLabel", {
    Size = UDim2.new(1, 0, 0, 30),
    Position = UDim2.new(0, 0, 0, 5),
    BackgroundTransparency = 1,
    Text = utf8.char(0x1F451) .. " RICK SPEED " .. utf8.char(0x1F451),
    TextColor3 = Color3.fromRGB(255, 255, 255),
    TextSize = 18,
    Font = Enum.Font.LuckiestGuy,
    TextStrokeTransparency = 0.4,
    TextStrokeColor3 = Color3.fromRGB(0, 0, 0),
    Parent = MainFrame
})

local TitleGlow = create("TextLabel", {
    Size = UDim2.new(1, 0, 0, 30),
    Position = UDim2.new(0, 0, 0, 5),
    BackgroundTransparency = 1,
    Text = utf8.char(0x1F451) .. " RICK SPEED " .. utf8.char(0x1F451),
    TextColor3 = Color3.fromRGB(255, 80, 80),
    TextSize = 18,
    Font = Enum.Font.LuckiestGuy,
    TextTransparency = 0.5,
    ZIndex = 0,
    Parent = MainFrame
})

local SpeedNoStealInput = create("TextBox", {
    Size = UDim2.new(0.3, 0, 0, 32),
    Position = UDim2.new(0.02, 0, 0, 42),
    BackgroundColor3 = Color3.fromRGB(35, 20, 15),
    BackgroundTransparency = 0,
    Text = "16",
    TextColor3 = Color3.fromRGB(255, 255, 255),
    TextSize = 14,
    Font = Enum.Font.LuckiestGuy,
    PlaceholderText = "No Steal",
    PlaceholderColor3 = Color3.fromRGB(150, 100, 80),
    BorderSizePixel = 0,
    Parent = MainFrame
})

create("UICorner", {
    CornerRadius = UDim.new(0, 8),
    Parent = SpeedNoStealInput
})

create("UIStroke", {
    Color = Color3.fromRGB(255, 120, 0),
    Thickness = 3,
    Transparency = 0,
    Parent = SpeedNoStealInput
})

local SpeedStealInput = create("TextBox", {
    Size = UDim2.new(0.3, 0, 0, 32),
    Position = UDim2.new(0.34, 0, 0, 42),
    BackgroundColor3 = Color3.fromRGB(40, 35, 10),
    BackgroundTransparency = 0,
    Text = "50",
    TextColor3 = Color3.fromRGB(255, 255, 255),
    TextSize = 14,
    Font = Enum.Font.LuckiestGuy,
    PlaceholderText = "Steal",
    PlaceholderColor3 = Color3.fromRGB(180, 160, 80),
    BorderSizePixel = 0,
    Parent = MainFrame
})

create("UICorner", {
    CornerRadius = UDim.new(0, 8),
    Parent = SpeedStealInput
})

create("UIStroke", {
    Color = Color3.fromRGB(255, 220, 0),
    Thickness = 3,
    Transparency = 0,
    Parent = SpeedStealInput
})

local JumpInput = create("TextBox", {
    Size = UDim2.new(0.3, 0, 0, 32),
    Position = UDim2.new(0.66, 0, 0, 42),
    BackgroundColor3 = Color3.fromRGB(10, 25, 40),
    BackgroundTransparency = 0,
    Text = "50",
    TextColor3 = Color3.fromRGB(255, 255, 255),
    TextSize = 14,
    Font = Enum.Font.LuckiestGuy,
    PlaceholderText = "Jump",
    PlaceholderColor3 = Color3.fromRGB(100, 150, 200),
    BorderSizePixel = 0,
    Parent = MainFrame
})

create("UICorner", {
    CornerRadius = UDim.new(0, 8),
    Parent = JumpInput
})

create("UIStroke", {
    Color = Color3.fromRGB(60, 180, 255),
    Thickness = 3,
    Transparency = 0,
    Parent = JumpInput
})

local SpeedNoStealLabel = create("TextLabel", {
    Size = UDim2.new(0.3, 0, 0, 14),
    Position = UDim2.new(0.02, 0, 0, 76),
    BackgroundTransparency = 1,
    Text = "No Steal",
    TextColor3 = Color3.fromRGB(255, 150, 80),
    TextSize = 10,
    Font = Enum.Font.LuckiestGuy,
    Parent = MainFrame
})

local SpeedStealLabel = create("TextLabel", {
    Size = UDim2.new(0.3, 0, 0, 14),
    Position = UDim2.new(0.34, 0, 0, 76),
    BackgroundTransparency = 1,
    Text = "Steal",
    TextColor3 = Color3.fromRGB(255, 220, 100),
    TextSize = 10,
    Font = Enum.Font.LuckiestGuy,
    Parent = MainFrame
})

local JumpLabel = create("TextLabel", {
    Size = UDim2.new(0.3, 0, 0, 14),
    Position = UDim2.new(0.66, 0, 0, 76),
    BackgroundTransparency = 1,
    Text = "Jump",
    TextColor3 = Color3.fromRGB(100, 200, 255),
    TextSize = 10,
    Font = Enum.Font.LuckiestGuy,
    Parent = MainFrame
})

local SpeedButton = create("TextButton", {
    Size = UDim2.new(0.47, 0, 0, 36),
    Position = UDim2.new(0.02, 0, 0, 95),
    BackgroundColor3 = Color3.fromRGB(180, 0, 0),
    BackgroundTransparency = 0.15,
    Text = "SPEED",
    TextColor3 = Color3.fromRGB(255, 255, 255),
    TextSize = 14,
    Font = Enum.Font.LuckiestGuy,
    BorderSizePixel = 0,
    AutoButtonColor = false,
    Parent = MainFrame
})

create("UICorner", {
    CornerRadius = UDim.new(0, 10),
    Parent = SpeedButton
})

create("UIStroke", {
    Color = Color3.fromRGB(255, 80, 80),
    Thickness = 3,
    Transparency = 0.1,
    Parent = SpeedButton
})

local SpeedGradient = create("UIGradient", {
    Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 255)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(200, 200, 200))
    }),
    Rotation = 90,
    Parent = SpeedButton
})

local JumpButton = create("TextButton", {
    Size = UDim2.new(0.47, 0, 0, 36),
    Position = UDim2.new(0.51, 0, 0, 95),
    BackgroundColor3 = Color3.fromRGB(0, 100, 180),
    BackgroundTransparency = 0.15,
    Text = "JUMP",
    TextColor3 = Color3.fromRGB(255, 255, 255),
    TextSize = 14,
    Font = Enum.Font.LuckiestGuy,
    BorderSizePixel = 0,
    AutoButtonColor = false,
    Parent = MainFrame
})

create("UICorner", {
    CornerRadius = UDim.new(0, 10),
    Parent = JumpButton
})

create("UIStroke", {
    Color = Color3.fromRGB(80, 180, 255),
    Thickness = 3,
    Transparency = 0.1,
    Parent = JumpButton
})

local JumpGradient = create("UIGradient", {
    Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 255)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(200, 200, 200))
    }),
    Rotation = 90,
    Parent = JumpButton
})

local speedActive = false
local speedConnection
local speedNoStealValue = 16
local speedStealValue = 50
local jumpValue = 50
local jumpActive = false

SpeedNoStealInput.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local text = SpeedNoStealInput.Text:gsub("%D", "")
        local num = tonumber(text) or 15
        num = math.clamp(num, 15, 100)
        speedNoStealValue = num
        SpeedNoStealInput.Text = tostring(num)
    end
end)

SpeedStealInput.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local text = SpeedStealInput.Text:gsub("%D", "")
        local num = tonumber(text) or 15
        num = math.clamp(num, 15, 100)
        speedStealValue = num
        SpeedStealInput.Text = tostring(num)
    end
end)

JumpInput.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local text = JumpInput.Text:gsub("%D", "")
        local num = tonumber(text) or 50
        num = math.clamp(num, 50, 150)
        jumpValue = num
        JumpInput.Text = tostring(num)
    end
end)

SpeedButton.MouseButton1Click:Connect(function()
    speedActive = not speedActive
    if speedActive then
        SpeedButton.Text = "OFF"
        SpeedButton.BackgroundColor3 = Color3.fromRGB(0, 180, 60)
        SpeedButton.UIStroke.Color = Color3.fromRGB(80, 255, 120)
        
        speedConnection = RunService.Heartbeat:Connect(function()
            if character and character.Parent and hrp and hrp.Parent and hum then
                local moveDirection = hum.MoveDirection
                if moveDirection.Magnitude > 0 then
                    local isSteal = hum.WalkSpeed < 25
                    local currentSpeed = isSteal and speedStealValue or speedNoStealValue
                    
                    hrp.AssemblyLinearVelocity = Vector3.new(
                        moveDirection.X * currentSpeed,
                        hrp.AssemblyLinearVelocity.Y,
                        moveDirection.Z * currentSpeed
                    )
                end
            end
        end)
    else
        SpeedButton.Text = "SPEED"
        SpeedButton.BackgroundColor3 = Color3.fromRGB(180, 0, 0)
        SpeedButton.UIStroke.Color = Color3.fromRGB(255, 80, 80)
        if speedConnection then
            speedConnection:Disconnect()
            speedConnection = nil
        end
    end
end)

JumpButton.MouseButton1Click:Connect(function()
    jumpActive = not jumpActive
    if jumpActive then
        JumpButton.Text = "ON"
        JumpButton.BackgroundColor3 = Color3.fromRGB(0, 180, 100)
        JumpButton.UIStroke.Color = Color3.fromRGB(80, 255, 180)
    else
        JumpButton.Text = "JUMP"
        JumpButton.BackgroundColor3 = Color3.fromRGB(0, 100, 180)
        JumpButton.UIStroke.Color = Color3.fromRGB(80, 180, 255)
    end
end)

UserInputService.JumpRequest:Connect(function()
    if jumpActive and character and hrp and hum then
        hrp.AssemblyLinearVelocity = Vector3.new(
            hrp.AssemblyLinearVelocity.X,
            jumpValue,
            hrp.AssemblyLinearVelocity.Z
        )
    end
end)

RunService.Heartbeat:Connect(function(dt)
    Gradient.Rotation = (Gradient.Rotation + 120 * dt) % 360
    StrokeGradient.Rotation = (StrokeGradient.Rotation + 120 * dt) % 360
end)
