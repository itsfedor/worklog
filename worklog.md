# Worklog

Daily entries of real work — appended automatically by a scheduled job.

## 2026-08-21

- Pushed the casino polish to itsfedor/demo-casino: Aviator-style Crash rebuild, Stake-style Dice controls, casino-standard audio and pacing for Plinko and Slots, sound ordering fix.
- Pushed a docs follow-up: dropped 2 em-dashes from the demo-casino README. Verified local HEAD matches remote main, Pages redeployed.
- Read all 31 Edvibe FAQ articles on exercise creation and built the edvibe-exercise-format skill: syntax cheat sheet plus rules for 26 exercise templates.
- Generated 3 Edvibe exercises (vocab matching, mixed conditionals) from an Engoo article on the Meta trial.
- Rewired the daily GitHub worklog cron into a two-phase approval flow: drafts go to the Telegram bot, nothing is pushed until approved.
- Fired a test run of the approval flow end to end.

## 2026-08-20

- GitHub portfolio overhaul: profile README with banner and featured projects
- New public repos: **ink-dictation** (macOS AI dictation app), **esl-automation-suite** (teaching pipelines), **worklog** (this log)
- READMEs and social previews added to all project repos
- Secret scan (gitleaks) across all public repos — clean; embedded API keys removed from Ink before publishing
- Built the Minecraft English Server repo (overview page + docs), later removed from GitHub: the 4 custom plugins now live in separate public repos (chat2earn, englishprogression, vocabquiz, dailyenglish)
- Removed **ink-dictation** from GitHub (app not ready for public release; keys stay local)
- Full secret audit of all repos: clean. Push protection blocked a Groq key before it left the machine; gitleaks CI added to content repos
- Removed presentation, presentation-video, and student-materials from GitHub. The C1 exercise pipeline is now the c1-visual-data-writing skill (cheat sheet, 3 chart tasks, image generation prompts, HTML template)
- Banner images added to all 4 plugin repos; C1 exercise + chart samples moved into esl-automation-suite examples
- Skill reworked: c1-visual-data-writing absorbed into test-english-adapt (any test-english.com exercise personalized for a student, with research on site formats and chart image generation)
