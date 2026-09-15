# Step 0: Readiness Assessment Report
### Keystone Grants Management System (KGMS) | Pre assessment gap analysis

> ### PORTFOLIO EXERCISE, SIMULATED SYSTEM
> **Keystone Grants Management System (KGMS) does not exist.** The Federal Workforce Development Agency (FWDA) is a fictional federal
> agency invented for this portfolio. Every organisation, person, system
> identifier, network address, finding, date and signature on this page is
> fabricated for training purposes. Nothing here is drawn from any real
> employer, client or government system, and no real document, artifact or
> data has been reproduced. This file is coursework, not a government record.

---

**Document:** Readiness Assessment Report  
**Simulated system:** Keystone Grants Management System (KGMS) | `FWDA-KGMS-2026-MOD`  
**Framework and standards:** FedRAMP readiness criteria, NIST SP 800-37 Rev 2 Prepare step  
**Author:** Nkeiru Sarah Adesida  
**Document date:** 14 October 2025  
**Status:** Complete

**Navigation:** [Repository home](../README.md) &nbsp;|&nbsp; [Step 1: Categorise the System ->](../step-01-categorization/README.md)

---

## Purpose

A readiness assessment is the conversation that happens before the real paperwork
starts. Somebody sits down with the system team and asks, honestly, whether this
system is anywhere near ready to be assessed. If the answer is no, finding that out
now costs a meeting. Finding it out during the formal assessment costs a schedule.

Plain language version: this is the pre inspection walk round. Before the official
inspector arrives, you walk the building yourself with the checklist and write down
what you already know is broken.

This document records that walk round for KGMS, completed on
14 October 2025.

---

## Section 1: System information

| Field | Detail |
|---|---|
| System name | Keystone Grants Management System (KGMS) |
| System identifier | `FWDA-KGMS-2026-MOD` |
| Operating agency | Federal Workforce Development Agency (FWDA) (fictional) |
| System Owner | Marcus T. Delacroix |
| ISSO | Nkeiru Sarah Adesida |
| Authorizing Official | Patricia L. Ambrose |
| Chief Information Security Officer | Daniel K. Osei |
| Hosting platform | AWS GovCloud (US-East) |
| Cloud Service Provider | Keystone Digital Services LLC (fictional) |
| Target baseline | FedRAMP Moderate, NIST SP 800-53 Rev 5 |
| Deployment model | Agency managed application on an authorised Infrastructure as a Service platform |
| Assessment window sought | First quarter 2026 |

### Why the Moderate baseline and not Low

KGMS holds personally identifiable information on individual peer reviewers and
applicants, and it generates payment instructions that move federal funds. A loss of
confidentiality would expose applicant and reviewer information; a loss of integrity
could misdirect an award. Neither of those is a limited adverse effect, which is the
threshold for Low in FIPS 199. Moderate is the floor, not a conservative choice.

---

## Section 2: Readiness criteria

Result values are Ready, Gap or Partial. Partial means the capability exists but the
evidence to prove it does not, which in an assessment is treated as a gap.

