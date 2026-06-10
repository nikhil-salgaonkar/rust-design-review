# rust-design-review

A Claude skill for conducting idiomatic Rust design reviews, grounded in the
[Rust Design Patterns book](https://rust-unofficial.github.io/patterns/)
by the rust-unofficial community.

## What it does

When you paste Rust code and ask Claude to review it, this skill walks through
three layers of analysis:

- **Idioms** — 15 community-agreed idioms: borrowed type arguments, `format!` for
  string concatenation, `Default` trait, `mem::take` in enum mutations, selective
  closure captures, `#[non_exhaustive]`, and more.
- **Design patterns** — Builder, RAII with Guards, Newtype, Typestate, Command,
  Visitor, Struct decomposition, and Rust-specific patterns like using traits
  instead of the Strategy pattern.
- **Anti-patterns** — Clone to satisfy the borrow checker, Deref polymorphism,
  `#[deny(warnings)]` in library code.

Reviews are structured as:
```
🔴 Must Fix   — correctness issues and anti-patterns
🟡 Should Fix — clear idiom violations
🔵 Consider   — pattern opportunities worth evaluating
✅ What's Done Well
```

## Trigger phrases

Claude will activate this skill when you say things like:

- "Review my Rust code"
- "Is this idiomatic?"
- "How would a Rust expert write this?"
- "Do a design review"
- "What patterns am I missing?"
- "What am I doing wrong in Rust?"

## Installation

1. Download `rust-design-review.skill` from the [Releases](../../releases) page.
2. Copy the `SKILL.md` file and `references/` folder to ~/.claude/skills/rust-design-review
3. Alternatively, in Claude Desktop, open **Customize** and drag in the `.skill` file.

## File structure

```
rust-design-review/
├── SKILL.md                  # Main skill instructions and review process
├── LICENSE                   # MPL-2.0
├── README.md                 # This file
└── references/
    ├── idioms.md             # Full idioms checklist with code examples
    └── patterns.md           # Design patterns & anti-patterns catalogue
```

`SKILL.md` is always in context (125 lines). The reference files are loaded
on demand during a review, keeping the always-loaded footprint small.

## Building

To repackage the `.skill` file after making changes:

```bash
# From the repo root (requires the skill-creator scripts)
python -m scripts.package_skill rust-design-review
```

## Reference

All patterns, idioms, and anti-patterns are drawn from:

> **Rust Design Patterns**
> https://rust-unofficial.github.io/patterns/
> © rust-unofficial contributors — Mozilla Public License 2.0

## License

This project is licensed under the [Mozilla Public License 2.0](LICENSE),
consistent with the upstream source material.
