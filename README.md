# MEOK AI Distribution Surface

Skill / agent / plugin manifests that distribute the MEOK Attestation API into agent runtimes.

```
meok-skills/
├── anthropic/
│   └── meok-trade-compliance/
│       └── SKILL.md          ← drop into ~/.claude/skills/ or submit to Anthropic
└── openai/
    └── meok-trade-compliance-gpt/
        ├── manifest.json     ← OpenAPI plugin manifest
        └── gpt_instructions.md ← paste into GPT Builder
```

## What each does

| Surface           | What                                               | Distribution             |
|-------------------|----------------------------------------------------|--------------------------|
| Anthropic Skill   | Claude invocation contract + tool wiring           | Skills registry          |
| OpenAI Plugin     | ChatGPT Actions via OpenAPI 3.1                    | GPT Store (200M users)   |

Both surfaces ultimately hit the same backend: `https://meok-attestation-api.vercel.app`. The OpenAPI spec is canonical at `/openapi.json`.

## Roadmap

- [ ] Microsoft Copilot connector — same OpenAPI manifest, target Copilot Studio (Q3 2026)
- [ ] Gemini Gem — Google's equivalent, JSON manifest
- [ ] Slack app — slash commands `/meok verify` (workflow #27 in the 33-move plan)
- [ ] Teams app (workflow #28)
- [ ] Zapier + n8n + Make (workflow #29 — auto-generated from OpenAPI)

## Submission process

### Anthropic Skill
Drop `SKILL.md` into `~/.claude/skills/meok-trade-compliance/` for personal use, or PR to https://github.com/anthropic/skills.

### ChatGPT GPT
1. Open https://chat.openai.com/gpts/editor (Plus subscription required)
2. Paste contents of `gpt_instructions.md` into the Instructions field
3. Under Actions → "Import from URL" → `https://meok-attestation-api.vercel.app/openapi.json`
4. Set name "MEOK Trade Compliance", description from `manifest.json`
5. Upload `https://haulage.app/og-image.jpg` as the logo
6. Publish → Everyone
