# The New Porker — Product Requirements Document

**Status:** Draft v0.1 · **Date:** 2026-09-26 · **Owner:** anhpnguyen95

> *The New Porker* is a satirical magazine website about animals doing wild things, written in the voice of a very serious literary weekly. It also has a daily games section that parodies prestige-magazine puzzles.

---

## 1. Summary

The New Porker is a parody news and culture site. Every story is fake, every subject is an animal, and every sentence is written with a straight face. It borrows the *conventions* of a highbrow weekly (long-form features, section rubrics, cartoons, a pompous masthead mascot, a daily puzzle habit) and applies them to raccoons unionizing, geese filing noise complaints, and an octopus who got into Yale.

The second pillar is **Games**: small, daily, shareable puzzles that parody magazine word games (Shuffalo → **Snuffalo**, Categories → **Catagories**, and others). Games are the retention engine; stories are the discovery engine.

## 2. Goals and non-goals

### Goals
1. **Make people laugh, then make them come back.** A reader who lands from a shared headline should find a daily game and return tomorrow.
2. **Nail the voice.** The comedy is in the gap between a solemn register and an absurd subject. Copy quality is the product.
3. **Ship a fast, cheap, static site** that one person can run. No servers required for v1.
4. **Make games shareable** with spoiler-free result cards (emoji grids, like the genre expects).

### Non-goals (v1)
- User accounts, comments, or real subscriptions.
- Real news. No real people as subjects of fabricated claims (see §4).
- Native apps.
- Ads. (A fake paywall joke is in scope; a real paywall is not.)

## 3. Audience

| Persona | Who | What they want |
|---|---|---|
| **The Sharer** | Scrolls social, sends links to group chats | One perfect headline and an image to screenshot |
| **The Daily Puzzler** | Already plays Wordle/Connections-style games | A 3–5 minute ritual, a streak, a result to post |
| **The Literary Lurker** | Actually reads *The New Yorker* | Pitch-perfect genre parody and deep-cut jokes (fact-checker notes, cartoon captions, "Goings On" listings) |

## 4. Parody and legal guardrails

These are requirements, not suggestions.

1. **Distinct identity.** Name is *The New Porker*. We do **not** use *The New Yorker*'s logo, the Irvin typeface, their Eustace Tilley artwork, their cover layouts, or their trade dress. Our mascot is an original character, **Eustace Swilley** (a pig with a monocle, examining a butterfly-shaped truffle).
2. **Visible disclaimer** in the footer of every page and on the About page: *"The New Porker is a work of satire. It is not affiliated with, endorsed by, or connected to The New Yorker or Condé Nast. All stories are fiction. All animals are fictional, except the ones who are just very good."*
3. **Game names are puns, not copies.** Mechanics are generic (word-finding, grouping, crosswords) and all puzzle content is original.
4. **No real humans as subjects of fake news.** Stories are about animals. Human public figures may not be quoted or depicted doing things they did not do.
5. **No real brands defamed.** Fictional companies only ("Chewy's rival, Gnawy").
6. `<meta>` tags and Open Graph cards carry the "Satire" label so shared links are not mistaken for news.

## 5. Information architecture

```
/                       Home (the "issue")
/news/                  Fake News — all stories, newest first
/news/<slug>/           Story page
/section/<section>/     Section index (see §6)
/games/                 Games hub
/games/snuffalo/        Daily word game
/games/catagories/      Daily grouping game
/games/name-droppings/  Daily guess-the-animal game
/games/crossbeak/       Daily mini crossword
/games/caption-contest/ Weekly cartoon caption contest (read-only in v1)
/cartoons/              Cartoon archive
/magazine/<issue-date>/ Weekly "issue" table of contents with a cover
/newsletter/            The Daily Trough (sign-up form, stubbed in v1)
/about/                 About + satire disclaimer
```

Primary nav: **News · Snouts & Murmurs · Culture · Cartoons · Games · The Magazine**. Utility nav: *Newsletter*, *Subscribe* (joke).

## 6. Content model

### 6.1 Sections (parodied rubrics)

| Our section | Parodies | Format |
|---|---|---|
| **Talk of the Farm** | Talk of the Town | Short, dry, first-person-plural dispatches ("We met the heron at a quiet table near the koi pond…") |
| **Snouts & Murmurs** | Shouts & Murmurs | Humor pieces, lists, open letters from animals |
| **The Burrow-witz Report** | The Borowitz Report | One-joke fake news, 150–300 words |
| **Annals of Instinct** | Annals of … | 3,000-word long-form, with fact-checker footnotes |
| **Goings On About the Barn** | Goings On About Town | Event listings: "Owl Poetry Night, 3 A.M., the old oak. Bring nothing. Expect to be judged." |
| **The Critics** | The Critics | Reviews: a cat reviews a cardboard box; a dog reviews the mailman |
| **Personal History** | Personal History | Memoir: "I Was a Seagull at a Wedding" |
| **Cartoons** | Cartoons | Single-panel gags with captions |

