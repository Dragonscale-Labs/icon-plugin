# icon.new Plugin for Claude Code

Generate AI icons using the [icon.new](https://icon.new) service directly from Claude Code.

## Setup

### 1. Get an API Key

1. Go to [icon.new/dashboard](https://icon.new/dashboard)
2. Create an account and get your API key

### 2. Set Environment Variable

Add to your shell profile (`.bashrc`, `.zshrc`, etc.):

```bash
export ICON_NEW_API_KEY="icon_your_api_key_here"
```

### 3. Install the Plugin

**Option A: Test locally during development**
```bash
claude --plugin-dir /path/to/icon-new-plugin
```

**Option B: Install from a marketplace**
```
/plugin install <marketplace-url>
```

## Usage

### Slash Command

Use the `/icon:new` command followed by your icon description:

```
/icon:new rocket launching into space
/icon:new shopping cart
/icon:new user profile avatar
```

### Natural Language

Claude will automatically use the icon generator skill when you ask to create icons:

- "Generate an icon of a rocket ship"
- "Create a gradient-style shopping cart icon"
- "I need an isometric database icon for my project"

## Plugin Structure

```
icon-new-plugin/
├── .claude-plugin/
│   └── plugin.json      # Plugin manifest
├── commands/
│   └── icon.md          # /icon slash command
├── skills/
│   └── icon-generator/
│       └── SKILL.md     # Icon generation skill
└── README.md
```
