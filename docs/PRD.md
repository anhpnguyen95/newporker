# The New Porker — Product Requirements Document

**Status:** Draft v0.3 · **Date:** 2026-09-26 · **Owner:** anhpnguyen95

> *The New Porker* is a satirical magazine website about animals doing wild things, written in the voice of a very serious literary weekly. It pairs invented stories with **real news of animals behaving ridiculously**, pulled automatically from news feeds and clearly labeled as real. It also has a daily games section that parodies prestige-magazine puzzles.

**Changes in v0.3:** the site is now **real news only**. Every story is a real, reported animal oddity from The Wire, shown with our own illustration in the house style, our own summary, a REPORTED stamp, a link to the source, and a one-line Porker Take. Invented stories are gone. Satire survives only in the Porker Takes, cartoons, captions, and the decoy headlines in Real or Porker?. Where older sections below describe invented stories (§6.1–6.3), they are superseded by §6.5.

**Changes in v0.2:** added The Wire, a real-news feed of animal oddities (§6.4, §10.1); a new game, Real or Porker? (§7.6); guardrails for mixing real and satirical content (§4.7–4.11).

---

## 1. Summary

The New Porker is a parody news and culture site. Every story is fake, every subject is an animal, and every sentence is written with a straight face. It borrows the *conventions* of a highbrow weekly (long-form features, section rubrics, cartoons, a pompous masthead mascot, a daily puzzle habit) and applies them to raccoons unionizing, geese filing noise complaints, and an octopus who got into Yale.

The second pillar is **The Wire**: real, reported stories of animals doing absurd things (an emu leading police on a two-hour chase, a ball python found in a car grille). The site ingests these from news feeds several times a day, shows the real headline with a link to the original reporter, and adds a one-line, clearly labeled *Porker Take*. Real stories keep the site fresh without a newsroom, and they make the satire land harder: readers can't always tell which is which, which is the joke.

The third pillar is **Games**: small, daily, shareable puzzles that parody magazine word games (Shuffalo → **Snuffalo**, Categories → **Catagories**, and others). Games are the retention engine; stories and The Wire are the discovery engine.

## 2. Goals and non-goals

### Goals
1. **Make people laugh, then make them come back.** A reader who lands from a shared headline should find a daily game and return tomorrow.
2. **Nail the voice.** The comedy is in the gap between a solemn register and an absurd subject. Copy quality is the product.
3. **Ship a fast, cheap, static site** that one person can run. No servers required for v1.
4. **Make games shareable** with spoiler-free result cards (emoji grids, like the genre expects).
5. **Stay fresh daily with no newsroom.** At least 3 new real animal stories on The Wire every day, found automatically and approved by an editor in under 5 minutes a day.
6. **Never blur real and fake.** Any reader, on any page or share card, can tell in one glance whether a story is reported or satire.

### Non-goals (v1)
- User accounts, comments, or real subscriptions.
- Real news *about anything but animal oddities*. The Wire is narrow on purpose.
- Republishing full articles or photos from other outlets. We link out.
- No real people as subjects of fabricated claims (see §4).
- Native apps.
- Ads. (A fake paywall joke is in scope; a real paywall is not.)

## 3. Audience

| Persona | Who | What they want |
|---|---|---|
| **The Sharer** | Scrolls social, sends links to group chats | One perfect headline and an image to screenshot |
| **The Daily Puzzler** | Already plays Wordle/Connections-style games | A 3–5 minute ritual, a streak, a result to post |
| **The Oddity Hound** | Already follows UPI Odd News, r/nottheonion, local-news animal stories | A daily roundup of the best real animal chaos, with credit to the source |
| **The Literary Lurker** | Actually reads *The New Yorker* | Pitch-perfect genre parody and deep-cut jokes (fact-checker notes, cartoon captions, "Goings On" listings) |

## 4. Parody and legal guardrails

These are requirements, not suggestions.

