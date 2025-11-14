--[[
    HUB RGB com Áreas e Color Picker Gradiente
    (Personalize como quiser e integre ao seu sistema!)
--]]

local Players = game:GetService("Players")
local LP = Players.LocalPlayer

local function applyColor(tipo, rgb)
    LP.startevent:FireServer(tipo, rgb)
end

local function toNormalized(r, g, b)
    return string.format("%.3f,%.3f,%.3f", r/255, g/255, b/255)
end

local function toRGB(str)
    local r, g, b = str:match("(%d+),(%d+),(%d+)")
    return tonumber(r), tonumber(g), tonumber(b)
end

-- Area Principal do HUB
local mainFrame = Instance.new("Frame", Window)
mainFrame.Size = UDim2.new(0,370,0,300)
mainFrame.Position = UDim2.new(0,15,0,60)
mainFrame.BackgroundTransparency = 1

local layout = Instance.new("UIListLayout", mainFrame)
layout.Padding = UDim.new(0,14)

-----------------------------------------------------
-- Área 1: Por números + quadrado de cor
local areaNum = Instance.new("Frame", mainFrame)
areaNum.Size = UDim2.new(1,0,0,95)
areaNum.BackgroundTransparency = 1
local subtitle1 = Instance.new("TextLabel", areaNum)
subtitle1.Position = UDim2.new(0,0,0,0)
subtitle1.Size = UDim2.new(1,0,0,16)
subtitle1.BackgroundTransparency = 1
subtitle1.Text = "Escolher cor por números (RGB)"
subtitle1.TextColor3 = Color3.new(1,1,1)
subtitle1.Font = Enum.Font.GothamBold
subtitle1.TextSize = 15

-- Campo números cabelo
local txtNumHair = Instance.new("TextBox", areaNum)
txtNumHair.PlaceholderText = "RGB cabelo (ex: 102,0,179)"
txtNumHair.Text = ""
txtNumHair.Font = Enum.Font.GothamSemibold
txtNumHair.TextSize = 15
txtNumHair.Position = UDim2.new(0,110,0,24)
txtNumHair.Size = UDim2.new(0,130,0,24)
txtNumHair.BackgroundColor3 = Color3.fromRGB(41,74,122)
txtNumHair.TextColor3 = Color3.new(1,1,1)

-- Quadrado mostrando cor cabelo atual
local squareHair = Instance.new("Frame", areaNum)
squareHair.Size = UDim2.new(0,24,0,24)
squareHair.Position = UDim2.new(0,250,0,24)
squareHair.BackgroundColor3 = Color3.fromRGB(102,0,179)
squareHair.BorderSizePixel = 2

local btnNumHair = Instance.new("TextButton", areaNum)
btnNumHair.Text = "Aplicar RGB p/ cabelo"
btnNumHair.Size = UDim2.new(0,130,0,24)
btnNumHair.Position = UDim2.new(0,110,0,56)
btnNumHair.Font = Enum.Font.GothamBold
btnNumHair.TextSize = 15
btnNumHair.BackgroundColor3 = Color3.fromRGB(41,74,122)
btnNumHair.TextColor3 = Color3.new(1,1,1)
btnNumHair.MouseButton1Click:Connect(function()
    local r,g,b = toRGB(txtNumHair.Text)
    if r and g and b then
        squareHair.BackgroundColor3 = Color3.fromRGB(r,g,b)
        applyColor("haircolor", toNormalized(r,g,b))
    end
end)

-- Campo números pele
local txtNumSkin = Instance.new("TextBox", areaNum)
txtNumSkin.PlaceholderText = "RGB pele (ex: 255,220,179)"
txtNumSkin.Text = ""
txtNumSkin.Font = Enum.Font.GothamSemibold
txtNumSkin.TextSize = 15
txtNumSkin.Position = UDim2.new(0,0,0,24)
txtNumSkin.Size = UDim2.new(0,100,0,24)
txtNumSkin.BackgroundColor3 = Color3.fromRGB(41,74,122)
txtNumSkin.TextColor3 = Color3.new(1,1,1)

-- Quadrado mostrando cor pele atual
local squareSkin = Instance.new("Frame", areaNum)
squareSkin.Size = UDim2.new(0,24,0,24)
squareSkin.Position = UDim2.new(0,100,0,56)
squareSkin.BackgroundColor3 = Color3.fromRGB(255,220,179)
squareSkin.BorderSizePixel = 2

local btnNumSkin = Instance.new("TextButton", areaNum)
btnNumSkin.Text = "Aplicar RGB p/ pele"
btnNumSkin.Size = UDim2.new(0,100,0,24)
btnNumSkin.Position = UDim2.new(0,0,0,56)
btnNumSkin.Font = Enum.Font.GothamBold
btnNumSkin.TextSize = 15
btnNumSkin.BackgroundColor3 = Color3.fromRGB(41,74,122)
btnNumSkin.TextColor3 = Color3.new(1,1,1)
btnNumSkin.MouseButton1Click:Connect(function()
    local r,g,b = toRGB(txtNumSkin.Text)
    if r and g and b then
        squareSkin.BackgroundColor3 = Color3.fromRGB(r,g,b)
        applyColor("skin", toNormalized(r,g,b))
    end
end)

