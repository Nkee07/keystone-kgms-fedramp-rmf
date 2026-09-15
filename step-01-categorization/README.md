# Step 1: FIPS 199 Security Categorisation Workbook
### Keystone Grants Management System (KGMS) | Impact analysis and the integrity adjustment

> ### PORTFOLIO EXERCISE, SIMULATED SYSTEM
> **Keystone Grants Management System (KGMS) does not exist.** The Federal Workforce Development Agency (FWDA) is a fictional federal
> agency invented for this portfolio. Every organisation, person, system
> identifier, network address, finding, date and signature on this page is
> fabricated for training purposes, with one exception: the author, Nkeiru Sarah Adesida, is a real person. Where her name appears in a scenario role, that role is fictional, and she has never worked for this agency, which does not exist. Nothing here is drawn from any real
> employer, client or government system, and no real document, artifact or
> data has been reproduced. This file is coursework, not a government record.

---

**Document:** FIPS 199 Security Categorisation Workbook  
**Simulated system:** Keystone Grants Management System (KGMS) | `FWDA-KGMS-2026-MOD`  
**Framework and standards:** FIPS 199, FIPS 200, NIST SP 800-60 Vol. II, NIST SP 800-37 Rev 2 Step 1  
**Author:** Nkeiru Sarah Adesida  
**Document date:** 7 November 2025  
**Status:** Complete

**Navigation:** [<- Step 0: Readiness Assessment](../step-00-readiness/README.md) &nbsp;|&nbsp; [Repository home](../README.md) &nbsp;|&nbsp; [Step 2: Select and Tailor Controls ->](../step-02-controls/README.md)

---

## Purpose

Categorisation answers one question: how bad would it be if this system's
information were exposed, altered, or unavailable? The answer decides how many
security controls the system has to carry, so getting it wrong at this step makes
every later step wrong too.

Plain language version: before you fit locks to a building you decide what is inside.
A garden shed and a bank vault get different locks. FIPS 199 is the rule for deciding
which one you are dealing with, and it grades three separate things: keeping secrets
(confidentiality), keeping information correct (integrity), and keeping it available
when needed (availability).

FIPS 199 is Federal Information Processing Standard Publication 199, the mandatory
federal standard for this decision. Each of the three is rated Low, Moderate or High.

---

## Section 1: Method

1. Identify every type of information the system stores, processes or transmits.
2. Rate each information type for confidentiality, integrity and availability.
3. Apply the **high water mark**: for each of the three, the system inherits the
   highest rating found across all information types. One High anywhere makes that
   objective High for the whole system.
4. Take the highest of the three as the overall system impact level.
5. Document any adjustment, with the reasoning, and have the Authorizing Official
   approve it.

Step 5 is the step most often skipped. The high water mark is a floor for analysis,
not the end of it. Applying it mechanically and stopping produces systems categorised
High because one report is time sensitive, which then carry hundreds of controls
nobody can resource.

---

## Section 2: Information types

Note on citations: the column below names the **SP 800-60 Volume II taxonomy area**
rather than a specific paragraph identifier. Publishing a precise identifier that has
not been verified against the current revision would be a fabricated citation, and a
fabricated citation is worse than a general one. In a real package each row would
carry the verified identifier from the current publication.

| # | Information type | SP 800-60 Vol. II taxonomy area | Confidentiality | Integrity | Availability |
|---|---|---|---|---|---|
| 1 | Grant application and proposal content | Services for Citizens | Moderate | Moderate | Low |
| 2 | Grantee organisation registration and eligibility records | Services for Citizens | Moderate | Moderate | Low |
| 3 | Award and obligation records | Government Resource Management | Moderate | High | Moderate |
| 4 | Disbursement and payment instruction records | Government Resource Management | Moderate | High | Moderate |
| 5 | Peer reviewer identity and conflict of interest records | Support Delivery of Services | Moderate | Moderate | Low |
| 6 | Merit review scores and panel deliberations | Services for Citizens | Moderate | Moderate | Low |
| 7 | Grantee performance and monitoring reports | Services for Citizens | Low | Moderate | Low |
| 8 | Audit and accountability records | Support Delivery of Services | Moderate | Moderate | Moderate |
| 9 | Public funding opportunity announcements | Services for Citizens | Low | Moderate | Moderate |
| 10 | System configuration and security documentation | Support Delivery of Services | Moderate | Moderate | Low |
| 11 | Help desk and correspondence records containing PII | Support Delivery of Services | Moderate | Low | Low |

### Reasoning behind the two High integrity ratings

Rows 3 and 4, award and obligation records and disbursement instruction records, are
rated High for integrity. Everything else is Moderate or Low. The reasoning:

