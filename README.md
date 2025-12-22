# Game Server Templates

Community-maintained collection of game server templates for the [Game Server Dashboard](https://github.com/natcoso9955/game-server-dashboard).

## 🎮 About

This repository contains pre-configured templates for popular game servers, making it easy to add new servers to your dashboard with proper settings, Steam query configurations, and background images.

## 📋 Available Templates

Browse the `templates/` directory to see all available game server templates:

- **Counter-Strike 2** - Competitive FPS
- **Valheim** - Viking survival adventure
- **ARK: Survival Evolved** - Dinosaur survival game
- **Rust** - Multiplayer survival game
- **7 Days to Die** - Zombie survival crafting
- **Sons of the Forest** - Survival horror
- **Palworld** - Creature-collecting survival

*...and more! See [templates/index.json](templates/index.json) for the complete list.*

## 🚀 Usage

### Automatic Sync
Templates are automatically synced when your dashboard container starts up. The sync process fetches the latest templates from this repository and populates your database.

### Manual Sync
You can also manually sync templates from the Admin Panel:
1. Log in to your dashboard
2. Go to Admin Panel
3. Click "Sync Templates"
4. Templates will be downloaded and updated

### Creating a Server from Template
1. In Admin Panel, click "+ Add Server"
2. Browse the template gallery
3. Click on a template to load its settings
4. Fill in your server's IP:Port
5. Customize as needed
6. Save!

## 🛠️ Template Structure

Each template consists of two files:

### 1. Template JSON (`templates/<game-id>.json`)
```json
{
  "template_id": "counter-strike-2",
  "name": "Counter-Strike 2",
  "game_id": "730",
  "default_port": 27015,
  "steam_query_port": 27015,
  "steam_launch_url": "steam://connect/<IP>:<PORT>",
  "recommended_fields": [
    "server_name",
    "map",
    "players",
    "vac_enabled"
  ],
  "description": "Tactical 5v5 competitive FPS"
}
```

### 2. Background Image (`templates/images/<game-id>.jpg`)
- **Format**: JPG or PNG
- **Recommended size**: 1920x1080 or 1280x720
- **Aspect ratio**: 16:9 preferred
- **File size**: Under 500KB recommended

## 📝 Template Fields Reference

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `template_id` | string | ✅ | Unique identifier (lowercase, hyphenated) |
| `name` | string | ✅ | Display name of the game |
| `game_id` | string | ✅ | Steam App ID ([find on SteamDB](https://steamdb.info/)) |
| `default_port` | number | ❌ | Default game server port |
| `steam_query_port` | number | ❌ | Port for A2S queries (usually same as default_port) |
| `steam_launch_url` | string | ❌ | Steam protocol URL template |
| `background_image_url` | string | ❌ | Full URL to background image |
| `recommended_fields` | array | ❌ | Suggested Steam query fields to display |
| `description` | string | ❌ | Brief game description |

### Available Steam Query Fields

Test what fields your server supports using the Steam Query test below.

Common fields:
- `server_name` - Server hostname
- `map` - Current map name
- `game` - Game type/mode
- `players` - Player count formatted as "X/Y"
- `player_count` - Current number of players
- `max_players` - Maximum player capacity
- `password_protected` - Whether server requires password
- `vac_enabled` - VAC anti-cheat status
- `version` - Game/server version
- `server_type` - Dedicated/Listen/HLTV
- `platform` - Operating system (Linux/Windows)

## 🧪 Testing Your Template

### Find Steam App ID
1. Visit [SteamDB](https://steamdb.info/)
2. Search for your game
3. Copy the App ID from the URL or page

### Test Steam Query
Use `a2s` Python library to test what information your server exposes:

```python
import a2s

# Replace with your server IP and query port
address = ('your.server.ip', 27015)

# Get server info
info = a2s.info(address)
print(f"Server Name: {info.server_name}")
print(f"Map: {info.map_name}")
print(f"Game: {info.game}")
print(f"Players: {info.player_count}/{info.max_players}")
print(f"Server Type: {info.server_type}")
print(f"Platform: {info.platform}")
print(f"Password Protected: {info.password_protected}")
print(f"VAC Enabled: {info.vac_enabled}")
print(f"Version: {info.version}")
```

Or use our dashboard's built-in query test (coming soon).

## 🤝 Contributing

**We welcome and encourage Pull Requests!** 🎉

### Adding a New Game Template

1. **Fork this repository**
2. **Find the Steam App ID** on [SteamDB](https://steamdb.info/)
3. **Test Steam Query** on a live server to see what fields are available
4. **Create template JSON** in `templates/<game-id>.json`
5. **Add background image** to `templates/images/<game-id>.jpg`
6. **Update index** - Add your template to `templates/index.json`
7. **Submit Pull Request** with:
   - Template JSON file
   - Background image
   - Updated index.json
   - Brief description in PR

### Quality Guidelines

✅ **DO:**
- Use high-quality background images (official artwork preferred)
- Test template on a live server before submitting
- Include accurate Steam App IDs
- Use descriptive, concise template names
- Keep image file sizes reasonable (<500KB)
- Follow existing naming conventions

❌ **DON'T:**
- Use copyrighted images without permission
- Include server passwords or private information
- Submit untested templates
- Use offensive or inappropriate content

### Example PR Description
```markdown
## New Template: Project Zomboid

- **Game**: Project Zomboid
- **Steam App ID**: 108600
- **SteamDB**: https://steamdb.info/app/108600/
- **Tested on**: Live server at example.com:16261
- **Available fields**: server_name, map, players, password_protected, version
- **Image source**: Official Steam artwork
```

## 📁 Repository Structure

```
game-server-templates/
├── templates/
│   ├── index.json              # Master list of all templates
│   ├── counter-strike-2.json   # Individual template files
│   ├── valheim.json
│   ├── rust.json
│   └── images/
│       ├── counter-strike-2.jpg
│       ├── valheim.jpg
│       └── rust.jpg
└── README.md                   # This file
```

## 🔗 Resources

- **SteamDB**: https://steamdb.info/ - Find Steam App IDs
- **A2S Protocol**: https://developer.valvesoftware.com/wiki/Server_queries - Technical documentation
- **Dashboard Repo**: https://github.com/yourusername/game-server-dashboard

## 📄 License

Templates are provided as-is for community use. Background images remain property of their respective copyright holders and are used for identification purposes only.

## 💬 Support

- **Issues**: Report problems or request new templates via [GitHub Issues](https://github.com/natcoso9955/game-server-templates/issues)
- **Discussions**: Share ideas in [GitHub Discussions](https://github.com/natcoso9955/game-server-templates/discussions)

---

**Made with ❤️ by the community, for the community**
