# The New Porker — Design Spec

Companion to [`PRD.md`](./PRD.md). A clickable mockup of the home page and two games lives at [`design/mockup.html`](../design/mockup.html).

> **v0.3 note:** the site is now real news only (see PRD v0.3). Every story uses the house illustration style (§8) and headline type (Gloock); the real-news signals are the REPORTED stamp, the Plex Mono source line (outlet · date), the Porker Take block, and the "Read it at [outlet] ↗" link. The green `--wire` surface is now used only in Real or Porker? to reveal a real headline.

## 1. Design principles

1. **Dress like a serious magazine, act like a barnyard.** The layout, typography, and spacing are restrained and literary. The jokes live in the words and the illustrations, never in the chrome.
2. **Echo the genre, not the brand.** Readers should recognize the *type* of magazine being parodied (centered masthead, rubrics, generous serif, cartoons), but no element is copied from *The New Yorker*'s trade dress.
3. **One loud color.** Pig pink is the only accent. Everything else is ink on paper.
4. **Games feel like toys.** Tactile tiles, satisfying presses, small in-voice messages.
5. **Real looks different from fake, at a glance.** Wire items (real news) use a different surface, stamp, and type treatment from satire, so the distinction survives a screenshot.

## 2. Brand

### Name and masthead
- Wordmark: **THE NEW PORKER**, set in Gloock, tracked slightly, with a small pink snout ◦◦ glyph standing in for nothing in particular. It is not set in any imitation of the Irvin face.
- Tagline under the masthead (rotates): *"All the news that's fit to snout." · "Est. whenever the pigs got literate." · "Reporting from the trough since 1925½."*

### Mascot: Eustace Swilley
An original pig in a top hat and monocle, inspecting a truffle as if it were a fine butterfly. Used on the About page, the games hub, puzzle win screens, and the favicon (head only).

### Voice
- Solemn, precise, slightly weary. Never winks.
- Datelines and sourcing jokes: "*a source close to the hedgehog*," "*the goose did not respond to requests for comment, but honked*."
- Fact-checker notes and corrections are a recurring format.
- UI microcopy stays in voice but stays clear: button labels are plain verbs ("Submit", "Shuffle", "Share results"); the joke goes in the toast, not the control.

## 3. Color

| Token | Light | Dark | Use |
|---|---|---|---|
| `--paper` | `#FCFBF8` | `#17141A` | Page background |
| `--ink` | `#1B1816` | `#EDE7E3` | Body text, rules |
| `--ink-soft` | `#6A5E57` | `#A89C96` | Bylines, metadata, captions |
| `--rule` | `#E3DDD6` | `#332D34` | Hairlines, card borders |
| `--snout` | `#D9536F` | `#F08CA2` | Accent: links on hover, rubric labels, games CTAs, masthead glyph |
| `--wire` | `#EEF1EC` | `#1E2320` | Background of Wire (real news) surfaces: a cool, faintly green newsprint that reads as "different paper" next to the warm page |
| `--wire-ink` | `#2F5D47` | `#8CC4A6` | REPORTED stamp, source names, outbound-link arrows |
| `--snout-wash` | `#FBE5EA` | `#3A2029` | Accent backgrounds (game strip, paywall) |

**Catagories difficulty bands** (each also carries a text label):

| Band | Light | Dark |
|---|---|---|
| Kibble | `#F2D66B` | `#B89A2E` |
| Tuna | `#9CCB86` | `#5E8C4C` |
| Catnip | `#8DB6E0` | `#4C77A3` |
| Hairball | `#B99AD6` | `#7D5CA0` |

## 4. Typography

| Role | Face | Notes |
|---|---|---|
| Masthead + display headlines | **Gloock** (Google Fonts) | High-contrast serif; headlines 32–56px, `text-wrap: balance` |
| Body copy | **Newsreader** | 18–20px, line-height 1.6, measure ~65ch; drop cap on long-form |
| Rubrics, labels, UI | **Libre Franklin** | Uppercase, 11–12px, letter-spacing 0.12em |
| Game tiles | **Libre Franklin** 700 | Uppercase, tabular numbers for scores |
| Wire headlines + datelines | **IBM Plex Mono** | Wire-copy feel; headline 16–18px, dateline 11px caps. Monospace appears *only* on real-news items, so the face itself signals "reported" |

Scale (px): 12 · 14 · 16 · 19 · 24 · 32 · 44 · 60.

## 5. Layout