| # | Capability | Result | Note |
|---|---|---|---|
| 1 | System boundary documented and agreed with the CSP | Ready | Boundary diagram and asset inventory current as of 2025-10-01 |
| 2 | Asset inventory maintained | Partial | Instances and managed services listed; container images not yet enumerated |
| 3 | Data flow diagram exists | Ready | Covers applicant submission, merit review and disbursement instruction paths |
| 4 | Privacy threshold analysis completed | Ready | Completed by Helen M. Barragan; a privacy impact assessment is required |
| 5 | Federated authentication for agency users | Ready | Agency identity provider, PIV card based |
| 6 | Multifactor authentication for all user populations | Gap | Contracted peer reviewers authenticate with a password only |
| 7 | Role based access control implemented | Ready | Nine application roles, least privilege reviewed quarterly |
| 8 | Privileged access request and approval records | Gap | Group membership exists without a completed approval record in some cases |
| 9 | Centralised logging | Ready | Seven log groups shipped to the agency log platform |
| 10 | Log retention meets the federal requirement | Partial | One log group configured to 90 days against a one year online requirement |
| 11 | Audit record review performed and evidenced | Partial | Daily alert review evidenced; weekly correlated review not consistently evidenced |
| 12 | Vulnerability scanning in place | Partial | Unauthenticated scanning only on the database tier |
| 13 | Patch management process documented | Ready | Monthly cycle with an emergency path |
| 14 | Configuration baselines defined | Ready | Hardened images per tier, derived from agency benchmarks |
| 15 | Configuration drift detection | Gap | No automated detection; drift found only at assessment |
| 16 | Encryption in transit | Ready | TLS 1.2 minimum on all external paths |
| 17 | Encryption at rest with a customer managed key | Partial | Primary region uses a customer managed key; the replica region does not |
| 18 | Backups performed and tested | Partial | Backups run nightly; a functional restore has never been tested |
| 19 | Contingency plan documented and exercised | Gap | Tabletop performed February 2025; no functional test |
| 20 | Incident response plan and reporting path | Ready | Documented, with reporting to the agency security operations centre |
| 21 | Security literacy and awareness training tracked | Partial | Eleven users past the annual due date |
| 22 | Personnel screening and separation process | Partial | Accounts disabled promptly; separation checklist not always on file |
| 23 | Supply chain risk management procedures | Gap | Draft exists, not approved |
| 24 | Interconnection agreements in place | Ready | Three interconnections, agreements executed |
| 25 | Secure development practices and code review | Ready | Peer review required, dependency scanning enabled |
| 26 | Input validation across all user supplied fields | Gap | Rich text fields on the application form not consistently encoded |

### Readiness summary

Of 26 criteria: **Ready on 11, Partial on 9, Gap on 6.** The six gaps are
authentication strength for reviewers, privileged access approval records,
configuration drift detection, contingency plan testing, supply chain procedures and
input validation. None of them is architectural. All six are achievable before an
assessment window, which is the finding that mattered: proceed to Step 1.

---

## Section 3: Gaps carried forward

Each gap and partial below is carried forward.

> **Note on the last column, and on dates.** The readiness assessment itself was issued
> on 14 October 2025. The right hand column, "Eventual outcome", was **added
> retrospectively on 31 August 2026** and its dates belong to that annotation, not to the
> original assessment. It is kept in the same table because a readiness assessment that
> nobody ever revisits teaches nothing, and the comparison between what was predicted and
> what actually happened is the most useful thing in this document. A document that
> reported 2026 outcomes as though it knew them in 2025 would simply be wrong, so the
> annotation is labelled rather than blended in.

| # | Gap | Priority | Owner | Target | Eventual outcome |
|---|---|---|---|---|---|
| R-01 | MFA missing for peer reviewers | High | Samuel P. Hargrave | 2026-01-30 | Not fixed in time. Became assessment finding SAR-001 and POA-001. Closed 2026-07-24. |
| R-02 | Privileged access approval records | High | Nkeiru Sarah Adesida | 2025-12-19 | Partly fixed. Recurred as SAR-003, remediated during fieldwork. |
| R-03 | Input validation on rich text fields | High | Priya N. Raghunathan | 2026-01-16 | Not fixed in time. Became SAR-002, remediated during fieldwork. |
| R-04 | Configuration drift detection | Moderate | Samuel P. Hargrave | 2026-02-27 | Not fixed in time. Contributed to SAR-005 and POA-003. Closed 2026-07-29. |
| R-05 | Contingency plan functional test | Moderate | Marcus T. Delacroix | 2026-02-27 | Not fixed. Became SAR-007 and POA-005, still open at the July 2026 report. |
| R-06 | Supply chain procedures approval | Moderate | Nkeiru Sarah Adesida | 2026-01-30 | Not fixed. Became SAR-008 and POA-006, still open at the July 2026 report. |
| R-07 | Authenticated scanning on the database tier | Moderate | Samuel P. Hargrave | 2026-02-13 | Fixed during fieldwork. SAR-009, closed 2026-03-20. |
| R-08 | Log retention on one log group | Low | Derrick A. Whitmore | 2026-01-30 | Not fixed in time. Became SAR-016, closed 2026-03-30. |
| R-09 | Replica region encryption key | Low | Samuel P. Hargrave | 2026-03-31 | Not fixed. Became SAR-011 and POA-007, still open at the July 2026 report. |
| R-10 | Training overdue for eleven users | Low | Yvonne C. Castellanos | 2025-12-19 | Not fixed in time. Became SAR-010, closed 2026-03-26. |

