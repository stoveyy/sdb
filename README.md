local Players = game:GetService ("Players")
local TeleportService = game:GetService ("TeleportService")

-- get the local player
local player = Players.LocalPlayer

-- get the character and the humanoid root part
local character = player.Character or player.CharacterAdded:Wait ()
local hrp = character:WaitForChild ("HumanoidRootPart")

-- create a list of other players in the server
local otherPlayers = {}

-- loop through all players and add them to the list if they are not the local player
for _, p in pairs (Players:GetPlayers ()) do
  if p ~= player then
    table.insert (otherPlayers, p)
  end
end

-- create a function to teleport to a random player from the list
local function teleportToRandomPlayer ()
  -- get a random index from the list
  local index = math.random (#otherPlayers)
  
  -- get the player at that index
  local targetPlayer = otherPlayers [index]
  
  -- get the character and the humanoid root part of the target player
  local targetCharacter = targetPlayer.Character or targetPlayer.CharacterAdded:Wait ()
  local targetHrp = targetCharacter:WaitForChild ("HumanoidRootPart")
  
  -- set the CFrame of the local player's humanoid root part to the target player's humanoid root part
  hrp.CFrame = targetHrp.CFrame
  
  -- wait for 5 seconds
  wait (5)
  
  -- teleport to another random player
  teleportToRandomPlayer ()
end

-- call the function
teleportToRandomPlayer ()
