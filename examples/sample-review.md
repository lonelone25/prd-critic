# PRD Review: PetPantry Vet-Diet Match

**Source:** `examples/sample-prd.md`
**Reviewed:** 2026-05-07
**Reviewers:** Staff Engineer · Staff Designer · CFO · Sales/GTM · Customer Success · Skeptical Exec

---

## Summary

The PRD has a sharp problem statement and a real, identifiable target user (owners of dogs on prescribed therapeutic diets). The core tension: the entire model assumes vets will route patients to PetPantry, but the PRD offers vets neither incentive, attribution, nor workflow integration — five of the seven blockers below trace back to this gap. Top blockers: success metrics in section 5 are unmeasurable as written, and the unit economics in section 6 are asserted ("healthy margin") without any underlying math. Full review below.

---

## What Works Well

- **Section 1 problem statement** — names a specific user (owner of a dog with chronic condition), a specific pain (3-month lapse rate), and a specific cause (fragmented buying experience). Most consumer PRDs don't get this concrete.
- **Section 3 target user** — a defined segment with a TAM estimate, not "pet owners." A reviewer can immediately picture the customer.
- **Section 4 scope** — explicit list of what's in v1, including the vet portal as a first-class surface rather than an afterthought.

---

## The Core Tension

The PRD is built on the assumption that vets will direct patients to PetPantry, but vets are mentioned only as a feature surface (the portal in section 4) and a future risk (section 8). There is no incentive structure, no clinical-attribution mechanism, no answer to what happens when the algorithm and the vet disagree, and no GTM motion targeting clinics. Without solving for the vet, the rest of the PRD describes a price-competitive food subscription against incumbents like Chewy with no defensible edge.

---

## Blockers

### 1. Success metrics in section 5 are unmeasurable as written
**Raised by:** Skeptical Exec, CFO
**Cites:** Section 5, "Increase user engagement by launch + 90 days"
**Concern:** None of the three metrics has a number, baseline, or measurement method. "Engagement" on a subscription product is undefined — is it monthly delivery acceptance rate? Cancellation rate? Reorder uplift? "Hit revenue targets for FY27" is circular. With this section as written, there is no kill criterion 90 days post-launch.
**Suggested edit:** Replace section 5 with: "(a) ≥75% of subscribers receive ≥3 consecutive deliveries without skip or cancel; (b) ≥500 vets register on the portal in first 6 months; (c) $X ARR run-rate by month 9, where X = (committed FY27 target / 12) × 0.4."

### 2. Unit economics in section 6 are asserted, not shown
**Raised by:** CFO
**Cites:** Section 6, "supports a healthy contribution margin"
**Concern:** No COGS, no fulfilment cost, no churn assumption, no LTV. Therapeutic dog food has heavy SKUs (often 30+ lb bags), which means shipping cost is a meaningful percentage of revenue and varies by zone. Brand wholesale terms for therapeutic SKUs are not the same as mainstream — Hill's, Purina Pro Plan Veterinary, and Royal Canin enforce minimum advertised pricing in some channels. The 15%-below-clinic claim may not survive their pricing policies.
**Suggested edit:** Add a unit economics table with per-order revenue, COGS, fulfilment, payment processing, and contribution margin at three churn assumptions (best / base / bear). Confirm wholesale terms for the four target brands before promising the price point.

### 3. Vet incentive and attribution are entirely absent
**Raised by:** Sales/GTM, Skeptical Exec, Customer Success
**Cites:** Section 4, "vet portal where vets can submit recommendations"
**Concern:** Why would a vet send patients to PetPantry instead of the in-clinic sale or a competitor? There is no commission, no rev-share, no clinic-tier programme, no co-branded materials, no clinical reporting back to the vet. Without this, the vet portal is a feature in search of a behaviour. The current model also cannibalises clinic revenue, which makes the vet's incentive actively negative.
**Suggested edit:** Add a section 4.1 "Vet Programme" specifying: (a) commission or rebate per active subscriber attributed to the clinic; (b) what reporting the vet gets back (adherence, reorder cadence); (c) co-branded onboarding email when a vet refers a patient.