### What this table is really showing

Six of ten readiness gaps were still open when the assessor arrived four months
later. That is the ordinary outcome, and writing it down is the point. A readiness
assessment that predicts nothing is a formality; this one predicted seven of the
sixteen findings the assessor eventually wrote.

---

## Section 4: Inherited controls

Controls inherited from the cloud platform are satisfied by the provider, not by the
agency. The agency still has to know which ones they are, because an assessor will
ask, and "the cloud handles it" is not an answer without a reference.

| Control family | Examples inherited | Inheritance type | Evidence relied on |
|---|---|---|---|
| PE, Physical and Environmental Protection | PE-2, PE-3, PE-6, PE-13 | Fully inherited for the data centre boundary | Provider authorisation package |
| MA, Maintenance | MA-2, MA-3, MA-5 | Fully inherited for the physical layer | Provider authorisation package |
| MP, Media Protection | MP-4, MP-6 | Fully inherited for physical media handling | Provider authorisation package |
| SC, System and Communications Protection | SC-5 partial, SC-7 partial | Shared. Provider supplies the edge protection; the agency configures it | Provider package plus agency configuration records |
| CP, Contingency Planning | CP-8, CP-9 partial | Shared. Provider supplies durable storage and regional redundancy; the agency owns the plan and the test | Provider package plus agency contingency plan |
| CM, Configuration Management | CM-8 partial | Shared. Provider supplies the inventory interface; the agency owns inventory accuracy | Agency inventory records |

A note on the honest limit of inheritance: five of the seven controls above are
shared, not fully inherited. The most common mistake at this stage is recording a
shared control as inherited and then having no agency side evidence when the
assessor asks for it.

---

## Section 5: Interconnections

| External system | Purpose | Connection type | Data exchanged | Agreement |
|---|---|---|---|---|
| Federal payment processing service (fictional) | Submits approved disbursement instructions | TLS 1.2 mutually authenticated API over a private link | Payment instruction records, confirmation receipts | Interconnection Security Agreement executed 2025-09-18 |
| Agency identity provider (fictional) | Authenticates agency users | SAML 2.0 federation | Authentication assertions, group membership | Internal memorandum of understanding 2025-08-22 |
| Entity registration verification service (fictional) | Verifies grantee organisation eligibility | TLS 1.2 REST API | Organisation identifiers, registration status | Interconnection Security Agreement executed 2025-10-02 |

---

## Section 6: Recommendation

Proceed to Step 1, categorisation, with the ten gaps above tracked to closure before
the assessment window opens. The two that most threaten the schedule are R-01
(reviewer authentication), because it requires procurement, and R-05 (contingency
plan test), because it requires an outage window. Both should be started
immediately rather than sequenced behind documentation work.

Signed in the scenario by Nkeiru Sarah Adesida, ISSO, and acknowledged by Marcus T. Delacroix, System Owner,
on 14 October 2025.

---

**Navigation:** [Repository home](../README.md) &nbsp;|&nbsp; [Step 1: Categorise the System ->](../step-01-categorization/README.md)

---

*Author: Nkeiru Sarah Adesida, Information System Security Officer (ISSO), portfolio scenario*  
*Simulated system: Keystone Grants Management System (KGMS) | FWDA-KGMS-2026-MOD*  
*This document is a portfolio exercise built on a fictional organisation. It is not a government record.*  
*[GitHub portfolio](https://github.com/Nkee07) | [LinkedIn](https://www.linkedin.com/in/nkeiru-adesida-grc)*
