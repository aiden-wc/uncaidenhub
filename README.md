function esp()

    local players = game:GetService("Players"):GetChildren()
    local RunService = game:GetService("RunService")
    local highlight = Instance.new("Highlight")
    highlight.Name = "Highlight"
    
    for i, v in pairs(players) do
        repeat wait() until v.Character
        if not v.Character:FindFirstChild("HumanoidRootPart"):FindFirstChild("Highlight") then
        local highlightclone = highlight:Clone()
        highlightclone.Parent = v.Character:FindFirstChild("HumanoidRootPart")
        highlightclone.Adornee = v.Character
        highlightclone.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
        highlightclone.Name = "Highlight"
    end
    end
    
    game.Players.PlayerAdded:Connect(function(player)
        repeat wait() until player.Character
        if not player.Character:FindFirstChild("HumanoidRootPart"):FindFirstChild("Highlight") then
            local highlightclone = highlight:Clone()
            highlightclone.Adornee = player.Character
            highlightclone.Parent = player.Character:FindFirstChild("HumanoidRootPart")
            highlightclone.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
            highlightclone.Name = "Highlight"
        end
    end)
    
    game.Players.PlayerRemoving:Connect(function(playerRemoved)
        playerRemoved.Character:FindFirstChild("HumanoidRootPart").Highlight:Destroy()
    end)
    
    RunService.Heartbeat:Connect(function()
        for i, v in pairs(players) do
            repeat wait() until v.Character
            if not v.Character:FindFirstChild("HumanoidRootPart"):FindFirstChild("Highlight") then
                local highlightclone = highlight:Clone()
                highlightclone.Adornee = v.Character
                highlightclone.Parent = v.Character:FindFirstChild("HumanoidRootPart")
                highlightclone.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                highlightclone.Name = "Highlight"
            end
        end
    end)
    
    
    end
-----end esp func


local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()
local Window = Rayfield:CreateWindow({
   Name = "uncle aidens hub",
   LoadingTitle = "uncle aidens hub",
   LoadingSubtitle = "by aiden_wc",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "Big Hub"
   },
   Discord = {
      Enabled = false,
      Invite = "noinvitelink", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },
   KeySystem = true, -- Set this to true to use our key system
   KeySettings = {
      Title = "uncle aidens hub",
      Subtitle = "aiden_wc",
      Note = "you need a key silly",
      FileName = "Key", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = false, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"YDBgHpJq0MI+jA+YB6dQEefWHJ2RXtfbKY3hdfQS/7Y="} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
   }
})



local Tab1 = Window:CreateTab("player", 4483362458) -- Title, Image
local Tab2 =  Window:CreateTab("tools", 4483362458) -- Title, Image
local TabC =  Window:CreateTab("combat", 4483362458) -- Title, Image
local TabG =  Window:CreateTab("guis", 4483362458) -- Title, Image
local Section1 = Tab1:CreateSection("player")
local Section2 = Tab2:CreateSection("tools")
local SectionC = TabC:CreateSection("combat")
local SectionG = TabG:CreateSection("guis")


local Slider = Tab1:CreateSlider({
   Name = "speed",
   Range = {16, 1000},
   Increment = 1,
   Suffix = "speed",
   CurrentValue = 16,
   Flag = "speedSlider", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value  
   end,
})

local Slider = Tab1:CreateSlider({
   Name = "jump",
   Range = {56, 1000},
   Increment = 1,
   Suffix = "jump",
   CurrentValue = 56,
   Flag = "jumpSlider", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = Value  
   end,
})

local Slider = Tab1:CreateSlider({
    Name = "health",
    Range = {0, 100},
    Increment = 1,
    Suffix = "health",
    CurrentValue = 100,
    Flag = "jumpSlider", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
         game.Players.LocalPlayer.Character.Humanoid.Health = Value  
    end,
 })

local Toggle = Tab1:CreateToggle({
    Name = "inf jump",
    CurrentValue = false,
    Flag = "infjumpToggle", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        local InfiniteJumpEnabled = Value
            game:GetService("UserInputService").JumpRequest:connect(function()
	            if InfiniteJumpEnabled then
		            game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")
	            end
            end)

    end,
 })

--------end t1

local Button = Tab2:CreateButton({
   Name = "tp tool",
   Callback = function()
    local mouse = game.Players.LocalPlayer:GetMouse()
    local tool = Instance.new("Tool")
    tool.RequiresHandle = false
    tool.Name = "Equip to Click TP"
    tool.Activated:connect(function()
        local pos = mouse.Hit+Vector3.new(0,2.5,0)
        pos = CFrame.new(pos.X,pos.Y,pos.Z)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = pos
    end)
    tool.Parent = game.Players.LocalPlayer.Backpack
   end,
})

-- end t2

local Toggle = TabC:CreateToggle({
    Name = "ESP",
    CurrentValue = false,
    Flag = "infjumpToggle", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
      esp()
    end,
 })

 local Label = TabC:CreateLabel("Once turned on, you can't turn off")

-- end tp

local Button = TabG:CreateButton({
    Name = "r spy",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/aiden-wc/spy-script/main/spyscript"))()
    end,
 })

 local Button = TabG:CreateButton({
    Name = "inf yield",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
    end,
 })

 ---- end tc