### 6.2 Story schema (MDX front-matter)

```yaml
title: "Raccoons Win Right to Collective Bargaining Over Municipal Bins"
dek: "After a three-week strike, the trash pandas have secured lid access and dental."
section: burrow-witz
byline: "Hortense Quill-Hogg"        # fictional staff
species: [raccoon]                   # used for tags and "More from the raccoon desk"
date: 2026-09-26
illustration: /art/raccoon-union.svg
illustration_credit: "Illustration by Barnaby Stoat"
reading_time: 4
fact_check_note: "An earlier version of this article misstated the number of raccoons in the union. It is all of them."
```

### 6.3 Launch content (minimum)
- 24 stories across all sections (at least 3 per section).
- 12 cartoons.
- 1 magazine issue with cover.
- 30 days of puzzles per game, pre-authored.

Sample headlines to set the voice:
- "Octopus Admitted to Yale Early Decision, Plans to Major in Escaping"
- "Local Goose Files 400th Noise Complaint Against Himself"
- "The Squirrel Who Buried a Nut in 2019 and Is Still Thinking About It" *(Annals of Instinct)*
- "Crows Launch Venture Fund Focused Exclusively on Shiny Things"
- "Opinion: I Am a Cat and I Did Not Ask to Be Born Into This Box" *(Snouts & Murmurs)*
- "Emperor Penguin Announces Divorce in Carefully Worded Instagram Post"
- "Beaver Dam Project Over Budget, Behind Schedule, Critics Say 'Very Beaver'"
- "Pigeon Arrested for Impersonating a Dove at Wedding"

## 7. Games

All games share a frame: date header, streak counter, "How to play" sheet, a results screen with a shareable text card, and archive access to previous days. One puzzle per day, same for everyone, rolling over at midnight America/New_York. State and stats are stored in `localStorage` in v1.

### 7.1 Snuffalo *(parodies Shuffalo)*
**Premise:** Eustace Swilley is snuffling for truffles. Help him root out words.

- Seven letter tiles sit in a trough; one center tile is the **Truffle** letter.
- Make words of 4+ letters; every word must contain the Truffle letter. Letters can repeat.
- A **Shuffle** button (the snout icon) reorders the outer tiles.
- Scoring: 4-letter word = 1 point; longer words = 1 point per letter; a word using all seven letters is a **Whole Hog** (+7 bonus).
- Rank ladder (percentage of max score): *Piglet → Shoat → Rooter → Truffler → Mudlark → Prize Hog → Hog Wild*.
- Invalid-word toasts in voice: "Not in the trough." "Too short, even for a piglet." "Missing the truffle."
- Share card: `The New Porker · Snuffalo 9/26 · Prize Hog 🐖 · 23 words · 1 Whole Hog`

**Acceptance criteria**
- Dictionary check is instant (client-side word list, profanity-filtered).
- Found words persist across reloads for that day.
- Keyboard input works (letters, Enter, Backspace, Space = shuffle).

### 7.2 Catagories *(parodies Categories)*
**Premise:** Sixteen tiles, four hidden groups of four. A cat is watching. If you make four mistakes, the cat knocks your puzzle off the table.

- Select four tiles, press **Submit**. Correct groups lock in with a color band and the group name.
- Difficulty colors: *Kibble* (yellow, easiest), *Tuna* (green), *Catnip* (blue), *Hairball* (purple, trickiest).
- Mistakes are shown as four paw prints; each wrong guess, a paw "swats" and disappears.
- "One away…" message when three of four are correct.
- Loss animation: the board slides off the table edge; all groups revealed.
- Example puzzle: **Things a cat knocks over** (glass, pen, vase, keys) · **___ nap** (cat, power, dirt, kid) · **Wild cats** (puma, lynx, ocelot, jaguar) · **Words hiding "cat"** (scatter, vacate, locate, educate).
- Share card uses the colored-square grid convention.

**Acceptance criteria**
- Tiles can be shuffled and deselected.
- Duplicate guesses do not cost a mistake.
- Works with keyboard and screen readers (tiles are toggle buttons with `aria-pressed`).

