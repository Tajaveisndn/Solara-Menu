-- Serviços
local TweenService = game:GetService("TweenService")
local HttpService = game:GetService("HttpService")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")

-- Configurações
local CONFIG = {
    TITLE = "SOLARA",
    VERSION = "v2.1",
    KEY_URL = "https://nowgarena.com/key/keycientsolaramenu.txt",
    COPY_LINK = "https://nowgarena.com/key/",
    THEME = {
        BACKGROUND = Color3.fromRGB(15, 15, 20),
        CONTAINER = Color3.fromRGB(20, 20, 25),
        ACCENT = Color3.fromRGB(65, 105, 225),
        DARK_ACCENT = Color3.fromRGB(45, 75, 180),
        TEXT = Color3.fromRGB(240, 240, 245),
        TEXT_DARK = Color3.fromRGB(150, 150, 160),
        SUCCESS = Color3.fromRGB(100, 200, 100),
        ERROR = Color3.fromRGB(220, 75, 75),
        GRADIENT_COLORS = {
            Color3.fromRGB(147, 112, 219),
            Color3.fromRGB(138, 43, 226),
            Color3.fromRGB(106, 90, 205),
            Color3.fromRGB(123, 104, 238),
            Color3.fromRGB(147, 112, 219)
        }
    }
}

-- Interface
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "SolaraAuth"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = Players.LocalPlayer:WaitForChild("PlayerGui")

-- Background
local Background = Instance.new("Frame")
Background.Size = UDim2.new(1, 0, 1, 0)
Background.BackgroundColor3 = CONFIG.THEME.BACKGROUND
Background.BackgroundTransparency = 0.4
Background.Parent = ScreenGui


-- Container Principal
local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 300, 0, 360)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -180)
MainFrame.BackgroundColor3 = CONFIG.THEME.CONTAINER
MainFrame.BorderSizePixel = 0
MainFrame.ClipsDescendants = true
MainFrame.Parent = ScreenGui

-- Sombra
local Shadow = Instance.new("ImageLabel")
Shadow.AnchorPoint = Vector2.new(0.5, 0.5)
Shadow.BackgroundTransparency = 1
Shadow.Position = UDim2.new(0.5, 0, 0.5, 0)
Shadow.Size = UDim2.new(1.1, 0, 1.1, 0)
Shadow.Image = "rbxassetid://1316045217"
Shadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
Shadow.ImageTransparency = 0.6
Shadow.ZIndex = -1
Shadow.Parent = MainFrame

-- Barra Superior com Gradiente
local TopBar = Instance.new("Frame")
TopBar.Size = UDim2.new(1, 0, 0, 2)
TopBar.BackgroundColor3 = CONFIG.THEME.ACCENT
TopBar.BorderSizePixel = 0
TopBar.Parent = MainFrame

local TopBarGradient = Instance.new("UIGradient")
TopBarGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, CONFIG.THEME.GRADIENT_COLORS[1]),
    ColorSequenceKeypoint.new(0.25, CONFIG.THEME.GRADIENT_COLORS[2]),
    ColorSequenceKeypoint.new(0.5, CONFIG.THEME.GRADIENT_COLORS[3]),
    ColorSequenceKeypoint.new(0.75, CONFIG.THEME.GRADIENT_COLORS[4]),
    ColorSequenceKeypoint.new(1, CONFIG.THEME.GRADIENT_COLORS[5])
})
TopBarGradient.Parent = TopBar

-- Título Principal
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 50)
Title.Position = UDim2.new(0, 0, 0, 20)
Title.BackgroundTransparency = 1
Title.Font = Enum.Font.GothamBold
Title.Text = CONFIG.TITLE
Title.TextColor3 = CONFIG.THEME.TEXT
Title.TextSize = 26
Title.Parent = MainFrame

