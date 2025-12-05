# The DFH Semantic Grounding Installation Guide
This is the modern implementation of Berners-Lee’s original Semantic Web map.”


The Transport Layer (TCP/IP) → moves packets

The Hyperlink Layer (HTTP/HTML) → shows documents

The Meaning Layer (DFH/Stack) → tells AI what those documents mean
 
The official installation & deployment guide for DFH (Deterministic First-Hop) — The public semantic grounding layer for AI and search. Includes spec, examples, validator, and a one-command installer.
the public semantic grounding layer for AI and search.

Learn how to:

- publish the `/.well-known/stack` file  
- configure the **Five Anchors** (`type`, `entity`, `url`, `sitemap`, `canonical`)  
- validate your DFH descriptor  
- ship a compliant **Semantic Stack Root** in minutes

---

## The Semantic Stack & Deterministic First-Hop (DFH)

A simple, decentralized semantic layer for the public web  
+ the strongest SEO primitive ever created.

- **Status:** Public Concept  
- **Version:** Draft v1.0  
- **Date:** 2025-11-23  
- **License:** MIT  

DFH defines a tiny, external, domain-based semantic layer that gives AI and search systems a **consistent first-hop** for any topic.

> **“DFH is DNS for meaning.”**

DFH is intentionally minimal:

- decentralized  
- deterministic  
- DNS-like  
- uses a single file (`/.well-known/stack`)  
- requires no new web standards  
- is universally adoptable on any host

For each topic (e.g., `water`, `automotive`, `healthcare`, `colloidal silver`), DFH provides:

- **One Root** domain  
- **Any number of Mirrors**  
- **Five Anchors**  
- **One DFH descriptor** at:

```text
https://yourdomain.com/.well-known/stack


README.md
# The Semantic Stack & Deterministic First-Hop (DFH)
_A simple, decentralized semantic layer for the public web + the strongest SEO primitive ever created._

**Status:** Public Concept  
**Version:** Draft v1.0  
**Date:** 2025-11-23  

[![DFH Ready](https://img.shields.io/badge/DFH-Ready-brightgreen)]()  
[![Spec Version](https://img.shields.io/badge/Spec-1.0-blue)]()  
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)]()

---

## 0. What This Repo Is

This repo defines the **Semantic Stack** and the **Deterministic First-Hop (DFH)** protocol — a tiny, external, domain-based semantic layer that gives AI and search systems a **consistent starting point** for any topic.

> **“DFH is DNS for meaning.”**

DFH is intentionally simple:

- decentralized  
- deterministic  
- DNS-like  
- uses only one file  
- requires no new web standards  
- universally adoptable  

Every topic (water, cars, healthcare, colloidal silver, etc.) gets:

- **One Root domain**  
- **Any number of Mirrors**  
- **Five Anchors**  
- **One DFH descriptor at `/.well-known/stack`**

DFH does **not** replace ontologies — it simply tells machines:

> **“Start here for this topic.”**

For the full formal spec, see: [`/docs/spec.md`](docs/spec.md).

---

## 1. Motivation: Why DFH Exists

### Problem 1 — No global semantic ground

Machines lack a deterministic “first hop” for meaning.  
Every knowledge system invents its own root: its own graph, its own embeddings, its own IDs.

DFH fixes that by defining **one canonical first-hop per topic**, per domain.

---

### Problem 2 — Meaning is scattered

Data about any topic is fragmented across:

- Wikidata / DBpedia  
- PDFs and paywalled journals  
- random HTML pages  
- corporate internal graphs  
- SEO spam

DFH does **not** centralize that information.  
It simply says: **“Here is where to start for this topic.”**

---

### Problem 3 — AI hallucinations come from ambiguous roots

LLMs hallucinate when:

- the root of a concept is ambiguous  
- multiple conflicting sources compete as “truth”  
- there is no stable identity for the topic

DFH doesn’t solve hallucinations alone — but it gives AI a **stable grounding point** that drastically improves behavior.

---

### Problem 4 — SEO is stuck at page-level

SEO today is mostly:

- page-level ranking  
- site-level authority  
- schema sprinkled across templates

There is **no stable topic-level identity**.  
DFH introduces **topic roots**, anchored by sitemaps and canonical URLs, to give search engines a **topic-level canonical**.

---

## 2. High-Level Architecture

```text
Semantic Stack
├── Root (topic base)
├── Mirrors (plural/category/context domains)
├── DFH (first-hop descriptor)
└── Anchors
    ├── /type
    ├── /entity
    ├── /url
    ├── /sitemap
    └── /canonical


DFH is delivered via a single JSON/JSON-LD file at:

https://yourdomain.com/.well-known/stack


Requirements:

Served over HTTPS

Content-Type: application/json (or application/ld+json)

Accessible without authentication or cookies

For full DFH file details, see /docs/dfh-file.md
.

3. The Five Anchors

Full details in /docs/anchors.md
.
This is the minimal anchor set for a topic root:

type – What kind of thing this topic is

entity – Concrete, resolvable entities of that type

url – Authoritative URLs for the topic

sitemap – Topic-level sitemap describing the surface

canonical – Canonical identifier for the topic

3.1 /type — Defines the class of thing

Example (for colloidal silver as a product type):

{
  "name": "ColloidalSilver",
  "type_category": "Product",
  "description": "A suspension of silver particles in water.",
  "dfh_version": "1.0"
}

