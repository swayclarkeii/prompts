# Parameters (Curriculum_Builder)

Use this file to define model + generation settings for two execution modes.

## A) Web (ChatGPT/Claude)
- Choose model/temperature in the UI.
- This file is the human-readable source of truth you copy from.

## B) API/Script
- A run script should load `params.json` and pass values to the API call.
- Edits to `params.json` affect subsequent runs if your script re-reads it each time.

## Recommended Defaults
- Model: gpt-5
- Temperature: 0.30 (deterministic, better for curricula)
- Max tokens: 1800
