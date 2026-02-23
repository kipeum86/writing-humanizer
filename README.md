# Humanizer
A Claude skill that detects and removes AI-generated writing patterns. Paste in text or hand it a file, and it rewrites the content to sound like a person actually wrote it.
Works in English and Korean (한국어).

## What it does
The skill scans text against 24 documented AI writing patterns from [Wikipedia's "Signs of AI writing"](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) guide, then rewrites flagged sections while keeping the original meaning intact.

It catches things like:
- "This serves as an enduring testament to the evolving landscape" → just say what it is
- "Additionally, it is crucial to delve into the intricacies" → AI vocabulary pile-up
- "highlighting... showcasing... underscoring..." → fake-depth -ing phrases
- 💡 **Bold emoji headers:** with colons → formatting that screams chatbot
- "획기적인 AI 기술을 기반으로 다양한 서비스를 제공하고 있으며" → 한국어 AI 패턴도 감지

It doesn't just strip bad patterns, though. Clean-but-lifeless text is equally obvious. The skill also injects voice: varied rhythm, actual opinions where appropriate, and the kind of specificity that signals a real person behind the words.

## Installation
Download the `.skill` file from the [latest release](../../releases/latest) and add it to your Claude skill library.
Or clone the repo and point Claude at the `SKILL.md` file directly.

## Usage
Just ask Claude to clean up your text. The skill triggers on phrases like:
- "humanize this"
- "make this sound less AI"
- "이거 너무 AI 같아, 고쳐줘"
- "clean up this AI slop"
- "rewrite this naturally"

You can paste text directly into the chat or upload a file (.md, .txt, .docx).

### Output modes
The skill supports two output modes — it'll ask which you prefer, or you can specify upfront:
**Full process** — draft rewrite, then a self-audit ("what still sounds AI here?"), then a final version. Useful if you want to see the thinking and iterate.
**Final only** — just the cleaned-up result. Say "just fix it" and this is what you get.

## Patterns detected
24 patterns organized into five categories:

| Category | Patterns |
|---|---|
| Content | Inflated significance, fake notability, superficial -ing analyses, promotional language, vague attributions, formulaic "challenges" sections |
| Language & grammar | AI vocabulary overuse, copula avoidance ("serves as" instead of "is"), negative parallelisms, rule of three, synonym cycling, false ranges |
| Style | Em dash overuse, boldface overuse, inline-header lists, title case headings, decorative emojis, curly quotes |
| Communication | Chatbot artifacts ("I hope this helps!"), knowledge-cutoff disclaimers, sycophantic tone |
| Filler & hedging | Filler phrases, excessive hedging, generic positive conclusions |

The full pattern reference with before/after examples for each pattern is in [`references/patterns.md`](references/patterns.md).

### Korean-specific patterns (한국어)
한국어 AI 텍스트에도 고유한 패턴이 있습니다:
- 과장 수식어: "획기적인", "선도적인", "차별화된"
- 의미 없는 강조 반복: "다양한", "중요한", "핵심적인"
- 접속사 남용: "또한", "더불어", "이를 통해"
- 종결어미 변화 없는 "~입니다/~습니다" 반복
- 모호한 출처: "전문가들은~", "업계에서는~"

## Example
**Before:**
> AI-assisted coding serves as an enduring testament to the transformative potential of large language models, marking a pivotal moment in the evolution of software development. In today's rapidly evolving technological landscape, these groundbreaking tools — nestled at the intersection of research and practice — are reshaping how engineers ideate, iterate, and deliver, underscoring their vital role in modern workflows.

**After:**
> AI coding assistants can make you faster at the boring parts. Not everything. Definitely not architecture. They're great at boilerplate: config files, test scaffolding, repetitive refactors. They're also great at sounding right while being wrong.

## Skill structure

```
humanizer/
├── SKILL.md                    # Core instructions (158 lines)
└── references/
    └── patterns.md             # Full pattern catalog with examples (309 lines)
```

SKILL.md contains the process, principles, and quick reference table. The detailed pattern catalog lives in `references/patterns.md` and gets loaded on demand.

## Credits
Pattern taxonomy based on [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), maintained by [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup).

## License
MIT