3.2 /entity — Specific instances

Example:

{
  "entity": "GodsGraceColloidalSilver16oz",
  "type": "Product",
  "manufacturer": "God's Grace Products LLC",
  "website": "https://godsgracecolloidalsilver.com"
}

3.3 /url — Authoritative URLs
{
  "canonical": "https://godsgracecolloidalsilver.com",
  "mirrors": [
    "https://example-colloidal-silver.com",
    "https://example-mirror.com"
  ]
}

3.4 /sitemap — Topic-level structure

This is typically a standard sitemap:

https://watersitemap.com/sitemap.xml

3.5 /canonical — Identity anchor
{
  "canonical_id": "colloidalsilver",
  "preferred_label": "Colloidal Silver",
  "aliases": ["Silver Hydrosol", "Silver Suspension"]
}

4. DFH Descriptor Example

Full spec: /docs/dfh-file.md
.

{
  "@context": {
    "dfh": "https://example.org/ns/dfh#",
    "skos": "http://www.w3.org/2004/02/skos/core#",
    "dct": "http://purl.org/dc/terms/"
  },
  "@id": "https://watersitemap.com/.well-known/stack",
  "skos:prefLabel": { "@value": "Water", "@language": "en" },
  "dfh:rootTopic": "water",
  "dfh:anchors": {
    "dfh:type": "https://watertype.com/",
    "dfh:entity": "https://waterentity.com/",
    "dfh:url": "https://waterurl.com/",
    "dfh:sitemap": "https://watersitemap.com/sitemap.xml",
    "dfh:canonical": "https://watercanonical.com/"
  },
  "dct:issued": "2025-11-23",
  "dfh:version": "1.0"
}

5. SEO Advantages

Detailed discussion in /docs/seo-benefits.md
.

DFH provides search systems with:

Topic-level canonical identity

Deterministic sitemap structure

Reduced ambiguity for entity resolution

Improved crawl efficiency (fewer dead ends)

Stronger E-E-A-T signals at the topic level

More reliable featured snippets

Faster indexing and reindexing

DFH is the strongest SEO primitive ever created because it finally provides
a stable semantic identity for an entire topic, not just a single page.

6. Installing DFH (≈5 Minutes)

From the root of your domain’s codebase:

mkdir -p .well-known
nano .well-known/stack


Paste your JSON-LD DFH descriptor.

Deploy to your host (Netlify, Vercel, Cloudflare, custom, etc.).

Then test:

https://yourdomain.com/.well-known/stack


If valid JSON loads in a browser or via curl, DFH is active.

For a one-command helper script, see: /tools/install-dfh.sh
.

7. Mirrors

Mirrors are context providers, not alternate roots.

A Root is the primary DFH topic root for a given semantic scope.

A Mirror is a domain that points back to the Root while adding context (industry, region, modality).

Example mirrors for water:

watersites.com

industrialwatersitemap.com

waterchemistry.com

More in /docs/mirrors.md
.

8. What DFH Is Not

❌ Not a truth authority
❌ Not centralized
❌ Not a replacement for ontologies
❌ Not a new web stack
❌ Not a proprietary product

DFH is:

✔ deterministic
✔ decentralized
✔ universal
✔ public
✔ simple
✔ compatible with all existing web standards (HTTP, DNS, sitemaps, JSON-LD)

9. Tools
DFH Validator

Validate a DFH descriptor:

node tools/dfh-validator.js https://example.com

Quick Installer

Install a baseline DFH file locally:

bash tools/install-dfh.sh

10. Adoption Path

See /docs/adoption.md
 for a full strategy.

In short:

No permissions needed

No central gatekeeper

Works with any hosting platform

AI systems can self-validate and self-debug DFH files

Zero licensing cost (MIT)

11. License

This project is licensed under the MIT License.
See LICENSE
.

12. Roadmap

High-level roadmap is maintained in ROADMAP.md
:

v1.0 — Core DFH spec, anchors, examples, tools

v1.1 — Governance recommendations, best practices, schema extensions

v2.x — Multi-language expansions, richer mirror semantics, alignment with major AI frameworks

13. Where to Start

Read docs/spec.md
.

Copy examples/water/.well-known/stack
.

Adapt it to your own domain and topic.

Run the validator.

Ship it.

Welcome to the Semantic Stack.


---

## `LICENSE` (MIT)

