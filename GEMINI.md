# Gemini Instructions: Razix Build Lights

Use this repository to check Razix build status and control WiZ lights.

## Primary Scripts

- `skills/razix-light-updates/scripts/run_razix_intent.py`
- `skills/razix-light-updates/scripts/razix_build_light.py`
- `skills/razix-light-updates/scripts/wiz_control.py`

Run commands from the repository root unless absolute paths are used.

## Preferred Execution Path

Prefer the intent wrapper for user-facing requests:

```bash
python3 skills/razix-light-updates/scripts/run_razix_intent.py --intent "<user request>"
```

Use `--dry-run` first when validating command mapping.

## Intent Mapping Rules

Map user requests to deterministic flags when possible:

- `sync build light` -> `--status --set-light`
- `last build status` / `build status` / `status` -> `--status`
- `fun stats` -> `--status --fun-stats`
- `fun stats lightshow` -> `--status --fun-stats --fun-lightshow`
- `lightshow` / `aura` / `party` -> `--fun-lightshow`

If request does not fit known patterns, pass through as NLP command:

```bash
python3 skills/razix-light-updates/scripts/razix_build_light.py --command "<user request>"
```

## Common Overrides

Append these when provided by user or needed:

- `--repo owner/name`
- `--workflow "CI Build"`
- `--ip 192.168.0.120`
- `--token <github_token>`
- `--delay 1.2`
- `--json`

## Operational Behavior

1. For status requests, execute and return key fields: workflow, run id, run number, branch, commit, status, conclusion, updated time, actions URL.
2. For sync requests, execute status + light update and report bulb response.
3. If GitHub API calls fail due to limits/auth, retry with `--token` or `GITHUB_TOKEN`.
4. Keep `wiz_control.py` colocated with `razix_build_light.py`.
