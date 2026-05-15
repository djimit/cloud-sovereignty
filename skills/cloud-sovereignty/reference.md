# Cloud Sovereignty — Reference

## Wettelijke grondslagen

### CLOUD Act (H.R. 4943, 2018)

De Clarifying Lawful Overseas Use of Data Act wijzigt de Stored Communications Act (18 U.S.C. § 2703) door:

1. Toevoegen van § 2703(h): comity-analyse voor buitenlandse dataverzoeken
2. Schrappen van het "data lokalisatie"-verweer: locatie van data is niet langer relevant
3. Invoeren van executive agreements (Art. 2523) voor directe data-toegang met "qualifying foreign governments" (VK, Australië)

### FISA Section 702 (50 U.S.C. § 1881a)

- Ingesteld in 2008 via FISA Amendments Act
- Vernieuwd in 2024 (RISAA Act, H.R. 7888) tot december 2025
- Target: niet-Amerikanen buiten de VS voor foreign intelligence
- Vereist FISA Court-goedgekeurde certificeringen (geen individuele warrants)
- PRISM: upstream collection via directe toegang tot provider-infrastructuur
- EO 12333: parallelle executieve collectieautoriteit zonder FISA Court-toezicht

### AVG Art. 48 — Verbod op directe buitenlandse toegang

"Een rechterlijke uitspraak of beslissing van een administratieve autoriteit van een derde land die vereist dat een verwerkingsverantwoordelijke of verwerker persoonsgegevens doorgeeft of openbaar maakt, kan op geen enkele wijze worden erkend of afdwingbaar gemaakt, tenzij deze is gebaseerd op een internationale overeenkomst (zoals een verdrag inzake wederzijdse rechtshulp) [...]"

### NIS2 Art. 21(2)(c) — Supply Chain Security

"De maatregelen omvatten ten minste: [...] beveiliging van de toeleveringsketen, inclusief veiligheidsgerelateerde aspecten betreffende de relaties tussen elke entiteit en haar rechtstreekse leveranciers of dienstverleners"

## EU-rechtelijke mijlpalen

| Jaar | Uitspraak / Besluit | Impact op cloud |
|------|--------------------|-----------------|
| 2015 | **Schrems I** (C-362/14) | Safe Harbor ongeldig verklaard |
| 2020 | **Schrems II** (C-311/18) | Privacy Shield ongeldig; SCC's blijven maar vereisen aanvullende waarborgen |
| 2022 | **Executive Order 14086** | Biden EO ter vervanging van Privacy Shield-basis; leidde tot EU-US DPF |
| 2023 | **EU-US DPF** aangenomen | Nieuw adequaatheidsbesluit, maar fundamentele FISA/CLOUD Act problemen niet opgelost |
| 2025 | **Schrems III** dreiging | NOYB heeft bezwaren aangekondigd tegen DPF |
| 2026 | **EUCS onderhandelingen** | Lidstaten discussiëren over soevereiniteitseisen in 'High' niveau |

## NL Government Cloud Contracts Framework

### GIBIT (Gemeentelijke Inkoopvoorwaarden bij IT)

Gemeentelijke standaardvoorwaarden voor IT-contracten. Cloud-specifieke elementen:

- Art. 11: continuïteit en exit
- Art. 14: gegevensbescherming en beveiliging
- Art. 17: audit- en controlerechten
- Art. 26: toepasselijk recht en geschillen (Nederlands recht, Nederlandse rechter)

### AGIBIT (Algemene Gemeentelijke Inkoopvoorwaarden bij IT)

Vernieuwde versie van GIBIT, meer cloud-native.

## Technical Deep Dive

### CLOUD Act Comity-analyse factoren (18 U.S.C. § 2703(h)(2))

Bij betwisting door provider beoordeelt de rechter:

1. **VS-belang**: Het belang van de VS bij de gevraagde data (strafrechtelijk onderzoek)
2. **Buitenlands belang**: Het belang van het buitenland in privacybescherming van de data
3. **Nationaliteit**: De nationaliteit en locatie van de data subject
4. **Alternatieven**: Beschikbare diplomatieke kanalen (MLA: Mutual Legal Assistance)
5. **Conflict**: Waarschijnlijkheid en ernst van wettelijk conflict met buitenlands recht

