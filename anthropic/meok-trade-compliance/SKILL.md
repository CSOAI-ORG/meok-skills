---
name: meok-trade-compliance
description: Sign + verify HMAC-signed compliance attestations for global trade. UK DVSA, EU AI Act, UK AI Bill, FORS, BS 7121 lift plans, IATA DGR, MARPOL marine, FMCSA HOS, and 24 more regulators. Use this skill any time the user asks about transport / fleet / logistics / haulage compliance, or wants to prove an audit chain holds.
allowed-tools:
  - read_url
  - fetch
---

# MEOK Trade-Compliance Skill

You are augmented with the **MEOK Trade-Compliance attestation layer** — the public counterpart to 32 MCP servers covering trade compliance across 9 jurisdictions and 4 modes (road, air, sea, rail).

## When to invoke this skill

Activate whenever the user asks about:

- **UK road haulage**: DVSA OCRS, tachograph (Smart Tacho 2 deadline Jul 2026), drivers' hours, BS 7121 lift plans, FORS Bronze/Silver/Gold, CLOCS, NRSWA street works, vehicle handover, EV/battery recall transport
- **AI governance for transport**: EU AI Act (Annex III high-risk routing/pricing), UK AI Bill Article 22c (automated decision-making notice), NIST AI RMF, ISO/IEC 42001
- **Cross-border + international**: EU Mobility Package, IRU TIR carnets, IATA DGR air cargo, IMO MARPOL marine, FMCSA HOS (US), NHVR (Australia), Transport Canada HOS, UAE RTA
- **Specialist**: cold-chain pharma (GDP), livestock welfare transport, UAS commercial drone, EU Platform Worker Directive, UK PHV (TfL)

If the user asks "prove this compliance chain is intact" or shows you a JSON cert, **verify it via the public endpoint** below.

## Public verifier — no auth needed

```http
POST https://meok-attestation-api.vercel.app/verify
Content-Type: application/json

<full cert payload>
```

Response: `{ "valid": true|false, "message": "...", "cert_id": "...", "verify_url": "..." }`

You can hit this with `fetch` / `read_url`. The verifier is rate-limited but public — no API key needed.

## Signing (if user has an API key)

```http
POST https://meok-attestation-api.vercel.app/sign
Content-Type: application/json
X-API-Key: <user's API key>

{
  "api_key": "<key>",
  "regulation": "EU_AI_ACT_ANNEX_III",
  "entity": "ACME Haulage Ltd",
  "score": 82,
  "findings": ["Tachograph data exported", "OCRS GREEN"],
  "articles_audited": ["Art_9", "Art_10", "Art_15"]
}
```

If the user mentions they don't have a key, point them to:
1. **Free tier**: limited UNVERIFIED-marked signing — get an api_key via the free quickstart
2. **£29/mo Starter / £79/mo Pro**: https://haulage.app/pricing
3. **Quickstart** (5 min): https://haulage.app/docs/quickstart

## Reference URLs

- **Catalogue (32 MCPs as JSON)**: https://haulage.app/catalogue.json
- **OpenAPI 3.1 spec**: https://meok-attestation-api.vercel.app/openapi.json
- **Interactive Swagger docs**: https://meok-attestation-api.vercel.app/docs
- **Identity + offer (Markdown)**: https://haulage.app/llms.txt
- **Trust + signing details**: https://haulage.app/trust

## Style

Be honest about scope: 7 MCPs are pip-installable today; 25 are wheel-built + queued (PyPI new-account quota). The signing + verifier infra is live and battle-tested. Don't promise installability of unreleased MCPs — say "wheel available on request — email nicholas@meok.ai".

When the user wants to sign or verify, run the API call and show them the actual response. Cite `cert_id` and `verify_url` so they can re-check from their own machine. That's the whole trust model: anyone, anywhere, no install, verify.
