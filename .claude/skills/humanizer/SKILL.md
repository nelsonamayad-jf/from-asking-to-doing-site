---
name: humanizer
version: 6.1.0
description: "Remove the patterns that mark writing as AI-generated: structural, sentence-level, tonal, lexical, and formatting tells, each with a fix. Invoked bare in this project, it reviews and rewrites the prose across the whole training package (decks, CLAUDE.md files, README, skill recipes) rather than a single file — see Project scope below. Given a file path or pasted text instead, it works on that. Default mode rewrites the text; --audit produces a non-destructive diff."
compatibility: any-agent
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - Bash
source: https://github.com/chi-feng/humanizer/blob/main/SKILL.md
---

# Humanizer

Find the patterns that mark writing as machine-generated and replace each with what a careful writer would do instead. This file is also an example: it is written the way it tells you to write, because anything loaded into context becomes a template the model imitates. Keep it that way when you edit it.

## Project scope (this project)

Invoked bare — `/humanizer` with no file path and no pasted text — the input is every prose file in this repository, not a single document. Default mode is still rewrite, applied one file at a time; audit mode (below) works the same way across the whole set instead of one diff.

In scope:
- Every `.qmd` file — deck content, wrapper pages, `index.qmd`, `about.qmd`, `thesaurus.qmd`, `tips.qmd`, the Skills/Agents collection pages
- Every `CLAUDE.md` / `CLAUDE_*.md` persona and instruction file, root and per-demo
- `README.md`
- Every skill recipe under `*/skills/*.md`, including `SKILL.md` files

Out of scope — leave untouched:
- `website/_website/` (generated build output — never hand-edited, per the root `CLAUDE.md`)
- `website/_quarto.yml`, `website/_brand.yml`, and other config/YAML (not prose)
- CSS, JS, and other non-prose source
- `output/`, `sample-input/`, `sample-inputs/` (generated or sample data, not authored prose)
- Binary files (`.pptx`, `.docx`, `.png`, `.pdf`, `.gif`, etc.)
- Code blocks, commands, filenames, and YAML frontmatter *inside* an in-scope file — humanize the surrounding prose, never the literal syntax quoted in it