```text
MIT License

Copyright (c) 2025 The Semantic Stack / DFH Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the “Software”), to deal
in the Software without restriction, including without limitation the rights  
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell  
copies of the Software, and to permit persons to whom the Software is  
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in  
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR  
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,  
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE  
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER  
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,  
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN  
THE SOFTWARE.

ROADMAP.md
# DFH Roadmap

This document tracks the **high-level roadmap** for the Semantic Stack & Deterministic First-Hop (DFH) protocol.

---

## Phase 0 — Concept Stabilization (Done)

- Define DFH as a **minimal semantic layer** built on existing web standards.
- Establish the **anchor set**: `type`, `entity`, `url`, `sitemap`, `canonical`.
- Publish a reference repo layout:
  - `README.md`
  - `docs/` with spec, anchors, mirrors, SEO, adoption, whitepaper
  - `examples/` for core topics (water, automotive, healthcare)
  - `tools/` with validator + installer
  - `diagrams/` for architecture

Status: ✅ Complete.

---

## Phase 1 — DFH v1.0 Spec (Current)

Goals:

- Finalize DFH v1.0 in [`docs/spec.md`](docs/spec.md).
- Define the DFH JSON-LD file in [`docs/dfh-file.md`](docs/dfh-file.md).
- Document rule sets for:
  - Anchors (`anchors.md`)
  - Mirrors (`mirrors.md`)
  - SEO behavior (`seo-benefits.md`)
  - Adoption strategies (`adoption.md`)
- Provide at least **3 real-topic examples**:
  - `water`
  - `automotive`
  - `healthcare`
- Ship tooling:
  - `tools/dfh-validator.js`
  - `tools/install-dfh.sh`

Status: 🚧 Drafting v1.0.

---

## Phase 2 — Reference Implementations

Goals:

- Provide reference DFH descriptors and sitemaps for:
  - Banking
  - Energy
  - Transportation
  - Housing
  - Food
  - Employment
- Add language-specific usage examples:
  - Node.js, Python, Go
- Provide a **DFH crawler reference implementation**:
  - Walk across roots & mirrors
  - Validate anchors and sitemaps

Status: ⏳ Planned.

---

## Phase 3 — Ecosystem & Governance

Goals:

- Define a **non-binding governance playbook**:
  - How to avoid competing roots for the same topic.
  - How mirrors should reference roots.
  - How conflict resolution might be handled socially (not enforced by protocol).
- Document **best practices** for:
  - Public institutions
  - Corporations
  - Independent researchers

Status: ⏳ Planned.

---

## Phase 4 — Align With AI & Search Systems

Goals:

- Document DFH consumption patterns for:
  - LLMs (pretraining + retrieval)
  - Traditional search engines
  - Vector and graph databases
- Provide **example integrations**:
  - “Given a topic, find its DFH root, then crawl anchors.”
- Propose an **informal standard** to AI/search vendors.

Status: ⏳ Planned.

---

## Phase 5 — Extensions & v2.0

Future possibilities:

- Multi-language canonical IDs and labels.
- Extended anchors for:
  - policies
  - licenses
  - provenance
- Richer mirror semantics (weights, trust, scope).
- Formal RFC-style process if the ecosystem demands it.

---

## Contributing to the Roadmap

DFH is intentionally minimal and decentralized.

If you want to propose changes:

1. Open an issue titled: `Proposal: <short-title>`.
2. Explain:
   - problem
   - rationale
   - minimal proposed change
3. If accepted, the roadmap will be updated here.

docs/spec.md
# DFH Specification (v1.0)

**Status:** Draft  
**Version:** 1.0  
**Date:** 2025-11-23  

This document defines the **Deterministic First-Hop (DFH)** protocol: a minimal, decentralized semantic layer that gives AI systems and search engines a **stable starting point** for any topic.

---

## 1. Scope

DFH specifies:

- A **single descriptor file** at: `/.well-known/stack`
- A set of **anchors** that describe:
  - type
  - entity
  - url
  - sitemap
  - canonical
- Optional **mirrors** that provide additional context.

DFH does **not** define:

- Truth, correctness, or authority of content.
- Any new transport protocol.
- Any new DNS or HTTP extensions.
- Any proprietary ranking, scoring, or ontology.

---

## 2. Terminology

- **Root**  
  A domain that publishes a DFH descriptor for a specific topic or topic family.

- **Topic**  
  A concept, entity class, domain of knowledge, product category, etc.  
  Examples: `water`, `automotive`, `healthcare`, `colloidal silver`.

- **Mirror**  
  A domain that references an existing Root and adds context (e.g., industry, regional, or categorical specialization).

- **Anchor**  
  A link or pointer from DFH to a structured resource that stabilizes one aspect of the topic:
  - `type`
  - `entity`
  - `url`
  - `sitemap`
  - `canonical`

- **DFH Descriptor**  
  The JSON or JSON-LD file at `/.well-known/stack` that enumerates anchors and metadata.

---

## 3. DFH Descriptor Location

The DFH descriptor **MUST** be served at:

```text
https://<domain>/.well-known/stack


Requirements:

https is REQUIRED.

Content-Type SHOULD be application/json or application/ld+json.

The file MUST be accessible without authentication.

The file SHOULD be stable over time (non-ephemeral).

4. DFH Descriptor Structure

At minimum, a DFH descriptor MUST contain:

dfhVersion

root

anchors

Example (simplified):

{
  "@context": "https://schema.org",
  "dfhVersion": "1.0",
  "root": "https://example.com",
  "anchors": {
    "type": "https://type.example.com",
    "entity": "https://entity.example.com",
    "url": "https://url.example.com",
    "sitemap": "https://example.com/sitemap.xml",
    "canonical": "https://canonical.example.com"
  }
}

4.1 @context

Optional but recommended.

If present, SHOULD use a well-known JSON-LD context such as https://schema.org or a DFH-specific vocabulary.

4.2 dfhVersion

MUST be a string indicating the DFH spec version the file targets.

Example: "1.0"

Consumers SHOULD treat unknown versions as best-effort compatible.

4.3 root

MUST be a URL representing the topic root.

SHOULD be the main domain or section representing the topic.

Example: "https://watersitemap.com".

4.4 anchors

MUST be an object with keys:

type

entity

url

sitemap

canonical

