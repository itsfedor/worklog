# 📓 Worklog

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A daily, machine-readable log of public work. The log keeps the profile honest
and alive: what was actually built, fixed, or shipped each day, in the owner's
own words. No filler, real entries only.

## How to read it

- `worklog.md` — one `## YYYY-MM-DD` entry per day, **newest first**.
- **Nothing to install.** This is a data repo: open [worklog.md](worklog.md) and read it.
- The same entries feed the "Recent activity" section of the [profile README](https://github.com/itsfedor/itsfedor).

## Format

```markdown
## 2026-08-29

- What was built or shipped, one bullet per item. Real work only —
  empty days produce no entry, nothing is fabricated.
```

## Automation

- **Producer:** a scheduled Hermes agent job that summarizes real session activity.
- **Approval:** drafts are sent to the owner for approval; nothing is pushed until approved.
- **Output:** append entry → commit → push (skipped entirely on empty days).

## License

[MIT](LICENSE)