-- Versão Estilizada
local Version = Instance.new("Frame")
Version.Size = UDim2.new(0, 60, 0, 22)
Version.Position = UDim2.new(0.5, 30, 0, 35)
Version.BackgroundColor3 = CONFIG.THEME.ACCENT
Version.BackgroundTransparency = 0.8
Version.Parent = MainFrame

local VersionGradient = Instance.new("UIGradient")
VersionGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, CONFIG.THEME.GRADIENT_COLORS[1]),
    ColorSequenceKeypoint.new(1, CONFIG.THEME.GRADIENT_COLORS[3])
})
VersionGradient.Rotation = 45
VersionGradient.Parent = Version

local VersionCorner = Instance.new("UICorner")
VersionCorner.CornerRadius = UDim.new(0, 4)
VersionCorner.Parent = Version

local VersionText = Instance.new("TextLabel")
VersionText.Size = UDim2.new(1, 0, 1, 0)
VersionText.BackgroundTransparency = 1
VersionText.Font = Enum.Font.GothamBold
VersionText.Text = CONFIG.VERSION
VersionText.TextColor3 = CONFIG.THEME.TEXT
VersionText.TextSize = 12
VersionText.Parent = Version

-- Campo de Input
local InputBox = Instance.new("Frame")
InputBox.Size = UDim2.new(0.85, 0, 0, 40)
InputBox.Position = UDim2.new(0.075, 0, 0, 100)
InputBox.BackgroundColor3 = CONFIG.THEME.BACKGROUND
InputBox.BorderSizePixel = 0
InputBox.Parent = MainFrame

local InputCorner = Instance.new("UICorner")
InputCorner.CornerRadius = UDim.new(0, 6)
InputCorner.Parent = InputBox

local KeyInput = Instance.new("TextBox")
KeyInput.Size = UDim2.new(0.9, 0, 1, 0)
KeyInput.Position = UDim2.new(0.05, 0, 0, 0)
KeyInput.BackgroundTransparency = 1
KeyInput.Font = Enum.Font.GothamSemibold
KeyInput.PlaceholderText = "Enter your key..."
KeyInput.Text = ""
KeyInput.TextColor3 = CONFIG.THEME.TEXT
KeyInput.PlaceholderColor3 = CONFIG.THEME.TEXT_DARK
KeyInput.TextSize = 14
KeyInput.Parent = InputBox

-- Botão de Verificação
local VerifyButton = Instance.new("TextButton")
VerifyButton.Size = UDim2.new(0.85, 0, 0, 40)
VerifyButton.Position = UDim2.new(0.075, 0, 0, 160)
VerifyButton.BackgroundColor3 = CONFIG.THEME.ACCENT
VerifyButton.BorderSizePixel = 0
VerifyButton.Font = Enum.Font.GothamBold
VerifyButton.Text = "VERIFY"
VerifyButton.TextColor3 = CONFIG.THEME.TEXT
VerifyButton.TextSize = 14
VerifyButton.AutoButtonColor = false
VerifyButton.Parent = MainFrame

local VerifyCorner = Instance.new("UICorner")
VerifyCorner.CornerRadius = UDim.new(0, 6)
VerifyCorner.Parent = VerifyButton

-- Botão Get Key
local GetKeyButton = Instance.new("TextButton")
GetKeyButton.Size = UDim2.new(0.85, 0, 0, 40)
GetKeyButton.Position = UDim2.new(0.075, 0, 0, 220)
GetKeyButton.BackgroundColor3 = CONFIG.THEME.BACKGROUND
GetKeyButton.BorderSizePixel = 0
GetKeyButton.Font = Enum.Font.GothamBold
GetKeyButton.Text = "GET KEY"
GetKeyButton.TextColor3 = CONFIG.THEME.TEXT
GetKeyButton.TextSize = 14
GetKeyButton.AutoButtonColor = false
GetKeyButton.Parent = MainFrame

local GetKeyCorner = Instance.new("UICorner")
GetKeyCorner.CornerRadius = UDim.new(0, 6)
GetKeyCorner.Parent = GetKeyButton

