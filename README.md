# TRACE: A Practical Operating Model for CTI Teams

**TRACE** stands for *Threat Relevance Assessment and Contextual Evaluation*. It is an opinionated operating model for Cyber Threat Intelligence work, built around a single analytical claim: **external severity is not internal priority**. A CTI team exists to determine what external intelligence means internally, whether the organization is exposed, which assets are at risk, which teams need to act, which telemetry can confirm or refute the threat, and which defensive actions should be prioritized first.

This repository contains the three documents that make up the TRACE model, intended to be forked, adapted, and used by CTI teams as a starting point for their own operating procedures.

## The question this model answers

When an intelligence trigger arrives, what should the CTI team actually do?

For example:

- A new critical CVE is published
- A security vendor reports an active campaign
- A peer organization in the same sector is compromised
- A threat actor changes targeting patterns
- A supply chain provider is breached
- A geopolitical event increases the likelihood of cyber activity
- A malware family gains a new capability relevant to the organization

TRACE provides a structured answer: a five-phase response procedure, a severity scoring matrix that combines intrinsic threat properties with organizational exposure, and a separate scoring model for threat actors that treats actor relevance as a persistent analytical assessment.

## Why TRACE exists

CTI teams are often judged by the quality of their intelligence products, but their real value depends on what happens after intelligence arrives. A report, advisory, CVE, campaign write-up, or actor profile is not automatically actionable. The CTI team must determine whether the information is credible, whether it applies to the organization, which teams need to act, what evidence should be collected, what detections or hunts should be prioritized, and how the threat should be tracked over time.

Without a defined procedure, this response becomes inconsistent. One analyst may escalate immediately, another may wait for corroboration, another may forward indicators without context, and another may spend days on analysis before involving operational teams. The result is delay, duplication, and uneven prioritization.

TRACE provides a repeatable workflow that helps CTI teams respond consistently when new intelligence arrives, with the analytical decisions at each step made explicit and defensible.

## From external intelligence to internal relevance

A central principle of TRACE is that intelligence only becomes operationally useful when it is contextualized.

A threat may be severe in the abstract but irrelevant to a specific organization. Conversely, a threat that appears moderate externally may be highly significant for an organization with the wrong exposure, weak controls, or critical dependencies. For example:

- A vulnerability affecting a technology the organization does not run may require tracking, but not emergency response
- A local privilege escalation vulnerability may become critical in a Linux-heavy environment with exposed multi-tenant systems
- A threat actor with world-class capability may not matter if there is no intent to target the organization, its sector, or its geography
- A campaign targeting telecommunications providers may be far more relevant to a telco than to an organization in an unrelated sector
- A supply chain compromise may be critical for one company and negligible for another, depending on vendor usage and dependency depth

This is why CTI should not simply repeat external severity ratings. The team must assess whether the threat is a threat **to the organization being defended**.

## The role of analytical scoring

The scoring models in TRACE are designed to make CTI prioritization more consistent, transparent, and defensible.

Analysts inevitably make judgments about credibility, relevance, capability, exposure, and urgency. The purpose of scoring is not to eliminate judgment or create false mathematical precision. Instead, analytical scoring helps analysts make their assumptions explicit, so that the reasoning behind a prioritization decision can be reviewed, challenged, and improved.

This matters because external reporting is noisy. Public attention, vendor marketing, media amplification, and community chatter can distort perceived urgency. A scoring model forces the team to return to the core analytical question: **how relevant and dangerous is this threat to us?**

## The three documents

TRACE has three components, designed to work together.

### 1. `TRACE_Emerging_Threat_Response_Procedure.md`

A five-phase operating procedure for handling emerging intelligence triggers, from intake to follow-up.

1. **Intake & Initial Triage** — Verify the trigger, assess source credibility, summarize the issue, assign provisional severity, and decide whether an early advisory is needed.
2. **Exposure Assessment** — Determine whether the organization is exposed technically, operationally, relationally, or through detection gaps.
3. **Deep-Dive Analysis** — Understand the threat in depth and translate it into realistic attack scenarios, detection opportunities, and hunt hypotheses.
4. **Stakeholder Notification & Final Threat Assessment** — Produce the formal assessment and notify the teams that need to act.
5. **Tracking & Follow-Up** — Reassess the threat over time, track remediation or hunting outcomes, and capture lessons learned.