- An undetected alteration to an award amount or a bank routing instruction results
  in federal funds moving to the wrong place. That is a severe adverse effect on
  agency operations and on the public, which is the FIPS 199 definition of High, not
  the serious adverse effect that defines Moderate.
- Confidentiality of those same records is only Moderate, because award amounts become
  public information once announced. Integrity and confidentiality genuinely diverge
  here, and rating them separately rather than together is the whole point of the
  three part method.

---

## Section 3: High water mark

| Security objective | Highest rating found | Driven by |
|---|---|---|
| Confidentiality | Moderate | Rows 1 to 6, 8, 10 and 11, all Moderate. No information type is rated High for confidentiality. |
| Integrity | High | Rows 3 and 4, award and disbursement records. |
| Availability | Moderate | Rows 3, 4, 8 and 9, all Moderate. |

**Provisional security category:** SC KGMS = {(Confidentiality, Moderate),
(Integrity, High), (Availability, Moderate)}

Provisional overall impact level: **High**, because the overall level is the highest of
the three.

---

## Section 4: Integrity impact adjustment, approved by the AO

The provisional result makes KGMS a High impact system. The ISSO recommended
adjusting integrity down to Moderate. The reasoning, the compensating control and the
decision are recorded here because an adjustment without a written rationale is an
adjustment an assessor will reverse.

### The argument for adjustment

KGMS is not the system of record for payment execution. It composes a payment
instruction and transmits it to the federal payment processing service, which is
independently authorised and holds the authoritative record. Three facts follow:

1. **An alteration inside KGMS does not by itself move money.** The receiving
   service performs its own validation against the obligation record before
   disbursing.
2. **A daily two way reconciliation exists.** Every instruction transmitted is matched
   against the confirmation receipt returned, and against the obligation balance in
   the award record. A mismatch raises an exception the same business day. This is the
   compensating control, and it is a detective control with a one day window, not a
   preventive one.
3. **The severe adverse effect is therefore not realised in this system.** The severe
   outcome requires an integrity failure in KGMS to survive the receiving
   service's validation and the daily reconciliation. Two independent controls stand
   between the alteration and the harm.

### What the adjustment costs, stated plainly

Moderate integrity removes roughly 40 control enhancements the High baseline would
have required, most of them in the SI and AU families. The residual exposure is a
window of up to one business day in which an altered instruction is in flight and
undetected. The agency accepts that window because the receiving service will not
disburse against an obligation balance that does not support the instruction.

If the daily reconciliation were ever removed, weakened, or moved to a weekly
cadence, **this adjustment is void and the system returns to High integrity.** That
dependency is recorded in the system security plan and is tested at every annual
assessment. It is the condition that makes the adjustment defensible rather than
convenient.

### Decision

| Field | Detail |
|---|---|
| Recommendation by | Nkeiru Sarah Adesida, ISSO |
| Reviewed by | Daniel K. Osei, Chief Information Security Officer |
| Privacy concurrence | Helen M. Barragan, Senior Agency Official for Privacy |
| Approved by | Patricia L. Ambrose, Authorizing Official |
| Decision | Integrity adjusted from High to Moderate, conditional on the daily reconciliation control remaining in place |
| Date approved | 7 November 2025 |
| Review trigger | Annual assessment, or any change to the reconciliation control |

---

## Section 5: Final security category

**SC KGMS = {(Confidentiality, Moderate), (Integrity, Moderate),
(Availability, Moderate)}**

**Overall system impact level: MODERATE.** Control baseline: NIST SP 800-53 Rev 5
Moderate, as profiled by FedRAMP.

---

## Section 6: What the Moderate baseline obliges

FIPS 200, the companion standard to FIPS 199, sets the minimum security requirements
for federal systems and organises them into control families. Selecting Moderate is
what makes SP 800-53 Rev 5 control selection binding rather than advisory. Step 2
does that selection.

Approved 7 November 2025. Signed in the scenario by Patricia L. Ambrose, Authorizing Official.

---

## Machine readable version

The worksheet above is also published as
[artifacts/kgms-fips199-information-types.csv](../artifacts/kgms-fips199-information-types.csv).

---

**Navigation:** [<- Step 0: Readiness Assessment](../step-00-readiness/README.md) &nbsp;|&nbsp; [Repository home](../README.md) &nbsp;|&nbsp; [Step 2: Select and Tailor Controls ->](../step-02-controls/README.md)

---

*Author: Nkeiru Sarah Adesida, Information System Security Officer (ISSO), portfolio scenario*  
*Simulated system: Keystone Grants Management System (KGMS) | FWDA-KGMS-2026-MOD*  
*This document is a portfolio exercise built on a fictional organisation. It is not a government record.*  
*[GitHub portfolio](https://github.com/Nkee07) | [LinkedIn](https://www.linkedin.com/in/nkeiru-adesida-grc)*