-- Status
local StatusText = Instance.new("TextLabel")
StatusText.Size = UDim2.new(0.85, 0, 0, 30)
StatusText.Position = UDim2.new(0.075, 0, 0, 280)
StatusText.BackgroundTransparency = 1
StatusText.Font = Enum.Font.GothamMedium
StatusText.Text = "Waiting for key..."
StatusText.TextColor3 = CONFIG.THEME.TEXT_DARK
StatusText.TextSize = 13
StatusText.Parent = MainFrame


-- Funções de Efeitos
local function createButtonEffect(button, baseColor)
    local hoverColor = baseColor:Lerp(Color3.new(1, 1, 1), 0.1)
    local clickColor = baseColor:Lerp(Color3.new(0, 0, 0), 0.1)

    button.MouseEnter:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {BackgroundColor3 = hoverColor}):Play()
    end)

    button.MouseLeave:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {BackgroundColor3 = baseColor}):Play()
    end)

    button.MouseButton1Down:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.1), {BackgroundColor3 = clickColor}):Play()
    end)

    button.MouseButton1Up:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.1), {BackgroundColor3 = hoverColor}):Play()
    end)
end

local function createShineEffect(frame)
    local shine = Instance.new("Frame")
    shine.BackgroundColor3 = Color3.new(1, 1, 1)
    shine.BorderSizePixel = 0
    shine.Size = UDim2.new(0.1, 0, 1, 0)
    shine.BackgroundTransparency = 0.9
    shine.ZIndex = frame.ZIndex + 1
    shine.Parent = frame

    local gradient = Instance.new("UIGradient")
    gradient.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0, 1),
        NumberSequenceKeypoint.new(0.5, 0.75),
        NumberSequenceKeypoint.new(1, 1)
    })
    gradient.Parent = shine

    spawn(function()
        while true do
            shine.Position = UDim2.new(-0.1, 0, 0, 0)
            local tween = TweenService:Create(shine, 
                TweenInfo.new(1, Enum.EasingStyle.Linear), 
                {Position = UDim2.new(1, 0, 0, 0)}
            )
            tween:Play()
            wait(3)
        end
    end)
end

local function createPulseEffect(button)
    local pulse = button:Clone()
    pulse.BackgroundTransparency = 0.8
    pulse.ZIndex = button.ZIndex - 1
    pulse.Text = ""
    pulse.AutoButtonColor = false
    pulse.Parent = button.Parent

    spawn(function()
        while true do
            pulse.Size = button.Size
            pulse.Position = button.Position
            local tween = TweenService:Create(pulse,
                TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
                {
                    Size = button.Size + UDim2.new(0, 20, 0, 20),
                    Position = button.Position - UDim2.new(0, 10, 0, 10),
                    BackgroundTransparency = 1
                }
            )
            tween:Play()
            wait(1.5)
        end
    end)
end

-- Aplicar Efeitos
createButtonEffect(VerifyButton, CONFIG.THEME.ACCENT)
createButtonEffect(GetKeyButton, CONFIG.THEME.BACKGROUND)
createShineEffect(Version)
createPulseEffect(VerifyButton)

-- Animação do Gradiente
spawn(function()
    local offset = 0
    RunService.RenderStepped:Connect(function()
        offset = (offset + 0.001) % 1
        TopBarGradient.Offset = Vector2.new(offset, 0)
    end)
end)



-- Função de Verificação
local function verificarKey(key)
    local success, response = pcall(function()
        return game:HttpGet(CONFIG.KEY_URL)
    end)
    
    if not success then return false end
    return string.find(string.lower(response), string.lower(string.gsub(key, "%s+", "")), 1, true) ~= nil
end

