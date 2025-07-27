# FPS-GUI
Script by Tula
-- FPS+++ by Tula
pcall(function()
    local StatsGui = Instance.new("ScreenGui")
    StatsGui.Name = "FPS+++"
    StatsGui.ResetOnSpawn = false
    StatsGui.IgnoreGuiInset = true
    StatsGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    StatsGui.Parent = game:GetService("CoreGui")

    local TextLabel = Instance.new("TextLabel", StatsGui)
    TextLabel.Size = UDim2.new(0, 200, 0, 30)
    TextLabel.Position = UDim2.new(0, 10, 0, 10)
    TextLabel.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    TextLabel.TextColor3 = Color3.new(1, 1, 1)
    TextLabel.Font = Enum.Font.Code
    TextLabel.TextSize = 18
    TextLabel.BorderSizePixel = 0
    TextLabel.Text = "FPS: ... | by Tula"

    -- FPS calculation
    local RunService = game:GetService("RunService")
    local frames, lastUpdate = 0, time()

    RunService.RenderStepped:Connect(function()
        frames += 1
        local now = time()
        if now - lastUpdate >= 1 then
            TextLabel.Text = "FPS: " .. frames .. " | by Tula"
            frames = 0
            lastUpdate = now
        end
    end)

    -- Frame lock to 120 FPS
    settings().Rendering.QualityLevel = Enum.QualityLevel.Level01
    setfpscap(120)
end)
