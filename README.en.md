# food-sc-license-checker · Food production licence (SC) & traceability domain

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Domain: food](https://img.shields.io/badge/domain-food-9cf.svg)](domain.manifest.json)
[![Status: RESERVED](https://img.shields.io/badge/status-RESERVED-orange.svg)](domain.manifest.json)

> **Status: RESERVED (placeholder · open for adoption)** — This repo scaffolds the
> industry-access four-file skeleton per the platform profile and awaits a qualified
> operator to claim it and fill in real rules.

Turns "may this food be produced, and is the traceability chain complete" into verifiable
attributes: the AI only surfaces prerequisites, it never hands down a food-safety verdict.

**Keywords**: food production licence · SC licence · traceability · food additives (GB 2760) ·
production category · cold chain · attribute verification · red lines · gate-map ·
privacy-by-default · food safety · regulatory compliance · MCP checker

## What this domain covers

Food production licensing (SC), traceability and additive compliance. Production licences
are issued by category; traceability and additive use are the key regulatory focus. The checker
lays out licence details, traceability completeness and additive use — safety and fitness
verdicts belong only to qualified testing bodies and the regulator.

## Domain identity

| Item | Value |
|---|---|
| Domain ID | `food` (globally unique, never reused) |
| Domain name | Food · production licence & traceability |
| Profile version | `domain/1.0` |
| Status | `RESERVED` |
| Reserved since | 2026-09-12 |

## Attribute catalogue

| Key | Type | Meaning |
|---|---|---|
| `food.production_license` | enum | licensed/pending/expired/revoked/not_required |
| `food.product_category` | string | category as stated on the licence |
| `food.traceability_status` | enum | full/partial/absent |
| `food.additive_use` | enum | compliant/over_limit/out_of_scope/undeclared/unknown |
| `food.cold_chain_status` | enum | compliant/deviation_recorded/not_applicable |

## Red lines (machine-readable)

1. Food category and licence details follow the regulator-issued certificate; AI must not infer them.
2. Never output "edible", "safe", or "meets food-safety standards" conclusions.
3. Never suggest out-of-scope / over-limit additive use or test evasion; the test report from a qualified body is the only basis.

## The four-file access kit

| File | Role |
|---|---|
| `domain.manifest.json` | Domain declaration: attributes, issuer requirements, TTL, red lines |
| `gate-map.json` | Friction per action: silent / warn / confirm / block / require-owner |
| `privacy.json` | Privacy statement: off by default, minimization, withdrawable, erasable |
| `checker.io.json` | Checker MCP tool I/O contract — shows & verifies only, never judges |

## Quick Start

```bash
git clone https://github.com/SynomosAI/food-sc-license-checker.git
cd food-sc-license-checker

# Validate the four JSON files with the Python stdlib
python -m json.tool domain.manifest.json > /dev/null
python -m json.tool gate-map.json > /dev/null
python -m json.tool privacy.json > /dev/null
python -m json.tool checker.io.json > /dev/null
```

## Examples

```bash
# List declared attribute keys and types
python -c "import json;m=json.load(open('domain.manifest.json',encoding='utf-8'));[print(a['key'],a['type']) for a in m['attributes']]"
```

```json
{
  "subject_ref": "mpp:cn:9f2c1a7b",
  "attribute_keys": ["food.production_license", "food.traceability_status"],
  "evidence": ["tsa:2026-09-12#sha256:3b1f..."],
  "request_id": "req-20260912-0001"
}
```

The checker answers only with `shown / missing / expired / unverifiable` plus the
provenance chain. It never returns "edible", "safe", or food-safety compliance verdicts.

## Core principles

The platform is an arena, not a shelf. The checker answers only "is this claim verifiable,
and what prerequisite is missing" — never "is this compliant, should it be done".

## How to adopt

This domain is open to qualified operators: fork the repo, fill in `operator` and
`checker_endpoint`, align attributes and red lines with current rules, run the platform
self-checker (all five criteria must pass), then open a PR with credentials.

## License

Code and configuration are MIT-licensed. Documentation copyright remains with SynomosAI.
See [LICENSE](LICENSE).

© 2026 SynomosAI. All rights reserved.
