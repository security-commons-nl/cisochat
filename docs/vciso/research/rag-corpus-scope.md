# RAG-corpus-scope (vCISO)

> Harde inventaris van welk normatief materiaal de RAG-grounding voedt: wat ligt klaar in Commons,
> wat ontbreekt, en de copyright-vorm per kader. Input voor sub-project 2 (Fase A: dirigent-skelet).
> Read-only geinventariseerd 30-06-2026 (alleen `X:/SECURITY-COMMONS-NL`; WERK-tenant + LIVIQ bewust
> buiten scope, muur). Bron: ATLAS-balie.

## Gouden regel (copyright)
Herverspreid **samenvattingen/mappings in eigen woorden**, nooit volledige NEN/ISO-normteksten.
Publieke wetgeving (AVG, EU AI Act, NIS2, NIST) mag vrij worden opgenomen.

## Status per kader

| Kader | In Commons? | Pad | Vorm | RAG-bruikbaar | Copyright |
|-------|-------------|-----|------|---------------|-----------|
| BIO 2.0 | ja | `beleid-assistent/data/bio2.json` | gestructureerde JSON, 300+ controls | ✅ direct | ⚠️ CIP-bron, licentie checken |
| EU AI Act | ja | `grc-platform/docs/eu-ai-act-classification.md` + classifier + `cisochat/docs/eu-ai-act-agentic.md` | docs + deterministische classifier | ✅ direct | ✅ publiek (EU-wet) |
| AVG/GDPR | deels | metadata `grc-platform/.../003_seed_reference_data.py` | metadata; tekst nog niet geingest | ⚠️ tekst toevoegen | ✅ publiek |
| NIST CSF 2.0 | research-only | `cisochat/docs/vciso/research/*.md` | OSS-research per functie, geen normcorpus | ❌ skelet maken | ✅ publiek |
| ISO 27001:2022 | metadata | `grc-platform/.../003_seed_reference_data.py` (`ims_standards`) | alleen metadata | ❌ alleen mappings | 🚩 NEN-copyright |
| ISO 27701 | metadata | idem (domain PIMS) | alleen metadata | ❌ alleen mappings | 🚩 NEN-copyright |
| ISO 22301 | metadata | idem (domain BCMS) | alleen metadata | ❌ alleen mappings | 🚩 NEN-copyright |
| NIS2 / Cbw | nee | — | — | ❌ betrekken | ✅ publiek |
| IBD-richtlijnen | nee | — | — | ❌ samenstellen | publiek (CIP/IBD) |
| NIST AI RMF 1.0 | in voorbereiding | `grc-platform/.../011_nist_ai_rmf.py` | metadata (toekomstig) | 🔄 na grc-platform Fase 2 | ✅ publiek |

## Klaar voor RAG (nu)
- BIO 2.0 (`beleid-assistent/data/bio2.json`)
- EU AI Act (`grc-platform/docs/eu-ai-act-classification.md` + `cisochat/docs/eu-ai-act-agentic.md`)

## Moet nog gemaakt/betrokken
- **NIST CSF 2.0-skelet** (kapstok; eigen woorden, per functie/categorie/subcategorie) <- kritieke maakklus, eerst.
- AVG volledige tekstfragmenten ingesten (artikel-nummering, publiek).
- NIS2/Cbw samenvatting (NL-context, zodra ontwerp finaal).
- ISO 27001/27701/22301: **mappings/samenvattingen** (geen normtekst).
- IBD-handreikingen per onderwerp.
- NIST AI RMF (volgt grc-platform alembic-011).

## Synergie / hergebruik
- `grc-platform` heeft al een normenkader-datamodel (`ims_standards` / `ims_requirements`). cisochat hoeft
  dat niet te dupliceren: hergebruiken als structuur/bron, en grc-platform is een logische
  **delegatie-target** voor de capability-router (GRC/compliance-functie).

## Conclusie voor Fase 1
RAG is **geen blocker** voor de MVP zolang de scope = **BIO 2.0 + EU AI Act + zelfgeschreven NIST CSF 2.0-skelet**.
Dat dekt de NL-norm, de AI-wet en de redeneer-kapstok. De rest is Fase 2-uitbreiding.

## Gerelateerd
- `ai-agent-security-bronnen-2026-06.md` · `xorcism-hergebruik-afweging.md` · `vciso-blueprint.md` (Fase A)