All five keys are REQUIRED in DFH v1.0.

Values SHOULD be fully qualified URLs.

5. Anchors

The full semantics of each anchor type are defined in anchors.md
, but this section summarizes the normative requirements.

5.1 type Anchor

MUST point to a resource defining the class of thing.

Could be:

a JSON/JSON-LD definition

a schema document

a type registry endpoint

Examples:

https://watertype.com

https://schema.example.com/types/water

5.2 entity Anchor

MUST point to a resource listing or defining instances of the type.

Could be:

a JSON list

an API endpoint

a graph export

Example:

https://waterentity.com

5.3 url Anchor

MUST point to a resource listing authoritative URLs for this topic.

Could be:

a curated list

an index page

an API endpoint

Example:

https://waterurl.com

5.4 sitemap Anchor

MUST point to a sitemap in a search-engine compatible format (e.g., sitemap.xml).

Example:

https://watersitemap.com/sitemap.xml

5.5 canonical Anchor

MUST point to a resource that defines canonical identity for the topic.

MUST specify:

canonical identifier

preferred label

optional aliases

6. Mirrors

A DFH descriptor MAY include mirrors:

{
  "mirrors": [
    "https://watersites.com",
    "https://industrialwatersitemap.com"
  ]
}


Rules:

A Root is a DFH descriptor that defines root as itself (or its main domain).

A Mirror SHOULD reference the Root either:

directly in its descriptor, or

indirectly through canonical/URL anchors.

Details in mirrors.md
.

7. Determinism Rules

Consumers SHOULD:

Fetch https://<domain>/.well-known/stack.

Validate:

the JSON structure

presence of required fields

presence of required anchors.

Treat that descriptor as the first hop:

Resolve anchors.

Traverse sitemaps.

Incorporate canonical identity.

If multiple candidate domains exist for a topic, a consumer MAY apply its own policies to decide which domain acts as the Root.

DFH does not enforce uniqueness at the protocol level.

8. Error Handling

Clients SHOULD handle:

HTTP 4xx / 5xx responses

Invalid JSON

Missing anchors

Partial descriptors

Recommended strategies:

Fallback to known mirrors or alternate roots.

Log warnings, not hard failures.

Use DFH as a hint, not a single point of failure.

9. Security Considerations

DFH is public metadata; do not store secrets in /.well-known/stack.

Root domains MAY be compromised; consumers SHOULD cross-check anchors with other signals.

DFH does not introduce new authentication mechanisms; it relies on existing HTTPS guarantees.

10. Versioning

DFH descriptors MUST declare dfhVersion.

Breaking changes to DFH will increment the major version.

Non-breaking additions will increment the minor or patch version.

Example: "1.0", "1.1", "2.0".

11. Non-Normative Appendices

For examples, SEO implications, and adoption patterns, see:

dfh-file.md

anchors.md

seo-benefits.md

adoption.md

whitepaper.md


---

## `docs/dfh-file.md`

```markdown
# DFH Descriptor File (`/.well-known/stack`)

This document describes the **shape and fields** of the DFH descriptor file.

Location:

```text
https://<domain>/.well-known/stack


Format: JSON or JSON-LD.

1. Minimal Example
{
  "@context": "https://schema.org",
  "dfhVersion": "1.0",
  "root": "https://example.com",
  "anchors": {
    "type": "https://type.example.com",
    "entity": "https://entity.example.com",
    "url": "https://url.example.com",
    "sitemap": "https://example.com/sitemap.xml",
    "canonical": "https://canonical.example.com"
  }
}

2. Recommended Extended Example
{
  "@context": {
    "dfh": "https://example.org/ns/dfh#",
    "skos": "http://www.w3.org/2004/02/skos/core#",
    "dct": "http://purl.org/dc/terms/"
  },
  "@id": "https://watersitemap.com/.well-known/stack",
  "dfhVersion": "1.0",
  "root": "https://watersitemap.com",
  "skos:prefLabel": { "@value": "Water", "@language": "en" },
  "dfh:rootTopic": "water",
  "anchors": {
    "type": "https://watertype.com",
    "entity": "https://waterentity.com",
    "url": "https://waterurl.com",
    "sitemap": "https://watersitemap.com/sitemap.xml",
    "canonical": "https://watercanonical.com"
  },
  "mirrors": [
    "https://watersites.com",
    "https://industrialwatersitemap.com"
  ],
  "dct:issued": "2025-11-23",
  "dct:modified": "2025-11-23"
}

3. Field Definitions
3.1 @context (optional but recommended)

Type: string or object

Purpose: JSON-LD context for semantic interoperability.

Example: "https://schema.org".

3.2 @id (optional)

Type: string

Purpose: Canonical identifier of the DFH descriptor itself.

SHOULD be the full URL to /.well-known/stack.

3.3 dfhVersion (required)

Type: string

Example: "1.0"

Purpose: Declares the DFH spec version.

3.4 root (required)

Type: string (URL)

Purpose: Topic root domain or URL.

SHOULD be the main domain for the topic.

3.5 anchors (required)

Type: object

Keys (all required in v1.0):

type

entity

url

sitemap

canonical

Values: URLs.

3.6 mirrors (optional)

Type: array of string (URLs)

Purpose: Context domains that mirror or expand the topic.

3.7 dct:issued / dct:modified (optional)

Type: string (ISO date)