### 4. "All 50 states at launch" ignores interstate veterinary regulations
**Raised by:** Staff Engineer, Customer Success
**Cites:** Section 4, "We will support all 50 US states at launch"
**Concern:** Therapeutic pet food sits in a regulatory grey zone — some states require an active VCPR (veterinarian–client–patient relationship) for prescription diets, and some brands restrict sale of certain SKUs to verified prescriptions. Operating across all 50 states without a state-by-state compliance review will likely surface a cease-and-desist within months and hit the team with unplanned legal work mid-launch.
**Suggested edit:** Replace with "Launch in 5 states selected for regulatory clarity and population density. Add states quarterly after compliance review per state."

### 5. No path for users without an existing vet relationship
**Raised by:** Staff Designer, Customer Success
**Cites:** Section 1 implies an active vet relationship; sign-up flow in section 4 requires "vet's recommended food"
**Concern:** A meaningful share of the addressable population has a recent diagnosis but limited recurring vet contact (rural users, lower-income users, owners between vet visits). The PRD's onboarding flow has no handling for this user — they can't sign up at all. This either silently shrinks the TAM or pushes users to fabricate a recommendation.
**Suggested edit:** Add a "no vet on file" branch that lets the owner upload a prescription image or enter the diagnosis, with a follow-up step to verify with a partner telehealth vet before the second shipment.

### 6. Vet portal data flow is undefined and likely regulated
**Raised by:** Staff Engineer
**Cites:** Section 4, vet portal feature
**Concern:** The PRD doesn't say what data the portal stores, who owns it, where it lives, or what consent the pet owner gives the vet to act on their behalf. "Vet recommendation" is medical-adjacent data; in some states it intersects with pet medical records and HIPAA-equivalent expectations. There is no mention of audit logs, role permissions, or data retention. This is a security and compliance review waiting to happen the week before launch.
**Suggested edit:** Add an NFR section: data classification, retention, audit logs, role model (vet vs. clinic admin vs. PetPantry support), and consent capture flow at sign-up.

### 7. Timeline is aggressive to the point of unserious
**Raised by:** Staff Engineer, Customer Success
**Cites:** Section 7, "Month 4: Public launch"
**Concern:** Four months covers catalogue ingestion (40 SKUs across 4 brands with wholesale negotiations), matching logic, subscription billing, fulfilment integration, vet portal, regulatory review across 50 states, and 100-user beta. Every one of those is a multi-month workstream alone. This timeline implies either no QA, no security review, or scope is much smaller than section 4 describes.
**Suggested edit:** Either cut scope (drop vet portal and 50-state launch from v1, plan as v2) or extend timeline to 8–10 months with named gates (catalogue locked, beta cohort retention ≥X%, regulatory clearance for launch states).

---

## Serious Concerns

### 1. No competitive positioning vs Chewy / Petco / brand-direct
**Raised by:** Sales/GTM
**Cites:** Section 1 mentions fragmented buying but doesn't name competitors
**Concern:** Chewy already sells therapeutic SKUs and has Autoship. The PRD doesn't say what PetPantry does that Chewy can't. "Vet recommendation captured at sign-up" is a thin moat — Chewy can ship that in a sprint. Without a clearer wedge (the vet relationship, deeper formulary expertise, faster veterinary onboarding), the team will struggle to explain to a buyer why they're switching.
**Suggested edit:** Add a "Why us, why now" section comparing PetPantry's wedge to the three named incumbents and to direct-to-consumer brand offerings.

### 2. "4-week cycle" assumes a single bag size and dog
**Raised by:** Staff Designer, Customer Success
**Cites:** Section 4, "Deliver on a 4-week cycle"
**Concern:** Therapeutic SKUs come in multiple bag sizes; consumption rate varies by dog weight (a 7kg Bichon eats meaningfully less than a 35kg Labrador on the same diet). A fixed 4-week cycle will overship for small dogs and undership for large ones, generating churn and cancellations. The PRD has no logic for per-dog consumption modelling.
**Suggested edit:** Replace "4-week cycle" with a per-dog cadence calculated from weight × kcal/kg/day × kcal/g of food, recalculated each delivery based on actual reorder timing.

