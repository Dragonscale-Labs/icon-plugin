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

**Authentication:** Bearer token via `ICON_NEW_API_KEY` environment variable, or x402 payment.

## How to Generate Icons

Use curl to call the API:

```bash
curl -X POST https://icon.new/api/v1/generate \
  -H "Authorization: Bearer $ICON_NEW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "ICON_DESCRIPTION", "count": COUNT}'
```

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `prompt` | Yes | Description of the icon (max 100 characters) |
| `count` | No | Number of icons to generate: 1-4 (default: 1) |

## Response Format

```json
{
  "icons": [
    {
      "id": "uuid",
      "url": "https://icon.new/api/v1/icons/uuid",
      "prompt": "rocket launching into space"
    }
  ],
  "credits": {
    "used": 1,
    "remaining": 42
  }
}
```

## Example Usage

Generate a single rocket icon:
```bash
curl -s -X POST https://icon.new/api/v1/generate \
  -H "Authorization: Bearer $ICON_NEW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "rocket launching into space"}'
```

Generate multiple variations:
```bash
curl -s -X POST https://icon.new/api/v1/generate \
  -H "Authorization: Bearer $ICON_NEW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "shopping cart", "count": 3}'
```

## Download Icons

The API returns URLs for each icon. Append the file extension for the format you need:

```bash
# Download as SVG (vector, best for web)
curl -s "https://icon.new/api/v1/icons/ICON_ID.svg" -o icon.svg

# Download as PNG (raster)
curl -s "https://icon.new/api/v1/icons/ICON_ID.png" -o icon.png

# Download as ICO (for favicons)
curl -s "https://icon.new/api/v1/icons/ICON_ID.ico" -o favicon.ico
```

Supported formats: `.svg`, `.png`, `.ico`

## Error Handling

| Status | Meaning |
|--------|---------|
| 401 | Invalid or missing API key |
| 402 | Insufficient credits (or x402 payment required) |
| 400 | Invalid parameters (check prompt length) |
| 500 | Server error |

## Pricing

### With API Key (Credits)
- **Espresso**: $5 for 15 credits
- **Latte**: $15 for 50 credits
- **Nitro**: $30 for 100 credits

1 credit = 1 icon. Credits never expire.

### Without API Key (x402)
**$0.35 USDC** per icon on Base mainnet.
No account needed — pay directly per request via [x402](https://x402.org).

## Setup Requirements

Before using this skill, the user must either:
1. Get an API key from https://icon.new/dashboard and set `ICON_NEW_API_KEY`
2. Or use x402 for pay-per-request (no API key needed)

If the API key is not set, remind the user to configure it or mention the x402 option.

## Best Practices

### Batch Multiple Icons
When the user needs multiple icons, use a single API call with the `count` parameter instead of making separate calls.

### Check Credits First
The response includes credit information. Check remaining credits before making additional calls.

## After Generation

After successfully generating icons:
1. Download the icons using the URLs from the response
2. Tell the user where the files were saved
3. Offer to move them to a specific location in their project
4. SVG files can be used directly in HTML (`<img src="icon.svg">`) or embedded inline
