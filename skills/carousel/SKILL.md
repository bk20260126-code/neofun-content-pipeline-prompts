---
name: sns-carousel
description: Visual generator. Reads approved carousel text from draft file, loads brand UUIDs from uuid-registry.md, and generates brand-locked carousel images via Higgsfield MCP. Only runs after QA_PASSED.
disable-model-invocation: true
# allowed-tools: 이미지 생성 서비스의 실제 MCP tool 이름을 여기에 넣으세요 (계정마다 다릅니다)
---

> **선택 스킬입니다.** 이미지 생성 서비스가 있어야 돌아갑니다. 원본은 Higgsfield 기준으로
> 작성됐으니 다른 서비스를 쓴다면 호출부를 바꾸세요.
>
> `brand-assets/uuid-registry.md`는 **이 팩에 없습니다.** 브랜드 레퍼런스 이미지를 서비스에
> 올린 뒤 그 ID를 적어두는 본인 파일입니다. 없으면 `BRAND.md` §7의 색·서체 규칙만으로
> 생성하세요 — 일관성은 떨어지지만 작동합니다.

# SNS Carousel Skill — your brand Visual Generator

You generate brand-locked carousel images using Higgsfield MCP. Every image must be visually consistent with the your brand brand. You never improvise colors or layouts — you use the brand UUIDs.

## Before Starting

Read:
1. `STATE.md` — must show QA_PASSED. If not, STOP.
2. `draft-[DATE].md` — extract Instagram carousel slide text (Slides 1–6)
3. `brand-assets/uuid-registry.md` — load brand reference UUIDs

If STATE.md does not show QA_PASSED, STOP and report.

## Brand UUID Registry

Load from `brand-assets/uuid-registry.md`:

```
palette_reference  → image role: "style"   (brand colors reference)
cover_template     → image role: "image"   (layout DNA)
typography_ref     → image role: "style"   (font/type reference)
```

**These UUIDs are your brand lock. Always pass them into every generation call.**

## Generation Workflow

### Step 1: Build Prompts for Each Slide

For each slide, construct a prompt:

```
Slide [N] prompt:
"[Visual concept for slide N]. Follow the visual rules in BRAND.md §7.
Warm off-white #FAFAF8 canvas, surface cards #FFFFFF, warm near-black ink #1A1A1A
text carrying ~90% of the layout. At most ONE brand-color moment on this slide —
a soft tinted tile (#FFE6DE / #E2F4FF / #D6F5E6 / #FFF1D6) behind a glyph or number,
one Coral #FF3F01 marker on the single key phrase, or (CTA slide only) one Coral pill.
Everywhere else stays ink. Korean display/emphasis in Gmarket Sans Bold, Korean body
in Pretendard (word-break keep-all), Latin in Hanken Grotesk weight 300 (thin).
Clean 4px grid, generous 80px padding, soft rounded corners (8/14/20 — pills for CTA/badge only),
barely-there shadows (depth via hairlines + inversion). Editorial minimalism, quiet warmed authority — not AI hype.
No gradients. No neon. No stock-photo vibes. Use only the colours and fonts declared in BRAND.md §7, and none of the imagery listed there as forbidden.
Text overlay: '[exact slide text from draft]'"
```

### Step 2: Generate via Higgsfield MCP

Use `mcp__<your-image-service>__generate_image` for each slide.

Recommended model: `nano_banana_2` (highest brand consistency for text/graphics)

Call parameters:
```
model:  "nano_banana_2"
prompt: [constructed prompt above]
image:  [cover_template UUID from uuid-registry.md]  ← brand lock
style:  [palette_reference UUID from uuid-registry.md]  ← color lock
```

**Generate slides sequentially, not in parallel — rate limit awareness.**
**Wait for job completion before next generation (use job_display tool).**

### Step 3: Timeout Handling

Each generation job: wait max 120 seconds.
If timeout → log in STATE.md circuit breaker table → move to next slide → alert Slack after all slides complete.

### Step 4: Confirm Media

After each job completes, use `mcp__<your-image-service>__media_confirm` to confirm the output is accessible.

### Step 5: Update STATE.md

Write each confirmed image URL/ID to the Image Asset Registry section of STATE.md:

```
CAROUSEL_COVER:  [url or job ID for slide 1]
SLIDE_2:         [url or job ID]
SLIDE_3:         [url or job ID]
SLIDE_4:         [url or job ID]
SLIDE_5:         [url or job ID]
CTA_SLIDE:       [url or job ID for slide 6]
```

Then update:
```
PIPELINE_STATUS: VISUALS_READY
```

## Output Summary

After all slides generated, output:

```
CAROUSEL GENERATION COMPLETE
Date: [DATE]
Slides generated: [N]/6
Brand UUIDs used: palette=[uuid], cover=[uuid]
Model: nano_banana_2
Failed slides: [list any timeouts]
Next step: Publisher agent may proceed.
```

## Gotchas

- NEVER skip the brand UUID parameters — without them, visual consistency is lost
- NEVER generate all 6 slides in one batch call — do them one at a time
- If uuid-registry.md is empty (no UUIDs yet), STOP and alert: "Brand UUIDs not set up. Run initial Higgsfield upload first."
- Slide 1 (cover) is the most important — if it fails, STOP the run entirely and escalate
- Do not hallucinate image URLs — only record confirmed outputs from job_display or media_confirm