-------------------------------------------------------
-- Área 2: Picker gradiente (Color Picker visual)
local areaPick = Instance.new("Frame", mainFrame)
areaPick.Size = UDim2.new(1,0,0,165)
areaPick.BackgroundTransparency = 1

local subtitle2 = Instance.new("TextLabel", areaPick)
subtitle2.Position = UDim2.new(0,0,0,0)
subtitle2.Size = UDim2.new(1,0,0,16)
subtitle2.BackgroundTransparency = 1
subtitle2.Text = "Escolher cor puxando gradiente (Picker Visual)"
subtitle2.TextColor3 = Color3.new(1,1,1)
subtitle2.Font = Enum.Font.GothamBold
subtitle2.TextSize = 15

-- Color Picker gradiente para cabelo
local gradHair = Instance.new("ImageLabel",areaPick)
gradHair.Position = UDim2.new(0,25,0,30)
gradHair.Size = UDim2.new(0,80,0,80)
gradHair.Image          = "rbxassetid://7712384361" -- Exemplo gradiente, troque pelo seu!
gradHair.BackgroundColor3 = Color3.new(1,1,1)
gradHair.BorderSizePixel = 2
gradHair.Name = "GradHair"

-- Quadrado mostrando cor escolhida pelo picker cabelo
local pickHair = Instance.new("Frame",areaPick)
pickHair.Position = UDim2.new(0,105,0,50)
pickHair.Size = UDim2.new(0,24,0,24)
pickHair.BackgroundColor3 = Color3.fromRGB(102,0,179)
pickHair.BorderSizePixel = 2

local btnPickHair = Instance.new("TextButton", areaPick)
btnPickHair.Text = "Aplicar Picker Cabelo"
btnPickHair.Size = UDim2.new(0,90,0,24)
btnPickHair.Position = UDim2.new(0,135,0,50)
btnPickHair.Font = Enum.Font.GothamBold
btnPickHair.TextSize = 15
btnPickHair.BackgroundColor3 = Color3.fromRGB(41,74,122)
btnPickHair.TextColor3 = Color3.new(1,1,1)

-- Escolher cor pelo picker (click no gradiente)
gradHair.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        local mx = input.Position.X - gradHair.AbsolutePosition.X
        local my = input.Position.Y - gradHair.AbsolutePosition.Y
        local x = math.clamp(mx/gradHair.AbsoluteSize.X,0,1)
        local y = math.clamp(my/gradHair.AbsoluteSize.Y,0,1)
        -- Exemplo: gradiente linear esquerda-direita (simplificado)
        -- Se usar gradiente HSV, deve mapear corretamente!
        local r = math.floor(255 * x)
        local g = math.floor(255 * y)
        local b = 179 -- Fixo para roxo escuro, personalize para HSV!
        pickHair.BackgroundColor3 = Color3.fromRGB(r,g,b)
        btnPickHair.MouseButton1Click:Connect(function()
            applyColor("haircolor", toNormalized(r,g,b))
        end)
    end
end)

-- Color Picker gradiente para pele
local gradSkin = Instance.new("ImageLabel",areaPick)
gradSkin.Position = UDim2.new(0,230,0,30)
gradSkin.Size = UDim2.new(0,80,0,80)
gradSkin.Image = "rbxassetid://7712384361" -- Exemplo gradiente pele!
gradSkin.BackgroundColor3 = Color3.fromRGB(1,1,1)
gradSkin.BorderSizePixel = 2
gradSkin.Name = "GradSkin"

local pickSkin = Instance.new("Frame",areaPick)
pickSkin.Position = UDim2.new(0,310,0,50)
pickSkin.Size = UDim2.new(0,24,0,24)
pickSkin.BackgroundColor3 = Color3.fromRGB(255,220,179)
pickSkin.BorderSizePixel = 2

local btnPickSkin = Instance.new("TextButton", areaPick)
btnPickSkin.Text = "Aplicar Picker Pele"
btnPickSkin.Size = UDim2.new(0,90,0,24)
btnPickSkin.Position = UDim2.new(0,340,0,50)
btnPickSkin.Font = Enum.Font.GothamBold
btnPickSkin.TextSize = 15
btnPickSkin.BackgroundColor3 = Color3.fromRGB(41,74,122)
btnPickSkin.TextColor3 = Color3.new(1,1,1)

gradSkin.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        local mx = input.Position.X - gradSkin.AbsolutePosition.X
        local my = input.Position.Y - gradSkin.AbsolutePosition.Y
        local x = math.clamp(mx/gradSkin.AbsoluteSize.X,0,1)
        local y = math.clamp(my/gradSkin.AbsoluteSize.Y,0,1)
        local r = 255
        local g = math.floor(220 * (1-y) + 110 * y)
        local b = math.floor(179 * (1-x) + 63 * x)
        pickSkin.BackgroundColor3 = Color3.fromRGB(r,g,b)
        btnPickSkin.MouseButton1Click:Connect(function()
            applyColor("skin", toNormalized(r,g,b))
        end)
    end
end)
