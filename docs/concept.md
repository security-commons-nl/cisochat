# cisochat — Concept

> Een AI-assistent die redeneert vanuit het perspectief van een CISO in de publieke sector.

---

## Het probleem

Een CISO bij een gemeente heeft dagelijks vragen die niet met een Google-zoekopdracht beantwoord worden:

- "Moeten wij als gemeente een DPIA uitvoeren voor dit systeem, of valt het onder de bestaande register?"
- "Hoe weeg ik een BIO-maatregel die technisch niet haalbaar is af tegen het restrisico?"
- "Een wethouder vraagt of we compliant zijn. Wat antwoord ik?"

ChatGPT geeft algemene antwoorden. Consultants geven dure antwoorden. Collega-CISO’s zijn niet altijd bereikbaar.

cisochat geeft antwoorden vanuit het perspectief van een ervaren CISO in de Nederlandse publieke sector — inclusief de afwegingen, de nuances, en de beperkingen.

---

## Wat het is

Een lokaal draaiende chat-interface met een CISO-persona. De assistent:

- Kent de Nederlandse normenkaders: BIO 2.0, ISO 27001, ISO 27701, ISO 22301, AVG
- Redeneert vanuit gemeentelijke context (DigiD, ENSIA, IBD, VNG, CISO-rol in gemeentelijke governance)
- Geeft advies met onderbouwing — inclusief wat er óók voor pleit en wat de risico’s zijn
- Is transparant over onzekerheid: "dit hangt af van..." is een valide antwoord
- Besluit nooit namens jou — adviseert altijd, beslist nooit

---

## Wat het niet is

- Geen juridisch advies
- Geen vervanging van een echte CISO of FG
- Geen generieke chatbot die toevallig over security gaat
- Geen systeem dat externe data verzendt

---

## Technische richting

**Kerncomponenten:**

| Component | Invulling |
|-----------|-----------|
| Taalmodel | Lokaal via Ollama (Mistral of vergelijkbaar) |
| Kennisbank | RAG op normatieve documenten (BIO 2.0, ISO-normen, AVG-tekst, IBD-richtlijnen) |
| Persona | Systeem-prompt die de CISO-rol, context en redeneerwijze definieert |
| Interface | Eenvoudige chat-UI, standalone of ingebouwd in grc-platform |
| Hosting | Lokaal of EU-gehost — geen data buiten de EU |

**RAG-aanpak:**

De assistent haalt bij elke vraag relevante passages op uit de kennisbank (vectordatabase met normatieve teksten), voegt die toe aan de context, en genereert een antwoord dat gegrond is in de daadwerkelijke normen — niet in trainingsdata van twee jaar geleden.

**Integratie met grc-platform:**

Op termijn kan cisochat context ophalen uit het GRC-platform van de eigen organisatie: "Gezien jullie huidige risicoprofiel en open controls..." Dat is fase 2.

---

## Gebruik

**Standalone:** CISO opent de chat, stelt een vraag, krijgt antwoord met bronverwijzing naar de relevante norm.

**Ingebouwd:** Vanuit het grc-platform een vraag stellen over een specifiek risico of control — de assistent heeft die context al.

**Kennisdeling:** Interessante gesprekken (geanonimiseerd) kunnen worden bijgedragen aan de kennisbank van security-commons-nl.

---

## Status

Concept-fase. Bijdragen welkom — zowel aan de technische uitwerking als aan de kennisbank (normatieve documenten, CISO-redeneerpatronen, use cases).

Zie [CONTRIBUTING.md](https://github.com/security-commons-nl/.github/blob/main/CONTRIBUTING.md) voor hoe je kunt bijdragen.
