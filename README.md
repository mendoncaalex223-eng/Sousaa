-- Blox Fruits GUI com Teleporte para Bosses, Auto Coleta de Frutas e M1
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Workspace = game:GetService("Workspace")
local UserInputService = game:GetService("UserInputService")
local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")

-- Criar ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "BloxFruitsGUI"
ScreenGui.Parent = PlayerGui

-- Frame principal
local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 350, 0, 400)
MainFrame.Position = UDim2.new(0.5, -175, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(30,30,30)
MainFrame.BorderSizePixel = 0
MainFrame.Parent = ScreenGui

-- Título
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1,0,0,50)
Title.Position = UDim2.new(0,0,0,0)
Title.BackgroundColor3 = Color3.fromRGB(50,50,50)
Title.Text = "Blox Fruits GUI"
Title.TextColor3 = Color3.fromRGB(255,255,255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 22
Title.Parent = MainFrame

-- Status
local Status = Instance.new("TextLabel")
Status.Size = UDim2.new(1,0,0,30)
Status.Position = UDim2.new(0,0,0,370)
Status.BackgroundColor3 = Color3.fromRGB(40,40,40)
Status.TextColor3 = Color3.fromRGB(255,255,255)
Status.Text = "Status: Inativo"
Status.Font = Enum.Font.Gotham
Status.TextSize = 16
Status.Parent = MainFrame

-- Função de toggle
local function createToggle(text, position, callback)
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0,200,0,40)
    label.Position = position
    label.BackgroundColor3 = Color3.fromRGB(60,60,60)
    label.Text = text
    label.TextColor3 = Color3.fromRGB(255,255,255)
    label.Font = Enum.Font.GothamBold
    label.TextSize = 16
    label.Parent = MainFrame

    local toggle = Instance.new("TextButton")
    toggle.Size = UDim2.new(0,100,0,40)
    toggle.Position = UDim2.new(0,200,0,position.Y.Offset)
    toggle.BackgroundColor3 = Color3.fromRGB(150,0,0)
    toggle.Text = "OFF"
    toggle.TextColor3 = Color3.fromRGB(255,255,255)
    toggle.Font = Enum.Font.GothamBold
    toggle.TextSize = 16
    toggle.Parent = MainFrame

    local state = false
    toggle.MouseButton1Click:Connect(function()
        state = not state
        toggle.Text = state and "ON" or "OFF"
        toggle.BackgroundColor3 = state and Color3.fromRGB(0,150,0) or Color3.fromRGB(150,0,0)
        callback(state)
    end)
end

-- Variáveis
local AutoFruit = false
local M1Enabled = false

-- Função Auto coleta de frutas
local function autoCollectFruits(state)
    AutoFruit = state
    Status.Text = state and "Status: Auto Fruit Ativo" or "Status: Inativo"
    if AutoFruit then
        spawn(function()
            while AutoFruit do
                wait(1)
                for _, fruit in pairs(Workspace:WaitForChild("Fruits"):GetChildren()) do
                    if fruit:FindFirstChild("TouchInterest") then
                        Player.Character.HumanoidRootPart.CFrame = fruit.Position + Vector3.new(0,3,0)
                    end
                end
            end
        end)
    end
end

-- Função Teleporte para Boss
local function teleportToBoss(island, bossName)
    local bosses = {
        ["Gorilla King"] = CFrame.new(100, 10, 100),
        ["Bobby"] = CFrame.new(200, 10, 200),
        -- Adicione as coordenadas dos outros bosses aqui
    }
    local bossPosition = bosses[bossName]
    if bossPosition then
        Player.Character.HumanoidRootPart.CFrame = bossPosition
        Status.Text = "Status: Teleportado para " .. bossName
    else
        Status.Text = "Status: Boss não encontrado"
    end
end

-- Função M1 (ataque com botão esquerdo do mouse)
local function toggleM1(state)
    M1Enabled = state
    Status.Text = state and "Status: M1 Ativo" or "Status: Inativo"
    if M1Enabled then
        spawn(function()
            while M1Enabled do
                wait(0.1)
                if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
                    if ReplicatedStorage:FindFirstChild("RemoteEvents") then
                        local remotes = ReplicatedStorage.RemoteEvents
                        if remotes:FindFirstChild("MeleeEvent") then
                            remotes.MeleeEvent:FireServer() -- envia ataque M1
                        end
                    end
                end
            end
        end)
    end
end

-- Criar toggles
createToggle("Auto Coleta Frutas", UDim2.new(0,20,0,70), autoCollectFruits)
createToggle("M1 (Ataque)", UDim2.new(0,20,0,130), toggleM1)

-- Criar botões de teleporte para bosses
local function createBossButton(bossName, position)
    local button = Instance.new
::contentReference[oaicite:95]{index=95}

 
