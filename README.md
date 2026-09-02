# cisochat

Een dirigent die de CISO helpt bij beleidsvragen en de weg wijst naar de juiste bron.

Status: concept. Ontwerp en documentatie; geen werkende code.

> Een AI-**dirigent** die redeneert als een CISO in de publieke sector: weegt af langs NIST CSF, grondt
> zich in de normen, adviseert, en stuurt open-source security-tooling aan. Adviserend - mens beslist.

[![Bijdragen](https://img.shields.io/badge/📝_Bijdragen-238636?style=for-the-badge)](../../issues/new/choose)&nbsp;&nbsp;&nbsp;&nbsp;[![Meepraten](https://img.shields.io/badge/💬_Meepraten-0969da?style=for-the-badge)](../../discussions)

👉 **Iets delen, feedback geven of een vraag stellen?** Klik op een van de knoppen hierboven - geen Git-ervaring nodig. Zie [CONTRIBUTING.md](CONTRIBUTING.md) voor meer opties.

## Voor wie

CISO's en ISO's bij publieke organisaties.

## Snel starten

Er is nog niets te draaien. Lees het ontwerp hieronder en denk mee via een issue.

## Bijdragen

Zie de [CONTRIBUTING](https://github.com/security-commons-nl/.github/blob/main/CONTRIBUTING.md) van de organisatie: daar staat per project een formulier, ook zonder Git-ervaring.

## Licentie

EUPL-1.2, zie [LICENSE](LICENSE).

## Wat het is
Een CISO doet veel meer dan vragen beantwoorden: strategie en beleid, risico, compliance, threat,
incident response en continuïteit. cisochat bootst die volle breedte na als een **dirigent, geen doos** -
het redenerende CISO-brein dat langs **NIST CSF 2.0** (Govern · Identify · Protect · Detect · Respond ·
Recover) afweegt, zich grondt in de normenkaders (BIO 2.0, ISO 27001/27701/22301, AVG, EU AI Act) via
RAG, en het juiste open-source instrument aanstuurt - of, waar geen volwassen tooling bestaat, zelf
adviseert. Lokaal of EU-gehost, geen data buiten de EU, auditbaar by design.

De oorspronkelijke chat-met-een-CISO-persona blijft één capability binnen dit geheel; de bredere visie is
een vCISO-orkestratielaag.

## Positionering binnen Security Commons NL
Security Commons NL is een verzameling **instrumenten** - elk project doet één security-taak goed (GRC/ISMS,
posture-meting, dreigings- en kill-chain-analyse, beleidsondersteuning, weerbaarheidstraining, een kennisbank).

cisochat is geen extra instrument in die rij, maar de **dirigent**: het CISO-brein dat *eroverheen* denkt.
Het is **standalone bruikbaar** (orkestreert externe open-source tooling + zijn eigen advies-brein) en
**complementair** aan de rest - geen harde afhankelijkheid, wel rijkere instrumenten naarmate je meer
Commons-tooling draait. Kort: *waar de andere projecten elk één taak uitvoeren, denkt cisochat eroverheen.*

## Capability: beleidsondersteuning
Het voormalige project `beleid-assistent` (AI-ondersteuning voor beleidsmedewerkers en juristen bij het
opstellen van en toetsen aan beveiligingsbeleid, langs BIO2-controls) is op 28-08-2026 in cisochat opgegaan.
Twee concepten met dezelfde stack en nul code naast elkaar houden kost meer dan het oplevert; binnen de
vCISO-blueprint is beleidsondersteuning één van de capabilities onder de CSF-functie Govern.

- [Concept beleidsondersteuning](docs/capabilities/beleidsassistent/concept.md): wat het is, voor wie, hoe het werkt
- [Architectuur beleidsondersteuning](docs/capabilities/beleidsassistent/architectuur.md): de vijf agents en hun samenspel
- [`data/bio2.json`](data/bio2.json): 148 BIO2-controls (v1.3). **Sinds 02-09-2026 is de repo
  [`normen`](https://github.com/security-commons-nl/normen) de gedeelde normenbron**, zonder de ISO-tekst;
  dit bestand blijft hier staan tot de laatste afnemer is omgezet en wordt niet meer bijgewerkt
  voor deze capability en voor de normen-grounding van de dirigent
- [`data/domeinen.json`](data/domeinen.json): beleidsdomeinen die BIO2-controls groeperen per beleidsdocument (ook overgenomen in `normen` als `bio2-domeinen.json`)

## Meer lezen
- [vCISO-blueprint](docs/vciso/vciso-blueprint.md) - **vastgesteld**: OSS-landschap per CSF-functie, capability-map, gap-analyse, orkestratie-ontwerp en roadmap
- [Architectuurplaat (interactief)](docs/vciso/architectuur.html) - visuele weergave: hoe een vraag stroomt · gelaagde architectuur · CSF-capability-map
- [Ontwerp & blueprint-opzet](docs/vciso-blueprint-ontwerp.md) - de architectuurkeuze (dirigent boven tools/skills/OSS)
- [Onderzoek per CSF-functie](docs/vciso/research/) - de onderbouwde sweeps met bron-URL's
- [Oorspronkelijk concept](docs/concept.md) - de eerste (smallere) RAG-chatbot-opzet
- [Bijdragen](https://github.com/security-commons-nl/.github/blob/main/CONTRIBUTING.md)

## Status
**Concept / blueprint-fase.** De blueprint (open-source-onderzoek + architectuur + roadmap) is *vastgesteld*,
maar er is **nog géén code gebouwd**. De bouw start met Fase A (fundament: grounding-laag, capability-router,
deterministische routing-gate + auditspoor). Bijdragen welkom - zowel technisch als inhoudelijk.

## Principes
Dit project volgt de [architectuur- en communityprincipes](https://github.com/security-commons-nl/.github/blob/main/PRINCIPLES.md) van security-commons-nl: EU-soevereiniteit, AI altijd adviserend, auditbaarheid by design, least privilege en open source als standaard.
