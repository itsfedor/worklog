# 📓 Worklog

A daily, machine-readable log of public work — appended automatically every
evening by a scheduled Hermes agent job.

The log keeps the profile honest and alive: what was actually built, fixed,
or shipped each day, in the owner's own words. No filler — real entries only.

## Format

`worklog.md` — one `## YYYY-MM-DD` entry per day, newest first.

## Automation

- **Schedule:** daily
- **Source:** real session activity (session search over the agent's work)
- **Output:** append entry → commit → push
- **Also updates:** the "Recent activity" section of the
  [profile README](https://github.com/itsfedor/itsfedor)

## License

[MIT](LICENSE)
