# Chat Title System

**Author:** ItoRenz00  
**Version:** 1.0.0

A customizable Roblox chat system that displays colored titles and names for players based on their assigned roles. Perfect for games that need role identification, staff management, or VIP systems.

---

## 🌟 Features

- 🎨 **Custom Colored Titles** - Display unique titles with custom RGB colors
- 👥 **Role-Based System** - Assign different roles to different players
- 🔄 **Automatic Sync** - Real-time role synchronization between server and clients
- 📱 **TextChatService Support** - Uses modern Roblox chat system
- ⚡ **Lightweight** - Optimized performance with minimal resource usage
- 🎯 **Easy Configuration** - Simple username-based role assignment
- 🔒 **Server-Authoritative** - Secure role management from server side

---

## 📋 Requirements

- Roblox Studio
- TextChatService enabled (default in new experiences)
- Basic understanding of Roblox scripting

---

## 🚀 Installation

### Step 1: Server Script Setup

1. Open your Roblox Studio project
2. Navigate to `ServerScriptService`
3. Create a new `Script` (not LocalScript)
4. Copy and paste the **server script code**
5. Name it `ChatTitleServer`

### Step 2: Client Script Setup

1. Navigate to `StarterPlayer` → `StarterPlayerScripts`
2. Create a new `LocalScript`
3. Copy and paste the **client script code**
4. Name it `ChatTitleClient`

### Step 3: Configuration

1. Open the **server script** in `ServerScriptService`
2. Find the `PlayerRoles` table
3. Replace the example usernames with your actual player usernames
4. Customize titles and colors as needed

---

## ⚙️ Configuration

### Adding Player Roles

Edit the `PlayerRoles` table in the server script:

```lua
local PlayerRoles = {
    ["Username"] = {"Title", Color3.fromRGB(R, G, B)},
}
```

**Parameters:**
- `Username` - Player's Roblox username (**case-sensitive!**)
- `Title` - Text displayed in brackets (e.g., "Owner", "VIP", "Admin")
- `Color3.fromRGB(R, G, B)` - RGB color values (0-255 for each)

### Example Configuration

```lua
local PlayerRoles = {
    -- Owner with red color
    ["PlayerName1"] = {"Owner", Color3.fromRGB(255, 0, 0)},
    
    -- Admin with orange color
    ["PlayerName2"] = {"Admin", Color3.fromRGB(255, 170, 0)},
    
    -- VIP with gold color
    ["PlayerName3"] = {"VIP", Color3.fromRGB(255, 215, 0)},
    
    -- Developer with blue color
    ["PlayerName4"] = {"Dev", Color3.fromRGB(0, 170, 255)},
    
    -- Moderator with green color
    ["PlayerName5"] = {"Mod", Color3.fromRGB(0, 255, 127)},
}
```

### Color Presets

Here are some popular color combinations:

| Role | Color | RGB Values |
|------|-------|------------|
| Owner | Red | `255, 0, 0` |
| Admin | Orange | `255, 170, 0` |
| Developer | Blue | `0, 170, 255` |
| Moderator | Green | `0, 255, 127` |
| VIP | Gold | `255, 215, 0` |
| Premium | Purple | `138, 43, 226` |
| Helper | Cyan | `0, 255, 255` |
| Streamer | Pink | `255, 105, 180` |

---

## 💬 Chat Format

Messages will appear in this format:

```
[Title] DisplayName: message content
```

**Examples:**
```
[Owner] John: Welcome to the game!
[VIP] Sarah: Thanks for the updates!
[Dev] Mike: Working on new features!
```

Both the title and display name will use the same color specified in the configuration.

---

## 🔧 Troubleshooting

### Titles Not Showing

**Problem:** Player titles don't appear in chat

**Solutions:**
- ✅ Verify username spelling matches exactly (case-sensitive)
- ✅ Check that `GetPlayerRole` RemoteEvent exists in ReplicatedStorage
- ✅ Ensure both server and client scripts are in correct locations
- ✅ Restart your game/server after making changes
- ✅ Check Output window for error messages

### Wrong Colors Displaying

**Problem:** Colors appear different than expected

**Solutions:**
- ✅ Confirm RGB values are between 0-255
- ✅ Use `Color3.fromRGB()` not `Color3.new()`
- ✅ Check for typos in the color values

### New Players Not Getting Roles

**Problem:** Players joining after game start don't see roles

