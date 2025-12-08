The Semantic Layer of the Public Internet (SLPI)

> **Status:** Public Concept  
> **Version:** 1.0  
> **Spec Family:** SFH / DFH (Semantic First-Hop / Deterministic First-Hop)  
> **License:** MIT  

---

## 0. Overview

The **Public Semantic Layer (PSL)** is the internet’s **deterministic starting point for meaning**.  

It provides a **universal, machine-readable anchor** that lets AI systems and search engines resolve canonical definitions **without crawling, ranking, or probabilistic guesswork**.

The **Semantic First-Hop / Deterministic First-Hop (SFH/DFH)** protocol defines a **universal, decentralized index of meaning** that lives between:

- **DNS** → location authority  
- **Content** → payload  

SFH/DFH turns domains into **root semantic authorities** and gives machines a **deterministic identity record** they can resolve before doing any heuristic interpretation.

---

## 1. Core Architecture & Deterministic Entry

SFH/DFH is intentionally built on **existing web primitives**:

- DNS
- HTTPS
- `/.well-known/` paths
- JSON-LD

No proprietary dependencies. No closed APIs. No hidden ranking logic.

Under SFH/DFH, a **domain**:

- Becomes the semantic root for its **declared topic**.
- Publishes a **DFH descriptor** (JSON-LD).
- Exposes **five anchors** that define the minimal semantic identity record.

### 1.1 Core Components

| Component        | Description                                                                                          |
|-----------------|------------------------------------------------------------------------------------------------------|
| Root Domain     | Publishes the canonical semantic definition for a topic. DNS proves origin & ownership.             |
| DFH Descriptor  | Machine-readable JSON-LD identity record at `https://<domain>/.well-known/stack`.                   |
| Five Anchors    | Minimal canonical identity record; removes guesswork before embeddings or KG lookups.               |
| Mirrors         | Optional supporting domains; extend context but cannot override the Root’s meaning.                  |

**Key Property:**  
Semantic identity becomes a **lookup**, not an inference.

---

## 2. The Five Anchors (Semantic Primitives)

Every DFH-compliant domain exposes five logical anchors.  
These anchors define the **minimal canonical identity record** for a topic.

They let AI systems deterministically ground meaning **before**:

- embeddings
- classification
- KG integration
- retrieval or ranking

### 2.1 Anchor Table

| Anchor       | Purpose             | Contents                                                              |
|-------------|---------------------|-----------------------------------------------------------------------|
| `/type`     | Ontological class   | Category: Product, Person, Company, AI Model, Concept, Topic, etc.    |
| `/entity`   | Instances           | Declared entities: SKUs, models, versions, variants, child topics.   |
| `/url`      | Origin control      | Canonical URL, alternate mirrors, ownership/provenance signals.      |
| `/sitemap`  | Topic topology      | Structured map of subtopics, sections, semantic routing table.       |
| `/canonical`| Stable identity     | Name, aliases, unique IDs, durable identifiers for the topic.        |

**Goal:**  
Provide enough **pre-KG structure** that a client never has to “guess” what the topic is.

---

## 3. DFH Descriptor

The DFH descriptor lives at:

```text
https://<domain>/.well-known/stack
It is a JSON-LD document that:

Declares the topic’s canonical meaning.

Lists the five anchors.

Optionally links to mirrors and external graphs.

3.1 Example DFH Descriptor (Minimal)
json
Copy code
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "Example Topic",
  "url": "https://example.com",
  "dfhVersion": "1.0",
  "dfhAnchors": {
    "type": "https://example.com/type",
    "entity": "https://example.com/entity",
    "url": "https://example.com/url",
    "sitemap": "https://example.com/sitemap",
    "canonical": "https://example.com/canonical"
  },
  "dfhMirrors": [
    "https://mirror1.example.org",
    "https://mirror2.example.net"
  ]
}
4. DFH → KG Arbitration Model (AI Truth Pipeline)
SFH/DFH is designed to plug directly into modern AI architectures that must balance:

deterministic declarations (DFH)

global coherence (KG)

safety & policy (RLHF, filters)

4.1 Authority Pipeline
text
Copy code
DNS → DFH → KG → RLHF → Model Output
4.2 Roles & Epistemic Authority
Layer	Role	Authority Class
DNS	Proves physical origin & control of the domain.	Highest physical authority
DFH	Declares canonical topic meaning & structure.	Strong deterministic input
KG	Validates, cross-checks, reconciles DFH + world.	Final semantic arbiter
RLHF	Applies safety, legal, policy rules.	Veto power
Output	What the user actually sees.	Policy-compliant truth

4.3 Critical Rule
Safety and systemic coherence always override deterministic claims.

Implications:

DFH is privileged but not absolute.

The Knowledge Graph (KG) decides whether DFH is:

accepted

modified

rejected

RLHF / safety can override even accurate DFH truth if it violates:

safety policies

legal constraints

platform rules

Mental model:

DFH → Deterministic intent

KG → Operational truth

RLHF → Permitted truth

5. AI Grounding & SEO Impact
SFH/DFH operates at the concept / topic level, not the individual page level.

This changes how:

AI systems ground meaning.

search engines compute authority.

crawlers and agents explore a domain.

5.1 AI Grounding Benefits
Instant Disambiguation
The topic’s identity is declared explicitly in DFH, not inferred from content.

Elimination of Root Hallucination
The model doesn’t have to guess “what this site is about” — DFH defines it.

Deterministic Bootstrap
First step becomes a lookup against DFH, not a fuzzy heuristic crawl.

5.2 SEO Advantages
Topic-Level Authority
Authority shifts upstream from individual pages to the canonical semantic definition.

Hardwired E-E-A-T
Expertise, experience, authority, and trust can be encoded in:

/canonical

/entity

/type
and consumed structurally by AI/KG systems.

Clean Deterministic Crawl Surface
Indexers can:

start from the DFH descriptor and /sitemap

avoid expensive exploratory crawling

immediately locate the “semantic spine” of the topic

6. Minimal Implementation Checklist
To make a domain SFH/DFH-ready:

Publish DFH descriptor

Create /.well-known/stack as a JSON-LD document.

Declare:

topic name

canonical URL

five anchor URLs

Expose the five anchors

Implement endpoints (static or dynamic) for:

/type

/entity

/url

/sitemap

/canonical

Use stable identifiers

Keep anchor locations stable.

Use durable IDs in /canonical and /entity.

Document mirrors (optional)

Use dfhMirrors to list supporting or regional domains.

Never let mirrors contradict the Root’s canonical definition.

7. Design Goals
Deterministic First-Hop
Replace “crawl & guess” with “resolve & ground.”

Decentralized Control
Every domain can declare its own canonical meaning without a gatekeeper.

Compatibility
Uses only:

DNS

HTTPS

/.well-known/

JSON-LD

AI-Native
Mirrors how LLMs and KGs already canonicalize internally, but makes the process public and inspectable.

8. Summary
The Semantic Layer of the Public Internet (SLPI), implemented through the SFH/DFH protocol, is:

a public, deterministic index of meaning

a missing semantic layer between DNS and payload

a new root primitive for:

AI grounding

SEO

structured indexing

It doesn’t replace search, KGs, or safety systems.
It gives them a clean, deterministic first-hop so they don’t have to guess what the internet means.
