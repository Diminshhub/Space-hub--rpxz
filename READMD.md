local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()
local Window = OrionLib:MakeWindow({Name = "Space - Hub", HidePremium = false, SaveConfig = true, ConfigFolder = "Space Bost Hub"})

-- Player Tab
local PlayerTab = Window:MakeTab({
    Name = "Player",
    Icon = "rbxassetid://77163241748860",
    PremiumOnly = false
})

-- Variáveis para controle de velocidade e pulo
local player = game.Players.LocalPlayer
local humanoid = player.Character:WaitForChild("Humanoid")

local currentSpeed = humanoid.WalkSpeed
local currentJumpPower = humanoid.JumpPower

-- Função para aumentar e diminuir a velocidade
local function adjustSpeed(increase)
    if increase then
        currentSpeed = math.min(currentSpeed + 5, 100) -- Aumenta a velocidade em 5, máximo de 100
    else
        currentSpeed = math.max(currentSpeed - 5, 16) -- Diminui a velocidade em 5, mínimo de 16
    end
    humanoid.WalkSpeed = currentSpeed
end

-- Função para aumentar e diminuir o tamanho do pulo
local function adjustJumpPower(increase)
    if increase then
        currentJumpPower = math.min(currentJumpPower + 10, 300) -- Aumenta o pulo em 10, máximo de 300
    else
        currentJumpPower = math.max(currentJumpPower - 10, 50) -- Diminui o pulo em 10, mínimo de 50
    end
    humanoid.JumpPower = currentJumpPower
end

-- Botão para aumentar a velocidade
PlayerTab:AddButton({
    Name = "Aumentar Velocidade",
    Callback = function()
        adjustSpeed(true)
    end    
})

-- Botão para diminuir a velocidade
PlayerTab:AddButton({
    Name = "Diminuir Velocidade",
    Callback = function()
        adjustSpeed(false)
    end    
})

-- Botão para aumentar o tamanho do pulo
PlayerTab:AddButton({
    Name = "Aumentar Tamanho do Pulo",
    Callback = function()
        adjustJumpPower(true)
    end    
})

-- Botão para diminuir o tamanho do pulo
PlayerTab:AddButton({
    Name = "Diminuir Tamanho do Pulo",
    Callback = function()
        adjustJumpPower(false)
    end    
})

-- Player 
local GamesfpsTab = Window:MakeTab({
    Name = "Home",
    Icon = "rbxassetid://77163241748860",
    PremiumOnly = false
})

-- Shift Lock Button
GamesfpsTab:AddButton({
    Name = "Shift Lock",
    Callback = function()
        local ShiftlockStarterGui = Instance.new("ScreenGui")
        local ImageButton = Instance.new("ImageButton")

        ShiftlockStarterGui.Name = "Shiftlock (StarterGui)"
        ShiftlockStarterGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
        ShiftlockStarterGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

        ImageButton.Parent = ShiftlockStarterGui
        ImageButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        ImageButton.BackgroundTransparency = 1.000
        ImageButton.Position = UDim2.new(0.921914339, 0, 0.552375436, 0)
        ImageButton.Size = UDim2.new(0.0636147112, 0, 0.0661305636, 0)
        ImageButton.SizeConstraint = Enum.SizeConstraint.RelativeXX
        ImageButton.Image = "http://www.roblox.com/asset/?id=182223762"

        local runservice = game:GetService("RunService")
        local character = game.Players.LocalPlayer.Character or game.Players.LocalPlayer.CharacterAdded:Wait()
        local root = character:WaitForChild("HumanoidRootPart")
        local humanoid = character.Humanoid
        local camera = workspace.CurrentCamera
        local active = false

        local function EnableShiftlock()
            humanoid.AutoRotate = false
            root.CFrame = CFrame.new(root.Position, Vector3.new(camera.CFrame.LookVector.X * 900000, root.Position.Y, camera.CFrame.LookVector.Z * 900000))
            camera.CFrame = camera.CFrame * CFrame.new(1.7, 0, 0)
        end

        local function DisableShiftlock()
            humanoid.AutoRotate = true
            camera.CFrame = camera.CFrame * CFrame.new(-1.7, 0, 0)
            if active then
                active:Disconnect()
                active = nil
            end
        end

        ImageButton.MouseButton1Click:Connect(function()
            if not active then
                active = runservice.RenderStepped:Connect(EnableShiftlock)
            else
                DisableShiftlock()
            end
        end)
    end    
})

-- FPS Boost Button - Remove Texturas e Efeitos
GamesfpsTab:AddButton({
    Name = "FPS Boost",
    Callback = function()
        for _, object in pairs(workspace:GetDescendants()) do
            if object:IsA("Texture") or object:IsA("Decal") or object:IsA("Terrain") then
                object:Destroy()
            elseif object:IsA("ParticleEmitter") or object:IsA("PointLight") or object:IsA("SpotLight") or object:IsA("SurfaceLight") then
                object.Enabled = false
            end
        end
        game.Lighting.GlobalShadows = false
        game.Lighting.FogEnd = 100000
        game.Lighting.Brightness = 1
    end    
})

-- Função para criar ESP automaticamente
local function createESP(player)
    if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        -- Cria o contorno com `Highlight`
        local highlight = Instance.new("Highlight")
        highlight.Name = "PlayerESP"
        highlight.Adornee = player.Character
        highlight.FillTransparency = 1 -- deixa o preenchimento invisível, mostrando apenas o contorno
        highlight.OutlineTransparency = 0 -- torna o contorno visível
        highlight.OutlineColor = Color3.fromRGB(255, 0, 0) -- cor do contorno em vermelho
        highlight.Parent = player.Character

        -- Cria o nome acima do jogador
        local nameLabel = Instance.ne
        