Purpose: Provide temporal metadata.

3.8 Additional Fields

DFH allows extra fields, provided they do not break the basic structure.
Consumers SHOULD ignore unknown fields gracefully.

4. Validation Rules

A DFH descriptor is considered structurally valid if:

JSON is well-formed.

dfhVersion is present and a string.

root is present and a string.

anchors is an object with keys:

type

entity

url

sitemap

canonical

The provided tools/dfh-validator.js checks these conditions.

5. Content Recommendations

Use stable URLs where possible (avoid ephemeral endpoints).

Treat DFH as public infrastructure: no cookies, no auth, no paywalls.

Keep the file small and cacheable.

For semantics of each anchor, see anchors.md
.


---

## `docs/anchors.md`

```markdown
# DFH Anchors

Anchors are the **core of DFH**.  
They define how a topic exposes its meaning to AI and search systems.

DFH v1.0 defines **five anchors**:

1. `type`
2. `entity`
3. `url`
4. `sitemap`
5. `canonical`

All five are **required**.

---

## 1. `type` Anchor

### 1.1 Purpose

`type` defines **what kind of thing** the topic is.

Examples:

- Substance
- Product
- Disease
- Vehicle
- Organization

### 1.2 Requirements

- MUST be a URL.
- SHOULD resolve to a human- and machine-readable resource.
- SHOULD describe:
  - name
  - category
  - short description

Example:

```json
{
  "name": "Water",
  "type_category": "Substance",
  "description": "A transparent, tasteless, odorless, and nearly colorless chemical substance.",
  "dfh_version": "1.0"
}

2. entity Anchor
2.1 Purpose

entity provides instances of the topic type.

Examples:

For water type:

bottled water brands

water quality databases

For automotive:

manufacturers

models

VIN-based lookups

2.2 Requirements

MUST be a URL.

SHOULD return structured data (JSON, CSV, RDF…).

SHOULD be stable over time.

Example:

{
  "entities": [
    {
      "id": "godsgrace-16oz",
      "label": "God's Grace Colloidal Silver 16oz",
      "type": "Product",
      "url": "https://godsgracecolloidalsilver.com"
    }
  ]
}

3. url Anchor
3.1 Purpose

url acts as a curated URL index for the topic.

3.2 Requirements

MUST be a URL.

SHOULD list or generate:

canonical URLs

important subdomains

related resources

Example:

{
  "canonical": "https://watersitemap.com",
  "related": [
    "https://waterchemistry.com",
    "https://waterquality.org"
  ]
}

4. sitemap Anchor
4.1 Purpose

sitemap is the crawl surface for the topic.

4.2 Requirements

MUST be a URL.

MUST point to a search engine compatible sitemap, typically:

sitemap.xml

or a sitemap index

This is where search and AI systems can walk the topic.

Example:

https://watersitemap.com/sitemap.xml

5. canonical Anchor
5.1 Purpose

canonical stabilizes the identity of the topic.

5.2 Requirements

MUST be a URL.

SHOULD resolve to a resource with:

canonical_id

preferred_label

aliases

Example:

{
  "canonical_id": "water",
  "preferred_label": "Water",
  "aliases": ["H2O", "Dihydrogen monoxide"]
}

6. Anchor Design Principles

Minimal — Only five anchors.

Compositional — Each anchor can link to arbitrarily complex structures.

Decentralized — Anyone can publish anchors for their own domain.

Deterministic — The first hop is always /.well-known/stack.

DFH does not mandate the internal structure of anchor targets.
It only defines their existence and purpose.


---

## `docs/mirrors.md`

```markdown
# Mirrors

Mirrors are **secondary domains** that:

- reference an existing DFH Root, and  
- add context, scope, or specialization.

They are **not alternate Roots**; they are **context amplifiers**.

---

## 1. Why Mirrors Exist

The web is messy:

- Multiple industries may care about the same topic.
- Different communities may curate different slices of the same concept.
- Regional or regulatory variants may exist.

Mirrors let ecosystems evolve organically **without forcing a single host** to own everything.

---

## 2. Mirror Structure

A Mirror MAY:

- host its own DFH descriptor at `/.well-known/stack`
- reference the Root and/or other mirrors in:
  - `anchors`
  - `mirrors`
  - any custom fields

Example (mirror of `water`):

```json
{
  "@context": "https://schema.org",
  "dfhVersion": "1.0",
  "root": "https://watersites.com",
  "anchors": {
    "type": "https://watertype.com",
    "entity": "https://waterentity.com",
    "url": "https://watersites.com/urls.json",
    "sitemap": "https://watersites.com/sitemap.xml",
    "canonical": "https://watercanonical.com"
  },
  "mirrors": [
    "https://watersitemap.com",
    "https://industrialwatersitemap.com"
  ],
  "role": "context-mirror"
}

3. Mirror vs Root

Root:

Semantically: “The main topic root for this domain’s scope.”

Often the domain that owns the primary sitemap and canonical identity.

Mirror:

Semantically: “I reflect and extend the topic with added context.”

May focus on:

industrial use

academic research

consumer guidance

regional policy

DFH does not enforce a global decision on “who is the true root”.
That is left to ecosystem consensus and consumer policies.

4. Best Practices

A Mirror SHOULD not claim to be the sole Root for the topic.

Mirrors SHOULD include at least one reference to:

the canonical Root (if known), or

