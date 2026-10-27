---
name: code-review-maintainability
description: Use when reviewing a pull request or module for long-term health — complexity, structure, file size, duplication, naming — rather than for bugs. Prefers a few high-conviction comments and changes that delete complexity over ones that move it around.
---

# Maintainability review

The question is: will this code be cheaper or more expensive to change six months from now? Bugs belong to `code-review-deep`; this review is about shape.

## Principles

- **Delete complexity, don't relocate it.** A refactor that moves the same branching into a new class, helper or layer is not an improvement. Ask what the change removes.
- **Few, high-conviction comments.** Three comments the author must act on beat twenty cosmetic ones. Do not comment on formatting, import order or naming nits that a linter or formatter can enforce — propose a lint rule instead.
- **Judge the change, not the codebase.** Old problems are out of scope unless the change grows them.

## Signals to check

| Signal | Threshold | Ask |
|---|---|---|
| File size | A file crossing ~1,000 lines | Justify or split by responsibility |
| Function size | A function crossing ~60 lines or 4 levels of nesting | Extract the inner decision |
| Conditional growth | New `if`/`when`/`switch` branches on a type or flag that already has branches elsewhere | Is a polymorphic or table-driven design cheaper? |
| Shallow modules | A new class/function whose interface is as complex as its body | Merge it back or deepen it |
| Duplication | The same logic in three places | Extract once; two places can wait |
| Leaky boundaries | UI knows about persistence, domain knows about HTTP | Move the dependency to the edge |
| Names | Names that need a comment to be understood; terms that differ from the project glossary | Rename to the domain term |
| Dead code | Commented-out code, unused parameters, flags that are always on | Delete it |
| Tests | Tests coupled to private details | Test through the public boundary |

The thresholds are defaults. A project can override them in its own CLAUDE.md or contributing guide.

## When to approve

Approve when the change leaves the touched area no harder to change than before, even if it is not how you would have written it. Request changes only when the change measurably adds complexity that will compound (a file past the threshold without justification, a new parallel conditional ladder, a broken boundary).

## Output

```
Verdict: approve | approve with comments | request changes
Must address:
- path:line — problem — proposed direction
Consider (optional):
- ...
```

## Known failures

_Record real mistakes here with a date and the rule that prevents them._
