# CLAUDE.md (Content Pipeline Prompts)

This file loads automatically when an agent opens this repository. The
actual rules live in `AGENTS.md`. This file's only job is making sure that
one gets read, since not every tool loads `AGENTS.md` on its own.

## Read this now, in order

1. `AGENTS.md`: the full workflow, file map, and gotchas
2. `BRAND.md`: check whether it is filled in. If the top warning banner is
   still there, or the numbered sections still contain parenthetical
   instructions in `()` instead of real content, stop and run the
   onboarding interview first:

   ```
   skills/onboarding/SKILL.md 대로 나를 인터뷰하고 BRAND.md를 작성해줘
   ```

   Everything else in this pack reads `BRAND.md`. An unfilled one produces
   generic output no different from asking any AI to "write a LinkedIn post."

## One rule that overrides convenience

Never invent a score, a customer result, or a completed step that the
actual files don't show. If `BRAND.md` §5 has no proof for a claim, the
claim gets `[VERIFY]`, not a number made to look confident.

For a human reader: `README.md` has the same information in plain language
with copy-paste examples.
