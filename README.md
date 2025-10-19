# Roblox Chat Title System

A customizable chat title/role system for Roblox games using TextChatService. Display player roles like Owner, Developer, Admin, VIP, and Streamer with custom colors in the chat.

![Roblox](https://img.shields.io/badge/Roblox-000000?style=for-the-badge&logo=roblox&logoColor=white)
![Lua](https://img.shields.io/badge/Lua-2C2D72?style=for-the-badge&logo=lua&logoColor=white)

## ✨ Features

- 🎨 **Customizable Titles** - Add any title you want (Owner, Dev, Admin, VIP, etc.)
- 🌈 **Color Customization** - Set custom RGB colors for each role
- 👤 **Display Name Support** - Shows player's Display Name instead of username
- 🔧 **Easy Configuration** - Simple username-based role assignment
- ⚡ **Modern Chat System** - Uses Roblox's TextChatService (new chat system)
- 🚀 **Client-Server Architecture** - Optimized performance with RemoteEvents

## 📋 Preview

```
[Owner] John: Hello everyone!
[Admin] Sarah: Welcome!
[VIP] Mike: Thanks!
Player123: Hi!
```

## 🛠️ Installation

### Step 1: Enable TextChatService

1. Open your game in **Roblox Studio**
2. Find **TextChatService** in Explorer
3. In Properties, change **ChatVersion** from `LegacyChatService` to **`TextChatService`**

### Step 2: Add ServerScript

1. Go to **ServerScriptService**
2. Create a new **Script**
3. Copy and paste the code from `ChatTitleServer`
4. Configure player roles (see Configuration section)

### Step 3: Add LocalScript

1. Go to **StarterPlayer > StarterPlayerScripts**
2. Create a new **LocalScript**
3. Copy and paste the code from `ChatTitleClient`

### Step 4: Test

- Use **Play** button or **Start Server and Players** (F7) to test
- Your titles should appear in chat!

## ⚙️ Configuration

Edit the `PlayerRoles` table in **ServerScript.lua**:

```lua
local PlayerRoles = {
    -- Format: ["Username"] = {"Title", Color3.fromRGB(R, G, B)}
    
    -- Examples:
    ["BuildermanRBLX"] = {"Owner", Color3.fromRGB(255, 0, 0)},      -- Red
    ["JohnDoe123"] = {"Dev", Color3.fromRGB(0, 170, 255)},          -- Blue
    ["SarahGamer"] = {"Admin", Color3.fromRGB(255, 170, 0)},        -- Orange
    ["ProPlayer"] = {"VIP", Color3.fromRGB(255, 215, 0)},           -- Gold
    ["StreamerPro"] = {"Streamer", Color3.fromRGB(138, 43, 226)},   -- Purple
    
    -- Add more players here:
    -- ["Username"] = {"Title", Color3.fromRGB(R, G, B)},
}
```

### Default Color Presets

| Role | Color | RGB |
|------|-------|-----|
| Owner | 🔴 Red | `255, 0, 0` |
| Developer | 🔵 Blue | `0, 170, 255` |
| Admin | 🟠 Orange | `255, 170, 0` |
| VIP | 🟡 Gold | `255, 215, 0` |
| Streamer | 🟣 Purple | `138, 43, 226` |

## 📁 File Structure

```
YourGame/
├── ServerScriptService/
│   └── ServerScript.lua          (Role configuration & server logic)
└── StarterPlayer/
    └── StarterPlayerScripts/
        └── LocalScript.lua        (Client-side chat display)
```

## 🔍 How It Works

1. **Server** stores all player roles and their configurations
2. **Client** requests role data from server via RemoteEvent
3. **TextChatService.OnIncomingMessage** intercepts chat messages
4. Script adds custom prefix with title and color to each message

## ⚠️ Important Notes

- ⚠️ **Usernames are case-sensitive!** Make sure to type them exactly as they appear on Roblox
- ⚠️ **TextChatService only** - This script requires the new chat system
- ✅ Works in Play mode, Test Server, and Published games
- ✅ Display Names are automatically shown

## 🐛 Troubleshooting

### Titles not showing up?
- ✅ Check if **ChatVersion** is set to `TextChatService`
- ✅ Verify username spelling (case-sensitive!)
- ✅ Make sure both scripts are in correct locations
- ✅ Check Output console for error messages

### Script errors in Play mode?
- ✅ Make sure you're using **both** ServerScript and LocalScript
- ✅ Try using "Start Server and Players" (F7) instead of Play button

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](../../issues).

## 💖 Support

If you found this helpful, please consider:
- ⭐ Starring this repository
- 🐛 Reporting bugs
- 💡 Suggesting new features

## 📧 Contact

Have questions? Feel free to open an issue or reach out!

---

Made with ❤️ for the Roblox development community
