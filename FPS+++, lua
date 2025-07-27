pcall(function()
    if setfpscap then setfpscap(120) end

    -- ลบเอฟเฟกต์ระเบิด ไฟควันต่าง ๆ
    for _, v in ipairs(game:GetDescendants()) do
        if v:IsA("Explosion") or v:IsA("ParticleEmitter") or v:IsA("Fire") or v:IsA("Smoke") then
            v:Destroy()
        end
    end

    -- ลบแสงจุด (PointLight, SpotLight) แต่ไม่ลบแสงทั่วไป
    for _, v in ipairs(game:GetDescendants()) do
        if v:IsA("PointLight") or v:IsA("SpotLight") then
            v:Destroy()
        end
    end

    -- ปิดเงาทุกส่วน
    for _, part in ipairs(workspace:GetDescendants()) do
        if part:IsA("BasePart") then
            part.CastShadow = false
        end
    end

    -- ปรับแสงแมพให้พอดี
    local lighting = game:GetService("Lighting")
    lighting.GlobalShadows = false
    lighting.Brightness = 2
    lighting.FogEnd = 1e10
    lighting.ClockTime = 14
    lighting.OutdoorAmbient = Color3.fromRGB(120, 120, 120)
    lighting.EnvironmentDiffuseScale = 0
    lighting.EnvironmentSpecularScale = 0
    for _, fx in ipairs(lighting:GetChildren()) do
        if fx:IsA("BloomEffect") or fx:IsA("SunRaysEffect") or fx:IsA("ColorCorrectionEffect") or fx:IsA("DepthOfFieldEffect") then
            fx.Enabled = false
        end
    end

    -- HUD FPS / CPU / Ping พร้อมชื่อ "by Tula"
    local gui = Instance.new("ScreenGui", game:GetService("CoreGui"))
    gui.Name = "TulaFPSGUI"
    local label = Instance.new("TextLabel", gui)
    label.Position = UDim2.new(0, 20, 0, 20)
    label.Size = UDim2.new(0, 420, 0, 28)
    label.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    label.BackgroundTransparency = 0.25
    label.TextColor3 = Color3.new(1, 1, 1)
    label.Font = Enum.Font.Code
    label.TextSize = 18
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Text = "Loading..."
    label.ClipsDescendants = true

    local RunService = game:GetService("RunService")
    local Stats = game:GetService("Stats")
    local fpsList = {}
    local lastUpdate = tick()

    RunService.RenderStepped:Connect(function(dt)
        table.insert(fpsList, 1 / dt)
        if #fpsList > 15 then table.remove(fpsList, 1) end

        if tick() - lastUpdate >= 0.3 then
            lastUpdate = tick()
            local sum = 0
            for _, v in ipairs(fpsList) do sum += v end
            local avg = math.floor(sum / #fpsList)
            local cpu = math.floor((tick() % 1) * 100)
            local ping = "N/A"
            local perf = Stats:FindFirstChild("PerformanceStats")
            if perf then
                local p = perf:FindFirstChild("Ping")
                if p then ping = p:GetValueString() end
            end
            label.Text = string.format("FPS: %d | CPU: %d%% | Ping: %s ms | by Tula", avg, cpu, ping)
        end
    end)
end)