**Solutions:**
- ✅ Verify `PlayerAdded` event is connected in server script
- ✅ Check that client script is in `StarterPlayerScripts`
- ✅ Ensure proper delays are in place for client initialization

### RemoteEvent Not Found Error

**Problem:** "GetPlayerRole" not found in ReplicatedStorage

**Solutions:**
- ✅ Make sure server script runs before client script
- ✅ Check that server script is in `ServerScriptService`
- ✅ Verify RemoteEvent creation code is present in server script

---

## 🎓 Advanced Usage

### Dynamic Role Changes

To change a player's role during runtime:

```lua
-- Server Script
local function updatePlayerRole(playerName, newTitle, newColor)
    PlayerRoles[playerName] = {newTitle, newColor}
    
    -- Notify all clients
    for _, player in ipairs(Players:GetPlayers()) do
        RoleEvent:FireClient(player, playerName, PlayerRoles[playerName])
    end
end

-- Example usage
updatePlayerRole("PlayerName", "SuperVIP", Color3.fromRGB(255, 0, 255))
```

### Group-Based Roles

Assign roles based on Roblox group ranks:

```lua
-- Server Script
Players.PlayerAdded:Connect(function(player)
    local groupId = 1234567 -- Your group ID
    local rank = player:GetRankInGroup(groupId)
    
    if rank >= 255 then
        PlayerRoles[player.Name] = {"Owner", Color3.fromRGB(255, 0, 0)}
    elseif rank >= 200 then
        PlayerRoles[player.Name] = {"Admin", Color3.fromRGB(255, 170, 0)}
    elseif rank >= 100 then
        PlayerRoles[player.Name] = {"Mod", Color3.fromRGB(0, 255, 127)}
    end
    
    -- Send updated role to all clients
    for _, otherPlayer in ipairs(Players:GetPlayers()) do
        local role = PlayerRoles[player.Name]
        if role then
            RoleEvent:FireClient(otherPlayer, player.Name, role)
        end
    end
end)
```

### GamePass-Based Roles

Grant roles to players with specific GamePasses:

```lua
-- Server Script
local MarketplaceService = game:GetService("MarketplaceService")

Players.PlayerAdded:Connect(function(player)
    local vipPassId = 123456 -- Your GamePass ID
    
    local hasPass = false
    local success, message = pcall(function()
        hasPass = MarketplaceService:UserOwnsGamePassAsync(player.UserId, vipPassId)
    end)
    
    if hasPass then
        PlayerRoles[player.Name] = {"VIP", Color3.fromRGB(255, 215, 0)}
        
        -- Notify all clients
        for _, otherPlayer in ipairs(Players:GetPlayers()) do
            RoleEvent:FireClient(otherPlayer, player.Name, PlayerRoles[player.Name])
        end
    end
end)
```

---

## 📁 File Structure

```
YourGame
├── ServerScriptService
│   └── ChatTitleServer (Script)
├── StarterPlayer
│   └── StarterPlayerScripts
│       └── ChatTitleClient (LocalScript)
└── ReplicatedStorage
    └── GetPlayerRole (RemoteEvent) - Created automatically
```

---

## 🔒 Security Notes

- ✅ All role assignments are server-authoritative
- ✅ Clients cannot modify their own roles
- ✅ Role data is validated before sending to clients
- ✅ Safe from client-side exploits

---

## 📝 Changelog

### Version 1.0.0 (Current)
- Initial release
- Basic role system with colored titles
- Server-client synchronization
- Automatic role distribution to new players
- Comprehensive documentation

---

## 🤝 Contributing

Feel free to fork this project and submit pull requests for improvements!

**Ideas for contributions:**
- Additional color presets
- Role priority system
- Multiple title support
- Animation effects
- Sound effects on role assignment

---

## 📄 License

This project is free to use and modify for your Roblox games.  
**Credit to ItoRenz00 is appreciated but not required.**

---

## 🆘 Support

If you encounter issues or have questions:

1. Check the **Troubleshooting** section above
2. Review the **Output** window in Studio for errors
3. Verify all installation steps were followed correctly
4. Open an issue on the GitHub repository

---

## 👨‍💻 Author

**ItoRenz00**

---

## ⭐ Show Your Support

If this system helped your game, consider:
- ⭐ Starring the repository
- 🔄 Sharing with other developers
- 💬 Leaving feedback

---

**Made with ❤️ by ItoRenz00**
