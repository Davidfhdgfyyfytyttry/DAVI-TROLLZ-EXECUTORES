-- Script: ToggleInvisibilityHandler (no ServerScriptService)

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")

-- Cria ou referencia o RemoteEvent.
local toggleEvent = ReplicatedStorage:FindFirstChild("ToggleInvisibility")
if not toggleEvent then
    toggleEvent = Instance.new("RemoteEvent")
    toggleEvent.Name = "ToggleInvisibility"
    toggleEvent.Parent = ReplicatedStorage
end

toggleEvent.OnServerEvent:Connect(function(player, toggle)
    local character = player.Character
    if not character then return end
    
    -- Percorre todas as partes do personagem e ajusta a propriedade Transparency.
    -- Como esta alteração é replicada, os adversários verão o personagem totalmente invisível (Transparência = 1) se toggle=true.
    for _, part in ipairs(character:GetDescendants()) do
        if part:IsA("BasePart") then
            part.Transparency = (toggle and 1) or 0
        end
    end
end)
