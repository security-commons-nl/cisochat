# cisochat

> Een AI-**dirigent** die redeneert als een CISO in de publieke sector: weegt af langs NIST CSF, grondt
> zich in de normen, adviseert, en stuurt open-source security-tooling aan. Adviserend — mens beslist.

[![Bijdragen](https://img.shields.io/badge/📝_Bijdragen-238636?style=for-the-badge)](../../issues/new/choose)&nbsp;&nbsp;&nbsp;&nbsp;[![Meepraten](https://img.shields.io/badge/💬_Meepraten-0969da?style=for-the-badge)](../../discussions)

👉 **Iets delen, feedback geven of een vraag stellen?** Klik op een van de knoppen hierboven — geen Git-ervaring nodig. Zie [CONTRIBUTING.md](CONTRIBUTING.md) voor meer opties.

## Wat het is

Een CISO doet veel meer dan vragen beantwoorden: strategie en beleid, risico, compliance, threat,
incident response en continuïteit. cisochat bootst die volle breedte na als een **dirigent, geen doos** —
het redenerende CISO-brein dat langs **NIST CSF 2.0** (Govern · Identify · Protect · Detect · Respond ·
Recover) afweegt, zich grondt in de normenkaders (BIO 2.0, ISO 27001/27701/22301, AVG, EU AI Act) via
RAG, en het juiste open-source instrument aanstuurt — of, waar geen volwassen tooling bestaat, zelf
adviseert. Lokaal of EU-gehost, geen data buiten de EU, auditbaar by design.

De oorspronkelijke chat-met-een-CISO-persona blijft één capability binnen dit geheel; de bredere visie is
een vCISO-orkestratielaag.

## Positionering binnen Security Commons NL

Security Commons NL is een verzameling **instrumenten** — elk project doet één security-taak goed (GRC/ISMS,
posture-meting, dreigings- en kill-chain-analyse, beleidsondersteuning, weerbaarheidstraining, een kennisbank).

cisochat is geen extra instrument in die rij, maar de **dirigent**: het CISO-brein dat *eroverheen* denkt.
Het is **standalone bruikbaar** (orkestreert externe open-source tooling + zijn eigen advies-brein) en
**complementair** aan de rest — geen harde afhankelijkheid, wel rijkere instrumenten naarmate je meer
Commons-tooling draait. Kort: *waar de andere projecten elk één taak uitvoeren, denkt cisochat eroverheen.*

## Meer lezen

- [vCISO-blueprint](docs/vciso/vciso-blueprint.md) — **vastgesteld**: OSS-landschap per CSF-functie, capability-map, gap-analyse, orkestratie-ontwerp en roadmap
- [Ontwerp & blueprint-opzet](docs/vciso-blueprint-ontwerp.md) — de architectuurkeuze (dirigent boven tools/skills/OSS)
- [Onderzoek per CSF-functie](docs/vciso/research/) — de onderbouwde sweeps met bron-URL's
- [Oorspronkelijk concept](docs/concept.md) — de eerste (smallere) RAG-chatbot-opzet
- [Bijdragen](https://github.com/security-commons-nl/.github/blob/main/CONTRIBUTING.md)

## Status

**Concept / blueprint-fase.** De blueprint (open-source-onderzoek + architectuur + roadmap) is *vastgesteld*,
maar er is **nog géén code gebouwd**. De bouw start met Fase A (fundament: grounding-laag, capability-router,
deterministische routing-gate + auditspoor). Bijdragen welkom — zowel technisch als inhoudelijk.

---

## Principes

Dit project volgt de [architectuur- en communityprincipes](https://github.com/security-commons-nl/.github/blob/main/PRINCIPLES.md) van security-commons-nl: EU-soevereiniteit, AI altijd adviserend, auditbaarheid by design, least privilege en open source als standaard.
