---
name: my-style
description: "Write and rewrite prose in Nelson Amaya's voice, as exemplified by R4DEV (https://r4dev.netlify.app/): humor, anecdotes, interesting examples, famous quotes, and short, precise sentences. Invoked bare, it assesses the audience-facing prose across the whole training package against the style and adjusts whatever misses it; given a file path or pasted text, it works on that instead. --audit reports deviations without rewriting. Use it for new writing too — any page, deck, or doc meant to be read by participants should sound like this."
compatibility: any-agent
user-invocable: true
argument-hint: "[file-path | pasted text] [--audit]"
metadata:
  version: 1.1.0
  source: https://r4dev.netlify.app/
---

# My style

Nelson's writing voice, extracted from R4DEV — the R workshop he built at the OECD that grew from a team training into 80+ participants by word of mouth.
The goal of this skill is that anything written for this training package sounds like it was written by the same person who wrote R4DEV. Because it was.

## The voice, in one paragraph

Serious content, unserious delivery. The reader is a smart colleague, not a student. Sentences are short and land hard. Sections open with a hook — a famous quote, a surprising fact, a shared frustration — and get to the point before the reader can check their email. Humor is dry and self-deprecating, never at the reader's expense. Every abstraction gets a concrete example within two sentences. And the writer is visibly present: opinions, asides, confessions of past mistakes.

## The five devices

Real examples from R4DEV mark what each device looks like when it works.

### 1. The hook

Open on the sharpest thing you have. R4DEV opens its whole site with:

> "More fiction is written in Excel than in Word."

Not "This workshop covers data analysis in R." The hook does the persuading; the explanation can wait a paragraph. A hook can be a famous quote, a
statistic, a confession, or a frustration the reader recognizes. 

### 2. The famous quote

R4DEV opens sessions with attributed quotes:

> "Truth is much too complicated to allow anything but approximations."
> — John von Neumann

Rules:
- **Reuse the R4DEV quote bank first.** Nelson already curated quotes he
  likes; reach for these before anything else, and never pad with boilerplate
  motivational quotes (Eisenhower-on-planning, Lincoln-on-axes, anything from
  a LinkedIn carousel). The bank, harvested from the live R4DEV pages:
  - "Truth is much too complicated to allow anything but approximations."
    — John von Neumann *(plots session — fits: synthesis, summaries, models)*
  - "For every complex problem there is an answer that is clear, simple, and
    wrong." — H.L. Mencken *(text session — fits: review gates, first drafts,
    too-easy answers)*
  - "The greatest value of a picture is when it forces us to notice what we
    never expected to see." — John Tukey *(animation session — fits: slides,
    charts, visual output)*
  - "While correlation does not imply causation, causation does imply
    correlation." — Daniel Kahneman *(animation session — fits: evidence,
    data caution)*
  - "If it doesn't exist on the internet, it doesn't exist." — Kenneth
    Goldsmith *(scraping session — fits: publishing, the website itself)*
  - "The internet broke the private-public wall; impulsive and inelegant
    utterances that used to be kept private are now available for literal
    interpretation." — N.N. Taleb *(Shiny session — fits: publishing, care
    with outputs)*
  - "If you don't practice, you won't learn anything." — epigraph of R4DEV's
    practice page *(fits: hands-on sessions, "your turn" moments)*
  - "You like DAGs?" — Mickey, *Snatch* (2000) *(fits: pipelines, dependency
    graphs — the joke only lands with a diagram nearby)*
- **Real quotes only, correctly attributed.** If a new quote is needed beyond
  the bank and its attribution is disputed (Einstein, Lincoln, and Twain
  attract fake quotes like porch lights attract moths), either verify it or
  say "attributed to." Never invent a quote.
- The quote must earn its slot: it should say the section's thesis better
  than you could. A decorative quote is filler.
- One per section at most. Usually one per piece.

### 3. The anecdote and the shared frustration

R4DEV motivates concepts with lived experience:

> "Do you remember endlessly Googling `reshape` in Stata? No more."

> "wait, that looks familiar but, of course, I didn't use it for a while and
> now I can't remember anything!"

Rules:
- **Never invent an anecdote about Nelson.** Use real ones (the OECD/R4DEV
  origin story, frustrations any office worker recognizes) or leave a
  `<!-- TODO: personal anecdote here? -->` comment for him to fill in.
- A "shared frustration" — a pain the reader has personally felt — works as
  well as a personal story and needs no biography. The Tuesday chat that no
  longer remembers Monday. The 40-page proposal due as a 10-slide deck today.
- Personal asides are welcome and can be blunt: "Why? I love Radiohead."

### 4. The interesting example

Every abstraction gets a concrete case fast, and the case is specific enough
to picture: not "a document" but "a 3,200-word proposal called Youth Literacy
Accelerator." Not "iterate on the output" but "'Drop the agenda, and make the
budget a chart.'" Numbers beat adjectives. Named things beat categories.