### 3. Open questions in section 8 are far too few
**Raised by:** Skeptical Exec
**Cites:** Section 8 lists 2 open questions
**Concern:** A PRD this scope-rich (subscription, multi-brand catalogue, vet portal, 50-state launch) with only two open questions signals the PM hasn't surfaced enough unknowns. Reviewers will assume blind spots until the open questions list is comprehensive.
**Suggested edit:** Expand section 8 to 8–12 open questions covering pricing elasticity, vet incentive structure, regulatory gating, COGS sensitivity, churn drivers, and competitive response.

### 4. No empty / error / not-eligible states described for sign-up
**Raised by:** Staff Designer
**Cites:** Section 4 sign-up flow
**Concern:** What does the user see when their vet's recommended food isn't in the catalogue? When the portal lookup of their vet returns no match? When their dog's diagnosis maps to multiple competing diets? The PRD describes only the happy path. Each of these states will either bounce users or silently fail.
**Suggested edit:** Add "Error and edge states" subsection enumerating: catalogue miss, vet not found, multiple diet match, owner outside launch state, dog under min weight for any SKU.

### 5. CS playbook for clinical-conflict cases is missing
**Raised by:** Customer Success
**Cites:** Section 8 mentions "vets who push back" but doesn't address resolution
**Concern:** When a vet calls support saying PetPantry shipped the wrong food, or the owner shows the vet a delivery that contradicts the recommendation, the CS team has no playbook. Clinical-adjacent disputes need a defined escalation, not improvisation. First few of these will become Twitter posts.
**Suggested edit:** Add a CS section covering: dispute categorisation, refund / reship policy, vet escalation contact, audit trail requirements.

---

## Unanswered Questions, by Persona

**Staff Engineer**
- What's the data model for vet ↔ owner ↔ pet ↔ recommendation, and who can edit each?
- What's the SLA for the vet portal and what's the failure mode when fulfilment integrations are down?
- How does the matching algorithm handle a vet recommendation for a SKU not in the catalogue?

**Staff Designer**
- What's the onboarding experience for an owner who doesn't know their dog's exact diagnosis?
- How does the user change their dog's prescribed diet mid-subscription if the vet updates it?

**CFO**
- What's the assumed annual churn rate, and what's the LTV at that churn?
- What's the CAC assumption and the channel mix supporting it?
- What's the sensitivity of contribution margin to shipping zone?

**Sales / GTM**
- What's the wedge against Chewy that survives a 90-day competitive response?
- Is the vet programme the GTM, or is paid acquisition the GTM with vet as a feature?

**Customer Success**
- What's the projected ticket volume per 1,000 active subscribers in the first 90 days?
- What's the change-management plan when a brand reformulates a SKU?

**Skeptical Exec**
- Why now — what's changed in the market that makes this the right moment vs. last year or next year?
- If we hit 50% of the FY27 target, do we kill, double down, or pivot?

---

## Suggested Next Revision

1. Rewrite section 5 success metrics with numbers, baselines, and measurement windows.
2. Add a section 4.1 "Vet Programme" with attribution, commission, and reporting.
3. Add a unit economics table with COGS, fulfilment, churn assumptions across three scenarios.
4. Replace "all 50 states at launch" with a defined launch-state list and quarterly expansion plan.
5. Add a "no vet on file" sign-up branch with telehealth verification.
6. Add an NFR / data section covering vet portal classification, retention, consent, and roles.
7. Either cut scope or extend the timeline; pick one before circulating v2.
8. Expand open questions to 8–12 items.

---

## Nits

- Section 2 has three goals but no priority order — which is the primary goal?
- Section 4's "4 major therapeutic brands" should name them.
- Section 6 should specify whether the 15%-below-clinic price holds for new customers only or for all customers.
- Section 7 milestone "Scale" in month 5+ has no definition.
- Author and reviewer fields in the header are missing.
