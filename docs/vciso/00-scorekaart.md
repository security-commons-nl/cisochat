# vCISO OSS-scorekaart & onderzoeksprotocol

> Standaardiseert elke open-source-toolbeoordeling in het vCISO-onderzoek. Elke tool in de
> research/-bestanden MOET alle velden ingevuld hebben, met minstens één bron-citaat per claim.

## Beoordelingsvelden (per tool)

| Veld | Toelichting | Schaal/format |
|---|---|---|
| Naam + URL | Projectnaam en canonieke repo/site | tekst + link |
| CSF-functie(s) | Welke van Govern/Identify/Protect/Detect/Respond/Recover | enum |
| Capability | Welke vCISO-capability het invult | tekst |
| Korte omschrijving | Wat het doet, in 1–2 zinnen | tekst |
| Rijpheid | Onderhoud: laatste release, commit-activiteit, contributors | hoog / midden / laag + onderbouwing |
| Licentie | SPDX-identifier + copyleft-implicatie voor open-core | tekst |
| EU-soevereiniteit | Zelf-hostbaar? Data buiten EU nodig? (zachte weging, zie rubriek) | ja/nee + toelichting |
| Integreerbaarheid | API / MCP / CLI / library; koppelbaar aan een dirigent? | enum + toelichting |
| AI-native koppelbaarheid | LLM-/agent-vriendelijk? MCP-server, schone API, gestructureerde output? | ja/deels/nee + toelichting |
| Stack/taal | Implementatietaal en runtime-eisen | tekst |
| Fit-score | Geschiktheid als vCISO-orgaan | 1–5 + 1 zin motivatie |
| Bronnen | Citaten die de bovenstaande claims dekken | links |

## Harde poort — open source only
Alleen écht open-source software komt in de findings. **Geen commerciële/proprietary tools.** Bij
**open-core** projecten (gratis community-editie + betaalde editie): beoordeel uitsluitend de
open-source community-editie, en noteer expliciet welke vCISO-relevante functies achter de betaalde
muur zitten. Puur-commerciële tools vallen volledig af (niet opnemen).

## Fit-score-rubriek (1–5)
- **5** — rijp, permissieve licentie, EU-soeverein/zelf-hostbaar, schone + AI-native integratie (MCP/API), actief onderhouden.
- **3** — bruikbaar maar met één serieus bezwaar (bv. copyleft dat open-core bemoeilijkt, zwakke/niet-AI-native API, of non-EU/SaaS-afhankelijkheid).
- **1** — bestaat, maar niet praktisch integreerbaar of niet onderhouden.
- **EU-weging (zacht):** non-EU of SaaS-only OSS mag opgenomen worden als het toonaangevend is, maar
  krijgt een expliciete waarschuwing en een lagere fit-score dan een vergelijkbaar EU-soeverein/zelf-hostbaar alternatief.

## Onderzoeksprotocol
1. Per CSF-functie een aparte deep-research-sweep (multi-source, fact-checked), plus één cross-cutting
   sweep naar bestaande AI-vCISO/"CISO-in-a-box"/GRC-copilot OSS-projecten (Taak 6b).
2. Breedte: elke sweep dekt zowel **governance/management**-tooling (GRC, ISMS, beleid, risk,
   rapportage) als **technische** tooling — niet alleen scanners.
3. Startbronnen: awesome-lists (bv. awesome-security, awesome-selfhosted), OWASP-projectenlijst,
   CNCF/Linux Foundation-landscapes, GitHub-topics, en onafhankelijke reviews — geen vendor-marketing
   als enige bron.
4. Elke tool-claim heeft minstens één onafhankelijk citaat. Onzekerheid expliciet benoemen.
5. Minimaal-volledigheid per functie: streef naar de relevante categorieën gedekt (niet één tool per
   functie). Bewust loggen wat NIET gevonden/gedekt is → voedt de gap-analyse.
6. Curatie: de sweeps zoeken breed (diep & breed), maar de blueprint (Taak 7) cureert per sub-categorie
   tot de top 2–3 volwaardige scorekaart-entries; de overige gevonden tools worden als "long tail" bij
   naam + URL genoemd, zonder volledige scorekaart.
7. Muur: geen proprietary/organisatie-specifieke bronnen of -IP in de open-source findings.