### 7.3 Name Droppings *(parodies Name Drop)*
Guess a famous (fictional or folkloric) animal from up to five clues, revealed one at a time from vaguest to most specific. Fewer clues used = better score, shown as dropping-sized icons (🟤 tasteful, 1–5). Autocomplete from an animal-name list.

### 7.4 The Crossbeak *(parodies the Mini crossword)*
A 5×5 daily mini with animal-themed clues. Timer, check/reveal, pencil mode. Completion message from Eustace: "Splendid. Now go roll in something."

### 7.5 Caption Contest: Hold Your Horses *(parodies the Cartoon Caption Contest)*
Weekly uncaptioned animal cartoon plus three "finalist" captions written by staff. v1: readers vote on finalists, votes stored locally only and shown with seeded fake percentages. v2: real submissions and voting (needs a backend).

## 8. Functional requirements

| ID | Requirement | Priority |
|---|---|---|
| F1 | Home page shows lead story, 6–10 secondary stories, a games strip with today's puzzles, and a cartoon | P0 |
| F2 | Story pages render MDX with illustration, byline, dek, section rubric, reading time, and end-of-story "diamond" dingbat (ours is a tiny hoof ♦) | P0 |
| F3 | Games hub with a card per game showing today's status (not started / in progress / solved) | P0 |
| F4 | Snuffalo and Catagories fully playable | P0 |
| F5 | Share result to clipboard with fallback text selection | P0 |
| F6 | Satire disclaimer on every page and in OG metadata | P0 |
| F7 | Name Droppings and Crossbeak playable | P1 |
| F8 | Fake paywall: after 3 stories, a dismissible modal: "You've read 3 of 3 free kibbles this month." with a "Subscribe for $0 and a belly rub" button that just closes it | P1 |
| F9 | Magazine issue page with illustrated cover and table of contents | P1 |
| F10 | Newsletter form (client-side validation, success message; no real submission in v1) | P2 |
| F11 | Caption contest voting | P2 |
| F12 | RSS feed of stories | P2 |

## 9. Non-functional requirements

- **Performance:** Lighthouse ≥ 95 on mobile for home and story pages; games JS ≤ 40 KB gzipped each.
- **Accessibility:** WCAG 2.2 AA. All games keyboard-playable and screen-reader-announced; color is never the only signal (Catagories bands carry text labels).
- **Responsive:** 360px to 1440px. Games are designed mobile-first.
- **Theming:** Light and dark mode.
- **SEO/Share:** Per-story OG image generated at build time (headline over illustration, "SATIRE" stamp).

## 10. Technical approach (recommended)

- **Framework:** Astro (static output) with MDX content collections for stories and JSON for puzzles.
- **Games:** Preact islands, one per game, sharing a `useDailyPuzzle(gameId)` hook for date resolution, persistence, and stats.
- **Puzzle data:** `src/content/puzzles/<game>/<YYYY-MM-DD>.json`. Build fails if a day in the next 14 is missing.
- **Word list:** Pre-built, filtered word list shipped as a compressed trie for Snuffalo.
- **Hosting:** Static host (Cloudflare Pages / Netlify / GitHub Pages). No backend in v1.
- **Analytics:** Privacy-friendly, cookieless (Plausible or similar): page views, game starts, completions, shares.

## 11. Success metrics (first 90 days)

| Metric | Target |
|---|---|
| Share-button clicks per game completion | ≥ 25% |
| D7 return rate among players | ≥ 20% |
| Median games played per returning visitor per day | ≥ 1.5 |
| Story → game click-through from home | ≥ 10% |
| Reports of "I thought this was real" | Low, and funny when it happens |

## 12. Milestones

| Milestone | Scope |
|---|---|
| **M0 — Design** | This PRD, design spec (`docs/DESIGN.md`), clickable mockup (`design/mockup.html`) |
| **M1 — Skeleton** | Astro project, layout, nav, footer disclaimer, story template, 6 stories |
| **M2 — Games I** | Games hub, Snuffalo, Catagories, share cards, streaks |
| **M3 — Content** | 24 stories, 12 cartoons, first magazine issue, 30 days of puzzles |
| **M4 — Games II** | Name Droppings, Crossbeak, fake paywall |
| **M5 — Launch** | OG images, analytics, performance and a11y pass |

## 13. Open questions

1. Do we want a recurring cast (e.g., a raccoon union rep who shows up across stories) to reward regular readers?
2. Should Catagories allow user-submitted puzzles later (moderation cost)?
3. Illustration pipeline: commission an illustrator, or a consistent in-house vector style?
4. Domain: `thenewporker.com` availability, and whether the name itself needs a trademark review.