### Encryptie-architectuur tegen CLOUD Act

Effectiviteit van encryptiestrategieën:

| Strategie | Effectiviteit | Toelichting |
|-----------|---------------|-------------|
| **Server-side encryption** (cloud provider keys) | Geen | Provider heeft sleutels → data is "onder control" |
| **BYOK** (Bring Your Own Key) | Beperkt | Provider heeft technisch toegang tot keyserver; operationele barrière maar geen juridische |
| **HYOK** (Hold Your Own Key, extern HSM) | Goed | Sleutels fysiek in eigen datacenter; provider kan niet ontsleutelen |
| **Client-side E2E encryption** (zero-knowledge) | Zeer goed | Data verlaat client al versleuteld; provider heeft nooit plaintext |
| **Air-gapped + FIPS 140-3 HSM** | Best | Fysieke scheiding, FIPS-gecertificeerde sleutelopslag |

### Netwerkbeveiliging tegen surveillance

| Maatregel | Beschermt tegen |
|-----------|-----------------|
| **Mutual TLS** (mTLS) tussen EU componenten | Trans-Atlantische interceptie van inter-service communicatie |
| **DNS over HTTPS/TLS** met EU-resolvers | DNS-monitoring en -manipulatie |
| **EU-only BGP peering** | Traffic hair-pinning via VS-netwerken |
| **EU-to-EU private connectivity** (AWS PrivateLink, Azure Private Link in EU-regio) | Data in transit over US netwerken |
| **Europese transit-providers** | VS-gebaseerde Tier 1 carrier monitoring |

## Key Vendors Deep-Dive

### Microsoft Azure / M365 Sovereign Opties

| Product | Claim | Realiteit |
|---------|-------|-----------|
| **EU Data Boundary** | Data blijft in EU | Juiste data-residentie; maar Microsoft US heeft nog steeds technische toegang ("managed access") |
| **Customer Lockbox** | Klant keurt Microsoft toegang goed | Alleen voor support-engineering; geen barrière tegen CLOUD Act warrant |
| **Double Key Encryption** | Klant houdt één sleutel | Theoretisch sterker, maar key wordt overgedragen aan M365 voor operatie |
| **Microsoft Cloud for Sovereignty** | Sovereign "policy guardrails" | Policy layer, geen jurisdictie-verandering; Microsoft Inc. blijft US entiteit |

**Conclusie:** Microsoft's soevereiniteitsclaims zijn datasovereign (locatie) maar niet jurisdictie-sovereign (wettelijk). De US ultimate parent blijft het fundamentele risico.

### AWS European Sovereign Cloud

AWS kondigde in 2023 een "European Sovereign Cloud" aan (Duitsland, 2025 operationeel):

- Fysiek en logisch gescheiden van commerciële AWS regions
- Beheerd door EU-gevestigd personeel
- Eerste region: Brandenburg, Duitsland
- **MAAR:** AWS Inc. (US) blijft de ultimate parent; data valt nog steeds onder "possession, custody, or control" van een US entiteit.

### Google Cloud Sovereign Controls

- Sovereign Controls pakket: data residency, encryptie, access transparency
- **MAAR:** Google LLC (US) = ultimate parent; geen jurisdictie-oplossing.

## Bronnen

- [CLOUD Act Full Text](https://www.congress.gov/bill/115th-congress/house-bill/4943/text)
- [FISA Section 702 Overview (CRS)](https://crsreports.congress.gov/product/pdf/IF/IF12682)
- [EPIC — FISA 702](https://epic.org/fisa-section-702/)
- [EU-US Data Privacy Framework](https://www.dataprivacyframework.gov/)
- [ENISA — EUCS](https://www.enisa.europa.eu/topics/cybersecurity-certification/cloud-services)
- [Schrems II — CJEU C-311/18](https://curia.europa.eu/juris/liste.jsf?num=C-311/18)
- [BZK — Overheidscloudbeleid](https://www.digitaleoverheid.nl/overzicht-van-alle-onderwerpen/cloud/)
- [GAIA-X Architecture](https://docs.gaia-x.eu/)
- [NOYB — Cloud & Privacy](https://noyb.eu/)
- [BIO2 Cloud Measure 5.23](https://www.bio-overheid.nl/)