other high-quality mirrors.

Mirrors SHOULD avoid misrepresenting their scope (e.g., claiming global canonical status if they only serve a region).

5. Consumption Guidelines

Clients MAY:

treat Roots with more weight than Mirrors.

use Mirrors to discover:

additional URLs

region-specific facets

specialized entities

Clients SHOULD:

treat mirrors arrays as optional hints, not mandatory chains.

remain resilient if mirrors are missing or inconsistent.


---

## `docs/seo-benefits.md`

```markdown
# SEO Benefits of DFH

DFH is designed to be the **strongest SEO primitive ever created** for topic-level identity.

---

## 1. From Page-Level to Topic-Level

Traditional SEO:

- works at the **page** level  
- infers meaning from:
  - titles
  - headers
  - content
  - links  
- has no stable **topic root**.

DFH adds:

- a **topic-level root** at `/.well-known/stack`
- explicit anchors for:
  - type
  - entities
  - URLs
  - sitemaps
  - canonical identity

---

## 2. Canonical Topic Identity

With DFH, search engines can:

- map a topic → a `root` domain unambiguously (or with clear candidates)
- understand **“this domain is about this topic”** at a structural level
- avoid mixing unrelated content into the same semantic bucket

---

## 3. Deterministic Sitemap

By mandating a `sitemap` anchor:

- crawlers know **exactly where** to start crawling the topic.
- no more guessing:
  - robots.txt quirks
  - random `/sitemap.xml` heuristics
- large sites can expose:
  - topic-specific sitemaps
  - multi-sitemap structures

---

## 4. Stronger E-E-A-T Signals

DFH supports E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness) via:

- consistent topic-level structure
- machine-readable identity
- clear boundaries between:
  - root content
  - mirror content
  - external entities

Search engines can combine DFH signals with:

- link graphs
- on-page content
- user behavior

---

## 5. Reduced Ambiguity and Hallucination

By giving AI systems a **stable first-hop**:

- query understanding improves
- document clustering improves
- knowledge graph linking becomes easier

This indirectly improves:

- featured snippets
- “People also ask”
- semantic SERP features

---

## 6. Implementation Recommendations

For site owners:

1. Publish a DFH descriptor at `/.well-known/stack`.
2. Ensure `anchors.sitemap` points to a high-quality, maintained sitemap.
3. Provide clear `canonical` identity information.
4. Keep DFH descriptors updated when structure or ownership changes.

Search engines and AI systems can treat DFH as:

- a **trusted hint**
- a **shortcut** to high-quality structure
- an input to ranking and clustering models

DFH does not dictate ranking.  
It makes ranking **easier and more accurate**.

docs/adoption.md
# DFH Adoption Guide

DFH is deliberately designed to be **easy to adopt**.

No standards body membership, no fees, no contracts.

---

## 1. Who Should Adopt DFH?

- Search-oriented websites
- Knowledge hubs
- Public institutions
- Large brands with topic authority
- Niche experts with deep curated content

---

## 2. Minimal Adoption (5-Minute Path)

1. Create `.well-known/stack` in your web root.
2. Paste a minimal DFH descriptor:

   ```json
   {
     "@context": "https://schema.org",
     "dfhVersion": "1.0",
     "root": "https://example.com",
     "anchors": {
       "type": "https://example.com/type.json",
       "entity": "https://example.com/entity.json",
       "url": "https://example.com/url.json",
       "sitemap": "https://example.com/sitemap.xml",
       "canonical": "https://example.com/canonical.json"
     }
   }


Deploy.

Confirm:

curl https://example.com/.well-known/stack

3. Recommended Adoption

After minimal adoption:

Improve anchor targets:

richer type definition

better entity listing

canonical URL registry

Add mirrors if:

you operate multiple topic domains

or collaborate with aligned domains

Keep dct:modified updated.

4. Ecosystem Adoption
4.1 Search Engines

Search engines can:

crawl DFH descriptors for:

initial topic discovery

sitemap bootstrapping

score DFH usage as:

a structural quality signal

a hint of topic-level intent

4.2 AI Systems

LLMs and knowledge graphs can:

use DFH as a topic bootstrap step:

topic → DFH root → anchors → data

mix DFH with:

embeddings

graph stores

external ontologies

5. Social and Governance Aspects

DFH avoids centralized governance by design.

Best-effort norms:

Don’t claim “global canonical” lightly.

Use descriptive, honest canonical_id and labels.

Link to other serious roots and mirrors.

If conflicts arise:

Search engines and AI systems will determine trust via:

link graphs

usage patterns

provenance

DFH does not enforce consensus.
It exposes structure and intent.


---

## `docs/whitepaper.md`

