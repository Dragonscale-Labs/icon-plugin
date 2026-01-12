# icon-new Plugin for Claude Code

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
claude --plugin-dir /path/to/icon-new-tool
```

**Option B: Install from a marketplace**
```
/plugin install <marketplace-url>
```

## Usage

### Slash Command

Use the `/icon-new:icon` command followed by your icon description:

```
/icon-new:icon rocket launching into space
/icon-new:icon shopping cart
/icon-new:icon user profile avatar
```

### Natural Language

Claude will automatically use the icon generator skill when you ask to create icons:

- "Generate an icon of a rocket ship"
- "Create a gradient-style shopping cart icon"
- "I need an isometric database icon for my project"

## Options

| Option | Values | Default |
|--------|--------|---------|
| Style | outline, filled, flat, gradient, isometric | outline |
| Size | 256, 512, 1024 | 1024 |
| Count | 1-4 | 1 |

## Credits

- 1 credit = 1 icon
- Check your balance at [icon.new/dashboard](https://icon.new/dashboard)

## Plugin Structure

```
icon-new-tool/
├── .claude-plugin/
│   └── plugin.json      # Plugin manifest
├── commands/
│   └── icon.md          # /icon-new:icon slash command
├── skills/
│   └── icon-generator/
│       └── SKILL.md     # Icon generation skill
└── README.md
```
