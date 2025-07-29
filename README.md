-- LocalScript (colocar no StarterScripts)
local players = game:GetService("Players")
local localPlayer = players.LocalPlayer
local camera = game.Workspace.CurrentCamera

-- Configurações
local aimbotEnabled = true
local espEnabled = true

-- Função para aimbot
local function aimbot()
    if aimbotEnabled then
        for _, player in pairs(players:GetPlayers()) do
            if player ~= localPlayer and player.Character and player.Character:FindFirstChild("Head") then
                local head = player.Character.Head
                local aim = camera:WorldToScreenPoint(head.Position)
                if aim then
                    -- Grudar na cabeça do inimigo
                    camera.CFrame = CFrame.new(camera.CFrame.Position, head.Position)
                end
            end
        end
    end
end

-- Função para ESP
local function esp()
    if espEnabled then
        for _, player in pairs(players:GetPlayers()) do
            if player ~= localPlayer and player.Character and player.Character:FindFirstChild("Head") then
                local head = player.Character.Head
                local billboardGui = Instance.new("BillboardGui")
                billboardGui.Parent = head
                billboardGui.Size = UDim2.new(0, 50, 0, 50)
                billboardGui.StudsOffset = Vector3.new(0, 2, 0)
                local textLabel = Instance.new("TextLabel")
                textLabel.Parent = billboardGui
                textLabel.Size = UDim2.new(1, 0, 1, 0)
                textLabel.BackgroundTransparency = 1
                textLabel.Text = player.Name
                textLabel.TextColor3 = Color3.new(1, 0, 0)
                textLabel.TextSize = 20
            end
        end
    end
end

-- Loop para atualizar o aimbot e ESP
game:GetService("RunService").RenderStepped:Connect(function()
    aimbot()
    esp()
end)