### 2. `TRACE_Severity_Tier_Matrix.md`

A two-axis scoring model that assigns an internal response tier (P1 to P4) to intelligence triggers. The two axes are:

- **Threat Severity** — How severe the threat is in the abstract, based on its intrinsic characteristics.
- **Exposure Level** — How exposed the organization is to that threat across technical, targeting, tradecraft, relational, and detection dimensions.

These two axes combine into a final contextual tier through a tier grid that deliberately weights exposure asymmetrically. The matrix helps the CTI team move from the external question *"how bad is this threat?"* to the internal question *"how bad is this threat for us?"*. The same trigger may be a P1 for one organization, a P3 for another, and a P4 for a third.

### 3. `TRACE_Threat_Actor_Scoring_Model.md`

The model scores three dimensions, drawn from the classical CTI threat triangle:

- **Intent** — Does the actor want to target us, our sector, our geography, or organizations like us?
- **Capability** — Can the actor execute operations at the level required to affect us?
- **Opportunity** — Does the actor have a realistic path to us through our sector, technology, exposure, relationships, or control gaps?

The three dimensions combine into a persistent **Threat Score** on a 0.0 to 1.0 scale.

## Suggested workflow

A practical way to use these files:

1. Start with the **Emerging Threat Response Procedure** when a new intelligence trigger arrives.
2. During Phase 1, assign a provisional severity based on the intrinsic properties of the trigger.
3. During Phase 2, assess exposure in the organization's actual environment.
4. Use the **Severity Tier Matrix** to assign the final contextual tier.
5. If the trigger relates to a threat actor, use the **Threat Actor Scoring Model** to assess the actor's persistent relevance.
6. During Phase 3, convert the threat into realistic attack scenarios, detection opportunities, and hunt hypotheses.
7. During Phase 4, issue a Threat Assessment with specific recommended actions for each stakeholder team.
8. During Phase 5, track remediation, detection deployment, hunt outcomes, re-tiering decisions, and lessons learned.

## Adopting and adapting TRACE

TRACE is opinionated and the choices it makes are deliberate, but they are not the only choices that work. The scoring weights (50% for Intent, 25% each for Capability and Opportunity), the tier thresholds, the SLAs, the band cutoffs, and the asymmetric weighting in the tier grid are reasonable defaults in my view, but any team adopting the model should calibrate them to its own context and risk appetite.

The model also assumes a set of capabilities that not every CTI team will have in place. The exposure assessment phase works only if the team can either query asset inventories directly or dispatch queries to domain owners under agreed response SLAs. The notification phase works only if relationships with stakeholder teams are already established. The actor scoring model works only if the team has the capacity to maintain persistent actor profiles and run a quarterly review cadence. The supporting documents list these pre-built dependencies explicitly.

If you adopt any of the model and find it useful, or if you find places where it breaks, feedback is welcome through GitHub issues or pull requests. CTI procedures improve through use across different organizations and different threat landscapes.

## Further reading

The TRACE model and its underlying rationale are described in narrative form in the accompanying blog post:

> [*From Intelligence to Action: A Practical Operating Model for CTI Teams*](https://medium.com/@mrtiepolo/from-intelligence-to-action-a-practical-operating-model-for-cti-teams-8169b6615c99)

The broader theoretical and practical foundations of the CTI and threat hunting work that TRACE supports are covered in my latest book:

> [*Advanced Cyber Threat Intelligence and Hunting*](https://www.amazon.com/Advanced-Cyber-Threat-Intelligence-Hunting/dp/1806380390), Packt Publishing.

---

**The most important idea behind TRACE is simple: a threat is not equally threatening to every organization. CTI exists to understand that difference.** The role of the CTI team is not only to know what is happening externally, but to determine what it means internally. That is what turns data into intelligence, and intelligence into action.