```markdown
# The Semantic Stack & Deterministic First-Hop (DFH)
_A public grounding layer for AI and search_

**Status:** Draft Whitepaper  
**Version:** 1.0  
**Date:** 2025-11-23  

---

## Abstract

Modern AI systems and search engines suffer from a lack of **stable semantic grounding**.  
Every provider maintains its own internal graph, embeddings, and ontologies.  
This leads to:

- duplicated effort  
- inconsistent semantics  
- hallucinations and misalignment  

This paper proposes the **Semantic Stack** with **Deterministic First-Hop (DFH)**:  
a minimal, external, domain-based layer that provides a **single, deterministic starting point** for any topic using one JSON/JSON-LD file at `/.well-known/stack`.

---

## 1. Introduction

The web solved addressing with **DNS**, and navigation with **URLs**, but never solved **semantic grounding** in a way that is:

- decentralized  
- public  
- enforceably minimal  

Decades of semantic web efforts (RDF, OWL, etc.) focused on expressive models but failed to become universal infrastructure.

At the same time, search engines and LLMs built powerful internal knowledge structures that are:

- proprietary  
- opaque  
- not directly reusable by the public  

DFH proposes a middle path:

- minuscule surface area  
- entirely host-controlled  
- built on top of existing web and DNS primitives

---

## 2. Problem Statement

AI and search suffer from:

1. **No deterministic semantic entry point**  
   Systems have to guess where to start understanding a topic.

2. **Fragmented and overlapping graphs**  
   Every company duplicates effort, building parallel ontologies.

3. **Ambiguous roots for entities and topics**  
   Multiple sites claim authority without a shared first-hop convention.

4. **Page-centric indexing for inherently topic-centric domains**  
   SEO optimizes pages, not topics.

---

## 3. Design Goals

DFH is designed to be:

- **Minimal** — a single JSON/JSON-LD file  
- **Deterministic** — fixed path: `/.well-known/stack`  
- **Decentralized** — any domain can publish a root  
- **Compatible** — uses HTTPS, DNS, sitemaps, JSON-LD  
- **Non-competitive** — does not replace ontologies or ranks content  

---

## 4. Architecture

### 4.1 Root

A **Root** is a domain that publishes a DFH descriptor for a topic.

- `root` field declares the topic root URL.
- `anchors` stabilize how the topic is exposed.

### 4.2 Anchors

Five anchors:

- `type` — what the topic is  
- `entity` — instances of that type  
- `url` — authoritative URLs  
- `sitemap` — crawl surface  
- `canonical` — canonical identity  

These anchors collectively form the **Semantic Stack** for the topic.

### 4.3 Mirrors

Mirrors provide additional context domains connected to the Root.

- They may host DFH descriptors themselves.
- They may extend or specialize the topic representation.

---

## 5. Protocol

1. A domain publishes `/.well-known/stack`.
2. Clients (search, AI, crawlers) fetch this file.
3. Clients validate:
   - structure
   - presence of anchors
4. Clients treat this file as the **first-hop** for the topic:
   - resolve anchors
   - traverse sitemaps
   - map canonical identity

The protocol is **read-only** and **stateless**.  
There is no handshake, no session, no negotiation.

---

## 6. Implementation

### 6.1 Site Owners

Implementation steps:

1. Decide the topics your domain is a Root for.
2. Implement `/.well-known/stack` with required fields.
3. Ensure `sitemap` anchor points to a maintained sitemap.
4. Keep the descriptor up to date.

### 6.2 Search Engines and AI Systems

Implementation steps:

1. Integrate DFH discovery into crawlers.
2. Use DFH as:
   - input to ranking features
   - bootstrap for semantic graphs
   - hint for canonical topic identity

---

## 7. Benefits

- Reduced duplication of semantic infrastructure.
- Clearer topic-level identity.
- Improved AI behavior via deterministic grounding.
- SEO improvements via topic-level signals.

---

## 8. Limitations

- DFH does not guarantee **truth** or **authority**.
- Malicious or low-quality roots may exist.
- Ecosystem trust must emerge from:
  - signals
  - links
  - usage patterns

DFH solves **where to start**, not **who to trust**.

---

## 9. Conclusion

DFH is deliberately small: one file, five anchors, one well-known path.

This structural constraint is its strength.

By giving the web a deterministic first-hop for meaning, DFH unlocks:

- better AI grounding  
- more powerful search and SEO  
- a truly public semantic layer  

without requiring any new transport, markup, or monetization scheme.

---

## References

- WebDAV / `.well-known` URI patterns  
- Sitemaps protocol  
- JSON-LD & Schema.org  
- Historical semantic web efforts (RDF, OWL, SKOS)

examples/water/.well-known/stack
{
  "@context": "https://schema.org",
  "dfhVersion": "1.0",
  "root": "https://watersitemap.com",
  "anchors": {
    "type": "https://watertype.com",
    "entity": "https://waterentity.com",
    "url": "https://waterurl.com",
    "sitemap": "https://watersitemap.com/sitemap.xml",
    "canonical": "https://watercanonical.com"
  },
  "mirrors": [
    "https://watersites.com",
    "https://industrialwatersitemap.com"
  ]
}

examples/water/sitemap.xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://watersitemap.com/</loc>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://watersitemap.com/chemistry</loc>
    <priority>0.8</priority>
  </url>
  <url>
    <loc>https://watersitemap.com/quality</loc>
    <priority>0.8</priority>
  </url>
</urlset>

examples/automotive/.well-known/stack
{
  "@context": "https://schema.org",
  "dfhVersion": "1.0",
  "root": "https://automotivesitemap.com",
  "anchors": {
    "type": "https://autotyperegistry.com",
    "entity": "https://autoentityregistry.com",
    "url": "https://autoindex.com",
    "sitemap": "https://automotivesitemap.com/sitemap.xml",
    "canonical": "https://autocanonical.com"
  },
  "mirrors": [
    "https://cardealersitemap.com",
    "https://usedcarsitemap.com"
  ]
}

examples/automotive/sitemap.xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://automotivesitemap.com/</loc>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://automotivesitemap.com/new</loc>
    <priority>0.9</priority>
  </url>
  <url>
    <loc>https://automotivesitemap.com/used</loc>
    <priority>0.9</priority>
  </url>
</urlset>

examples/healthcare/.well-known/stack
{
  "@context": "https://schema.org",
  "dfhVersion": "1.0",
  "root": "https://healthcaresitemap.com",
  "anchors": {
    "type": "https://healthtype.com",
    "entity": "https://healthentity.com",
    "url": "https://healthurl.com",
    "sitemap": "https://healthcaresitemap.com/sitemap.xml",
    "canonical": "https://healthcanonical.com"
  },
  "mirrors": [
    "https://hospitaldirectory.com",
    "https://healthservicesitemap.com"
  ]
}

examples/healthcare/sitemap.xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://healthcaresitemap.com/</loc>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://healthcaresitemap.com/providers</loc>
    <priority>0.9</priority>
  </url>
  <url>
    <loc>https://healthcaresitemap.com/services</loc>
    <priority>0.9</priority>
  </url>
</urlset>

tools/dfh-validator.js
#!/usr/bin/env node

/**
 * DFH Validator
 * Checks for structural validity of a /.well-known/stack file.
 */

const fetch = require("node-fetch");

async function validate(url) {
  if (!url) {
    console.error("Usage: dfh-validator <domain>");
    process.exit(1);
  }

  const target = `${url.replace(/\/$/, "")}/.well-known/stack`;
  console.log(`🔎 Checking DFH file at: ${target}\n`);

  try {
    const res = await fetch(target, {
      headers: { Accept: "application/json" }
    });

    if (!res.ok) {
      throw new Error(`HTTP ${res.status}: Unable to fetch DFH file`);
    }

    const json = await res.json();
    console.log("✔ Valid JSON received\n");

    const anchors = json.anchors || {};
    const required = ["type", "entity", "url", "sitemap", "canonical"];

    console.log("DFH Version:", json.dfhVersion || "⚠ Missing");
    console.log("Root:", json.root || "⚠ Missing");

    console.log("\nAnchors:");
    required.forEach((a) => {
      if (anchors[a]) {
        console.log(`  ✔ ${a}: ${anchors[a]}`);
      } else {
        console.log(`  ⚠ Missing anchor: ${a}`);
      }
    });

    const missing = required.filter((a) => !anchors[a]);
    if (!json.dfhVersion || !json.root || missing.length > 0) {
      console.log("\n❌ DFH descriptor is NOT structurally complete.");
      process.exitCode = 1;
    } else {
      console.log("\n✅ DFH descriptor is structurally valid.");
    }
  } catch (err) {
    console.error("❌ Error:", err.message);
    process.exitCode = 1;
  }
}

validate(process.argv[2]);

tools/install-dfh.sh
#!/bin/bash
# DFH Installer Script
# Creates a baseline /.well-known/stack file in the current directory.

set -e

mkdir -p .well-known

cat <<EOF > .well-known/stack
{
  "@context": "https://schema.org",
  "dfhVersion": "1.0",
  "root": "https://example.com",
  "anchors": {
    "type": "https://type.com",
    "entity": "https://entity.com",
    "url": "https://url.com",
    "sitemap": "https://example.com/sitemap.xml",
    "canonical": "https://canonical.com"
  }
}
EOF

echo "✔ DFH installed at .well-known/stack"
echo "Remember to update root and anchors to match your domain."

diagrams/architecture.mmd
flowchart TD

  subgraph Web
    A[Domain<br/>example.com]
  end

  A --> B[/.well-known/stack<br/>DFH Descriptor]

  subgraph Anchors
    T[type]
    E[entity]
    U[url]
    S[sitemap]
    C[canonical]
  end

  B --> T
  B --> E
  B --> U
  B --> S
  B --> C

  subgraph Consumers
    SE[Search Engine]
    AI[AI System / LLM]
    Crawler[Generic Crawler]
  end

  SE --> B
  AI --> B
  Crawler --> B

  SE --> S
  Crawler --> S

  AI --> T
  AI --> E
  AI --> C

diagrams/overview.txt
The Semantic Stack & DFH — High-Level Overview
==============================================

          +-----------------------------+
          |        Consumers            |
          |  - Search Engines           |
          |  - AI / LLM Systems         |
          |  - Crawlers                 |
          +--------------+--------------+
                         |
                         | HTTP GET /.well-known/stack
                         v
               +---------+---------+
               |   Domain Root     |
               |  example.com      |
               +---------+---------+
                         |
                         v
               +-------------------+
               | DFH Descriptor    |
               | /.well-known/stack|
               +---------+---------+
                         |
       +-----------------+------------------------------+
       |                 |              |              |
       v                 v              v              v
+-------------+    +-----------+   +----------+   +-----------+
| type anchor |    | entity    |   | url      |   | sitemap   |
+-------------+    +-----------+   +----------+   +-----------+
                                                        |
                                                        v
                                                +---------------+
                                                |  Crawl Surface|
                                                |  sitemap.xml  |
                                                +---------------+

The DFH descriptor is the "first hop" for meaning:
- It is small, deterministic, and public.
- It points to richer structures via anchors.
- Consumers treat it as the canonical topic bootstrap.
