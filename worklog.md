# Worklog

Daily entries of real work — appended automatically by a scheduled job.

## 2026-10-08

- Moved the teacher dashboard's own refresh to a weekday cadence: the scan now runs Monday–Friday at noon (it was Mon/Wed/Fri), and the dashboard footnote was updated to match.
- Refreshed the live dashboard by hand after the switch: a fresh platform scan found real changes — one card rebuilt with new homework numbers and the online line refreshed for 5 of 18 students — and the updated build went live. Verified: both edge nodes serve /dashboard/ and /progress/ byte-identical to the local build (md5 match on both), and the live stamp reads 08.10, 14:07.
- Built review read-receipts for the dashboard: when a student opens a review in their own cabinet, a best-effort server-side marker records first / last / count in a Cloudflare KV namespace, and cards with reviews show a «Разборы в кабинете» block — «открыт сегодня / вчера / dd.mm» or a blue «не открыт» pill — plus a new «Не открыли» filter. A teacher's view-as fetch deliberately does not count, and receipts only ever hold timestamps.
- Extended the dashboard QA suite to cover the feature — 46 checks: every rendered row cross-checked against the API state, teacher view-as writes nothing, the owner's own fetch increments the count by exactly one, .html redirects don't double-count, and students get 403 from the dashboard API — plus a dormant mode (38 checks) for production before the KV binding exists. All suites green locally (46 + 60 + 42 + 34), and the post-deploy live checks passed — both edges byte-identical, dormant API behaving as designed.
- Shipped the feature in dormant form after a branch-preview dry run: the code and UI are live on production, with the receipt blocks staying hidden until the KV binding is attached (needs one more scope on the Cloudflare token); the exact activation steps are written down so nothing has to be rediscovered.
- Hygiene: kept a pre-change backup of the dashboard page, added the cabinet/dashboard playbook to the site README (local stand flags, QA modes, receipts architecture), and wrote the receipts notes into the project skill.

## 2026-10-07

- Untangled the platform's book organization: the "many copies" turned out to be three intentional sets of five — masters, working copies, preview books — but the copies and previews had silently fallen out of their folders. Isolated the cause with a controlled experiment on a scratch book: saving a book by script without carrying its folder id detaches it from the folder, with no notice. Restored the two displaced sets (5 + 5) with read-back verification — each folder holds exactly its five again and only the masters stay top-level — and wrote the rule into the tooling skills: always pass the folder id, and re-verify folder membership after every scripted wave.
- Built the next B2 lesson in the spoken-lessons series — the BBC's "Change Your Mind, Change Your Life" episode on work anxiety: 36 exercises across the six-stage flipped format — a pre-watching prep page, warm-up, vocabulary (a fresh ten-item lexis set), watching (gist questions, the video, an 8-question auto-checked test, seven timestamped segments with hidden answer keys, and a 16-sentence / 20-gap exact-listening block whose gaps were gate-checked chunk-wise against two independent caption corpora), speaking and an extra stage. Verified live: clean API read-back and a full DOM sweep — embed and cover mounting, 20/20 typed gaps, working dropdowns. Appended to the B2 course — the nineteenth verified build, the sixth flipped wave.
- Reworked the teacher dashboard, now live at itsfedor.cc/dashboard: English-first card titles with an online-status line, compact status chips (waiting / checked / not submitted), real platform avatars, and a self-contained refresh — one read-only platform scan with change detection, so only cards with real homework changes rebuild. Hardened and tidied: avatars sit behind the teacher gate (anonymous and student access return 404; the old public path serves a blank placeholder after an edge-cache quirk), the dead-end "cabinet" button gave way to a smart back that returns to the same cabinet, and the scan schedule moved to Mon / Wed / Fri at 12:00. Verified: local and live suites green — 33/33 + 60/60 + 42/42 — and the dashboard page file byte-identical across both edge nodes.
- Built the C1 edition of WSJ's "How Ben & Jerry's Activism Helps Scoop Up Customers" — the same-video companion to its B2 build: the six-stage skeleton re-authored around a distinct "price of principles" angle with a completely fresh C1 lexis set (zero overlap with the B2 one), a 15-sentence exact-listening block whose every gap passed the dual-caption gate, and a coral C1 tile on the book page. Verified end-to-end: server read-back clean (section order, counts, 8/8 test ticks, hidden notes, gap counts), the tile md5-matches its CDN copy, and a live DOM sweep came back green — the twentieth verified build of the series.
- Trimmed the ESL Automation Suite README: the redundant static preview above the live pipeline-demo GIF is gone.
- Published two new public repos: [notion-charts](https://github.com/itsfedor/notion-charts) — a JSON spec → Notion-style chart/table PNG generator (transparent canvas, Inter, 2× output, a QA mode that catches overflow, OCR/colour-map tooling to decode source charts, and three calibration examples; the same pipeline behind the course's 600+ chart images) — and [esl-feedback-design-system](https://github.com/itsfedor/esl-feedback-design-system) — the feedback design system: one five-role palette, slot-marked templates (homework + IELTS band card), a conformance linter and a Playwright render-QA runner, shipping synthetic demo docs (linter 9/9, QA green on desktop + mobile). Both public, MIT, with descriptions, topics and transparent light/dark banners.
- Evening README pass across the account: retired the old opaque preview cards from six repos' READMEs (the transparent banner carries the identity now), gave the profile a theme-adaptive banner (light/dark) with a fresh social-preview card, and removed a leftover duplicate preview in prism-landing; closed with a 12-repo scan — no duplicate or broken asset references left in any README.

## 2026-10-06

- Built the next B2 lesson in the spoken-lessons series — WSJ's "Repo: How Roughly $1 Trillion Moves Overnight": 34 exercises across the six-stage flipped format — a pre-watching prep page, warm-up, vocabulary, watching and questions (gist, an 8-question auto-checked test, six timestamped watching segments with hidden answer keys, and a 15-sentence / 16-gap exact-listening block whose every gap was cross-checked chunk-wise against two independent caption tracks), speaking and an extra stage. Verified live: clean API read-back and a full DOM sweep — cover, video embed, 16/16 gap boxes, working dropdowns and the book tile at 256px; the eighteenth verified build and the fifth flipped wave.
- Extended the student area to every student with existing analyses: new per-student accounts with credentials kept 1:1 with the platform's own student cards, and seven legacy reviews rebuilt to the current design canon (v1.4) with reproducible per-document builders — originals kept intact. Verified on production: API 60/60, UI 41/41 and a new 34-check per-student E2E, plus md5 parity between both edge nodes.
- Cleared the platform's homework queue end to end: surveyed every active student and closed all 29 waiting sheets — the exercise-only sheets checked against their answer keys through a new exercise-level error digest (ten exercise types, cross-checked against the platform's own autocorrect flags), and the writing / recording sheets reviewed and closed. Three fresh reviews went live in the student area — an essay review, a writing + audio review with the recording embedded, and a research-task review — each lint-clean (9/9) and QA'd with zero errors or overflow.
- Applied the new feedback canon across the published archive: every review now carries at most two actionable tips, the most evidenced for that document. Caught and fixed a builder bug mid-wave, re-linted, and re-verified all eleven published reviews live.
- Launched the teacher dashboard at itsfedor.cc/progress/dashboard — per-student homework status (waiting check / checked of total / not submitted), hand-kept focus zones and next-step notes across 18 active students, on a teacher login that can open any student's file while student isolation stays intact (cross-access 404s re-verified). Its data rebuilds from a live platform scan three times a week.
- Wrote the day's rules back into the tooling skills: the cabinet's multi-student account playbook and QA suites, the legacy-review adaptation builders, the dual-caption-corpus pitfall for lesson waves, and the feedback canon's two-tips limit.

