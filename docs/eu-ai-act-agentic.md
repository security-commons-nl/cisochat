# EU AI Act & Agentic AI — Kennisbank

> Kennisbank-entry voor cisochat. Gebruik als RAG-bron bij vragen over EU AI Act compliance en Zero Trust voor AI-agents in gemeentelijke context.

---

## EU AI Act: Wat betekent het voor gemeenten?

### Kernprincipe: Risicoclassificatie

De EU AI Act verdeelt AI-systemen in vier categorieën:

| Categorie | Omschrijving | Gemeentelijk voorbeeld |
|-----------|-------------|----------------------|
| **Verboden** | AI-praktijken die fundamenteel rechten schenden | Social scoring op basis van gedrag |
| **Hoog-risico** | AI in kritieke sectoren met strenge eisen | Beslissingsondersteunende AI bij uitkeringen, handhaving |
| **Beperkt risico** | Transparantieverplichtingen | Chatbots die als mens kunnen doorgaan |
| **Minimaal risico** | Geen specifieke verplichtingen | Spamfilters, spellingscorrectie |

**Cruciale regel voor gemeenten:** AI-systemen in de publieke sector vallen **bijna automatisch** in de hoog-risico categorie. Dit betekent dat de gemeente voor elk AI-systeem een conformiteitsbeoordeling moet uitvoeren.

### Tijdlijn (fasering EU AI Act)

| Datum | Verplichting |
|-------|-------------|
| Augustus 2024 | Verboden AI-praktijken van kracht |
| Augustus 2025 | GPAI-model verplichtingen + governance (art. 4) |
| Augustus 2026 | Hoog-risico systemen: volledige compliance verplicht |
| Augustus 2027 | Hoog-risico systemen geïmplementeerd vóór 2026 onder nieuwe regels |

**Advies:** Start nu met de AI-inventarisatie. Wacht niet op 2026 — de registratie- en beoordelingsprocessen kosten tijd.

### Verplichtingen voor hoog-risico AI-systemen

Als CISO/FG ben je betrokken bij de volgende verplichtingen:

1. **AI-register**: Catalogiseer alle AI-systemen, classificeer per risicoprofiel
2. **Conformiteitsbeoordeling**: Per hoog-risico systeem een formele beoordeling
3. **Technische documentatie**: Architectuur, trainingsdata, prestatielimieten
4. **Logging**: Automatische logboeken van de werking (audit trail)
5. **Transparantie**: Gebruikers informeren dat ze met AI werken
6. **Menselijk toezicht**: Mechanismen voor menselijk ingrijpen
7. **Nauwkeurigheid, robuustheid, cybersecurity**: Technische eisen aan het systeem

### Overlap met AVG/GDPR

De EU AI Act werkt naast de AVG, niet in plaats ervan:

| AVG | EU AI Act |
|-----|-----------|
| DPIA verplicht bij hoog risico voor persoonsgegevens | Conformiteitsbeoordeling verplicht bij hoog-risico AI |
| Verwerkingsregister | AI-systemenregister |
| Data Protection Officer (FG) | AI-verantwoordelijke (nieuw) |
| Recht op uitleg bij geautomatiseerde beslissingen | Menselijk toezicht + transparantie |

**Praktisch:** Als je al een DPIA doet voor een AI-systeem dat persoonsgegevens verwerkt, combineer dit met de EU AI Act-conformiteitsbeoordeling. Er is grote overlap.

---

## Zero Trust voor AI-agents

### Waarom traditionele security niet volstaat

AI-agents zijn geen passieve tools. Ze:
- Handelen **autonoom** namens gebruikers en systemen
- Hebben toegang tot **meerdere systemen** tegelijk
- Voeren acties uit met **echte impact** (mailen, opslaan, aanvragen)
- Zijn **moeilijk te voorspellen** in hun gedrag

Traditionele perimeter-gebaseerde security — "vertrouw alles binnen het netwerk" — is onvoldoende.

### Zero Trust principes voor AI-agents

**1. Never trust, always verify**
Elke actie van een AI-agent wordt geauthenticeerd en geautoriseerd, ook intern. Geen impliciete vertrouwensrelaties.

**2. Least privilege**
Agents krijgen alleen de minimale rechten nodig voor de **specifieke, huidige taak** — niet voor het hele systeem of alle denkbare taken.

**3. Micro-segmentation**
Agents opereren in geïsoleerde omgevingen met beperkte netwerktoegang. Ze kunnen niet zomaar met andere systemen communiceren.

**4. Continuous monitoring**
Alle agent-acties worden gelogd en geanalyseerd. Afwijkend gedrag triggert alerting.

**5. Identity-centric**
Elke agent heeft een unieke digitale identiteit (machine identity) — geen gedeelde accounts of API-keys.

### Praktische implementatie voor gemeenten

```
Stap 1: Inventariseer alle AI-agents in gebruik
  → Welke systemen handelen autonoom namens de gemeente?
  → Wat zijn hun rechten?
  → Wie is eigenaar/verantwoordelijke?

Stap 2: Definieer minimale rechten per use case
  → Welke systemen heeft de agent echt nodig?
  → Welke acties mag de agent uitvoeren?
  → Wanneer is menselijke goedkeuring verplicht?

Stap 3: Implementeer audit trails
  → Log elke agent-actie: wie, wat, wanneer, waarom
  → Maak logs onveranderlijk (immutable)
  → Koppel logs aan de identiteit van de agent

Stap 4: Definieer escalatiepaden
  → Wanneer stopt de agent en vraagt een mens?
  → Wie is de menselijke toezichthouder?
  → Hoe snel wordt ingegrepen bij afwijkend gedrag?
```

### Agentic AI & EU AI Act: combinatie

Zero Trust voor AI-agents is geen optionele best practice — het is een **vereiste** vanuit de EU AI Act voor hoog-risico systemen:

| EU AI Act vereiste | Zero Trust implementatie |
|-------------------|------------------------|
| Menselijk toezicht (art. 14) | Escalatiepaden + HITL-checkpoints |
| Logging & monitoring (art. 12) | Immutable audit logs per agent-actie |
| Cybersecurity (art. 15) | mTLS, JIT-toegang, micro-segmentatie |
| Transparantie (art. 13) | Audit trail beschikbaar voor gebruikers |

---

## Vragen die cisochat kan beantwoorden

Met deze kennisbankentry kan cisochat vragen beantwoorden zoals:

- "Valt onze AI-chatbot voor meldingen onder de EU AI Act? Hoog-risico of niet?"
- "We willen een AI-agent inzetten voor documentverwerking. Welke Zero Trust maatregelen zijn minimaal vereist?"
- "Hoe combineer ik de EU AI Act-conformiteitsbeoordeling met onze bestaande DPIA-procedure?"
- "Een leverancier zegt dat hun AI-systeem 'compliant' is. Welke vragen moet ik stellen?"
- "Moeten we een AI-register bijhouden? Wat moet er in?"

---

## Referenties

- EU AI Act (Verordening 2024/1689) — officiële tekst
- [ENISA — AI Threat Landscape](https://www.enisa.europa.eu/publications/enisa-threat-landscape-for-ai) — dreigingslandschap AI
- [IBD — Handreiking AI Governance voor gemeenten](https://www.informatiebeveiligingsdienst.nl/) — IBD publicaties
- BIO 2.0 — Baseline Informatiebeveiliging Overheid, maatregel 18 (toeleveranciersrisico's), relevant voor AI-leveranciers
- Zie `architectuur.md` voor technische implementatie van cisochat
