# Parameters (Curriculum Builder)

Use this file to define model + generation settings for two execution modes:

## A) Web (ChatGPT/Claude)
- You manually choose the model in the UI.
- Temperature / max tokens are controlled by the UI.
- Edits to this file do not auto-apply; treat this as the source of truth you copy from.

## B) API/Script (recommended for automation)
- Your run script reads the JSON below (or a separate params.json) and passes values to the API call.
- Edits here affect subsequent runs only if your script loads these values each time.

### Suggested JSON block (copy into your run script or a params.json if you prefer):

{
  "model": "gpt-5",
  "temperature": 0.3,
  "max_tokens": 1800
}

