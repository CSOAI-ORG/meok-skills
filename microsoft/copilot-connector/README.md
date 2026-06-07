# MEOK Trade Compliance — Microsoft Copilot Connector

Connector + declarative agent for **Microsoft Copilot Studio** + **Microsoft 365 Copilot**.

## Files

| File              | Purpose                                                                                   |
|-------------------|-------------------------------------------------------------------------------------------|
| `connector.json`  | App manifest — Teams / Copilot AppSource submission package metadata.                     |
| `agent.json`      | Declarative agent — instructions, actions, conversation starters.                         |
| `openapi.yaml`    | API actions schema — fetched live from `https://meok-attestation-api.vercel.app/openapi.json`. |

## Submission

1. Open https://copilotstudio.microsoft.com/
2. New agent → "Start from scratch" → Import this folder.
3. The agent automatically picks up the OpenAPI actions at `agent.json` → `actions[].file`.
4. Test in the right-pane chat — try the conversation starters in `agent.json`.
5. Publish → choose audience (Just me / My organization / Microsoft 365 Copilot).

## Authentication

- **Verifier** (`/verify`): no auth — actions table calls it directly.
- **Sign** (`/sign`): user-supplied API key via `X-API-Key` header. Configure the connector for "User authentication" → "API key in header".

## See also

- [OpenAI GPT manifest](../openai/meok-trade-compliance-gpt/)
- [Anthropic Skill](../anthropic/meok-trade-compliance/)
