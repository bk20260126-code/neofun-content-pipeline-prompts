# Voice Rules — Avoid Slop

Every agent in this pipeline must check output against these rules before writing to a file.
If any of these patterns appear, rewrite the sentence. No exceptions.

---

## Forbidden Opener Patterns

Never start a post, slide, or hook with:
- "In today's fast-paced world..."
- "In this post, I'll share..."
- "Today I want to talk about..."
- "As an AI..."
- "It's no secret that..."
- "In the age of AI..."
- "The future is here..."
- "Game-changer"
- "Revolutionary"
- "Unlock the power of"
- "Dive into"
- "Let's explore"
- "Did you know?"

## Forbidden Body Phrases

Never use these anywhere in the content:
- "Groundbreaking"
- "Cutting-edge"
- "State-of-the-art"
- "Leverage" (use "use")
- "Utilize" (use "use")
- "Synergy" / "Synergize"
- "Move the needle"
- "Low-hanging fruit"
- "At the end of the day"
- "Circle back"
- "Deep dive" (use "look at" or just say what you mean)
- "Robust"
- "Seamless"
- "Streamline"
- "Holistic approach"
- "Best-in-class"
- "World-class"
- "Next-level"
- "Supercharge"
- "Skyrocket"
- "Skyrocketed"
- "Transformative"
- "Disruptive"
- "Paradigm shift"
- "Thought leader"
- "Ecosystem" (unless describing actual software ecosystems)
- "In conclusion" / "To summarize" / "In summary"
- "According to experts"
- "Studies show" (without citing the actual study)
- "Many people don't realize..."
- "Here's the thing:"
- "The truth is..."
- "Honestly,"
- "Simply put,"

## Forbidden Structural Patterns

- Lists of more than 7 items with no grouping
- Ending every bullet with a period (bullets are not sentences)
- Three consecutive sentences of the same length
- Emojis used as bullet points
- Rhetorical questions stacked more than once in a row

## Korean-Specific Forbidden Phrases

These are the Korean equivalents of slop — clichéd phrases that signal generic AI content:

**범용 금지 — 어느 브랜드에나 해당합니다:**
- "생산성 향상" — 뜻이 없다
- "원활한 통합" / "seamless" — 절대
- "혁신적인" / "혁신" — 절대
- "자동화"를 그 자체로 파는 말 — 항상 구체적인 작동 방식을 붙인다
- "AI 시대에..." — "In today's fast-paced world"의 한국어판
- "많은 분들이 모르시는..." — 독자를 낮춰 보는 말
- "솔직히 말씀드리면" / "사실은..." / "여러분도 아시다시피" — 빈 도입부
- 과장: "혁명적", "게임 체인저", "초격차" — 절대
- 공개 글에서 도구 이름 나열 — 절대

**내 브랜드 금지어 — `BRAND.md` §6에서 읽는다:**
브랜드마다 팔지 않는 것이 다릅니다. 예를 들어 효율이 아니라 결과를 파는 브랜드라면
"시간 절약"과 "비용 절감"이 금지어이고, 대신 무엇으로 바꿔 말할지도 정해져 있어야 합니다.
그 목록은 여기가 아니라 `BRAND.md`에 있습니다. **작성 전에 반드시 읽으세요.**

**내부 용어 유출 금지 — `BRAND.md` §6에서 읽는다:**
내부에서만 쓰는 방법론 이름·약어를 공개 글에 그대로 쓰지 않습니다.
`BRAND.md` §6에 내부 용어와 공개용 쉬운 표현이 짝지어 있습니다. 항상 오른쪽을 쓰세요.

**우리 실제 문장 — `BRAND.md` §4에서 읽는다:**
톤은 설명으로 배우는 게 아니라 예문으로 배웁니다. 작성 전에 §4의 실제 문장을 읽고
그 리듬에 맞추세요. 비어 있으면 브랜드 담당자에게 3개 이상 채워달라고 요청하세요.

## What Good Looks Like Instead

Replace vague with specific:
- ❌ "AI is transforming marketing"
- ✅ "A 3-person team at [Company] replaced their entire briefing process with one BRAND.md file"

Replace hype with mechanism:
- ❌ "Supercharge your content workflow"
- ✅ "The Strategist reads your Slack message at 8AM and builds the brief from it — you never touch a brief template again"

Replace passive authority with direct claim:
- ❌ "Experts agree that consistency is key"
- ✅ "We ran the same brand through 3 different AI tools. The one with BRAND.md looked identical every time. The others drifted."
