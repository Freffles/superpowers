# Superpowers for Google Antigravity (manual pattern)

This is a practical integration pattern for trying Superpowers with Google Antigravity.

Because Antigravity integration details can change quickly, this document focuses on a robust **manual** setup that works even when there is no official plugin installer.

## Goal

Make Antigravity aware of Superpowers skills so it can:

- discover skill names and descriptions,
- apply skills when a task matches,
- and consistently follow workflow skills (brainstorming, planning, TDD, review, finish).

## 1) Clone Superpowers locally

```bash
git clone https://github.com/obra/superpowers.git ~/superpowers
```

## 2) Load bootstrap instructions into Antigravity

In your Antigravity project/session instructions, add a short bootstrap like:

```text
You have access to a local skills repository at ~/superpowers/skills.
Before responding to any task, check for relevant skills by reading SKILL.md metadata (name + description).
If a skill is relevant or explicitly requested, follow it.
Always prioritize process skills first (brainstorming/debugging/planning), then execution skills.
```

If Antigravity supports a stronger system prompt or policy file, place this there instead of in a one-off chat message.

## 3) Expose the skills directory to the runtime

Depending on your Antigravity environment:

- mount or grant file access to `~/superpowers/skills`, or
- copy the `skills/` folder into a location Antigravity can read.

The key requirement is that Antigravity can open `SKILL.md` files inside each skill directory.

## 4) Start with a skill-triggering prompt

To verify behavior, begin with something that should obviously trigger a skill, for example:

```text
Help me plan this feature before writing code.
```

Expected behavior:

1. It identifies and applies brainstorming/planning skills.
2. It asks clarifying/design questions before coding.
3. It proposes a staged implementation plan.

## 5) Keep skills updated

```bash
cd ~/superpowers && git pull
```

## Recommended first checks

- Confirm Antigravity can read `~/superpowers/skills/*/SKILL.md`.
- Confirm it announces skill usage when relevant.
- Confirm it follows process order (design/plan before implementation).

## Known limitation

This repo currently does not include an Antigravity-specific one-command installer. If Antigravity introduces native plugin or skill discovery support, this guide can be replaced with a first-party install path.