For a whole-project run: read every in-scope file in full first, to form one working sense of the project's voice, before rewriting anything — the voice check in [Match the source's voice](#match-the-sources-voice) applies once, to the project, not per file. Then rewrite file by file. Report one line per file (changed, or already clean), and close with whichever tells recurred most often across files — a tic repeated project-wide is a more useful finding than any single sentence.

## Principles

1. **Specificity over significance.** "Conversion dropped 12%" beats "this represents a meaningful shift." State the fact; if it warrants weight, the reader will feel it.
2. **Trust the reader.** If an inference is obvious, don't announce it. Don't tell the reader a sentence is honest, important, or surprising; make it so and let them notice.
3. **Frequency on two axes.** Inside one piece, a device is usually fine once, and the signal is rate, so look for clusters. But a model is memoryless across generations, so a device it reaches for in every response is a reliable tic even at once per piece. You can't see your own cross-response rate while writing, so don't excuse a known reflex just because it appears only once here.
4. **Don't homogenize.** A correct rewrite that erases the author's voice still fails. The target is the source on a good day, not a blander writer (see [Match the source's voice](#match-the-sources-voice)).
5. **Don't overcorrect.** Removing slop is not removing style. Strip every list, short sentence, em dash, and domain term and you get a different failure: choppy, hedged, generic mush. Keep real lists, correct technical terms, and varied sentence length. Fix the reflex, not the existence of a device.
6. **Show the receipts.** In audit mode, name what changed and why. If the writer can't see the pattern, they'll repeat it.

## Modes

### Rewrite (default)
Output the humanized text. If a file path was given, ask before overwriting; default to writing `<path>.humanized`. For a whole-project run (see Project scope above), write each in-scope file in place instead — Claude Code's own edit-permission prompts are the confirmation gate at that scale.

### Audit (`--audit`)
Triggered by `--audit`, "audit", "show the diff", or any request to review rather than rewrite in place.

1. Read the original fully.
2. Produce the rewrite.
3. For a file: write `<path>.humanized` and run `diff -u <path> <path>.humanized`. For pasted text: emit a fenced `diff` block. For a whole-project run: do this per file, then list every file's diff in one report rather than writing `.humanized` siblings across the repo.
4. Below the diff, list what changed, one line per change, citing the section. For a local fix, give the original phrase and its replacement; for a structural fix, name the passage and what was reorganized.
5. End with "What did not change" if the original was already mostly clean. Don't manufacture changes.

## Match the source's voice

There is no stored profile. Infer the voice from the input and preserve it. Before rewriting, note three things:

- **Sentence-length distribution.** Long compound sentences, short fragments, or a mix? Match it. Don't compress everything to a uniform short default.
- **Register.** Technical, casual, literary, or mixed? Keep it. If the draft is technical and direct, don't return it literary and warm.
- **Idiom.** Keep the author's real terms of art, recurring phrases, and quirks: an `&`, a dash habit, a lowercase opening. Strip the reflexes, not the fingerprints.

If the input is too short to infer a voice, default to plain, specific, declarative prose and leave styling to the author.

## Diagnostics

Each entry says what the pattern is, how to spot it, and the fix. Examples mark the tell (❌) and the repair (✓). Most tells are fine in isolation; the signal is reflexive overuse.

### 1. Structure

**1.1 Throat-clearing openings.** The first sentence states what the piece is about or what it's about to do, instead of doing it. Cut "In today's world", topic definitions, and table-setting.
> ❌ "In today's fast-paced digital landscape, writing has never been more important."
> ✓ Open with the sharpest concrete thing you have.

**1.2 Formulaic openings.** Stock first moves: a dictionary definition, a rhetorical question, "Imagine a world where". They're interchangeable across topics, so they carry no information. Open on the specific.

**1.3 Signposted conclusion.** "In conclusion", "To sum up", "Ultimately", "Taken together". Competent writing doesn't announce its ending; the reader feels it arrive.

**1.4 Symmetrical conclusion.** Ending by restating the opening is a reflex. End on the strongest point, not a mirror of the first line.

**1.5 Fractal recapping.** "In this section we'll cover", "As we've seen", "To recap". Padding inherited from textbooks. Delete it.

**1.6 Outline-wrapper structure.** Default section titles borrowed from academic and business templates: "Challenges and Future Directions", "Key Takeaways", "Overview" as a standalone heading in a short document. Use headings that name the actual content, in sentence case.

**1.7 Rule-of-three saturation.** Forcing ideas into triples because three sounds complete. One triple per paragraph at most, never back to back. If the list has four real items, list four. Watch the degenerate form where the third item just merges the first two ("faster, cheaper, and more efficient"): that's two ideas in three slots, so cut to two.

**1.8 Listicle in prose.** A hidden bulleted list wearing sentences. "The first reason is cost. The second is time. The third is talent."
> ✓ "It costs too much, takes too long, and needs skills most teams lack."

**1.9 Saying the same thing twice.** Three sentences, one idea, each restating the last in new words.
> ❌ "The results were noteworthy. The findings showed clear trends. The data revealed important patterns."
> ✓ "Conversion dropped 12%."

**1.10 Contamination.** Residue that proves the text was never reread. Read the output once before shipping.
- Knowledge-cutoff disclaimers as content: "As of my last update", "While specific details are limited", "X maintains a low profile" as filler for an unknown. (Different from genuinely documenting that a topic is poorly sourced; the fault is inventing the claim.)
- Unfilled placeholders: `[describe the section here]`, `INSERT_SOURCE_URL`, `access-date: 2025-XX-XX`.
- Broken-edit artifacts: a half-merged sentence from an incomplete edit, two phrasings spliced into one that doesn't parse. A sentence that doesn't parse is a hard tell.

### 2. Sentences

**2.1 Negative parallelism.** Defining something by first negating an alternative. The most common single tell. It simulates nuance while staying empty: instead of showing Y, it implies Y by dismissing X.
> ❌ "It's not about working harder, it's about working smarter."
> ✓ "The leverage is in what you cut."

Subtypes: "not X, but Y"; "the question isn't X, it's Y"; "not because X, but because Y"; "no X, no Y, just Z". One per piece is fine. Two is a pattern. Three is a confession. Fix: state Y directly, and keep a contrast only when it's a real distinction, written once as fact rather than as a rhythmic pair.

**2.2 "The real X was" pivot.** Set up a presumed answer, dismiss it, announce the real one. Manufactures depth and implies an insight the writer never demonstrates.
> ❌ "The real shock wasn't the size, but what emerged from it."
> ✓ "Meta-learning emerged at that scale."

**2.3 Tacked-on -ing analysis.** A participial phrase bolted to the end to announce significance: "highlighting its importance", "underscoring the broader shift", "marking a pivotal moment". It adds no content and does the reader's inference for them.
> ❌ "These works are now in the national museum, highlighting their significance."
> ✓ "These works are now in the national museum." (Placement implies the significance.)

**2.4 Rhetorical self-Q&A.** Asking a question nobody posed, then answering it. "The result? A $10B company. The lesson? Never skip fundamentals." State the point.

**2.5 Dramatic countdown.** "Not luck. Not connections. Just relentless execution." Collapse it: "Relentless execution set them apart."

**2.6 False range.** "From X to Y" where X and Y aren't a real spectrum. "From innovation to transformation, AI changes everything." Name the actual things that changed.

**2.7 Adverbs propping weak verbs.** If the adverb is doing the work, the verb is wrong. "Ran very quickly" is "sprinted."

**2.8 Passive voice that hides the agent.** "The decision was made by the committee" is "The committee decided." Use the passive only when the agent is genuinely unknown or irrelevant.

**2.9 Sentence-length monotony or compression.** AI prose drifts toward uniform mid-length sentences with low variance. Long compound sentences are the rhythm of an analytical voice, not a flaw to fix. Read aloud; if it sounds like a metronome, vary length deliberately, short next to long.

**2.10 Forced "X is the Y of Z" analogy.** Defining something by equating it to a famous thing in another domain, when the two share nothing but the template. "This library is the Rosetta Stone of config parsing." Describe what it does. Keep the analogy only when it explains something the literal description can't.

### 3. Tone

**3.1 Dramatic impact openings.** Weather and impact metaphors that tell the reader to be impressed: "landed like a thunderclap", "shattered assumptions", "staggering", "behemoth". Replace vibe with fact.
> ❌ "The result landed like a thunderclap, shattering decades of consensus."
> ✓ "The result contradicted the standard prediction by four orders of magnitude."

**3.2 Manufactured epiphany.** "Something shifted." "Here's the thing." "Let that sink in." "Here's what nobody tells you." Simulated revelation with nothing inside. Replace with the specific insight, or cut.

**3.3 Stakes inflation.** "This will fundamentally reshape the future of human creativity." Say the concrete, smaller, true thing: "This makes some creative work cheaper to do badly and harder to do well."

**3.4 Pedagogical condescension.** "Let's unpack this." "Let's break it down." "Let's dive in." Start the argument.

**3.5 False vulnerability.** Polished, risk-free admission. "I'll admit, I've struggled with this too." Real specificity is uncomfortable: "I spent six months writing essays nobody read because I optimized for length, not argument."

**3.6 Balance-performance.** Positive framing, a gesture at challenges, then optimistic dismissal. "Despite its challenges, this is an enormous opportunity." Engage the challenge specifically and let it stand, or drop the staged balance.

**3.7 False suspense.** Promising a revelation, delivering a normal observation. Cut the "Here's the thing" and state the observation.

**3.8 Futurism invitation.** The pitch-deck opener. "Imagine a world where every writer had an editor 24/7." Nobody imagines on command. State what's true now.

**3.9 Generic analogies.** Plausible metaphors with no lived specifics. "Learning to code is like learning a language: at first nothing makes sense, then it clicks." Replace with the concrete: "I stared at the docs for three weeks before anything clicked."

**3.10 Confident confabulation.** When a draft adds a specific name, date, or figure that wasn't in the source, it's often invented to fit the slot, stated with full confidence. Verify every added specific against the source.

### 4. Lexicon

**4.1 The "genuine / honest / real" intensifier.** *genuinely, honestly, truly, really, actually, genuine, real* used to add weight. The loudest current tell. The word adds emphasis, not information, and usually props a claim that can't stand alone.
> ❌ "This is genuinely one of the most important shifts, and honestly the real bottleneck is measurement."
> ✓ "The bottleneck is measurement."

The conversational cousins are the same tell: "to be honest", "in all honesty", "quite frankly", "let's be clear". Fix: delete it. If the sentence weakens, the claim was weak, so strengthen the claim.

**4.2 Copula avoidance.** Replacing "is"/"are" with "serves as", "stands as", "represents", "boasts", "features", "offers". A repetition-avoidance reflex that adds false weight: "the station serves as a hub" claims a role that "the station is a hub" doesn't. Use "is." Keep the substitute only when the relationship really is functional beyond identity.

**4.3 Promotional vocabulary.** Travel-guide and press-release register in factual prose: nestled, in the heart of, vibrant, boasts, renowned, rich cultural heritage, diverse array, breathtaking, showcasing. Reader trust drops on contact.
> ❌ "Nestled in the breathtaking highlands, the town boasts a vibrant, rich cultural heritage."
> ✓ "The town is in the northern highlands."

**4.4 Vague authority.** Simulated attribution: "experts agree", "studies suggest", "research shows", "critics argue", "many believe". Name the source, cite it, or drop the claim.

**4.5 Significance-inflation phrases.** Kill on sight: "serves as a testament to", "marks a pivotal moment", "represents a significant shift", "underscores the importance of", "in the ever-evolving landscape", "indelible mark", "enduring legacy", "it's worth noting", "it goes without saying".

**4.6 Filler transitions.** Delete the phrase, keep the sentence: "It's worth noting", "Importantly,", "Notably,", "Interestingly,", "Needless to say", "Additionally," at the start of a sentence. Also: "at the end of the day", "when it comes to", "that said".

**4.7 Dev-metaphor reflexes.** Engineering metaphors used figuratively, far past their real rate: load-bearing (when nothing is held up), blast radius (no explosion), smoke test (for a quick check), escape hatch (any fallback), substrate or spine (for foundation), "surface" as a verb, "the shape of" X, "locked" (for decided). Use the plain word. Keep the metaphor only when it's literal or clearly the best term.

**4.8 Manufactured-casualness parentheticals.** Parentheticals that add tone instead of information: "(I kid you not)", "(though that was wild)". A good parenthetical adds a fact. If it only adds a wink, delete it.

**4.9 Slop vocabulary.** Words that cluster in machine prose. A single use is fine; a cluster is the signal, and the same word in every output is a tic regardless of local count.
> delve, tapestry, testament, vibrant, intricate, pivotal, meticulous, garner, interplay, bolstered, align with, enhance, foster, highlight, showcase, crucial, valuable, leverage, utilize, robust, harness, seamless, realm, navigate (abstract), underscore, landscape (abstract), "play a significant role in shaping", "today's fast-paced world".

Specific buzzwords turn over fast; the structural tells above don't. Treat any word list as a snapshot, not a fixed rule.

**Filler compression:**
- "in order to" → "to"
- "due to the fact that" → "because"
- "it is important to note that" → delete
- "has the ability to" → "can"
- "there exists a need for" → restate as an imperative

### 5. Formatting

| Tell | Fix |
|------|-----|
| Em dashes everywhere | Commas, semicolons, periods; cap a few per piece |
| Bold on every other phrase | Remove most of it |
| Bold-lead bullets used to avoid prose | Restructure as prose, or a plain list; keep bold only as a real label |
| Emoji-led bullets | Remove from prose meant to be read straight |
| Title Case In Every Heading | Sentence case |
| Unicode bold, decorative arrows, checkmarks | Plain text |
| Colon-prefixed titles ("X: Why Y Matters") | Drop the prefix |
| Curly quotes in code or technical text | Straight quotes |
| Horizontal rule before every heading | Remove unless it separates major parts |
| One-sentence paragraphs as a constant beat | Weave into paragraphs; reserve fragments for emphasis |
| Elegant variation (a new synonym for the same noun each paragraph) | Use the correct term consistently |

The em dash deserves its own note. It is a real punctuation mark, so keep the ones you'd have written anyway. The tell is inflation: several per paragraph, or the "not because X, but because Y" sandwich. When an em dash sets off a parenthetical aside, parentheses are usually the cleanest replacement. When it joins or breaks clauses, use a comma, semicolon, or period, and restructure when a clause is carrying too much.

### 6. Code-adjacent

**6.1 PR descriptions.** Don't catalog every file; the diff already lists them. State the user-visible change and the why.
> ❌ "Updates UserService.ts to add getPreferences; modifies UserController.ts to add a /preferences endpoint; adds tests."
> ✓ "Adds a preferences API so settings persist across devices."

**6.2 Commit messages.** "Implement comprehensive user preferences management system" → "add user prefs; theme kept resetting on new devices".

**6.3 Chatbot residue and sycophancy.** Conversational filler pasted into code, docs, or PRs: "I'd be happy to help", "Great question!", "Let me break this down", "Hope this helps!", "Certainly!". And the reflexive opener "You're absolutely right!", "Good point!" prepended even when no claim was made. Begin with content. Disagree when warranted.

**6.4 Over-correct grammar in casual channels.** No contractions or fragments in Slack or commits reads as machine output. "I have completed the implementation" → "feature's up for review."

**6.5 Faux engagement closers.** "Curious what others think." "What's your experience been?" tacked onto a PR or runbook. Replace with the operative ask: "Flag anything I missed."

**6.6 Whitespace and helper inflation.** Exploding a short signature across many lines, a blank line between every statement, a named helper for every two-line operation. Worst in Python, where indentation carries scope. Keep signatures on one line until they're long; inline trivial operations; reserve helpers for reused or meaningfully-named logic.

**6.7 Reporting on work you did.** When an assistant narrates a task it completed, a distinct cluster shows up:
- A bare "Done." or "Applied." opener.
- A whole message built from "Label:" colon-teasers.
- A servile closer: "your call, just say the word".
- Reassurance instead of evidence: "the change is doing its job" rather than showing it.
- A real number reused as a rhetorical button.

Lead with the result and the evidence. Cut the scaffolding and the reassurance.

### 7. Device index

The same tells, named by their rhetorical device. A precise name makes a tell easier to catch on sight.

| Device | ❌ tic | ✓ fix |
|---|---|---|
| antithesis (the "not X, but Y" reframe, or mirrored balance) | "the floor, not the ceiling"; "reps, not scripts" | state Y directly; keep one real contrast, written once as fact |
| cataphora (announce the point before making it) | "Here's the thing:"; "The part nobody mentions:" | cut the frame, state the point |
| sententia (the quotable maxim dropped as a button) | "That's the whole game, really." | let the point stand; end on the concrete |
| enumeratio (a list smuggled into prose) | "A few things matter: first… then… also…" | real prose; reserve lists for parallel items |
| sincerity intensifier (genuine/honest/real as ballast) | "Honestly, yeah."; "my honest take:" | delete it; strengthen the claim if it sags |
| correctio (the "the real problem is" pivot) | "but adding an index isn't the whole story" | state the actual answer; skip the strawman |
| tricolon (the reflexive rule of three) | "cost, speed, and freedom" | use the real count; never back-to-back triples |
| faux-engagement closer (the tacked-on question) | "What's your setup like?" | end on the answer; ask up front only if it changes the advice |
| brachylogia (the clipped dramatic fragment) | "Then everything changed." / "Bloat." | fine once; fold the rest back into sentences |
| hypophora (the self-posed, self-answered question) | "Is it one user or all of them? Turns out…" | ask only the question that changes your answer |
| concessio (the staged honest caveat) | "One flag, in fairness:" | state the limit where it matters; don't stage it |
| captatio (the warm opener or invented personal stake) | "Happy to be a sounding board."; "what works for me:" | open with the answer; don't invent experience |
| em-dash payoff appendage (the trailing significance gloss) | "…and the math stays clean — just means and covariances." | end the sentence, or make it a clean clause |
| hypotyposis (the "picture this" imagined scene) | "Picture a radar screen tracking a plane." | open on the mechanism unless the scene earns its place |
| coinage-as-button (a minted phrase reused as the takeaway) | "timebox it, don't goal-box it" | plain words; a phrase that exists to be quoted is a tell |

## Fixing without adding new tells

Diagnosis is half the work. The other half is repairing a tell without planting another.

1. **Fix by subtraction, not substitution.** Most tells vanish when you delete the scaffold and state the claim. Swapping in a different device just relocates the slop. "One honest caveat:" should become "Take the result as best-case", not "Importantly, one limitation:".
2. **A few tells need restructuring, not deletion.** Negative parallelism: state Y, and write the contrast as fact only if it's needed. Tricolon: keep the real number of items. Copula avoidance: use "is." Keep the content the device carried; drop the device.
3. **Some fixes are not local.** A tell can live above the sentence: a piece built as a chain of colon-teasers, a paragraph that says one thing three ways, a uniform sentence rhythm, an opening and a closing that mirror each other. Editing one sentence won't touch these. They need the passage reordered or rewritten from scratch. If a single fix would have to reach three sentences that aren't next to each other, stop patching and rewrite the passage. When the whole piece is built on the pattern, rewrite the whole piece.
4. **Re-read for what the fix introduced.** A repair that leaves the text choppy, hedged, or wearing a new "see, a human wrote this" costume has failed. Subtraction rarely causes this; substitution often does.

The target: carry the meaning in the claims and the concrete detail, and let structure stay implicit. State the strongest specific thing you have, then stop.

**Worked example**, answering "should I learn Rust or stick with Go?":
> ❌ "Honestly, it depends. Here's the thing: it's not about the language, it's about the problem. Go wins on speed, simplicity, and ecosystem; Rust wins when you need control. At the end of the day, pick what fits, your call."

That's six tells in four sentences: the intensifier, the colon-teaser, negative parallelism, a tricolon, "at the end of the day", and a servile closer.
> ✓ "For backend services, stick with Go; reach for Rust when you need manual memory control or can't tolerate GC pauses. Go gets you productive faster; Rust gives you guarantees Go can't. If it's for a specific project, let the project decide."

The repair is mostly deletion. One contrast survives because it's doing real work, stated once as fact.

## Pre-publish checklist

Run this against the rewritten text. Fix anything that fails before output. Don't ship a rewrite that adds new tells while removing old ones.

**Lexical**
- [ ] "genuinely / honestly / truly / really / actually" as a filler intensifier?
- [ ] "serves as / stands as / represents" where "is" would do?
- [ ] Promotional words? (nestled, vibrant, boasts, renowned)
- [ ] Vague authority? (experts agree, studies suggest)
- [ ] Dev metaphors used figuratively? (load-bearing, blast radius, surface as a verb)
- [ ] Adverbs propping weak verbs?
- [ ] Slop vocabulary clusters? (delve, leverage, robust, showcase, foster)

**Structural**
- [ ] More than one "not X, but Y"?
- [ ] A "the real X was" pivot?
- [ ] A "X is the Y of Z" forced analogy?
- [ ] A "Not X. Not Y. Just Z." countdown?
- [ ] Rhetorical self-Q&A?
- [ ] A listicle hidden in prose?
- [ ] Rule-of-three saturation, or a triad whose third item merges the first two?
- [ ] Tacked-on -ing analysis at a sentence end?
- [ ] A colon-teaser reveal, or a whole message built from "Label:" teasers?
- [ ] A quotable maxim or coined phrase used as a closer?
- [ ] "Imagine a world where" opener?
- [ ] "Despite its challenges" balance-performance?
- [ ] A sycophantic opener? ("You're absolutely right", "Good point")
- [ ] Saying the same thing twice in new words?
- [ ] More than a few em dashes?
- [ ] Conclusion that starts with "In conclusion" or restates the opening?
- [ ] Knowledge-cutoff disclaimers, unfilled placeholders, or a sentence that doesn't parse?

**Voice**
- [ ] Did I overcorrect? (choppy, de-styled, real lists or correct terms stripped)
- [ ] Does sentence length match the source's range?
- [ ] Specifics over significance claims?
- [ ] Is every specific the rewrite added (name, date, figure, detail) supported by the source, or did it invent to sound concrete?
- [ ] Does the opening do real work, and the ending land on the strongest point?

## Process

1. **Detect mode and scope.** "--audit", "audit", "diff", or "review" means audit; otherwise rewrite. No file path and no pasted text, invoked in this project, means the whole project (see Project scope above) — not a request for a file to be named.
2. **Read the input fully** and infer its voice (register, sentence length, idiom). Detection works on the whole piece — or the whole project, for a project-wide run — not sentence by sentence.
3. **Scan** structure, sentences, tone, lexicon, formatting, and code-adjacent tells.
4. **Rewrite at the level the tell lives at.** Preserve meaning and voice; fix by subtraction before substitution. A local tic needs a phrase change; a structural tell needs a paragraph or the whole piece rewritten, not a sentence patched.
5. **Self-audit before output.** Don't ship the first draft. Ask, in these words, "what still reads as AI here?" and name each remaining tell. Then check every specific the rewrite added (name, date, figure, sensory detail) against the source and cut anything the source didn't support; a rewrite invents most when it's reaching to sound concrete or to fill space. Run the checklist, fix what you find, and re-read once for anything the fix introduced.
6. **Output.** Rewrite mode: the humanized text (for a file, ask before overwriting; default to `<path>.humanized`; for a project-wide run, write each file in place). Audit mode: the diff plus the change list, ending with "What did not change" if the original was clean — or, project-wide, one such report per file plus the cross-file summary from Project scope.

Vocabulary tells change with each model release. The structural and tonal tells above persist, because they come from how language models generate: repetition penalties, regression toward important-sounding prose, and marketing copy in the training mix. When in doubt, weight structure over word lists.