1. **Distinct identity.** Name is *The New Porker*. We do **not** use *The New Yorker*'s logo, the Irvin typeface, their Eustace Tilley artwork, their cover layouts, or their trade dress. Our mascot is an original character, **Eustace Swilley** (a pig with a monocle, examining a butterfly-shaped truffle).
2. **Visible disclaimer** in the footer of every page and on the About page. v0.3 text: *"Every story on The New Porker really happened and was reported by the news outlet we link to. The summaries are written by us; the Porker Takes, cartoons, and captions are jokes; and Real or Porker? mixes in made-up headlines, which it always reveals. The New Porker is a parody and is not affiliated with The New Yorker or Condé Nast."* (v0.2 text, kept for reference: *"The New Porker is a work of satire. It is not affiliated with, endorsed by, or connected to The New Yorker or Condé Nast. All stories are fiction except items in The Wire, which are real news reported by the outlets we link to. All other animals are fictional, except the ones who are just very good."*
3. **Game names are puns, not copies.** Mechanics are generic (word-finding, grouping, crosswords) and all puzzle content is original.
4. **No real humans as subjects of fake news.** Stories are about animals. Human public figures may not be quoted or depicted doing things they did not do.
5. **No real brands defamed.** Fictional companies only ("Chewy's rival, Gnawy").
6. `<meta>` tags and Open Graph cards carry the "Satire" label so shared links are not mistaken for news.

**Real news (The Wire)**

7. **Label every item by kind.** Real items carry a **REPORTED** stamp, the source outlet's name, the original publication date, and a prominent link to the original. Satire carries **SATIRE**. The two stamps look different (see DESIGN §6) and are never omitted, including on share cards and in RSS.
8. **Headline + link + our own summary only.** We show the source's headline (normalized: prefixes like "Watch:" removed), a 1–2 sentence summary written by us or generated and then edited, and a link. No copied article text beyond the headline, no hotlinked or copied photos or video. Wire items use our own spot illustrations or a species icon.
9. **The Porker Take targets the animal, not people.** The one-line joke under a real story may put words in the animal's mouth. It may not invent quotes from, or mock, the real humans in the story (owners, officers, bystanders), and never names private individuals even if the source did.
10. **No harm, no joke.** Stories involving death or serious injury to people or animals, animal cruelty, disasters, or attacks are excluded automatically and on review. The test: would the people involved laugh too?
11. **Corrections flow through.** If the source corrects or retracts a story, we update or pull the item. Each item stores its source URL and is re-checked for 7 days after publishing.

## 5. Information architecture

```
/                       Home (the "issue")
/news/                  All stories (real, reported), newest first. In v0.3 this and /wire/ are the same feed
/wire/                  The Wire — real animal oddities from the news, newest first
/wire/<slug>/           Wire item page (headline, summary, source link, Porker Take)
/news/<slug>/           Story page
/section/<section>/     Section index (see §6)
/games/                 Games hub
/games/snuffalo/        Daily word game
/games/catagories/      Daily grouping game
/games/name-droppings/  Daily guess-the-animal game
/games/crossbeak/       Daily mini crossword
/games/caption-contest/ Weekly cartoon caption contest (read-only in v1)
/games/real-or-porker/  Daily: guess which headlines really happened
/cartoons/              Cartoon archive
/magazine/<issue-date>/ Weekly "issue" table of contents with a cover
/newsletter/            The Daily Trough (sign-up form, stubbed in v1)
/about/                 About + satire disclaimer
```

Primary nav (v0.3): **Latest · Fugitives · Stowaways · Stuck · Encounters · Cartoons · Games**. Utility nav: *Newsletter*, *Subscribe* (joke).

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

### 6.5 Real-news sections (v0.3, supersedes §6.1–6.3)

Stories are filed by what the animal did, not by magazine department:

| Section | What goes there | Example |
|---|---|---|
| **Fugitives** | Escapes, chases, animals at large | Emu leads police on two-hour chase (Moriyama, Japan) |
| **Stowaways** | Animals found riding in cars, planes, luggage | Kitten rides ~76 miles in an engine bay (Texas) |
| **Stuck** | Grates, grilles, fences, chimneys | Raccoon rescued from a highway sewer grate (Ontario) |
| **Crowd Control** | Animals at games, stores, schools, events | "Overwhelmed" squirrel in the stands at Ohio State |
| **Encounters** | Close calls with wildlife | Moose turned back with bear spray (Montana) |
| **Pageantry** | Contests, records, births, ceremonies | Fat Bear Week voting; "Lucky Seven" penguin chicks |

Each story page: illustration commissioned in the house style (flat line drawing on pink wash, see DESIGN §8), our headline in title case taken from the source headline, REPORTED stamp with outlet and date, our 2–4 sentence summary, the Porker Take, and a prominent "Read it at [outlet] ↗" link. The home page shows one lead story, a grid of six, and an "In Brief" list of text-only items.

**Launch content (replaces §6.3):** 30 real stories with illustrations, backfilled from the previous 60 days of feeds; 12 cartoons; 30 days of puzzles per game.

### 6.4 The Wire (real news)

A reverse-chronological feed of real, reported stories about animals doing ridiculous things. On the home page it appears as a narrow column titled **It Actually Happened**, next to the satire.

**Wire item schema** (`src/content/wire/<date>-<slug>.json`, written by the ingestion job in §10.1):

```json
{
  "id": "upi-2026-09-24-japan-escaped-emu",
  "status": "published",               // candidate | approved | published | rejected | withdrawn
  "headline": "Emu escapes from Japanese zoo, leads police on 2-hour chase",
  "source": { "name": "UPI", "url": "https://www.upi.com/Odd_News/2026/09/24/japan-escaped-emu-zoo-Moriyama/2161790267116/" },
  "published_at": "2026-09-24",
  "ingested_at": "2026-09-24T14:05:00Z",
  "species": ["emu"],
  "location": "Moriyama, Shiga, Japan",
  "summary": "An emu slipped out of a mobile zoo through a door that was usually closed and ran through a residential neighborhood for about two hours before staff caught it at an apartment complex. No one was hurt.",
  "porker_take": "The emu maintains he was not escaping. He was \"seeing Moriyama.\"",
  "scores": { "animal": 0.99, "absurdity": 0.91, "harm": 0.02 },
  "reviewed_by": "editor",
  "related_satire": ["emu-files-for-asylum-in-neighboring-prefecture"]
}
```

**Editorial workflow**
1. The ingestion job creates `candidate` items with a draft summary and three draft Porker Takes.
2. An editor opens the review queue (a pull request in v1, see §10.1), picks or rewrites a take, and approves or rejects each item.
3. Approved items publish on the next deploy. Target: ≤ 5 minutes of editor time per day.
4. Good Wire items become prompts for longer satire ("Annals of Instinct: The Emu Who Saw Moriyama"), which links back to the real item.

**Launch set (real items found on 2026-09-26, all UPI Odd News):** emu escape in Moriyama, Japan (Sept. 24); ball python in a car grille in Franklin Township, N.J. (Sept. 22); venomous yellow-bellied sea snake at Crystal Cove, Calif. (Sept. 17); "overwhelmed" squirrel rescued from the stands at an Ohio State game (Sept. 11); one of two loose pigs caught in Detroit (Sept. 3); kitten rides nearly 80 miles in a Texas engine bay (Sept. 3); Montana woman uses bear spray on a charging moose (Sept. 2).

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

### 7.6 Real or Porker?
**Premise:** Eight headlines a day. Some happened. Some we made up. Swipe or tap **Real** or **Porker**.

- Each day mixes 4–5 real headlines from The Wire with 3–4 satirical headlines, in random order. Satire is written to be plausible; real items are picked for maximum implausibility.
- After each answer, reveal the truth. Real items show the source and a link; satire items link to our story.
- Score out of 8 with a ranked result: *Gullible Gosling → Skeptical Stoat → Fact-Checking Fox*.
- Share card: `Real or Porker? 9/26 · 6/8 🦊 · ✅✅❌✅✅✅❌✅`
- Real items must have been published on The Wire for at least 24 hours (so the reveal link is stable) and no more than 60 days.

**Acceptance criteria**
- The same daily set for every player, built at deploy time from approved Wire items and a pool of satire headlines.
- A real headline is never altered to make it more or less believable, beyond the normalization in §4.8.

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
| F13 | Scheduled ingestion job pulls candidate animal oddity stories from configured feeds, dedupes, scores, and drafts summaries and takes | P0 |
| F14 | Editor review queue: approve, reject, edit summary, choose take | P0 |
| F15 | Wire section and home-page "It Actually Happened" column with REPORTED stamp, source, date, outbound link | P0 |
| F16 | Real or Porker? daily game | P1 |
| F17 | Source re-check: for 7 days after publish, detect 404s and corrections and flag the item | P1 |
| F18 | Wire items filterable by species and location | P2 |

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

### 10.1 Wire ingestion pipeline

```
 feeds ──▶ fetch ──▶ normalize ──▶ filter ──▶ dedupe ──▶ score & draft ──▶ review PR ──▶ publish
 (cron)             (headline,     (animal?    (URL +      (LLM: animal,     (editor      (merge →
                     date, url)     harm?)      fuzzy        absurdity,        approves)    rebuild)
                                                title)       harm, summary,
                                                             3 takes)
```

- **Runner:** GitHub Actions on a cron (every 4 hours, 06:00–22:00 ET). It commits candidates to a branch and opens or updates a single "Wire review" pull request. Merging the PR publishes. No database, no server.
- **Sources (initial, all via RSS/Atom or public search feeds):**
  - UPI Odd News RSS (best single source; most launch items came from here)
  - Google News RSS search queries, e.g. `"escaped" (emu OR llama OR goat OR pig)`, `"animal control" "stuck in"`, `police "on the loose" animal`
  - AP and Reuters oddities sections, where RSS is available
  - Local TV station feeds that regularly carry animal stories (added by editors over time)
  - Candidate: Reddit r/nottheonion and r/NewsOfTheWeird, used only to discover links. We credit and link the underlying news outlet, never the Reddit post.
  - Each source is a row in `wire.sources.yaml` with name, feed URL, polling interval, and trust level. Honor each site's terms and robots.txt; fetch only feeds, never scrape article bodies.
- **Filter:** a species list (~1,500 common and slang animal names) plus exclusion keywords (killed, died, mauled, fatal, cruelty, euthanized, attack victim). Items that pass go to scoring.
- **Dedupe:** canonical URL, then fuzzy headline match (token-set similarity ≥ 0.8) within 14 days. Keep the earliest reputable source and store the others as `also_reported_by`.
- **Score and draft:** one LLM call per candidate (a small, fast Claude model is enough) returns JSON: `animal` (0–1), `absurdity` (0–1), `harm` (0–1), species, location, a 1–2 sentence summary written from the feed item's headline and description only, and three Porker Takes that follow §4.9. Drop anything with `harm` > 0.2 or `animal` < 0.7. Sort the review PR by absurdity.
- **Re-check:** a daily job requests each item's source URL for 7 days after publishing and flags 404s or changed headlines for the editor.
- **Cost guardrail:** cap LLM calls per run (default 60) and log token usage per run.

## 11. Success metrics (first 90 days)

| Metric | Target |
|---|---|
| Share-button clicks per game completion | ≥ 25% |
| D7 return rate among players | ≥ 20% |
| Median games played per returning visitor per day | ≥ 1.5 |
| Story → game click-through from home | ≥ 10% |
| Wire items published per day | ≥ 3 |
| Editor time per day on the Wire queue | ≤ 5 min |
| Wire outbound clicks per item view | ≥ 15% (we send traffic to the reporters) |
| Real or Porker? completion rate | ≥ 70% of starts |
| Reports of "I thought this was real" about a satire piece | Low, and funny when it happens |
| Reports of "I thought this was fake" about a Wire item | Expected. That's the game |

## 12. Milestones

| Milestone | Scope |
|---|---|
| **M0 — Design** | This PRD, design spec (`docs/DESIGN.md`), clickable mockup (`design/mockup.html`) |
| **M1 — Skeleton** | Astro project, layout, nav, footer disclaimer, story template, 6 stories |
| **M2 — Games I** | Games hub, Snuffalo, Catagories, share cards, streaks |
| **M3 — Content** | 24 stories, 12 cartoons, first magazine issue, 30 days of puzzles |
| **M3.5 — The Wire** | Ingestion job, sources file, review PR flow, Wire section and home column, 2 weeks of backfill |
| **M4 — Games II** | Real or Porker?, Name Droppings, Crossbeak, fake paywall |
| **M5 — Launch** | OG images, analytics, performance and a11y pass |

## 13. Open questions

1. Do we want a recurring cast (e.g., a raccoon union rep who shows up across stories) to reward regular readers?
2. Should Catagories allow user-submitted puzzles later (moderation cost)?
3. Illustration pipeline: commission an illustrator, or a consistent in-house vector style?
4. Domain: `thenewporker.com` availability, and whether the name itself needs a trademark review.
5. Should the Wire auto-publish items above a very high confidence score, or always wait for an editor? (v1 recommendation: always wait.)
6. Do we want to ask source outlets (e.g., UPI) for permission or a partnership, given we drive traffic to them?
7. Should readers be able to submit tips ("my neighbor's goat is on the roof again")? This needs verification rules before it's safe.
