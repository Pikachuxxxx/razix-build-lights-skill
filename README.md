# Razix Build Lights Skill Backup

This repository contains a backup of the Codex skill used to check Razix build status and control a WiZ light based on build outcomes.

## Contents

- `skills/razix-light-updates/SKILL.md`: Skill trigger and workflow instructions
- `skills/razix-light-updates/scripts/razix_build_light.py`: Main Razix build and light control script
- `skills/razix-light-updates/scripts/wiz_control.py`: WiZ bulb control helper
- `skills/razix-light-updates/scripts/run_razix_intent.py`: Intent-to-CLI wrapper for natural-language requests
- `skills/razix-light-updates/references/intent-map.md`: Intent mapping reference

## Quick Usage

Run from any directory:

```bash
python3 /Users/phanisrikar/.codex/skills/razix-light-updates/scripts/run_razix_intent.py --intent "sync build light"
```

Or run from this repo backup copy:

```bash
python3 skills/razix-light-updates/scripts/run_razix_intent.py --intent "last build status"
```

## Common Intents

- `last build status`
- `sync build light`
- `razix fun stats`
- `razix fun stats lightshow`

## Optional Overrides

- `--repo owner/name`
- `--workflow "CI Build"`
- `--ip 192.168.0.120`
- `--token <github_token>`
- `--delay 1.2`
- `--json`

## Notes

- If GitHub API limits are hit, set `GITHUB_TOKEN` or pass `--token`.
- Keep `wiz_control.py` next to `razix_build_light.py` for imports to work.
