# Worklog

Daily entries of real work — appended automatically by a scheduled job.

## 2026-09-15

- Portfolio overhaul: audited all 10 public repos — gitleaks over full history (no credentials, current or historical), personal names redacted from 4 files (history rewrite queued for 3 repos), missing build files + Gradle wrappers added to englishprogression, vocabquiz and dailyenglish, download steps, dependency links and troubleshooting sections added to every plugin README, the missing LICENSE added to this repo, and all social-preview images refreshed in a Notion-dark style.
- Added a screenshot gallery, pipeline-architecture diagram and copy-paste agent-install instructions to esl-automation-suite; cross-linked the four plugin READMEs and made every badge clickable.
- Merged hermes-skills into esl-automation-suite: video-review summaries now install with the suite (one command, 3 skills, 6 pipelines); hermes-skills archived as a pointer so old links keep working.
- Renamed the GitHub account to itsfedor and rebranded every repo, image and commit to Fedor Molodtsov: cross-links, GitHub Pages URLs, release links and git history all updated.

## 2026-08-29

- Finished the video pipeline end to end: Deepgram Nova-3 transcription with EN+RU detection verified live (raw-body upload workaround for the sandbox proxy), normalizer, transcript packer.
- Edited the 16-minute homework review recording: silence removed, bilingual captions added, 720p render with verified segment timing.
- Turned the same recording into a student-facing HTML homework summary (A2 student, Unit 3): 11 task sections, color-coded fixes, test-english practice tips, strengths box.
- Published the first skill repo on GitHub (itsfedor/hermes-skills): harness-agnostic SKILL.md, README, MIT license, social preview, 11 topics; added the repo to the GitHub profile featured projects.
- Installed video-use, the browser-use team's agent-native video editing toolkit (21.2k stars, MIT): uv sync plus 6 Python deps, registered as a Hermes skill so it auto-loads on any video edit request. Found transcription is hardcoded to ElevenLabs Scribe, so the pipeline needs an ElevenLabs key or an OpenAI whisper-1 fallback.
- SEO pass over all 8 public repos: rewrote descriptions to the 2026 top-repo pattern (what it is, who it is for, stack), expanded topics from 6-9 to 9-13 per repo, linked the demo-casino homepage to its live GitHub Pages. Verified by reading the state back via the API.

## 2026-08-27

- Built a clean-B1 teacher's guide from the TED-Ed Prohibition video (Rod Phillips): simpler vocabulary than the B1+ version (ban, smuggling, corruption), stronger everyday phrases (make off with, stock up, meet the demand), comprehension by timestamps, differentiation for weak and strong students.
- Drafted homework for the clothes-quality video pair: a Past Simple vs Present Perfect block staged as Test-Teach-Test, true/false statements with video evidence, second video cut at 12:25 with the rest saved as the next lesson opener.

## 2026-08-26

- Built a B1+ teacher's guide from "What AI Does to the Minds of Novice Coders" (JetBrains Academy, 7:29) for the same developer student: psychology-heavy vocabulary, comprehension in timestamped sections, verb-pattern grammar block taken from the script.
- All quoted lines in the guide verified programmatically against the fetched transcript; AI-ism scan clean.

## 2026-08-25

- Built a full B1+ lesson around "Therapy for the Vibe-Coded Brain" (Clara / JetBrains Academy, 10 min video) for a student who codes at a Russian FinTech, pitched on metacognition for developers.
- Lesson shipped as an HTML teacher's guide with answer keys; all 25 quoted transcript lines verified verbatim against the source.
- Drew a B2 IELTS-style line graph for the second student using an imaginary country (Velmora): matplotlib render from verified data, yearly shares sum to 100, exact labels, delivered as PNG.
- Finished the HDR video color fix: final 202 MB corrected mp4 encoded (work started Aug 24, render completed today).

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
- Removed presentation, presentation-video, and a personal student-materials repo from GitHub. The C1 exercise pipeline is now the c1-visual-data-writing skill (cheat sheet, 3 chart tasks, image generation prompts, HTML template)
- Banner images added to all 4 plugin repos; C1 exercise + chart samples moved into esl-automation-suite examples
- Skill reworked: c1-visual-data-writing absorbed into test-english-adapt (any test-english.com exercise personalized for a student, with research on site formats and chart image generation)
