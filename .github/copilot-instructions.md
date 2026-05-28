# Copilot Instructions — cloud-sovereignty

> See root `.github/copilot-instructions.md` for global conventions.

Claude Code plugin voor **CLOUD Act blootstellingsanalyse en digitale soevereiniteit**. Identificeert Amerikaanse jurisdictierisico's in cloud-architecturen, analyseert dataflows op extraterritoriale toegang, en adviseert BIO2-conforme soevereine alternatieven.

## Structure

```
.claude-plugin/plugin.json    # Plugin metadata (name, description, version, keywords)
skills/cloud-sovereignty/
  SKILL.md                    # Skill definition — triggers, model config, scope
  reference.md                # Reference material — cloud classificatie, vendor assessment
```

## Installation

```bash
claude install djimit/cloud-sovereignty
```

## Typical Usage

- **Jurisdictierisico-analyse** — Toets cloud-architecturen op CLOUD Act, FISA 702, Patriot Act, EO 12333
- **Cloud classificatie** — Classificeer diensten volgens BZK CIO-Rijk cloudbeleid
- **Vendor assessment** — Voer due diligence uit op hyperscalers en SaaS-leveranciers
- **Soevereine alternatieven** — Adviseer over GAIA-X, SecNumCloud, EUCS, EU-sovereigne clouds
- **DPIA cloud** — Koppel cloud-soevereiniteitsrisico's aan AVG DPIA's

## Domain Keywords

CLOUD Act, FISA 702, digitale soevereiniteit, cloud governance, jurisdictierisico, extraterritoriale toegang, data residency, data lokalisatie, vendor lock-in, hyperscaler risico, GAIA-X, SecNumCloud, EUCS, European Cybersecurity Certification, BBN cloud, Schrems, Data Privacy Framework, DPF, DPIA cloud

## License

MIT (see `plugin.json`)
