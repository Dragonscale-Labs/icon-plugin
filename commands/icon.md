---
description: Generate an icon using the icon.new AI service
---

# Generate Icon

Generate an icon based on the user's description: "$ARGUMENTS"

## Instructions

1. First, check if the `ICON_NEW_API_KEY` environment variable is set by running:
   ```bash
   echo ${ICON_NEW_API_KEY:+API key is set}
   ```

2. If not set, inform the user they need to:
   - Get an API key from https://icon.new/dashboard
   - Set it with: `export ICON_NEW_API_KEY="icon_your_api_key_here"`

3. If the API key is set, generate the icon by calling the API:
   ```bash
   curl -s -X POST https://icon.new/api/v1/generate \
     -H "Authorization: Bearer $ICON_NEW_API_KEY" \
     -H "Content-Type: application/json" \
     -d '{"prompt": "USER_PROMPT_HERE"}'
   ```

4. Parse the JSON response and present:
   - The icon download URL(s)
   - Remaining credits

5. Ask if the user wants to download the icon to a specific location in their project.

## Parameter Hints

If the user didn't specify, you can ask about:
- **Style**: outline (default), filled, flat, gradient, or isometric
- **Size**: 256, 512, or 1024 pixels
- **Count**: 1-4 icons to generate

## Example Prompts

- `/icon-new:icon rocket ship`
- `/icon-new:icon shopping cart --style gradient --size 512`
- `/icon-new:icon user profile avatar`
