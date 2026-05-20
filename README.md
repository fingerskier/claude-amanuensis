# claude-amanuensis

A Claude Code plugin that helps authors draft and edit **in their own voice**. It captures how you write, expands sketches into prose, and runs targeted review passes — always proposing edits as a numbered list before touching the text.

> An _amanuensis_ is a scribe who writes what another dictates. This plugin is meant to serve the author, not replace them.

---

## Prerequisites

- Claude Code (CLI, desktop, or web) — version supporting plugins / slash commands
- A git repo for your project (the plugin reads/writes `STYLE.md` and `VOICE.md` at the repo root)
- Optional: `codex` and/or `gemini` CLIs on `PATH` for second-opinion passes

## Install

```sh
/plugin install fingerskier/claude-amanuensis
```

Or clone into your Claude plugins directory:

```sh
git clone https://github.com/fingerskier/claude-amanuensis ~/.claude/plugins/claude-amanuensis
```

## Quickstart

```sh
/capture ./my-essays/*.md     # learn your voice from existing work
/expound outline.md            # turn a sketch into prose
/review structure              # then: craft, copy, proof
```

Each `/review` pass returns a **numbered list** of proposed edits. You pick which to apply. See [docs/USAGE.md](docs/USAGE.md) for a full walkthrough.

---

## Commands

### `/capture`
Import voice & style from files, URLs, or prompts. Writes findings into `VOICE.md` (rhythm, diction, stylistic quirks) and `STYLE.md` (mechanics, conventions, formatting).

### `/expound`
Generate prose from a prompt, outline, or dictated sketch. Anchors output against `VOICE.md` and `STYLE.md` so the result sounds like _you_.

### `/review <pass>`
Run one of four passes. **Each pass should be a separate invocation with a clean context** for best results.

| Pass        | Focus                                  |
|-------------|----------------------------------------|
| `structure` | Developmental — arc, pacing, structure |
| `craft`     | Line — sentence-level craft            |
| `copy`      | Copy — grammar, consistency            |
| `proof`     | Proofread — typos, final pass          |

Output is a **numbered list of proposed edits by default**. Rewrites only happen from such a list — see _Diff Always_ below.

---

## Principles

### Anchoring
- Glean examples of the author's work into `VOICE.md` / `STYLE.md`
- Preserve idiosyncratic word choices, rhythm, and intentional stylistic quirks
- Score every output on its **voice fidelity** against the anchors
- Maintain a separate style-sheet per form (fiction, technical, long-form, casual)

### Diff Always
- Generate a diff or numbered list of proposed edits **first**
- Rewrite only from that list — never silent, in-place edits

### Second Opinions
- Invoke `codex` and/or `gemini` for an independent read on the same passage
- Spin up multiple agents and collate their notes when stakes are high

### Scribing
- Expand dictation or a sketch into prose (`/expound`)
- Compress prose back down without losing voice

---

## Canonical files

The plugin reads and writes two files at your project root:

- **`VOICE.md`** — your voice fingerprint: rhythm, diction, recurring images, intentional quirks, things you _never_ do
- **`STYLE.md`** — mechanical conventions: heading style, citation format, oxford comma, dash usage, etc.

Both are plain Markdown. Edit them by hand any time — the plugin treats them as ground truth.

---

## License

See [LICENSE](LICENSE).
