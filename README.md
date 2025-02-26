local button = script.Parent
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local skinIds = {
    "11405608979", 
    "", 
    "", 
    "17254265328", 
    "", 
    "", 
    "12283967892", 
    "15058312012", 
    "13662772002",
    "12654750434",  
    "",  
    ""  
}
local currentSkinIndex = 1
local hasSkin = false

local function equipSkin()
    if hasSkin then
        return
    end

    local pants = Instance.new("Pants")
    pants.PantsTemplate = "rbxassetid://" .. skinIds[currentSkinIndex]
    pants.Parent = character

    local shirt = Instance.new("Shirt")
    shirt.ShirtTemplate = "rbxassetid://" .. skinIds[currentSkinIndex + 3]
    shirt.Parent = character

    if currentSkinIndex > 3 then
        local accessory = Instance.new("Accessory")
        accessory.AssetId = "rbxassetid://" .. skinIds[currentSkinIndex]
        accessory.Parent = character
        accessory.AttachmentPoint = humanoid:WaitForChild("Head")
    end

    if currentSkinIndex > 6 then
        local hair = Instance.new("Accessory")
        hair.AssetId = "rbxassetid://" .. skinIds[currentSkinIndex]
        hair.Parent = character
        hair.AttachmentPoint = humanoid:WaitForChild("Head")
    end
    
    hasSkin = true
end

local function removeSkin()
    if not hasSkin then
        return
    end
    
    for _, accessory in pairs(character:GetChildren()) do
        if accessory:IsA("Pants") and accessory.PantsTemplate == "rbxassetid://" .. skinIds[currentSkinIndex] then
            accessory:Destroy()
        end
    end
    
    for _, accessory in pairs(character:GetChildren()) do
        if accessory:IsA("Shirt") and accessory.ShirtTemplate == "rbxassetid://" .. skinIds[currentSkinIndex + 3] then
            accessory:Destroy()
        end
    end
    
    for _, accessory in pairs(character:GetChildren()) do
        if accessory:IsA("Accessory") and accessory.AssetId == "rbxassetid://" .. skinIds[currentSkinIndex + 6] then
            accessory:Destroy()
        end
    end
    
    for _, accessory in pairs(character:GetChildren()) do
        if accessory:IsA("Accessory") and accessory.AssetId == "rbxassetid://" .. skinIds[currentSkinIndex + 9] then
            accessory:Destroy()
        end
    end
    
    hasSkin = false
end

local function switchSkin()
    removeSkin()
    currentSkinIndex = currentSkinIndex + 1
    if currentSkinIndex > #skinIds then
        currentSkinIndex = 1
    end
    equipSkin()
end

button.MouseButton1Click:Connect(function()
    switchSkin()
end)
