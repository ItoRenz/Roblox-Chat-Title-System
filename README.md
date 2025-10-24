# 💬 Roblox Chat Title System

[![Roblox](https://img.shields.io/badge/Roblox-Studio-00a2ff?logo=roblox&logoColor=white)](https://www.roblox.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-1.1.0-blue.svg)](https://github.com/yourusername/roblox-chat-title-system)

A fully customizable chat title system for Roblox that displays colored titles next to player names in chat. Perfect for showing roles like Owner, Developer, Admin, VIP, Moderator, and more!

## ✨ Features

- 🎨 **Fully Customizable Colors** - Set any RGB color for titles and names
- 👥 **Multiplayer Support** - All players can see each other's titles
- ⚡ **Real-time Updates** - Titles appear instantly when players join
- 🔄 **Automatic Sync** - Server automatically broadcasts role updates to all clients
- 🎯 **Easy Configuration** - Simple table-based role management
- 🛡️ **Optimized Performance** - Efficient client-server communication
- 🧹 **Auto Cleanup** - Removes data when players leave

## 📸 Preview

```
[Owner] PlayerName: Hello everyone!
[Dev] DeveloperName: Working on new features!
[VIP] VIPPlayer: Thanks for the VIP!
```

## 🚀 Installation

### Step 1: Install Server Script

1. Open Roblox Studio
2. Navigate to `ServerScriptService`
3. Create a new `Script`
4. Copy and paste the **Server Script** code
5. Configure the `PlayerRoles` table with your players

### Step 2: Install Client Script

1. Navigate to `StarterPlayer > StarterPlayerScripts`
2. Create a new `LocalScript`
3. Copy and paste the **Client Script** code

### Step 3: Test!

Press **Play** in Studio and chat to see your custom titles!

## ⚙️ Configuration

Edit the `PlayerRoles` table in the **Server Script**:

```lua
local PlayerRoles = {
    -- Format: ["Username"] = {"Title", Color3.fromRGB(R, G, B)}
    
    ["YourUsername"] = {"Owner", Color3.fromRGB(255, 0, 0)},        -- Red
    ["DevUsername"] = {"Dev", Color3.fromRGB(0, 170, 255)},         -- Blue
    ["AdminUsername"] = {"Admin", Color3.fromRGB(255, 170, 0)},     -- Orange
    ["VIPUsername"] = {"VIP", Color3.fromRGB(255, 215, 0)},         -- Gold
    ["ModUsername"] = {"Mod", Color3.fromRGB(0, 255, 127)},         -- Green
    ["StreamerUsername"] = {"Streamer", Color3.fromRGB(138, 43, 226)}, -- Purple
}
```

### 🎨 Color Examples

| Role | RGB Code | Preview |
|------|----------|---------|
| Owner | `255, 0, 0` | 🔴 Red |
| Developer | `0, 170, 255` | 🔵 Blue |
| Admin | `255, 170, 0` | 🟠 Orange |
| VIP | `255, 215, 0` | 🟡 Gold |
| Moderator | `0, 255, 127` | 🟢 Green |
| Streamer | `138, 43, 226` | 🟣 Purple |
| Helper | `255, 192, 203` | 🩷 Pink |
| Tester | `0, 255, 255` | 🩵 Cyan |

## 📁 File Structure

```
YourGame/
├── ServerScriptService/
│   └── ChatTitleServer.lua          -- Server-side role management
├── StarterPlayer/
│   └── StarterPlayerScripts/
│       └── ChatTitleClient.lua      -- Client-side title display
└── ReplicatedStorage/
    └── GetPlayerRole                -- Auto-created RemoteEvent
```

## 🔧 How It Works

1. **Server** manages all player roles in a central table
2. When a player joins, the **Server** broadcasts their role to all clients
3. Each **Client** receives and stores role data locally
4. When a chat message is sent, the **Client** formats it with the colored title
5. All players see the formatted message with titles!

## 🛠️ Troubleshooting

### Titles not showing?

- ✅ Make sure both scripts are in the correct locations
- ✅ Check that usernames are spelled correctly (case-sensitive!)
- ✅ Verify the RemoteEvent "GetPlayerRole" exists in ReplicatedStorage

### Titles only visible to one player?

- ✅ Make sure you're using **version 1.1.0** with broadcast support
- ✅ Check the server console for broadcast confirmation messages

### Colors not working?

- ✅ RGB values must be between 0-255
- ✅ Use `Color3.fromRGB()` not `Color3.new()`

## 📝 Changelog

### Version 1.1.0 (Current)
- ✨ Added multiplayer support - all players can now see titles
- ✨ Implemented broadcast system for role updates
- ✨ Added automatic role cleanup when players leave
- ✨ Improved client-server communication protocol
- 🐛 Fixed titles only visible to single player
- 🐛 Fixed new player roles not appearing for existing players

### Version 1.0.0
- 🎉 Initial release
- ✨ Basic title display system
- ✨ Color customization
- ✨ Role management

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**ItoRenz00**

- GitHub: [@ItoRenz00](https://github.com/ItoRenz)
- Roblox: [YourRobloxProfile](https://www.roblox.com/users/7976793837/profile)

## 🌟 Support

If you find this project helpful, please consider:
- ⭐ Starring the repository
- 🐛 Reporting bugs
- 💡 Suggesting new features
- 📢 Sharing with other developers

## 📞 Contact

For questions or support, please open an issue on GitHub.

---

Made with ❤️ for the Roblox Developer Community
