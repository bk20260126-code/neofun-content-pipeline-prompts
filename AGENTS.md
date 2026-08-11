# AGENTS.md (Content Pipeline Prompts)

## What this repo is

A set of role prompts that turn one piece of raw material (글감) into
platform-ready social drafts, gated by a brand-fit interview and an idea
quality score. There is no publishing automation here. Every run ends at a
reviewed draft, not a posted one.

## Before anything else

Check whether `BRAND.md` is actually filled in, not just present. If the
top warning banner is still there, or a numbered section still holds
parenthetical instruction text in `()` instead of real content, run the
interview before touching anything else in this file:

```
skills/onboarding/SKILL.md 대로 나를 인터뷰하고 BRAND.md를 작성해줘
```

Every step below reads `BRAND.md`. An unfilled one makes every later step
produce generic output, indistinguishable from asking any AI to "write a
LinkedIn post" with no brand behind it.

## Workflow

| Step | File | Input | Stops if |
|---|---|---|---|
| 1. Score | `agents/idea-scorer.md` | one 글감 (a sentence or two) | score < 8/12 → return feedback, do not proceed |
| 2. Brief | `skills/strategist/SKILL.md` | the scored 글감 | (none) |
| 3. Draft | `skills/writer/SKILL.md` | the brief | (none) |
| 4. Review | `skills/qa-editor/SKILL.md` | the draft | 2 consecutive rejections → stop, hand both reports back to the user |

Optional, each needs an external service the user must have configured:

| File | Needs |
|---|---|
| `skills/carousel/SKILL.md` | an image generation service |
| `skills/analyst/SKILL.md` | an analytics data source |

Every step reads `BRAND.md` and `rules/avoid-slop.md`. Read both once per
session rather than re-reading on every step of the same run.

## Gotchas

- **`skills/*/SKILL.md` files are not under `.claude/skills/`.** Claude
  Code's native skill auto-trigger will not fire on them by matching
  intent alone. If a request matches one of these, for example "브랜드
  인터뷰 해줘" or "이 아이디어 채점해줘," read the relevant file yourself and
  follow it. Do not improvise the workflow from general knowledge instead;
  that silently skips the brand check and the rejection gate.
- **A score below 8 is feedback, not a dead end.** `idea-scorer` returning
  a low score should produce a revised 글감 with the missing mechanism
  added, not a lower bar to clear.
- **QA_FAIL_2 stops the pipeline, it does not escalate anywhere.** Do not
  self-retry a third time by silently rewriting and resubmitting again.
  Hand both rejection reports back to the user, per
  `skills/qa-editor/SKILL.md`. There is no one else in this pack to hand
  it to.
- **No invented proof.** A claim in a draft needs a matching entry in
  `BRAND.md` §5. If it is not there, the claim does not go in the draft.
  Mark it `[VERIFY]` in `BRAND.md` instead of writing around the gap.
- **No em dash in any generated draft.** Comma, period, or parentheses
  instead. This is a voice rule for output content, not for this file.
- **Publishing is out of scope.** Nothing here should be extended to
  actually post content on the user's behalf without them asking for that
  explicitly, separately from running the pipeline itself.

## Where the detail lives

- `README.md`: the same workflow written for a human reader, with
  copy-paste examples
- `BRAND.md`: the member's own voice, audience, and proof, read by every
  step above
- `rules/avoid-slop.md`: the full forbidden-phrase and forbidden-pattern
  list
