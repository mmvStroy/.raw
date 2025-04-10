-- Создание кнопки для включения полета
local flyButton = Instance.new("TextButton")
flyButton.Name = "FlyButton"
flyButton.Parent = Frame
flyButton.BackgroundColor3 = Color3.fromRGB(255, 249, 74)
flyButton.Position = UDim2.new(0.702823281, 0, 0.491228074, 0)
flyButton.Size = UDim2.new(0, 56, 0, 28)
flyButton.Font = Enum.Font.SourceSans
flyButton.Text = "FlyMax"
flyButton.TextColor3 = Color3.fromRGB(0, 0, 0)
flyButton.TextSize = 14.000

-- Переменная для проверки статуса полета
local isFlying = false
local bodyGyro, bodyVelocity

-- Функция включения/выключения полета
flyButton.MouseButton1Down:Connect(function()
    local player = game.Players.LocalPlayer
    local character = player.Character
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    local torso = character:FindFirstChild("HumanoidRootPart")

    if isFlying then
        -- Останавливаем полет
        bodyGyro:Destroy()
        bodyVelocity:Destroy()
        humanoid.PlatformStand = false
        isFlying = false
        flyButton.Text = "FlyMax"  -- Меняем текст на кнопке
    else
        -- Включаем полет
        humanoid.PlatformStand = true
        
        bodyGyro = Instance.new("BodyGyro", torso)
        bodyGyro.P = 9e4
        bodyGyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
        bodyGyro.cframe = torso.CFrame
        
        bodyVelocity = Instance.new("BodyVelocity", torso)
        bodyVelocity.velocity = Vector3.new(0, 0.1, 0)
        bodyVelocity.maxForce = Vector3.new(9e9, 9e9, 9e9)
        
        isFlying = true
        flyButton.Text = "Stop Fly"  -- Меняем текст на кнопке
    end
end)# .raw