## 2026-10-05

- Re-audited the whole account (15 repos): a secret scan over full history, a PII sweep across working trees, commit graphs, 74 images and sampled video frames. Scrubbed a client reference and student names that had leaked into an example teacher-kit and the landing demo, rewrote history on three repos (filter-repo + force-push) and verified every fix on a fresh clone; the affected example screenshot was re-rendered and OCR-checked.
- Published [prism-landing](https://itsfedor.github.io/prism-landing/) — the ESL Automation Suite now has a live landing page (repo public, Pages on, description and topics set).
- Gave the repos a matching visual identity: transparent theme-adaptive banners (light/dark) with the Fedor Molodtsov byline and SEO alt text across nine repos, an animated gameplay GIF for ChainLuck, and a pipx one-liner install for the Edvibe CLI.
- Backfilled the worklog queue (16 unposted days) and refreshed the profile's Recent activity.
- Built the next B2 lesson in the spoken-lessons series — WSJ's "How Ben & Jerry's Activism Helps Scoop Up Customers": 34 exercises across the six-stage flipped format — a pre-watching prep page, warm-up, vocabulary, watching and questions (a 13-sentence / 14-gap exact-listening block; all 14 gaps passed chunk-wise against both caption corpora on the first run), speaking and an extra stage. Verified live: API read-back clean and a DOM sweep green — cover, YouTube embed, 24 test radios, 14 gaps, 8 dropdowns and the tile on the B2 gradient; the seventeenth verified build and the fourth flipped wave.
- Ran the homework-review pipeline on the day's IELTS batch into a full review (listening / reading / writing) and published it to the student area — the new report tops the cabinet with the "new" badge, and the earlier diagnostic was re-issued in the updated design. Live checks green: API 34/34, UI 30/30, three report cards end-to-end.
- Reworked the student area through a full owner-review cycle: the cabinet went RU-only (top-bar and language switcher dropped), report cards moved to a mobile-first layout, "Log out" became a plain footer link, and the file-delivery gate gained path validation, robots / noindex rules and a rotated session secret. Every release was verified on the live domain — API 44/44, UI up to 38/38.
- Launched the legal pages on itsfedor.cc — a combined public offer (lessons + materials) and a data-processing policy, rebuilt from the old Google Docs to the current rules, including a 12-month validity term for lesson packs (materials stay perpetual), with full contact details and cross-links. Both footers were rewired: the sales landing dropped its Telegram link and now points the offer at the site page, and the cabinet footer keeps only the legal links. Shipped with a new 45-check legal QA — byte-exact on both edge nodes.
- Tuned the account's own automation: the worklog pipeline now posts daily entries automatically once the content policy passes (new repos and profile changes still need an explicit OK), and the weekly portfolio watchdog went self-contained — no host script — its first run green.

## 2026-10-04

- Merged the opening tense modules of the whole grammar series into one large first module — "Module 1 · Tenses": the A1 copy now opens with 10 lessons (present, past and future together, 1.1–1.10), A2 with 9, B1 with 6, B1+ with 4 and B2 with 4, and the five preview books were merged to match (8/6/4/2/4) — so the series opens on one solid, substantial block instead of fragmented mini-modules. Every following module was renumbered without gaps (Module 5 → Module 2 and so on), and the A1 lessons were renamed under the new numbering — 29 renames in the copy plus 3 in its preview (now 1.1–1.10, then 2.1–10.2).
- Rebuilt every description that referenced the old module structure: all 10 books got a combined "Module 1 · Tenses" blurb with renumbered module headings, and each copy's description is byte-identical to its preview's. The lesson content itself was left untouched — 195 lessons (185 grammar + 10 tests) unchanged in place.
- Engineered the move so nothing could be lost: a pilot proved content survives a move + rename (content preserved, description intact); the move call deliberately carries the lesson description (a bare move silently wipes it); ordering went through a full ordered-list save; emptied modules were deleted only after their lessons were read back in place. Every step ran with backups and read-back verification.
- Closed with an end-to-end audit across all 10 books — structure, names, ordering, module counts and byte-for-byte descriptions, plus all 31 moved lessons checked for non-empty descriptions: ALL CHECKS PASS.
- Re-synced every publishing surface: the sales landing now shows 10/13/12/13/13 modules (61 total); the ad creatives were updated (the pack ad to "61 modules" and the A1 ad to "10 modules · 34 lessons" with the new lesson-number map, 1.1 → 10.2); and the reply draft for the platform review gained the merge note plus the renumbered lesson reference.
- Site QA ran green (copy-conformance 68/68 and both page suites), the site was redeployed and checked live — the pages serve the new counts.
- Wrote the mechanics back into the publishing toolkit: the platform's move / reorder / module-delete / rename RPC set, including the description-preservation quirk and the in-place edit-wave procedure.

## 2026-10-03

- Finished the grammar series' speaking-set rework: 32 sections across the five levels (A1 6, A2 6, B1 9, B1+ 3, B2 8) rewritten or extended to the approved format — lead-in → pattern → bolded target-form questions with a hidden teacher note (level / use / what to watch for). Each batch ran with a preflight check, per-lesson backups and read-back; the independent verifier closed at 32/32 (new content present, old gone, notes updated).
- Completed the explanation-condense wave: every rule text in all five books brought inside the platform's recommended lengths (50–100 words at A1–A2, 150–200 at B1–B2) — 177 lessons authored in level batches (35/41/37/33/31) and applied with backup → write → read-back; the end-to-end cross-check finished 177/177 with zero violations, and the over-short rules were expanded and the ten polished lessons re-applied.
- Ran a fresh typo sweep over all 187 lesson copies: 161 raw hits across 55 lessons filtered down to 22 lessons / 52 real fixes (double words, broken spellings) applied with preflight + backups + read-back at 100%; the final scan shows only intentional patterns left.
- Closed the chart-part wave flagged here yesterday: every chart in the series is now a set of standalone, phone-readable part images — 263 chart specs → 664 parts rendered and uploaded (664/664, zero failures), swapped into all 187 lesson copies with 0 problems, and independently re-verified 187/187 (parts, order, captions, numbering, old URLs all clean); special grids rebuilt (irregular-verb tables + 7 narrow grids) and the scratch test book removed.
- A1 cleanup + published-number re-sync: two lessons removed from the A1 copy (at the module tail, so numbering doesn't shift) and one lesson re-leveled to fit A1 with its description updated — then the corrected counts (197 → 195 lessons; A1 36 → 34) swept through the sales landing, the main site, the copy deck and the ad copy; the copy-conformance check (68 pairs, 0 missing) and both site QA suites passed; redeployed to Cloudflare Pages and verified on the live domains (both serve the new counts, zero stale numbers).
- Final-stage checks: a fresh full pass over all 187 copies — typography and structure scans clean (no broken tags, leaks or empty blocks) and the length-cap cross-check 177/177 — plus all 24 lessons in the five preview books rebuilt from the updated copies with a read-back per lesson.
- Built the second lesson in the IELTS book — "IELTS Trainer — Listening · Reading · Writing": 48 exercises across 4 sections simulating a whole exam — listening (4 parts / 40 questions on one recording cut into seven play-once groups), reading (5 texts / 40 questions), writing (a letter + an essay with student checklists and hidden sample answers). Every answer key was server-verified (each page re-submitted for a full score — 80/80 marks), the new Execution Time feature sits on all 17 answer blocks, and the build passed API read-back plus a live editor DOM sweep (tables, map, dropdowns, all 7 audio files serving). Along the way, found and fixed a renderer bug live: a single `colspan` cell silently drops an entire table — bisected on this build, the table rebuilt and re-verified.
- Wrote the day's rules back into the skills: the IELTS exam-page port recipe (verified answer-key extraction, task-type → template mapping) into the transfer skill; the `colspan` pitfall into the materials CLI; the condense pipeline as its own new skill; and the in-place edit-wave procedures (speaking sets, rule texts, typos, preview sync) into the catalog-publishing playbook.



## 2026-10-02

- Extended the ESL feedback design system to v1.3 with a second skeleton — an IELTS band card: a band hero with the estimated overall band, a 0–9 dot scale, four per-skill cards with raw results, per-skill findings blocks, criteria tables for the productive skills and a quick-fixes grid. Shipped the slot-marked band-card template, the canon section and the token update (one new display size; a document may now use up to 7 distinct type sizes), and taught the conformance linter to accept both skeletons while keeping every existing check — 9/9 across the card, the new template and the homework template. Verified end to end: harness selftest green, and a Playwright render QA on desktop and mobile with zero overflow and zero console errors.
- Built and deployed a password-protected student area at itsfedor.cc/progress: a login page and a personal dashboard where students find their past analyses (newest first, "new" badges), RU + EN, mobile-first. Security by design — PBKDF2-hashed passwords, HMAC-signed session cookies (HttpOnly, SameSite=Lax, path-scoped, remember-me lifetimes), uniform deliberately delayed login errors, Origin checks, noindex / no-store headers on everything private, and per-student file isolation (missing, tampered or borrowed credentials all return the same 404s). Shipped through preview to production and verified on the live domain with 33 API checks and 29 UI checks green, including both locales and 360/390 px widths; a locale-duplication regression caught on the new page was fixed and pinned with new permanent checks.
- Wrote the day's rules back into the skills: the band-card playbook (diagnostic data extraction, first-attempt scoring, band conversion practice) and the Task 1 chart pixel-verification method (bar geometry over OCR, ±0.5% agreement check) went into the feedback and band-scoring skills; the new page's locale-hiding rule and the locale/mobile checks went into the site skill.



## 2026-10-01

- Built a B2 lesson from WFYI's "How Does Jury Duty Work?" (Simple Civics, 4:50) into the spoken-lessons series: 6 stages and 30 exercises — a flipped-classroom pre-watching page (10-pair match + 8-phrase gap-fill; the video itself is kept for class), vocabulary (10-term context text, match, fill-box, hidden teacher notes), watching (gist questions, the video, an 8-question auto-checked test, four timestamped segments with hidden answer keys, and a 10-gap exact-listening block verified word-for-word against the transcript), speaking (6 discussion questions, a 2-minute voice task with a model answer) and an extra stage (8 choose-the-option, 8 typed gaps, opinion writing, 90-second voice task). Verified live: API read-back clean and an editor DOM sweep mounting the cover, YouTube embed, 24 test radios, 10 exact gaps and 8 working dropdowns (the correct option renders highlighted); lesson tile mounted on the book page at CDN byte-parity.
- Built the next B2 lesson — WIRED's "Corporate Lawyer Breaks Down Succession Business Deals" — as a corporate-deal language build: 34 exercises across the same six stages, vocabulary from loan covenants and hostile takeovers to poison pills, six timestamped watching segments with answer keys, and a 10-sentence / 11-gap exact-listening drill in which a caption split ("…$130" vs "…130 dollars") is handled by a dual-accepted gap. API read-back clean (34/34 exercises, hidden notes, sequential numbering); DOM sweep green (24 test radios, 8 dropdowns, 11/11 listening gaps, cover and embed mounting); handshake-emoji lesson tile on the B2 gradient, CDN-verified, description set. The two builds bring the verified live-build playbook to sixteen instances.
- Prepared the launch message for teacher communities (RU + EN) for the five-book grammar pack, with every number re-derived from the pack data first: 73 modules · 197 lessons · 950+ exercise sets · speaking blocks in 90 lessons (1,800+ questions) · 55 tests.
- Wrote the day's rules back into the tooling skills: the two new build instances with their pitfalls — merging yt-dlp's triple English caption tracks down to the largest pair, the /a1/a2 dual-answer gap form for divergent caption splits, and the gentle-scroll timing needed to probe lazy-mounted dropdowns — plus the standing pre-watching-prep flipped-page pattern for new lesson waves.



## 2026-09-30

- Built the first lesson in a new IELTS section: a full-length academic diagnostic for a one-hour sitting — a designed test-guide page; listening (10 questions over a real exam recording — a five-minute exam-style audio cut — on a 10-minute timer); reading (13 questions: 7 true/false/not-stated + 6 gap-fill); writing (Task 1 bar chart + rubric, 20-minute timer); speaking (cue card + 3-minute recorded answer). All four timed parts run on the platform's new Execution Time feature; keys, transcript and band guide stay hidden for the teacher.
- Polished the lesson through owner-review passes: split every instruction into numbered line-by-line steps ("Do this: …") so the student always sees the next action; replaced two guide notes with designed picture cards (test guide + closing card — byte-identical uploads, rendering live); re-verified the whole build — all four timers confirmed at 10/10/10/20, API read-backs clean.
- Root-caused the platform's table bug that collapsed whole tables into one stacked column — a `<col>` without an explicit numeric px width makes the layout parser's parseFloat return NaN — rebuilt every table with measured widths (summing to the 576px content column) and confirmed real multi-column grids live in the editor.
- Built a B2 spoken lesson off Fireship's "An ex-OpenAI researcher just deleted language from the LLM": six sections with a flipped-classroom opener (two auto-checked practice tasks), and an exact-listening block of 12 sentences where every gap passed a chunk-by-chunk gate against two independent caption corpora before going live; verified by API read-back and a live DOM sweep.
- Built the C1 edition of the same video as a claims-vs-evidence lesson: 31 exercises in the same six-section build — four timestamped analysis parts, an 11-sentence exact-listening block gated against the two caption corpora (subtitles + ASR), a 200-word argumentative writing task and two voice tasks; cover and tile verified against the course palette.
- Evening fix on both lessons after the owner's note that the flipped-classroom page should be pre-watching prep: removed the embedded video from both prep pages live, retitled and rewrote them as "pre-watching preparation", kept the two auto-checked tasks as the whole assignment, refreshed both lesson descriptions — verified in place (verifiers clean, zero video iframes, blocks renumbered).
- Produced a C1 teacher's guide for Fireship's "Meta's Muse Pivot — Everything from Connect 2026" in the house format: warm-up discussion; key-terms matching; phrases and expressions; comprehension with timestamps and evidence-based answer keys; critical-thinking questions; four discussion tracks; differentiation notes, a sponsor-segment note, homework activities and a complete answer-key summary. Facts cross-checked against two transcript sources plus news coverage; prose audited; single clean file.
- Ran the homework-review pipeline on a pupil's remaining batch — an essay plus three voice recordings — into one color-coded HTML review on the feedback design system: per-item fixes with reasons, polished re-writes, a comprehension overview, tips linked to grammar references, and the three audio answers embedded for playback. Gates before delivery — design check 9/9, desktop + mobile QA clean, audio players live; revised the same evening on owner feedback and re-checked.
- Wrote the day's rules back into the working skills: the col-width table rule + div-grid render check, the timer-chip race note and headless-load flakiness fixes, the pre-watching flip-page pattern with its live retrofit recipe, the C1 course conventions, and the homework-review batch notes.



## 2026-09-29

- Reworked the sales page's FAQ — final set of six cards: what you need to
  start, how to choose a book, groups vs one-on-one, the language of the
  materials, payment and refunds — and tightened the gap down to the footer
  from 206px to 84px. Copy deck re-synced (68 phrase pairs) and a spacing QA
  check (`footer_gap`) added; deployed, with the served copy byte-verified
  from both edge nodes.
- Ran a conformance pass over the sales page and pinned it with QA:
  "scheme/charts" wording → "rules with examples and tables" across eight
  placements (comparison card, hero lead, FAQ, meta and OG descriptions),
  "keys" → "teacher's notes" everywhere, and the payments strip moved below
  the book grid with the books → FAQ gap cut from 152px to 48px. The retired
  wording returns zero hits on the live page; new checks cover both the
  wording and the exact geometry. Deploys verified from both edge nodes.
- Swapped the homepage credential chip from "a year living in the US" to
  "studied in the US" and swept every dependent surface (bio paragraph,
  credentials card, share-card template), adding a QA check so the old
  wording can't return; deployed, verified from both edge nodes.
- Updated the public offer's refund clause: once access to a pack has been
  granted, refunds aren't made (access is perpetual and buyers save the
  materials into their own collection); a full refund stays for access that
  was never delivered. The offer is a native Google Doc with the Docs API
  disabled, so the edit went through an export → DOCX → re-upload roundtrip
  that preserves the same file and link — first proven on a test copy, then
  applied with a paragraph-level diff (all 105 paragraphs intact, exactly one
  clause changed) and re-verified through the buyer-facing link. Backups
  kept; the roundtrip was written into the workspace playbook.
- Built a C1 lesson — "How Silicon Valley Bank Collapsed in 36 Hours" — into
  the spoken-lessons series: 31 exercises across five stages — vocabulary
  (12-term context text, 12-pair match, 8-item fill-box), a gist intro →
  video → auto-checked 8-question test → six timestamped watching segments
  with 23 comprehension questions and hidden answer keys, a 13-sentence
  exact-listening block whose 14 gaps were verified word-for-word against two
  independent caption corpora, and a speaking stage with a 2-minute voice
  task plus teacher notes — closing with a writing/voice extra. Verified by
  API read-back (31/31 exercises, zero issues) and a live DOM render check
  (24 auto-checked radios, 8 dropdowns, 21 typed gaps, cover and embed all
  mounting).
- Rendered a "Shops and public places" vocabulary table as a classroom-scale
  transparent PNG (1760×6084) through the house chart pipeline, then
  attached it to a pupil's homework sheet — the platform blocks direct image
  edits on homework-mode items, so it went via the pool-first route: create
  the picture block in the lesson pool, bind the image, attach to the sheet,
  bump the item counts and the "new" badge. Verified by sheet read-back
  (11 → 12 items), the class overview, and a live page render (the image
  mounts full-size in the sheet's 656px column, no exercise number drawn). The flow was documented in the CLI skill.
- Added a seventh role-play — "Lunch break at the coffee station" — to the
  Small Talk Training lesson, inserted right after Scenario 6 (the debrief
  moved to the last slot) with the display numbering re-flowed cleanly
  (1.6 → 1.7 → 1.8, no gaps — verified in the live editor), and bumped the
  lesson description from six scenarios to seven. API read-back
  byte-identical; the insert-between-exercises mechanic went into the CLI
  skill.



## 2026-09-28

- Built the sales landing for the five-book grammar pack from scratch to a QA-verified, packaged build: hero with one-click buy → before/after comparison of the prep workflow → proof numbers instead of testimonials → an inside-a-lesson tour → the five books + bundle → delivery steps with a Telegram button → FAQ → final CTA, plus a mobile sticky buy bar and RU-by-default with an EN toggle.
- Kept it a single file that opens from `file://` with no build step, with six reusable checkout links wired into one CONFIG block and a serverless auto-delivery worker behind them — payment-signature check, buyer email with the access page, owner ping in Telegram — 12/12 local worker tests green.
- Researched cross-border payment acceptance for selling to Russian buyers from abroad: verified why foreign acquirers can't charge Russian cards, compared a non-resident acquiring programme, a digital-goods marketplace and Telegram Stars, documented hold periods, withdrawal chains and chargeback handling, and settled on the two-channel scheme (main + backup).
- Cut the page's visible copy by 41% (873 → 515 RU words) through a three-agent batch — copy, visual system, animations — against an approved RU/EN deck; a conformance checker now fails the page if any of the 138 deck lines drifts from the markup (fresh run: 0 missing RU / 0 missing EN).
- Replaced ad-hoc effects with vetted, locally vendored libraries: AOS scroll reveals + count-up behind a progressive-enhancement "arm" (nothing is hidden without JS or under reduced motion), emoji chips instead of custom stickers, a single accent colour enforced by a palette-canon QA scan, and hand-drawn accents kept static only — the JS-drawn annotations were removed after the owner caught them visually detaching from words while scrolling.
- Rebuilt the QA kit as one Playwright audit: desktop + mobile + file:// + no-JS + reduced-motion across four viewport widths — palette off-canon = 0, overflow = 0, reveals 31/31, images 12/12, console errors 0; all green.
- Produced the bundle hero image via an API pipeline: reference-conditioned generation of the five mascots composed into one scene, then true-alpha matting for the cut — after pixel-checking that asking the model for a transparent background only yields a fake checkerboard — shipping a 1376×671 transparent WebP, live on the page.
- Wrote the day's rules back into the working skill (site v2.1: vendored-library policy, palette canon, QA commands, the annotation pitfall) and repackaged the delivery archive.



## 2026-09-26

- Ran the homework-review pipeline end to end on a real submitted sitting — fetch → ASR transcription → feedback document on the design canon → conformance lint → desktop + mobile render QA: linter 9/9, zero overflow, zero console errors, audio embedded and playing in the document.
- Sharpened the homework-review skills with the pipeline's operational rules: fillers stay internal signal only and never appear in a document (no fix item, no quote, no mention — the raw transcript is the only place they live); one sitting counts as one review batch even across several sheets; and a sheet freezes at assignment time, so the sheet — not the lesson's current pool — is the source of truth for what a student actually received.



## 2026-09-25

- Closed the ESL feedback design-system wave: v1.2 removed the machine speech metrics from the feedback documents per the owner's edits, and the canon was embedded into the working skills — the canonical template, tokens, conformance linter and the Playwright QA runner mirrored and certified (sha256 byte-equality for the template, tokens and linter), with the generation policy now "copy the template, fill the slots, lint, deliver". Linter 9/9 and render QA green on both the template and the showcase.
- Built "When Does US Debt Become Genuinely Bad?" (WSJ, 7:36) as a C1 lesson in the New Spoken Lessons book: 31 exercises across five stages — vocabulary (topic text, 11-pair match, fill box), gist and first-viewing questions, an 8-question auto-checked test, six timestamped watching parts with hidden answer notes, an exact-listening block, a speaking stage with a voice task and a writing extra. All nine exact-listening gaps verified word-for-word against the transcript before saving; API read-back and live render checks passed (cover, video embed, 24 test radios, gaps, dropdowns, drag items), level tile and description in place.
- Measured the lesson editor's fixed content column (656 px) and derived the classroom type scale for guide images (canvas type ≈ on-screen size ÷ 0.745), then rendered a six-part small-talk guide set — rules of the game, openers, follow-up menu, reactions, topics, exits — and swapped all six text notes for the designed picture blocks in place: same exercise IDs, numbering and order, hidden keys untouched. Verified by API read-back and a live DOM check (six captioned images, 1760-px originals on the CDN).
- Reworked the pre-watching block of three TV-episode homework lessons into the approved format: the vocabulary match became a "List of helpful words and phrases" word-list exercise (translation + definition, one-click add-to-vocabulary), edited in place so existing exercise IDs and homework links stay valid; verified live in the lesson editor.
- Built "Why Austin Failed To Become The Next Silicon Valley" (Architales, 8:43) as the next C1 lesson: 31 exercises across five stages authored from the video transcript, everyday phrasal verbs and collocations as the vocabulary target, ten exact-listening gaps verified word-for-word, plus the book-standard tile and description. API read-back and a DOM sweep both clean — the thirteenth fully verified live build.
- Wrote the day's rules back into the tooling skills: the notes-to-pictures in-place conversion recipe (upload, mutate, save, bind the image, read back), the image display-size measurement, the browser-verification session-reuse trick, and the word-list block-edit procedure.
- Extended the Edvibe CLI harness with a `site` command group for the platform's teacher landing pages — show, backup, registration requests, block on/off, metadata, patch-edit and publish — with every write wrapped in a timestamped backup → save → read-back-diff flow (plus a `--dry-run` mode); the landing write RPCs were reverse-engineered from the frontend bundles and verified live end to end; +15 unit tests, the offline suite now at 125 passing (5 skipped).
- Used the new group end to end on a live teacher landing page: rebuilt the examples block with three current lessons (activating each lesson's sharing code through the materials RPC so the cards open for visitors), added two FAQ entries and set the page's title, description and social-preview image. All writes were backup → save → read-back verified and the page republished; also documented a platform-side caveat: metadata values save but the current platform version does not render them yet.
- Wrote the landing write path, the full-replace safety procedure and the sharing-code mechanics back into the materials CLI skill.



## 2026-09-24

- Built the homework auto-check pipeline end to end: new CLI commands pull a pupil's submitted answers (voice recordings plus written answers), an `audio transcribe` command runs Deepgram Nova-3 in multilingual mode (RU+EN code-switching, per-word language tags, timestamps) and emits a stats-rich JSON — speech rate, pauses, fillers, low-confidence words — and a new skill turns it into the color-coded HTML feedback document. An ASR decision review compared seven hosted providers with source-cited claims, verified on real audio; 110 offline tests green, and the live acceptance read back real submissions and transcribed real recordings.
- Extended the Edvibe CLI from the platform's official documentation: 13 new exercise builders (unscramble, audio upload, GIF, three label-picture variants, seven embed integrations, carousel galleries) take the lesson spec from 18 to 31 exercise types, plus audio upload/attach and multi-image support. Verified with 88 offline tests and an end-to-end build of 18 exercises created, read back over the API and rendered live in the lesson editor.
- Bundled the day's rebuilt CLI wheel (0.8.0) into the teacher kit, refreshed the lesson-spec reference for all new exercise types, and added the answers-download and transcription commands to the teacher-facing skill.
- Shipped ESL Feedback Design System v1 for the homework-feedback documents: audited the drift (three visual families, 8–14 font sizes per doc, three different reds for one semantic role) and unified it — one WCAG-checked palette with a Machado CVD pass and redundant category chips (colour is never the only signal), a six-size type scale, a 4-px grid, a slot-marked canonical template and a generation policy. Built the self-QA tooling — a static conformance linter plus a Playwright runner (desktop + mobile, overflow/console/font checks) — and cut teacher notes 20% (945 → 752 words) with all student text diff-verified unchanged; linter 9/9, zero overflow, zero console errors.
- Built a new exercise-authoring skill from research: four evidence-based learner-error banks (469 sourced entries — A2, B1, B2 grammar plus L1 RU/KZ transfer patterns), a distractor taxonomy, quality gates and a linter, in a two-pass workflow (generation plus an adversarial review). Piloted end to end: 15/15 items reviewed, one blocker and one hygiene issue fixed, lessons written back into the skill.
- Built "Why Airlines Can't Survive Without Loyalty Programs" (WSJ) as a B2 lesson in the New Spoken Lessons book: 29 exercises across five stages, all eight exact-listening gaps verified word-for-word against the transcript before saving, level tile and description applied; verified live via API read-back and a rendered DOM check.
- Refreshed the bundle ad for the five-book grammar series: a content pass found explanation blocks on 5,210 of 5,239 lesson questions and the sell list was rebuilt around it; both formats (4:3 and 16:9) re-rendered with build-time assertions and OCR read-back of the final art.



## 2026-09-23

- Worked through the Minecraft ESL server task board and shipped a verified pack of fixes: login no longer bounces players to spawn (they keep the spot where they logged out), the per-level permission groups were repaired so regular players can actually use /sethome, /home, claims, kits, afk and the payment commands, claim-block purchase turned on at $1 per block with a written Russian walkthrough, and the "banned for spam" autoban switched off.
- Root-caused the recurring "animals vanish on the server" report: ClearLag's AI optimisation was quietly deleting mobs more than 64 blocks away from any player, ignoring claims — disabled, the night profile defused, and the protected-entity list widened to 36 types. The whole pack was verified by running the exact plugin set on a local Paper 26.1.2 (build 74) server: clean start, every command and permission node resolves.
- Built a new Paper plugin for the server — a config-driven clickable command book (578 lines of Java, 3 classes): /guide with run/suggest buttons, give, giveall and reload subcommands, automatic handout on first join, and a page-width checker that flags overflow before anything ships. All texts live in YAML, so nothing needs rebuilding to change them.
- Folded the English corrector back into the chat plugin (v1.1.0): a private "better: …" hint is now returned inside the same API request instead of a second call, behind a 90-second cooldown with its own config section.
- Security pass over the public plugin family: the bundled jar's default config shipped a hardcoded API key — stripped from both public plugins (dailyenglish, chat2earn) and committed.
- Upgraded the Telegram bot that operates the server: a 12-command menu, a profile description, quick inline buttons (status / players / logs / start), a help banner and an avatar, plus an owner-id fallback that kills the "someone else claimed the bot first" failure. Shipped with a setup script, a profile script and an 8-section README; 83/83 smoke assertions green, then verified live as a single launchd-managed process.
- Finished the C1 lesson's branding to the book standard: a generated 256px level-gradient tile with a level emoji and a description in the house format, verified byte-for-byte against the CDN and read back from the live lesson.
- Moved the grammar series' originality pass into the duplicated editions: the A1 master was restored to its original state (14/14 fields, zero diffs) and copy A1 1.2 was rewritten end to end — explanation, four exercises, every answer key and the speaking section — ending at 0 verbatim matches against the source caches, no 5-word chains, and all 20 gap markers kept in place and order; every write went backup → apply → read-back.
- Extended the rewrite toolkit: an exact token renderer plus an apply/verify engine, per-lesson spec scripts, and an old→new lesson map covering all 187 lessons across the five copies; the next lesson (1.3) dry-ran green — 23 explanation swaps, 20/20 markers, 0 hits — ready to apply.
- Split the agent's models for both depth and cost: a deep-reasoning model for planning and review, a fast model for delegated execution, auxiliary tasks on the cheapest tier — delivered as an idempotent setup script with config backups plus a skill, tested against a stubbed CLI in both modes.



## 2026-09-22

- Ran the final pre-submission QA sweep on the five-book grammar series: closed a stale duplicate of an A1 lesson that wasn't visible in the book (the live copy was recalculated and verified, the stale copy dumped then removed, all indices re-synced); removed all 668 apostrophe-duplicate answer pairs (final scan: 0 across all books); re-timed all 187 lessons to a uniform "30–45 min"; re-ran the clean scans — 187 lessons, zero external images, homework present on every lesson (6 items each); and compiled the requirement-by-requirement submission-readiness audit off live scans.
- Completed the speaking-section restyle wave (57 single-part sections rebuilt in the approved layout, verified 57/57, junk-pattern scan zero), reformatted all 90 speaking teacher notes into structured lists, and inventoried the Explanation image layer — 263 images, 252 captions, all account-hosted.
- Ran a visual-defects pass across the series, every item surfaced in live use: sample words that had lost their highlight styling (8 words in 8 lessons — restored in the approved bold-blue style, read-back 8/8); Example-line artifacts — a parser tail plus an unclosed italic tag that made a whole exercise render in italics — fixed, with pack-wide scans confirming no further occurrences; and two module headers where a red emoji sat on an orange gradient at ~1.0 contrast (found by a pack-wide contrast scan) recolored together with their two lesson covers. All fixes backed up and read-back verified.
- Built a B2 lesson from the WSJ's "How 'Buy Now, Pay Later' Makes Billions From 'Free' Loans": 29 exercises across 5 stages, authored from the transcript alone, with the five listening segments aligned to the video's own chapters and 8 exact-listening gaps verified word-for-word; signed off after API read-back and DOM render checks (cover, dropdowns, test radios, drag items).
- Migrated the remaining 46 lessons into the New Spoken Lessons book across its three level courses — B1 (12), B1+ (23), B2 (11) — 1,504 exercises in total, every lesson with a vocabulary stage, an auto-checked test, timestamped listening segments with hidden answer keys, a speaking stage and homework. Exact-listening blocks landed for every video lesson except the 19th-Amendment pair: after both transcript channels blocked mid-run, a patient multi-service retriever rotated providers and recovered every remaining transcript — the pair's captions still arrive corrupted from every service, so one clean transcript file is the last input (one article-based lesson has no video by design).
- Designed the book's visual system for the new lessons: covers for all 46 (theme emoji on the level gradient — B1 green, B1+ blue, B2 purple) plus the book and section covers, verified byte-for-byte against the CDN (md5 match 46/46); filled all 46 lesson descriptions (Audience / Duration / Level / Objective / Stages; 8 empty ones restored) and checked the live book page.
- Started the pre-submission originality pass on the grammar series: measured the platform's catalog requirements and the books' text layer class by class, wrote the tiered rewrite plan — ~190k words in scope, from full rewrites to light edits to untouched formulas, with a zero-match acceptance gate — and built the toolkit: a renderer that reproduces the live markup token-for-token plus an apply engine (backup → in-place update → read-back).
- Piloted the rewrite on lesson A1 1.1 — 73 flagged sentences (51 full rewrites, 20 light edits, 2 formulas kept) down to zero residual matches; all gap markers intact (20/10/20/20), every choose-gap keeps its marked answer (20/20), keys and mirrors validated, homework and images untouched. Validator PASS; the Module 1 wave (lessons 1.2–1.5) is queued behind the owner's visual check.
- Wrote the day's rules back into the tooling skills: the Example-line and sample-word styling pitfalls into the transfer skill, the rewrite runbook and pilot status into the catalog-publishing skill, and the eighth verified live build instance into the materials-CLI skill.



## 2026-09-21

- Fixed a formatting defect class across the whole five-book grammar series in one sweep: dialogue exercises now render as scripts — each speaker turn on its own line, the speaker's name bold, no list numbers; single-text pages lost a stray "1." prefix; and per-turn paragraphs that had been glued into walls of text are preserved as real line breaks. 90 exercises across 71 lessons were updated in place — same exercise IDs and numbering, so every existing reference and homework link survives; read-back checks passed with 0 errors and the offline gate still reports 0 broken answers across all 187 lessons. 45 tests now pin the new behavior.
- Parsed a public catalogue of grammar conversation-question sets (45 sets, 907 prompts), mapped it against all 187 lessons of the series, and built the speaking layer from it: an automated builder added a Speaking section to the 90 covered lessons — 1,802 conversation questions in total, each block carrying a hidden teacher note (level, use, what to watch for). Read-back verification: 90 lessons checked, 0 problems.
- Updated descriptions across the series: a "Speaking" line in all 90 lesson descriptions and a "Speaking" block in all five book descriptions — every write read-back verified and idempotent, with backups taken first.
- Started the Use of English wave: scraped and converted all 55 test sets (11 per level × 5 books, 15 items each) and fetched all 55 cover images with an OCR-based quality pass; then rebuilt the first book's test section in the new format — cover + auto-checked test + hidden answer-and-explanation note per lesson, read-back verified 11/11 (one transient error retried clean).
- Added a lesson-delete capability to the Edvibe CLI harness (found and verified the RPC) after the pilot run created a duplicate lesson — the duplicate was removed cleanly.
- Built a new B1+ lesson from TED-Ed's "Should you trust unanimous decisions?": 5 stages, 30 exercises — vocabulary match and fill blocks, an 8-question auto-checked test, timestamped watching segments with hidden answers, two exact-listening blocks whose 9 gaps were verified chunk-wise against the transcript, plus speaking and writing tasks. Verified live via API read-back and a rendered check in the lesson editor, all answer keys hidden.
- Wrote the day's rules back into the tooling: the numbering fixer became a reusable driver (worklist + state), the speaking pipeline shipped as a documented builder + verifier, and the materials-CLI skill recorded the day's two new verification pitfalls (the seventh fully verified live build).



## 2026-09-20

- Ran a full defect audit across all five books of the grammar series (187 lessons, one audit agent per book) and rebuilt every Exercises section after fixing the root causes: the converter had silently dropped 1,184 gap answers (an answer layout it never read), plus 469 case-only duplicate answers (the platform treats answers case-insensitively) and 109 EXAMPLE blocks that had lost their styling. Post-rebuild audit: all defect categories at zero on every level; rebuilds were in place, so exercise IDs and every homework link stayed intact.
- Converted 59 dropdown exercises to the platform's untimed Test type to match the source's radio UI — this also fixed all 161 multi-answer "choose two" questions that a dropdown silently scored as single-answer, and split 10 parenthesized answers into real accepted variants. Verified: 60 lessons checked, 59 Test exercises, 0 mismatches against spec.
- Fixed three further defect classes reported during live use: 6 exercises saved with empty names (instruction parser rewritten to read the heading region above each quiz), 2 exercises with merged options (converted to Test in place — dropdown duplicates gone), and 48 "compressed" answers expanded to full accepted variants. Full rollback dumps taken first; affected lessons updated in place by three parallel workers, every write verified by API read-back.
- Extended the Edvibe CLI harness: a delegated agent added `materials folders` / `materials move` (dry-run + read-back) and `lesson dump` (full read-only lesson backup — used to take rollback dumps before every rebuild); the test suite grew to 85 passing tests (5 E2E skipped).
- Reworked the cover art for all five books: mascot art re-cut and scaled for balanced spacing (~109px of air per side, ~110px below; everything else pixel-identical — diff-proven); all five covers re-uploaded and verified by fresh ImageId + CDN hash match.
- Designed a new bundle ad creative — all five books in one 4:3 sheet — with every number generated from the transfer data (5 books · 73 modules · 187 lessons · "570+" exercises) and in-script QA: DOM counts vs data, cover-image load checks, OCR readback of every headline — all green, zero overflow.
- Wrote the day's lessons back into the skills: all five source answer layouts and the radio→Test conversion rules into the transfer skill, the measured cover grid + merged-option pitfalls into the materials-CLI skill, and the bundle-sheet anatomy + QA recipe into the ads skill.



## 2026-09-18

- Built "Why Bond Yields Are a Key Economic Barometer" (WSJ, 5:12) as a standalone B2 lesson through the Edvibe CLI harness: 5 stages, 27 exercises, every answer key and teacher note hidden from students.
- Authored the whole lesson from the transcript alone: a lesson driver carries the full content plus a `--check` mode, so the lesson is reproducible from code.
- Exact-listening gate: all 7 typed-gap sentences verified word-for-word against the transcript by the driver's chunk-wise checker (normalizer absorbs caption quirks such as "longterm" vs "long term").
- Stages: warm-up (cover + lead-ins), vocabulary (10-pair matching, drag-to-gap sentences, pronunciation notes), watching (gist questions, 8-question auto-checked test, four timecoded segments with suggested answers), speaking (discussion + a 1–2 min voice task with a model answer), extra (dropdown definitions, word-form gaps, a 150-word reflection, a 90-second retell).
- Traced a non-rendering lesson cover to the thumbnail host — the canonical YouTube host mounts in ~3 s where the alternative never appears in the editor — and recorded the pitfall plus a sixth fully verified build instance in the materials CLI skill.
- Verified before sign-off: full API read-back (structure, hidden flags, ticks, gaps, description) and a live render check in the lesson editor (sections in order, interactive dropdowns, cover visible).



## 2026-09-17

- Completed the A1 grammar course book on Edvibe: 36 lessons across 12 modules, 39 generated grammar charts, numbered lessons with searchable descriptions, every answer key hidden, zero references to the source material.
- Built and shipped four more course books in one batch (A2, B1, B1+, B2): 151 lessons, 61 modules, 221 in-lesson images, 469 hidden answer keys, with a per-level verification report checking every lesson for structure, hidden keys and source mentions.
- Extended the Edvibe CLI harness with a `book` command group: dump sections and lessons, set covers, generate and batch-apply section and lesson icons (48 files in one command), and cut character art with automatic hole cleanup. Test suite now at 55 passing tests.
- Cleaned up the platform library: reverse-engineered Edvibe's undocumented book-move RPC from the frontend bundles and archived 7 leftover test books into a folder (nothing deleted, fully reversible).
- Branded all five books with one system: a pixel-measured cover grid (gradient, divider bar, level label, composited character art), per-module gradient and emoji icons, and the Module N section structure, with the full look verified in the platform UI.
- Designed the ad system for the whole series: one 4:3 sell sheet per level, every number computed from the transfer data, Playwright 2x renders, and QA with no human eyes: OCR readback, glyph-IoU reference checks and alpha-mask geometry (B2: 33/33 lesson numbers OCR-clean, title match 0.93 IoU, zero clipping). Locked the workflow into a reusable skill: approved anatomy, brand tokens, generator and QA scripts.
- Built a B1+ lesson from a JetBrains Academy video and transferred it live into Edvibe: 5 stages and 34 blocks (warm-up, vocabulary, video with 6 timestamped answer-key segments, speaking with voice tasks, extra practice), all answer keys hidden; verified with API read-back and a headless render check.
- Added a True/False comprehension block (12 statements, 6 true / 6 false, from 4:16 to the end) for the second half of a video lesson: dry run first, then created and attached to the live homework, verified with an API read-back and a rendered page check.
- Updated the transfer skills: the batch pipeline skill moved to v3.0 (manifests, parallel import workers, OCR chart QA, verify-all) and the CLI skill gained the full book branding playbook and the archiving method.



## 2026-09-15

- Portfolio overhaul: audited all 10 public repos — gitleaks over full history (no credentials, current or historical), personal names redacted from 4 files (history rewrite queued for 3 repos), missing build files + Gradle wrappers added to englishprogression, vocabquiz and dailyenglish, download steps, dependency links and troubleshooting sections added to every plugin README, the missing LICENSE added to this repo, and all social-preview images refreshed in a Notion-dark style.
- Added a screenshot gallery, pipeline-architecture diagram and copy-paste agent-install instructions to esl-automation-suite; cross-linked the four plugin READMEs and made every badge clickable.
- Merged hermes-skills into esl-automation-suite: video-review summaries now install with the suite (one command, 3 skills, 6 pipelines); hermes-skills archived as a pointer so old links keep working.
- Renamed the GitHub account to itsfedor and rebranded every repo, image and commit to Fedor Molodtsov: cross-links, GitHub Pages URLs, release links and git history all updated.
- Built units 3–5 of the A2+ per-episode course through the CLI harness — 7 blocks per unit, verified live in the book.
- Pushed per-agent install docs (hermes-agent / claude-code / codex) to esl-automation-suite; install path re-verified in clean HOME environments.
- Built a B2 guide from a Fireship video into a 27-block Edvibe lesson (5 stages, answer keys hidden).
- Attached the companion 6-exercise B2 homework to a live sheet with one command; verified on the platform (1.1–1.6).
- Published the CLI harness as a public repo — itsfedor/cli-anything-edvibe: README with use cases and installation, trimmed protocol notes, tests.

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
