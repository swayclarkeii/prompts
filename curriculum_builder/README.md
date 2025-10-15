# Curriculum_Builder

**Purpose:** Generate a clear, step-by-step curriculum with daily tasks, time boxes, guardrails, and acceptance checks.

## Folder Structure
- `curriculum_builder_v1.md` — the prompt template (Markdown).
- `parameters.md` — human-readable guidance for model/temperature and usage notes.
- `params.json` — machine-readable config for API/scripts (`model`, `temperature`, `max_tokens`).
- `tests/input/` — source inputs for runs (e.g., `day2_source.md`).
- `tests/expected/` — expected or approved outputs (golden files for regression).

## File Roles
- **parameters.md:** documentation; copy values manually for ChatGPT web.
- **params.json:** used by scripts/automations; update to change future runs.
- **\*_v1.md / \*_v2.md:** versioned prompts; update when behavior changes.
- **tests/input:** paste raw notes/bullets to feed into the prompt.
- **tests/expected:** store best/approved outputs to compare against.

## Usage (ChatGPT Web)
1. Open `curriculum_builder_v1.md` and copy the whole prompt.
2. Paste into ChatGPT, then paste the content of `tests/input/day2_source.md` into the **Input** section.
3. Manually set model/temperature using `parameters.md` (or mirror `params.json`).
4. Run. Copy the model’s output and save it to `tests/expected/day2_expected.md`.
5. Iterate: adjust the prompt, re-run, and commit with a versioned message.

## Usage (API/Script)
- Load `curriculum_builder_v1.md` as a string.
- Load settings from `params.json`.
- Inject variables/inputs from `tests/input/`.
- Save outputs alongside `tests/expected/` for comparison.
