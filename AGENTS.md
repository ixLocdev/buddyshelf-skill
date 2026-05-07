# AGENTS.md — BuddyShelf-Skill

## What this is

This repository is **not** an app — it's a Claude skill (a markdown skill file) that teaches Claude how to interact naturally with users of **BuddyShelf**, the Mac app that wraps Git in plain English. The skill defines:

- When to suggest "shelving" (committing) work
- The three-tier terminology mapping (Buddy / Both / Git)
- The `buddyshelf://` URL scheme for triggering BuddyShelf actions from a terminal
- Tone: a helpful coding partner, not a Git lecturer

The single deliverable is `buddyshelf-skill.md`, which is consumed by Claude Code (and other compatible agent harnesses) as a skill definition. The repo also has a short `README.md` describing what the skill is.

Target audience for the skill itself: vibe coders and non-developers using BuddyShelf to manage their projects.

## Stack & tooling

- **No build system.** No language. No tests.
- Pure markdown (`buddyshelf-skill.md` + `README.md`).
- Distributed via GitHub: `https://github.com/ixLocdev/buddyshelf-skill.git`
- Loaded by agent harnesses that read skill markdown files with YAML frontmatter.

## Project layout

```
BuddyShelf-Skill/
├─ buddyshelf-skill.md   The skill itself — YAML frontmatter + skill body
├─ README.md             Short human-facing description
├─ .buddyshelf.json      BuddyShelf metadata (synced to GitHub)
└─ .gitignore
```

## Conventions

- **YAML frontmatter** at the top of `buddyshelf-skill.md` defines `name` and `description` — these control when Claude auto-invokes the skill. Edit carefully; the description is what triggers selection.
- **Tone in the skill body** is instructional second-person ("You are a coding partner who…"). Match that voice when editing.
- Terminology table has three columns (Buddy / Both / Git) — keep all three in sync if a row is added.
- URL-scheme examples must be valid — `?message=...` values must be URL-encoded.

## Commands

There is nothing to build, run, or test. To ship a change:

1. Edit `buddyshelf-skill.md`.
2. Shelf it (commit) and back it up to GitHub.
3. Users pull/install the updated skill.

## Buddy-family context

Part of Lucas's **Buddy** family (BuddyShelf, BuddyBackup, BuddyBar, BuddyBell, BuddyHealth, BuddySet, BuddyShip). This repo is the *companion skill* to **BuddyShelf** specifically — the Mac app at https://buddyshelf.com (also `buddyshelf.io`, `buddyshelf.app`). The skill embeds the same friendly Buddy brand voice the app itself uses.

The global Claude config (`~/.claude/CLAUDE.md`) also embeds a condensed BuddyShelf integration block. If the canonical skill in this repo changes meaningfully, the global config should be reviewed for parity.

## Gotchas

- **Don't add Git jargon** to user-facing examples. The whole point of the skill is plain English.
- **Suggesting shelving has rules** — only at meaningful breakpoints, never after one-line tweaks, max one suggestion per breakpoint. Preserve those guardrails when editing.
- The frontmatter `description` triggers skill auto-selection. Changing the wording changes when Claude invokes the skill — test before shipping.
- This project itself uses BuddyShelf for version control (it's `isSynced: true` and connected to GitHub).
- The skill explicitly forbids running raw `git` commands when working with BuddyShelf users — that rule applies to anyone editing this skill too.
