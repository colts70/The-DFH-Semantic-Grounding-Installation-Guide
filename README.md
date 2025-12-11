# DFH v1.0 — Official Installation & Deployment Guide

**This repo is the official DFH v1.0 installation and deployment guide.**  
For the conceptual definition / whitepaper, see your **DFH Concept Root** repo (e.g. `The-Semantic-Stack-DFH-Concept-Root`).

> *“This is the modern implementation of Tim Berners-Lee’s original Semantic Web map.”*  
> *“DFH is DNS for meaning.”*

---

## 0. What This Repo Is

This repo is the **ops + install guide** for the Semantic Stack & DFH:

- How to publish `/.well-known/stack`
- How to configure the **Five Anchors** (`type`, `entity`, `url`, `sitemap`, `canonical`)
- How to validate your DFH descriptor
- How to ship a compliant **Semantic Stack Root** in minutes

It includes:

- A **minimal DFH descriptor** you can copy–paste
- **Examples** for `water`, `automotive`, and `healthcare`
- A **validator** (`tools/dfh-validator.js`)
- A **one-command installer** (`tools/install-dfh.sh`)
- Docs for spec, anchors, mirrors, SEO, and adoption

**Status:** Public Concept  
**Version:** Draft v1.0  
**Date:** 2025-11-23  
**License:** MIT  

---

## 1. The Real Semantic Layer

The web layers:

- The **Transport Layer (TCP/IP)** → moves packets  
- The **Hyperlink Layer (HTTP/HTML)** → shows documents  
- The **Meaning Layer (DFH / Semantic Stack)** → tells AI what those documents *mean*

DFH defines a tiny, external, domain-based semantic layer that gives AI and search systems a **consistent first-hop** for any topic.

For each topic (e.g. `water`, `automotive`, `healthcare`, `colloidal silver`), DFH provides:

- **One Root** domain  
- **Any number of Mirrors**  
- **Five Anchors**  
- **One DFH descriptor** at:

```text
https://yourdomain.com/.well-known/stack
DFH does not replace ontologies or ranking. It simply tells machines:

“Start here for this topic.”

For the full v1.0 spec, see: docs/spec.md.

2. Repository Layout
High-level structure:

text
Copy code
DFH-Installation-Guide/
├── README.md           # This file: official install & deployment guide
├── LICENSE             # MIT license
├── ROADMAP.md          # DFH roadmap and phases
├── docs/
│   ├── spec.md         # DFH v1.0 specification
│   ├── dfh-file.md     # DFH descriptor file shape
│   ├── anchors.md      # Five anchors: type/entity/url/sitemap/canonical
│   ├── mirrors.md      # Mirror semantics
│   ├── seo-benefits.md # SEO behavior and advantages
│   ├── adoption.md     # Adoption guide and patterns
│   └── whitepaper.md   # Conceptual / theoretical background
├── examples/
│   ├── water/
│   │   ├── .well-known/stack
│   │   └── sitemap.xml
│   ├── automotive/
│   │   ├── .well-known/stack
│   │   └── sitemap.xml
│   └── healthcare/
│       ├── .well-known/stack
│       └── sitemap.xml
├── tools/
│   ├── dfh-validator.js # Node-based DFH descriptor validator
│   └── install-dfh.sh   # Shell script to scaffold a baseline DFH file
└── diagrams/
    ├── architecture.mmd  # Mermaid diagram of DFH architecture
    └── overview.txt      # ASCII overview of DFH flow
3. Requirements
To host DFH:

A web server or static host (Netlify, Vercel, Cloudflare, custom, etc.)

Ability to serve files at /.well-known/ from your domain root

HTTPS enabled (strongly recommended)

To use the tools in this repo:

Node.js ≥ 18

npm (or another Node package manager)

bash (for install-dfh.sh) on macOS / Linux / WSL

curl or a browser to test your DFH descriptor

4. Quick Install (≈ 5 Minutes)
This is the minimal path to putting DFH live on your domain.

Step 1 — Decide Your Topic & Domain
Pick a topic and the domain that will act as its Root, e.g.:

Topic: water

Root domain: https://watersitemap.com

Step 2 — Create .well-known/stack
On your site’s codebase or file system, create the directory and file:

bash
Copy code
mkdir -p .well-known
nano .well-known/stack
Step 3 — Paste a Minimal DFH Descriptor
Paste this minimal JSON (adapt domains/URLs to your site):

json
Copy code
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
Update:

root → your root domain

Each anchor URL → real, stable endpoints you control

See docs/dfh-file.md for details on each field.

Step 4 — Deploy to Your Host
Deploy your changes:

Static hosts (Netlify, Vercel, Cloudflare Pages, etc.):
Ensure .well-known/stack is included in your build output.

Custom servers (Nginx/Apache/etc.):
Place .well-known/stack in the web root directory, or configure your server so the file is served at:

text
Copy code
https://yourdomain.com/.well-known/stack
Step 5 — Verify in a Browser or via curl
Test in a browser:

text
Copy code
https://yourdomain.com/.well-known/stack
Or use curl:

bash
Copy code
curl -s https://yourdomain.com/.well-known/stack | jq .
You should see valid JSON or JSON-LD. If you can fetch it without auth and without cookies, DFH is physically installed.

Step 6 — Validate the DFH Descriptor (Recommended)
Use the validator in tools/dfh-validator.js to check structure and required anchors.

See Section 6 (Validator) below.

5. DFH Descriptor Basics (/.well-known/stack)
The DFH descriptor must be served at:

text
Copy code
https://<domain>/.well-known/stack
5.1 Required Fields (v1.0)
At minimum, DFH v1.0 requires:

dfhVersion — string, e.g. "1.0"

root — URL of the topic root (usually your main domain)

anchors — object with five required keys:

type

entity

url

sitemap

canonical

Example (simplified):

json
Copy code
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
Details for each field and anchor are in:

docs/dfh-file.md

docs/anchors.md

6. DFH Validator (tools/dfh-validator.js)
The validator checks:

That /.well-known/stack is reachable

That it is valid JSON

That dfhVersion and root are present

That all five anchors are present: type, entity, url, sitemap, canonical

6.1 Installation
From the repo root:

bash
Copy code
# Clone this repo (or copy tools/ into your own)
git clone <this-repo-url> dfh-install
cd dfh-install

# Install dependencies (node-fetch)
npm install node-fetch
# or, if you have a package.json already, add node-fetch there and run:
# npm install
If you plan to integrate the validator into your own project, add node-fetch to your own package.json and move tools/dfh-validator.js into your tooling folder.

6.2 Usage
Run the validator, passing your domain URL (without /.well-known/stack — the script adds it):

bash
Copy code
node tools/dfh-validator.js https://yourdomain.com
Example output:

text
Copy code
🔎 Checking DFH file at: https://yourdomain.com/.well-known/stack

✔ Valid JSON received

DFH Version: 1.0
Root: https://yourdomain.com

Anchors:
  ✔ type: https://yourdomain.com/type.json
  ✔ entity: https://yourdomain.com/entity.json
  ✔ url: https://yourdomain.com/url.json
  ✔ sitemap: https://yourdomain.com/sitemap.xml
  ✔ canonical: https://yourdomain.com/canonical.json

✅ DFH descriptor is structurally valid.
If required fields are missing, you will see warnings like:

text
Copy code
DFH Version: ⚠ Missing
Root: https://yourdomain.com

Anchors:
  ✔ type: ...
  ⚠ Missing anchor: entity
  ...
❌ DFH descriptor is NOT structurally complete.
In that case, update your /.well-known/stack file to include the missing pieces and run the validator again.

7. One-Command Installer (tools/install-dfh.sh)
The installer script creates a baseline DFH descriptor in the current directory.

⚠ This is a scaffold only — you must edit the generated file to match your real domain and anchors.

7.1 Usage
From your project root:

bash
Copy code
bash tools/install-dfh.sh
This will:

Create .well-known/ if it doesn’t exist

Write a minimal .well-known/stack file with placeholder values

Generated file (baseline):

json
Copy code
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
Then:

Open .well-known/stack in your editor.

Replace https://example.com and other placeholder URLs with your real endpoints.

Deploy and validate as described above.

8. Examples
The examples/ directory contains working example stacks for three topics:

examples/water/

examples/automotive/

examples/healthcare/

Each example includes:

A DFH descriptor at .well-known/stack

A corresponding sitemap.xml

8.1 Water Example
examples/water/.well-known/stack:

json
Copy code
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
examples/water/sitemap.xml is a simple sitemap for that topic surface.

8.2 Automotive & Healthcare
Automotive and healthcare follow the same pattern:

Topic-specific root

Five anchors pointing at type/entity/url/sitemap/canonical URLs

Optional mirrors array

Use these examples as templates for your own topic domains.

9. Hosting Notes
DFH is designed to work on any hosting platform that can serve static files.

9.1 Static Hosts (Netlify / Vercel / Cloudflare)
Ensure .well-known/stack is part of your repository or build output.

On deployment, confirm:

text
Copy code
https://<your-site>/.well-known/stack
returns your JSON.

9.2 Traditional Servers (Nginx / Apache)
Place .well-known/stack in the document root.

Ensure your server configuration does not block the .well-known/ path.

Confirm that the file is served with:

text
Copy code
Content-Type: application/json
(or application/ld+json if using JSON-LD).

10. Mirrors
Mirrors are secondary domains that:

Reference an existing Root, and

Add context, scope, or specialization (industry, region, modality, etc.)

A Mirror can host its own DFH descriptor at /.well-known/stack, but it does not claim to be the sole Root.

See docs/mirrors.md for:

Mirror structure

Best practices

Consumption guidelines

11. SEO & AI Behavior
DFH is designed as a topic-level SEO primitive and an AI grounding hint:

Moves from page-level to topic-level identity

Provides a deterministic sitemap via the sitemap anchor

Strengthens E-E-A-T signals at the topic level

Gives AI systems a stable first-hop to reduce ambiguity and hallucinations

See docs/seo-benefits.md for a full discussion.

12. Adoption Path
Summary from docs/adoption.md:

Minimal Adoption (5-Minute Path)

Publish /.well-known/stack with minimal anchors.

Verify and validate.

Recommended Adoption

Improve anchor targets (richer type/entity/canonical structures).

Add mirrors if you operate multiple topic domains.

Keep descriptors updated (dct:modified).

Ecosystem Adoption

Search engines treat DFH as a structural quality hint.

AI systems use DFH as a topic bootstrap step:
topic → DFH root → anchors → data.

13. Roadmap
The high-level roadmap for DFH and this repo is in ROADMAP.md.

Phases include:

Phase 0 — Concept stabilization (done)

Phase 1 — DFH v1.0 spec (current)

Phase 2 — Reference implementations

Phase 3 — Ecosystem & governance

Phase 4 — AI & search alignment

Phase 5 — Extensions & v2.0

5.2 Provenance Layer — Anchors 6–10 (DFH v1.0 Extension)

Meaning Layer (Anchors 1–5) tells AI what the topic is.
Provenance Layer (Anchors 6–10) tells AI who said it, when, how, and under what authority.

The Provenance Layer eliminates ambiguity, strengthens trust, and allows DFH to function as a verifiable semantic root inside AI grounding pipelines.

These five anchors are optional for minimal installs but recommended for every Root domain.

### The Ten-Anchor Set (Full DFH Identity + Provenance Model)
Layer	Anchors	Purpose
Meaning Layer	1. type
2. entity
3. url
4. sitemap
5. canonical	Defines the what of the domain
Provenance Layer	6. authority
7. license
8. modified
9. issued
10. signature	Defines the who, when, and legitimacy
5.2.1 Anchor 6 — authority

Declares who controls the topic root.

Used by: AI systems, search engines, KG arbitration layers.

Example (JSON):

"authority": {
  "name": "Water Semantic Root Foundation",
  "url": "https://watersitemap.com",
  "verifiedByDNS": true
}


Rules:

Name must be human-readable.

URL must be under your control.

DNS verification MUST resolve to your Root.

5.2.2 Anchor 7 — license

Declares rights & re-use conditions for the semantic material.

Example:

"license": {
  "spdx": "MIT",
  "url": "https://watersitemap.com/license"
}


Rules:

SPDX identifiers recommended (MIT, CC0, CC-BY, Apache-2.0).

Used by search engines + AI for attribution logic.

5.2.3 Anchor 8 — modified

Timestamp of last semantic update to the Root.

Example:

"modified": "2025-12-11T08:15:00Z"


Rules:

MUST be ISO-8601.

Drives freshness scoring in AI grounding pipelines.

5.2.4 Anchor 9 — issued

Declares when the Root identity was created.

Example:

"issued": "2025-11-23T00:00:00Z"


Rules:

Immutable after initial declaration.

Used for provenance scoring and temporal ranking.

5.2.5 Anchor 10 — signature

Cryptographic signature proving authorship of the Root declaration.

Example:

"signature": {
  "alg": "ed25519",
  "publicKey": "https://watersitemap.com/key.pub",
  "signedAt": "2025-12-11T08:15:00Z",
  "value": "BASE64_SIGNATURE_HERE"
}


Rules:

Optional today → required in DFH v2.0.

Prevents impersonation or disputed topic claims.

AI systems treat signed Roots as higher confidence.

✅ FULL EXAMPLE — DFH Descriptor With All 10 Anchors

(Drop this into examples/water/.well-known/stack to make it “full provenance correct.”)

{
  "@context": "https://schema.org",
  "dfhVersion": "1.0",
  "root": "https://watersitemap.com",

  "anchors": {
    "type": "https://watersitemap.com/type.json",
    "entity": "https://watersitemap.com/entity.json",
    "url": "https://watersitemap.com/url.json",
    "sitemap": "https://watersitemap.com/sitemap.xml",
    "canonical": "https://watersitemap.com/canonical.json",

    "authority": {
      "name": "Water Semantic Root Foundation",
      "url": "https://watersitemap.com",
      "verifiedByDNS": true
    },

    "license": {
      "spdx": "MIT",
      "url": "https://watersitemap.com/license"
    },

    "modified": "2025-12-11T08:15:00Z",
    "issued": "2025-11-23T00:00:00Z",

    "signature": {
      "alg": "ed25519",
      "publicKey": "https://watersitemap.com/key.pub",
      "signedAt": "2025-12-11T08:15:00Z",
      "value": "BASE64_SIGNATURE_HERE"
    }
  },

  "mirrors": [
    "https://watersites.com",
    "https://industrialwatersitemap.com"
  ]
}

✅ Sitemap Provenance Requirement (Add to your sitemap docs)

Your sitemap must reflect the same provenance identity.

Add this to the <urlset> header:

<!-- DFH Provenance -->
<dfh:root>https://watersitemap.com/.well-known/stack</dfh:root>
<dfh:issued>2025-11-23T00:00:00Z</dfh:issued>
<dfh:modified>2025-12-11T08:15:00Z</dfh:modified>


This binds the sitemap to the Root declaration.

14. License
This project is licensed under the MIT License.
See LICENSE for full text.

text
Copy code
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
15. Where to Start
Read docs/spec.md for the full DFH v1.0 spec.

Copy examples/water/.well-known/stack (or the minimal JSON above).

Adapt it for your domain and topic.

Deploy .well-known/stack.

Run node tools/dfh-validator.js https://yourdomain.com.

Your domain is now a DFH Root for that topic.
Welcome to the Semantic Stack.


🌐 DFH / SLPI: Optional 10-Anchor Extension for High-Trust Domains
Why Most Companies Only Need 5 Anchors — And Why Some Need All 10

DFH / SLPI is designed around a minimal, deterministic core that any domain can deploy in under a minute.
This core is the 5-Anchor Meaning Layer, which communicates the what, who, and where of a domain in a machine-verifiable way.

But for high-trust industries — research, journalism, finance, government, legal, scientific publishing — meaning alone is not enough.

They also need provenance.

This post explains the optional 10-Anchor Extension, why it exists, and who should use it.

✅ The 5-Anchor Meaning Layer (Default, Recommended for 99% of Domains)

These anchors define the deterministic identity of your domain:

Anchor	Purpose
/type	What kind of thing this domain represents
/entity	The entity’s unique identity
/url	The domain’s authoritative location
/canonical	The canonical name / label / ID
/sitemap	The surface area the domain exposes

This layer is:

minimal

universal

backward-compatible

enough for all AI systems to lock onto meaning deterministically

For most companies, this is all that is required for full DFH compliance.

Deploy it → and your domain becomes AI-readable, indexable, and meaning-stable.

🔐 The Optional 10-Anchor Extension (For Heavy Hitters Only)
The Provenance Layer: “Why Trust It?”

Some domains must provide more than meaning.
They must provide verifiable provenance — the origin, lineage, and trust properties of what they publish.

For those cases, DFH offers the optional† provenance anchors:

Anchor	Purpose
/source	Who asserted the identity or claim
/derivation	What the content was derived from
/history	How it changed over time
/license	Legal permissions for use
/integrity	Checksums / signatures for tamper-proofing

These anchors are recommended for:

scientific institutions

academic research domains

financial or regulatory bodies

news and journalism outlets

legal or compliance-critical systems

archival, preservation, and distributed-trust networks

These organizations rely on traceability, auditability, and chain-of-custody guarantees — which standard 5-anchor identity cannot provide.

🧩 Layered by Design: Minimal Core, Optional Trust Expansion

DFH’s architecture deliberately follows a layered protocol approach:

Layer 1 = Meaning (Anchors 1–5)

Mandatory

Minimal

Zero dependencies

Layer 2 = Provenance (Anchors 6–10)

Optional

High-trust domains only

Adds cryptographic and lineage semantics

This keeps DFH:

simple for everyday use

industrial-strength for organizations that need it

future-proof for AI grounding and regulatory frameworks

🏁 Summary

If you run a typical business or website → deploy Anchors 1–5.

If you publish knowledge that must be trusted, verified, or regulated → extend to Anchors 6–10.

One protocol. Two layers. Universal adoption, optional provenance.

This is the cleanest and most scalable model:
maximum simplicity for the web, maximum trust for the institutions that require it.
