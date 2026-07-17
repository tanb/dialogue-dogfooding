---
id: STATE-PRODUCT-DIRECTION-001
type: state
title: Dialogue Product Direction v1
status: active
scope:
  project: dialogue
  domain: product
  subject: product-direction-v1
revision: 1
created_at: "2026-07-17T23:59:31+09:00"
updated_at: "2026-07-17T23:59:31+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROJECT-CHARTER-001
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0012
  - CHANGE-0012
canonical_for: dialogue/product/direction-v1
owners:
  - person:project-owner
extensions:
  document_kind: product-direction
  version: 1
  session: office-hours-2026-07-17
---

# Dialogue Product Direction v1

`STATE-PRODUCT-SCOPE-001` is the source of truth that defines the deliverables and acceptance criteria of Product v1. This document sits above it and is the source of truth for the direction, positioning, next step, and North Star; it does not change the scope contract.

## Thesis

**Decided facts should live in one place.**

What Dialogue provides is not a knowledge management tool but a **single source of truth for decisions**. Not in the code, the chat logs, or the Git commit history — only "what was decided and why" lives in one place. Both humans and multiple AI Agents read from the same source of truth and write to the same source of truth. Even when working multi-agent by multi-human, decisions stay singular.

## Two pillars

1. **Governance (single source of truth for decisions + conflict → human Escalation)**
   When multiple Actors update the same knowledge and disagree, do not let the source of truth silently branch via last-write-wins. Stop and escalate to a human. This "stop and ask a human" is the substance of Governance, not the shared storage itself.

2. **Anti-rot (detection of staleness and duplication + continuous curation by an Agent)**
   Dialogue treats duplication, contradiction, broken references, and staleness as targets of continuous maintenance, and promises to have an Agent curate them. Human documents rot if left alone. Agent-driven continuous maintenance keeps knowledge "rot-free." This is the killer differentiator — the deciding factor for "this is what I wanted."

## Positioning and differentiation

- **Primary differentiation (vs. Agent memory: CLAUDE.md / rules, etc.)**
  Agent memory is "one agent's private notes," siloed per repo and per person, and it detects neither rewrites nor contradictions. Dialogue is shared, canonical, and escalates on conflict. It unifies everyone's memory into one and stops the variance.

- **Promotional headline (vs. wikis such as Notion / Confluence)**
  "Nothing is as sloppy as human document management." A wiki is a human-facing UI that an Agent cannot mechanically discover and verify, and it does not detect rot. Dialogue has Agent-native discovery via `.dialogue.yml`, mechanical verification via Schema + Conformance, and a Governance Protocol built for Agents.

## Canonical placement is configurable

The location of the source of truth can be chosen in `.dialogue.yml`. It can be an independent Repository, or you can point the Knowledge root at the same Repository. However, if the same Repository is made the source of truth, a per-branch source-of-truth state arises, so a merge operational burden occurs. This burden must be chosen with the adopter understanding it. The Protocol is neutral about placement and does not force an independent Repository.

## Next step (decided): Collision & rot demo

The biggest bottleneck in conveying the direction is the absence of "evidence that can be shown." The next step is a working example Knowledge Repository and a driver-based live demonstration.

1. A scene where two Agents update the same decision and collide, and Dialogue stops and escalates to a human.
2. A scene where staleness and duplication are detected and an Agent curates them.

Reuse the existing `tests/conformance`, the Product Skill's `resolve-source`, and the `.dialogue.yml` template. This demo becomes a prerequisite for both the North Star (below) and promotion.

## North star: Turbovec-backed MCP for fast canonical search

As a North Star, we record the concept of, in the future, preparing an MCP integrated with Turbovec to provide fast search over the source of truth. Speeding up access to the source of truth leads to faster document reference and decision-making, and can become killer content.

**Constraints (protecting canonicity):**

- The Turbovec search layer is positioned **not as the source of truth, but as a derived read accelerator that sits on top of the Git source of truth**. This is consistent with Dialogue's principle that "RAG and search indexes are derived artifacts and are not the source of truth of knowledge."
- Because vector/semantic search is approximate and lossy, it is used **to speed up discovery (where and what is handled, and the related decisions)**, and the authoritative read (what did we decide) is **handed off to the exact source-of-truth record** rather than an approximate guess.
- This concept is **outside the Product v1 scope** and does not contradict "Outside initial scope: RAG or Vector Database" in `STATE-PRODUCT-SCOPE-001`. It is not implemented in v1; the demo above (the next step) goes first.

## Relationship to Product Scope v1

- This document does not change the scope contract or acceptance criteria of `STATE-PRODUCT-SCOPE-001`.
- The Turbovec MCP is a North Star outside the v1 scope and is a derived layer that is not the source of truth, so it is consistent with the Vector Database exclusion of the scope doc.
- Of the Two pillars, Governance coincides with the primary flow of v1 (Human Escalation, independent Change Record). This document canonicalizes for the first time the Anti-rot "continuous curation by an Agent" as an explicit product promise.

## Open questions

1. To what extent should Anti-rot (staleness and duplication detection, and Agent curation) be specified as a formal operation of the Protocol (a future Approach B candidate)?
2. Through which flow and document should the branch-and-merge operational burden of same-Repository canonicity be presented to adopters?
3. The concrete design of the discovery → source-of-truth handoff boundary of the Turbovec MCP (after v1).