- **Grid:** 12 columns, max width 1200px, 24px gutters; 16px side padding on mobile.
- **Home:** centered masthead → hairline nav → lead story (illustration left 7 cols, headline right 5 cols) → three-column story grid → **It Actually Happened** Wire band (horizontal scroll of real items on mobile, 3-up grid on desktop) → pink **Games strip** → cartoon of the day → "Talk of the Farm" list → footer with disclaimer.
- **Wire page:** single column at 720px, filter chips for species at the top, then Wire cards in date order with a date divider per day.
- **Story page:** single column at 65ch, rubric above headline, dek in italic, byline in small caps, full-bleed illustration, drop cap, fact-checker note in a boxed aside at the end, "More from the raccoon desk" related stories.
- **Games:** single centered column, max 520px, header with game name + date + streak, board, controls row, results sheet.

## 6. Components

| Component | Spec |
|---|---|
| **Rubric** | Libre Franklin caps in `--snout`, e.g. `THE BURROW-WITZ REPORT` |
| **Story card** | Illustration (3:2), rubric, headline (Gloock 24px), dek (Newsreader italic 16px), byline. No box, no shadow; separated by whitespace and a hairline rule |
| **Satire stamp** | Small outlined `SATIRE` tag used on OG images and story headers |
| **Games strip** | `--snout-wash` band with one card per game: icon, name, one-line pitch, today's status pill |
| **Game tile** | 1:1, 2px ink border, radius 6px, pressed state inverts to ink bg / paper text, 90ms press scale 0.96 |
| **Toast** | Ink pill centered above board, 1.6s, e.g. "Not in the trough." |
| **Paywall modal** | Pink wash sheet from bottom: "You've read 3 of 3 free kibbles this month." Buttons: "Subscribe for $0 and a belly rub" / "Keep reading anyway" |
| **Wire card** | `--wire` fill, 1px `--rule` border, square corners. Top row: REPORTED stamp + source name + date (Plex Mono caps, `--wire-ink`). Headline in Plex Mono 17px. Summary in Newsreader 16px. Divider, then **Porker Take** label (Libre Franklin caps, `--snout`) with the one-liner in Newsreader italic. Footer link: "Read it at UPI ↗" |
| **REPORTED stamp** | Outlined rectangle, Plex Mono 10px caps, `--wire-ink`, 1.5px border, slight −2° rotation like a rubber stamp |
| **SATIRE stamp** | Same geometry in `--snout` with Libre Franklin; never rotated, so the two stamps differ in shape, color, face, and angle |
| **Footer** | Sections list, newsletter mini form, disclaimer paragraph in `--ink-soft` |

## 7. Game screens

### Snuffalo
- Seven hexagonal-ish **truffle tiles** in a flower pattern; the center Truffle letter is filled `--snout`.
- Above: current word input with blinking caret. Below: **Delete · Shuffle (snout icon) · Enter**.
- Rank progress bar with seven dots labelled on tap (*Piglet … Hog Wild*); Eustace's head moves along it.
- Found-words list collapses into a single line on mobile ("You have found 12 words ▾").

### Catagories
- 4×4 tile grid; selected tiles invert.
- Mistakes row: four paw prints; a wrong guess animates one paw swatting away.
- Solved groups collapse to a full-width band in the difficulty color with the group name and its four words.
- Loss: the grid tilts 8° and slides off to the right ("The cat has knocked your puzzle off the table."), then all groups reveal.

### Real or Porker?
- One headline card at a time, centered, in a neutral card that hides whether it is Wire or satire (Newsreader headline, no stamp, no source).
- Two large buttons below: **Real** (`--wire-ink` outline) and **Porker** (`--snout` outline). Keyboard: R / P.
- On answer, the card flips to its true treatment: it becomes a Wire card with the source link, or a satire card with the SATIRE stamp. A ✓ or ✗ and a one-line reaction ("It happened. We're as upset as you are.").
- Progress: eight small squares at the top filling ✓/✗.

## 8. Illustration direction

- Flat vector, two ink weights, limited palette (ink + one tint per piece), lots of paper showing. Animals drawn with human dignity: posture, props, and expression do the comedy.
- Cartoons: single panel, ink line only, caption in Newsreader italic below.
- Credits under every illustration in the fictional staff's names.
- Real stories never use source photos. Each story gets its own illustration in this style, drawn from what the report says happened (an emu passing an apartment block, a python threaded through a car grille, a raccoon's head up through a sewer grate). The drawing shows the animal, never identifiable people. In Brief items are text-only.

## 9. Motion

- Only in games and the paywall. Articles do not animate.
- Durations 90–240ms, ease-out. All motion respects `prefers-reduced-motion` (falls back to instant state changes).

## 10. Accessibility

- Contrast: all text ≥ 4.5:1 on its background in both themes (pink accent is used for text only at ≥ 14px bold or on large rubrics; links are underlined).
- Game tiles are `<button>`s with `aria-pressed`; results announced via an `aria-live="polite"` region.
- Catagories never relies on color alone: each band shows its difficulty name.
- Visible focus ring: 2px `--snout` outline with 2px offset.
