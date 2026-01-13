---
name: icon-generator
description: Generate AI icons using icon.new. Use when the user wants to create icons, generate icon assets, or needs visual icons for their project.
---

# Icon Generator Skill

Generate icons using the icon.new API service.

## When to Use This Skill

Use this skill when the user:
- Asks to generate or create an icon
- Needs icon assets for their project
- Wants AI-generated icons with specific styles

## API Details

**Endpoint:** `POST https://icon.new/api/v1/generate`

**Authentication:** Bearer token required. The API key should be stored in the environment variable `ICON_NEW_API_KEY`.

## How to Generate Icons

Use the Bash tool to call the API with curl:

```bash
curl -X POST https://icon.new/api/v1/generate \
  -H "Authorization: Bearer $ICON_NEW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "ICON_DESCRIPTION", "size": SIZE, "style": "STYLE", "count": COUNT}'
```

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `prompt` | Yes | Description of the icon (max 100 characters) |
| `size` | No | Icon size in pixels: 256, 512, or 1024 (default: 1024) |
| `style` | No | Icon style: outline, filled, flat, gradient, or isometric (default: outline) |
| `count` | No | Number of icons to generate: 1-4 (default: 1) |

## Available Styles

- **outline**: Simple line-based icons
- **filled**: Solid filled icons
- **flat**: Flat design icons
- **gradient**: Icons with gradient fills
- **isometric**: 3D isometric style icons

## Response Format

The API returns JSON with:
- `icons`: Array of generated icons with `id`, `url`, and `prompt`
- `credits`: Current credit usage statistics

## Example Usage

Generate a single rocket icon:
```bash
curl -X POST https://icon.new/api/v1/generate \
  -H "Authorization: Bearer $ICON_NEW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "rocket launching into space"}'
```

Generate multiple gradient-style icons:
```bash
curl -X POST https://icon.new/api/v1/generate \
  -H "Authorization: Bearer $ICON_NEW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "shopping cart", "style": "gradient", "count": 3, "size": 512}'
```

## Error Handling

| Status | Meaning |
|--------|---------|
| 401 | Invalid or missing API key |
| 402 | Insufficient credits |
| 400 | Invalid parameters (check prompt length, size, style values) |
| 500 | Server error |

## Setup Requirements

Before using this skill, the user must:
1. Get an API key from https://icon.new/dashboard
2. Set the environment variable: `export ICON_NEW_API_KEY="icon_your_api_key_here"`

If the API key is not set, remind the user to configure it.

## Best Practices

### Batch Multiple Icons
When the user needs multiple icons, use a single API call with the `count` parameter instead of making separate calls.

```bash
curl -s -X POST https://icon.new/api/v1/generate \
  -H "Authorization: Bearer $ICON_NEW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "funny cat", "count": 3}'
```

### Download Icons
The API returns direct URLs for each icon. Download them with curl:

```bash
# Download a single icon
curl -s "https://icon.new/api/v1/icons/ICON_ID" -o icon.svg

# Download multiple icons from a response
curl -s -X POST https://icon.new/api/v1/generate \
  -H "Authorization: Bearer $ICON_NEW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "icon description", "count": 3}' \
  | jq -r '.icons[].url' | while read -r url; do \
    id=$(basename "$url"); \
    curl -s "$url" -o "$id.svg"; \
  done
```

### Check Credits First
The response includes credit information. If you need to generate many icons across multiple calls, check the credits in the first response before making additional calls.

## After Generation

After successfully generating icons:
1. The icons are already saved as SVG files in the current directory
2. Tell the user where the files were saved
3. Offer to move them to a specific location in their project
4. The SVG files can be used directly in HTML (`<img src="icon.svg">`) or embedded inline
