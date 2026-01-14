---
description: Generate an icon using the icon.new AI service
---

# Generate Icon

Generate an icon based on the user's description: "$ARGUMENTS"

## Instructions

1. First, check if the `ICON_NEW_API_KEY` environment variable is set by running:
   ```bash
   test -n "$ICON_NEW_API_KEY" && echo "API key is set" || echo "API key not set"
   ```

2. If not set, inform the user they need to:
   - Get an API key from https://icon.new/dashboard
   - Set it with: `export ICON_NEW_API_KEY="icon_your_api_key_here"`
   - Or use x402 for pay-per-request ($0.35 USDC per icon, no account needed)

3. If the API key is set, generate the icon(s). Use the `count` parameter if multiple icons are needed (max 4 per call):
   ```bash
   curl -s -X POST https://icon.new/api/v1/generate \
     -H "Authorization: Bearer $ICON_NEW_API_KEY" \
     -H "Content-Type: application/json" \
     -d '{"prompt": "USER_PROMPT_HERE", "count": 1}'
   ```

4. Parse the JSON response. Each icon has a `url` field with a direct download link:
   ```json
   {
     "icons": [{"id": "abc123", "url": "https://icon.new/api/v1/icons/abc123", "prompt": "..."}],
     "credits": {"used": 1, "remaining": 5}
   }
   ```

5. Download icons to the user's project. Use the file extension for the format needed:
   ```bash
   curl -s "https://icon.new/api/v1/icons/ICON_ID.svg" -o icon.svg
   curl -s "https://icon.new/api/v1/icons/ICON_ID.png" -o icon.png
   curl -s "https://icon.new/api/v1/icons/ICON_ID.ico" -o favicon.ico
   ```

6. Tell the user:
   - Which files were saved and where
   - Remaining credits

## Parameter Hints

If the user didn't specify, you can ask about:
- **Style**: outline (default), filled, flat, gradient, or isometric
- **Size**: 256, 512, or 1024 pixels
- **Count**: 1-4 icons to generate

## Example Prompts

- `/icon-new:icon rocket ship with confetti fuel`
- `/icon-new:icon shopping cart full of toys`
- `/icon-new:icon cute alien user avatar`