-- Eventos
VerifyButton.MouseButton1Click:Connect(function()
    local key = KeyInput.Text
    
    if key == "" then
        StatusText.Text = "🔴Please enter a key!"
        StatusText.TextColor3 = CONFIG.THEME.ERROR
        return
    end
    
    StatusText.Text = "🟡 Verifying..."
    StatusText.TextColor3 = CONFIG.THEME.ACCENT
    
    task.wait(0.5)
    if verificarKey(key) then
        StatusText.Text = "🟢 Key verified successfully!"
        StatusText.TextColor3 = CONFIG.THEME.SUCCESS
        
        wait(1)
        
        -- Animação de saída
        local exitTween = TweenService:Create(MainFrame,
            TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.In),
            {Size = UDim2.new(0, 0, 0, 0), Position = UDim2.new(0.5, 0, 0.5, 0)}
        )
        exitTween:Play()
        
        local fadeTween = TweenService:Create(Background,
            TweenInfo.new(0.5),
            {BackgroundTransparency = 1}
        )
        fadeTween:Play()
        
        wait(0.5)
        ScreenGui:Destroy()
        
        -- Carregar o script principal
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Tajaveisndn/hfgdsfiyagdw/refs/heads/main/README.md"))();
    else
        StatusText.Text = "Invalid key!"
        StatusText.TextColor3 = CONFIG.THEME.ERROR
        
        -- Efeito de erro
        local errorShake = TweenService:Create(MainFrame,
            TweenInfo.new(0.1, Enum.EasingStyle.Bounce, Enum.EasingDirection.InOut),
            {Position = MainFrame.Position + UDim2.new(0, 10, 0, 0)}
        )
        errorShake:Play()
        
        wait(0.1)
        
        local returnShake = TweenService:Create(MainFrame,
            TweenInfo.new(0.1, Enum.EasingStyle.Bounce, Enum.EasingDirection.InOut),
            {Position = UDim2.new(0.5, -150, 0.5, -180)}
        )
        returnShake:Play()
    end
end)

GetKeyButton.MouseButton1Click:Connect(function()
    -- Efeito de clique
    local clickEffect = TweenService:Create(GetKeyButton,
        TweenInfo.new(0.1, Enum.EasingStyle.Quad),
        {BackgroundColor3 = CONFIG.THEME.DARK_ACCENT}
    )
    clickEffect:Play()
    
    StatusText.Text = "Copying link..."
    StatusText.TextColor3 = CONFIG.THEME.ACCENT
    
    -- Copiar link para área de transferência
    setclipboard(CONFIG.COPY_LINK)
    
    wait(0.1)
    
    local returnEffect = TweenService:Create(GetKeyButton,
        TweenInfo.new(0.1, Enum.EasingStyle.Quad),
        {BackgroundColor3 = CONFIG.THEME.BACKGROUND}
    )
    returnEffect:Play()
    
    StatusText.Text = "Link copied to clipboard!"
    StatusText.TextColor3 = CONFIG.THEME.SUCCESS
    
    -- Abrir navegador
    task.spawn(function()
        wait(0.5)
        StatusText.Text = "Opening browser..."
        wait(0.5)
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "SOLARA",
            Text = "Link copied! Opening browser...",
            Duration = 5
        })
    end)
end)


-- Anti AFK
local VirtualUser = game:GetService("VirtualUser")
Players.LocalPlayer.Idled:Connect(function()
    VirtualUser:CaptureController()
    VirtualUser:ClickButton2(Vector2.new())
end)

-- Proteção contra exploits simples 
local function protectGui()
    local protected = {ScreenGui, MainFrame, KeyInput, VerifyButton}
    
    for _, obj in ipairs(protected) do
        obj.Name = HttpService:GenerateGUID(false)
    end
end
protectGui()

-- Efeito de inicialização
MainFrame.Size = UDim2.new(0, 0, 0, 0)
MainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
Background.BackgroundTransparency = 1

local openTween = TweenService:Create(MainFrame,
    TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
    {Size = UDim2.new(0, 300, 0, 360), Position = UDim2.new(0.5, -150, 0.5, -180)}
)

local fadeTween = TweenService:Create(Background,
    TweenInfo.new(0.5),
    {BackgroundTransparency = 0.4}
)

openTween:Play()
fadeTween:Play()