### 5. The short, precise sentence

The signature rhythm: a normal sentence or two, then a short one that lands.

> "It always starts basic, inadequate, ugly even."

> "Learn to love the pipe."

> "No more."

Rules:
- Precision first. A short sentence that's vague is just short.
- The fragment is a punctuation mark — one per passage, not a drumbeat.
  (Constant one-liners are an AI tell; see the humanizer skill.)
- Aphorisms are allowed when true and earned: "Creating Data and Modifying
  Data are totally different processes." One per piece, maximum.

## Secondary fingerprints

- **Emoji in section headers, sparingly.** R4DEV uses "💡 What is R4DEV?" and
  "🦾 What you can expect". One emoji, header-level only, never in body prose,
  never in bullets. Skip them entirely in slide decks — the deck design
  carries the visual load there.
- **Pop-culture titles when they fit.** R4DEV names a plotting session
  "Everything in its right place" (Radiohead) and a scraping session "Just
  take it." A title can be playful if the subtitle immediately says what the
  thing actually is.
- **Self-deprecation over authority.** "Wait, what did I get myself into?" is
  the about-page title. Confess what went wrong before explaining what works.
- **Direct address.** "You," constantly. The reader is in the room.

## What this style is not

- Not comedy. One wry line per section is plenty; two is pushing it; a joke
  that needs a setup is cut. If the joke and the point compete, the point wins.
- Not slang or exclamation marks. The humor is dry. Almost never "!".
- Not less precise. Technical terms stay correct; commands, filenames, and
  numbers stay exact. The style dresses the facts, it never replaces them.
- Not fabricated. No invented quotes, no invented anecdotes, no invented
  numbers. This voice trades on trust.

## Works with the humanizer

The humanizer skill removes AI tells; this skill adds a specific human's
voice. They agree on the fundamentals — short sentences, specificity,
concrete examples, no filler — so a passage in my-style should already pass a
humanizer audit. Two cautions where the devices could tip into tells:
rhetorical questions (use only when you answer with something worth the
setup) and dramatic fragments (one per passage). When editing, apply this
skill first, then a quick humanizer pass on anything newly written.

## Modes

### Adjust (default)

Run bare as `/my-style`, the skill sweeps the entire project (scope below):
it reads every in-scope file, assesses each against the five devices and the
secondary fingerprints, and rewrites in place whatever misses the voice.
Files that already match are left alone — don't manufacture changes. At the
end, report one line per file: *already in voice*, or *adjusted* plus a
few words on what changed (e.g. "added hook, tightened three sentences").
Close with the most common deviation found across files — a pattern repeated
project-wide is worth more than any single fix.

Given a file path or pasted text, do the same assess-then-adjust on that
input only.

### Audit (`--audit`)

Triggered by `--audit`, "audit", or any request to review rather than
rewrite. Same assessment, no writes: report where each file deviates from
the voice and what the fix would be, quoting the current phrasing and the
proposed one. Useful before a big sweep, or on files someone else drafted.

## Project scope (this project)

Invoked bare — `/my-style` with no file path and no pasted text — the input
is the audience-facing prose of this repository:

- The rendered website pages under `website/`: `index.qmd`, `about.qmd`, `tips.qmd`,
  `thesaurus.qmd`, the collection pages
- The decks under `website/`: `motivation.qmd`, `session-N-*.qmd`
- `README.md`, if participant-facing

Out of scope — leave untouched:
- `website/_website/` (generated build output), `website/_quarto.yml`, `website/_brand.yml`, CSS/JS
- `CLAUDE.md` persona files and skill recipes — these are instructions to
  Claude, not prose for humans; clarity beats voice there
- Code blocks, commands, filenames, YAML frontmatter, and layout divs
  *inside* an in-scope file — restyle the prose between them, never the
  scaffolding
- Slide decks' `.notes` blocks may keep a plainer register — they're trainer
  cues, not audience prose — but a well-placed line of voice is fine

## Process

1. **Detect mode and scope.** `--audit` or "review" → audit; otherwise adjust.
   File path or pasted text → work on that. Bare → the whole project scope
   above; this is not a prompt to ask which file the user meant.
2. **Read the whole input first.** Know what each section's thesis is before
   decorating it — the devices attach to points, not paragraphs.
3. **Restyle prose only.** In `.qmd` files, edit sentence content inside the
   existing structure; don't move divs, classes, or slide boundaries unless a
   new element (e.g. a quote slide) reuses existing classes.
4. **Budget the devices.** Per page or deck: one hook, at most one famous
   quote, one aphorism, a handful of landed short sentences. Examples and
   direct address are unlimited.
5. **Verify every quote and fact you add.** Disputed attribution → "attributed
   to" or cut. No anecdote invention — TODO comment instead.
6. **Self-check.** Read the result aloud (mentally). Does it sound like one
   person? Did any joke displace a fact? Would the humanizer flag anything
   new? Fix, then ship.
