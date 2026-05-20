# Usage walkthrough

A canonical session with `claude-amanuensis`, from blank page to polished draft.

## 1. Capture your voice

Point `/capture` at things you've already written — essays, blog posts, chapters, even a public URL.

```sh
/capture ./essays/*.md ./blog/2025-*.md
/capture https://my-site.example/about
```

The command analyzes the corpus and writes two files at your project root:

- `VOICE.md` — rhythm, diction, recurring images, intentional quirks
- `STYLE.md` — heading conventions, punctuation preferences, formatting

Open both. Edit by hand. They're the ground truth for everything that follows.

> Tip: maintain a separate pair per form. A `fiction/VOICE.md` and a `technical/VOICE.md` keep registers from bleeding into each other.

## 2. Expound from a sketch

Got an outline, a voice memo transcript, or three scribbled bullet points? Hand them to `/expound`.

```sh
/expound outline.md
/expound "a 400-word opener about the smell of wet pine"
```

`/expound` reads `VOICE.md` and `STYLE.md` and drafts prose anchored to them. Output goes to a new file (or stdout) — never overwriting existing text.

## 3. Review in four passes

Run each pass as a **separate invocation with a clean context**. Mixing passes blurs the focus.

```sh
/review structure   # arc, pacing, what's missing
/review craft       # sentence rhythm, verb choice, cliché
/review copy        # grammar, agreement, consistency
/review proof       # typos, final sweep
```

Each pass returns a numbered list:

```
1. ¶3, sentence 2 — "very quickly" → "quickly" (voice: tighten adverbs)
2. ¶4 — split the 38-word sentence at "and then"
3. ¶7 — repeated word "however" (used in ¶6)
...
```

You reply with the numbers you want applied — e.g. `apply 1, 3, 7` — and only those edits land.

## 4. Get a second opinion

For high-stakes passages, fan the same passage out to other models:

```sh
/review craft --with codex
/review structure --with gemini
```

Notes are collated alongside Claude's. Disagreements are flagged, not averaged.

## 5. Compress

`/expound` also runs in reverse — give it prose and a target length, and it tightens without flattening voice.

```sh
/expound --compress chapter-03.md --target 0.7
```

---

## End-to-end example

```sh
# one-time
/capture ./published/*.md

# new piece
/expound notes/pine-smell.md > drafts/pine-smell.md

# iterate
/review structure   # apply 2, 4
/review craft       # apply 1, 3, 5, 6
/review copy        # apply all
/review proof       # apply all
```

That's the loop. The author drives; the amanuensis scribes.
