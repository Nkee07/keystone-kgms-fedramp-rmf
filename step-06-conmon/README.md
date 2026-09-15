# Step 6: Continuous Monitoring Plan and July 2026 Monthly Report
### Keystone Grants Management System (KGMS) | Monitoring the authorisation after it was granted

> ### PORTFOLIO EXERCISE, SIMULATED SYSTEM
> **Keystone Grants Management System (KGMS) does not exist.** The Federal Workforce Development Agency (FWDA) is a fictional federal
> agency invented for this portfolio. Every organisation, person, system
> identifier, network address, finding, date and signature on this page is
> fabricated for training purposes. Nothing here is drawn from any real
> employer, client or government system, and no real document, artifact or
> data has been reproduced. This file is coursework, not a government record.

---

**Document:** Continuous Monitoring Plan v1.0 and July 2026 Monthly Report  
**Simulated system:** Keystone Grants Management System (KGMS) | `FWDA-KGMS-2026-MOD`  
**Framework and standards:** NIST SP 800-137, NIST SP 800-37 Rev 2 Step 7, FedRAMP continuous monitoring requirements  
**Author:** Nkeiru Sarah Adesida  
**Document date:** 12 August 2026  
**Status:** Complete

**Navigation:** [<- Step 5: Authorize the System](../step-05-authorization/README.md) &nbsp;|&nbsp; [Repository home](../README.md)

---

## Purpose

An Authorization to Operate is not a certificate on a wall. It is a statement about a
system at a moment, and systems change. Continuous monitoring is how the AO's decision
stays connected to reality.

Plain language version: passing the inspection once is not the job. The job is proving
every month that the building is still safe, that the snag list is shrinking, and that
nothing new has broken. When something does break, you say so before you are asked.

Part A is the plan. Part B is a real monthly report against it, for July 2026.

---

# PART A: CONTINUOUS MONITORING PLAN

Effective 29 May 2026, two weeks after authorisation.

## A1: Governance

| Field | Detail |
|---|---|
| System | Keystone Grants Management System (KGMS) \| `FWDA-KGMS-2026-MOD` |
| Plan owner | Nkeiru Sarah Adesida, ISSO |
| Reports to | Patricia L. Ambrose, Authorizing Official |
| Reviewed by | Daniel K. Osei, Chief Information Security Officer |
| Primary reference | NIST SP 800-137, Information Security Continuous Monitoring |
| Related controls | CA-7 Continuous Monitoring, RA-5 Vulnerability Monitoring and Scanning, SI-2 Flaw Remediation, SI-4 System Monitoring, CM-3 Configuration Change Control |
| Reporting cadence | Monthly, due by the 15th of the following month |
| Tooling | Tenable Nessus for scanning, ServiceNow for issue and remediation workflow, RSA Archer for control level reporting and evidence retention |
| Plan version | 1.0 |

## A2: Monitoring activities and frequencies

| Activity | Frequency | Method | Responsible | Deliverable |
|---|---|---|---|---|
| Authenticated infrastructure vulnerability scan | Weekly | Tenable Nessus, credentialed | Samuel P. Hargrave | Scan report, findings to ServiceNow |
| Authenticated web application scan | Monthly | Tenable Nessus web application scanning | Priya N. Raghunathan | Scan report |
| Container image scan | Every build | Pipeline integrated scanning | Priya N. Raghunathan | Build gate result |
| Configuration baseline compliance | Continuous | Platform compliance rules | Samuel P. Hargrave | Drift exceptions |
| Privileged account activity review | Weekly | Correlated query across application, database and control plane | Derrick A. Whitmore | Weekly review record |
| Alert queue triage | Daily | Detection rules on 7 log groups | Derrick A. Whitmore | Ticket record |
| Access review | Quarterly | Export, supervisor attestation line by line | Nkeiru Sarah Adesida | Signed attestation in RSA Archer |
| POA&M status review | Monthly | Evidence validation against each open item | Nkeiru Sarah Adesida | POA&M status update |
| Significant change review | Per change | Security impact analysis before deployment | Nkeiru Sarah Adesida | Impact analysis record |
| Interconnection agreement review | Annual | Confirm agreements current and accurate | Marcus T. Delacroix | Review memorandum |
| Payment reconciliation control verification | Monthly | Confirm the daily reconciliation ran every business day | Nkeiru Sarah Adesida | Verification record. This control underpins the integrity categorisation |
| Contingency plan test | Annual | Functional restore of the database tier | Marcus T. Delacroix | After action report |
| Incident response exercise | Annual | Tabletop plus one functional element | Derrick A. Whitmore | Exercise report |
| Security literacy and awareness training | Annual per user, tracked monthly | Agency training platform | Yvonne C. Castellanos | Completion report |
| Control reassessment | Annual | One third of controls plus every previously failed control | Rebecca J. Tran | Assessment report |

## A3: Vulnerability remediation service levels

| Severity | CVSS band | Remediate within | Basis |
|---|---|---|---|
| Critical | 9.0 to 10.0 | 30 days | FedRAMP continuous monitoring requirement |
| High | 7.0 to 8.9 | 30 days | FedRAMP continuous monitoring requirement |
| Moderate | 4.0 to 6.9 | 90 days | FedRAMP continuous monitoring requirement |
| Low | 0.1 to 3.9 | 180 days | FedRAMP continuous monitoring requirement |

A missed service level does not become acceptable by going unreported. It becomes a
POA&M item with a deviation request, submitted to the AO before the date passes rather
than after.

## A4: What counts as a significant change

A change is significant, and needs a security impact analysis before deployment, if it
does any of the following:

- alters the authorization boundary, adds or removes an interconnection
- changes the information types handled, which could change the FIPS 199 categorisation
- changes the authentication model for any user population
- alters the daily payment reconciliation control in any way, including its cadence,
  because the integrity categorisation depends on it
- introduces a new third party component or dependency into the boundary
- changes encryption, key management or logging scope

## A5: Escalation

| Trigger | Action | Timeframe |
|---|---|---|
| Critical or High vulnerability on an internet reachable component | Notify the CISO and the ISSO; assess for emergency change | Same business day |
| Suspected incident | Report to the security operations centre, follow the incident response plan | Within one hour |
| POA&M target date at risk | Deviation request to the AO with justification and revised date | Before the original date passes |
| Significant change deployed without impact analysis | Report to the CISO, retrospective analysis, record as a control deficiency | Within one business day of discovery |
| Failure of the daily payment reconciliation for more than one business day | Notify the AO directly; the integrity categorisation basis is affected | Same business day |

---

# PART B: MONTHLY CONTINUOUS MONITORING REPORT, JULY 2026

| Field | Detail |
|---|---|
| Reporting period | 1 July 2026 to 31 July 2026 |
| Report submitted | 12 August 2026, within the 15th of month deadline |
| Prepared by | Nkeiru Sarah Adesida, ISSO |
| Submitted to | Patricia L. Ambrose, Authorizing Official |
| Authorisation status | Active. Granted 15 May 2026, terminates 14 May 2029 |

## B1: Summary for the AO

Four of the ten POA&M items open at authorisation were closed this period, including
**SAR-001 and POA-001, the High risk reviewer authentication finding, closed on 24 July,
seven days inside the condition the AO attached to the authorisation.**

Two new items were raised from July scanning, one of them High. Open items therefore
moved from 10 to 6 plus 2 equals
8.

One service level was met on every closed item. No incidents occurred. No significant
changes were deployed without a prior impact analysis. The daily payment reconciliation
ran on all 22 business days in July.

## B2: POA&M status

| POA&M ID | Weakness | Risk | Status at 31 July 2026 | Evidence or progress |
|---|---|---|---|---|
| POA-001 | Multifactor authentication not enforced for the peer... | High | Closed 2026-07-24 | Reviewer portal federated to the FWDA IdP; MFA enforced for all 65 reviewer accounts; screenshots of enforcement policy and a failed single factor login attempt retained |
| POA-002 | Unremediated OpenSSH vulnerability on two bastion ho... | Moderate | Closed 2026-06-26 | OpenSSH updated on both bastion hosts; authenticated rescan on 2026-06-29 returned no finding for CVE-2024-6387 |
| POA-003 | Configuration baseline deviations on four of eleven ... | Moderate | Closed 2026-07-29 | All four instances rebuilt from the approved image; drift detection rule active in the configuration service; two consecutive clean compliance reports retained |
| POA-004 | Audit record review is performed but not evidenced a... | Moderate | Open | Review template approved 2026-07-15. Automation in build. Two of the four required consecutive weeks of evidence produced. |
| POA-005 | Contingency plan test not performed within the last ... | Moderate | Open | Contingency plan updated 2026-07-28. Functional restore test scheduled 2026-09-15, on track. |
| POA-006 | Supply chain risk management procedures drafted but ... | Moderate | Open | Procedure finalised 2026-07-24 and submitted to the System Owner. Awaiting approval signature. |
| POA-007 | Backup snapshots in the secondary region not encrypt... | Low | Open | Secondary region customer managed key created 2026-07-30, ahead of the 2026-08-14 milestone. Re-encryption not started. |
| POA-008 | Authenticator management policy predates the current... | Low | Closed 2026-07-15 | Policy section v2.0 published early; authenticator language now matches the configured identity provider behaviour |
| POA-009 | Separation checklist not evidenced for two of nine s... | Low | Open | One of the two missing checklists recovered. Workflow tool change request raised with Human Capital. |
| POA-010 | Component inventory omits three container images | Low | Open | Three container images added to the inventory 2026-07-22. Pipeline automation in design. |

| POA&M movement this period | Count |
|---|---|
| Open at the start of the period | 10 |
| Closed during the period | 4 |
| Remaining open from the original register | 6 |
| New items raised this period | 2 |
| **Total open at 31 July 2026** | **8** |

10 minus 4 plus 2 equals
8. The arithmetic is stated because a status report whose
opening balance, movements and closing balance do not reconcile is not a status report.

### The condition the AO attached

The authorisation required SAR-001 closed by 31 July 2026. Closed 24 July 2026.
Evidence retained: the identity provider enforcement policy configuration, the
enrolment report showing 65 of 65 reviewer accounts enrolled in multifactor
authentication, and a screenshot of a rejected single factor login attempt. The ISSO
validated this evidence against the finding text before marking the item closed.

## B3: New items raised this period

| POA&M ID | Control | Weakness | Risk | Owner | Target close | Note |
|---|---|---|---|---|---|---|
| POA-011 | RA-5 | Two managed database instances missing from the July authenticated scan scope | Moderate | Samuel P. Hargrave | 2026-10-29 | Instances provisioned for the July release were not added to the scan target group. |
| POA-012 | SI-2 | Unremediated Apache Log4j 2 vulnerability in a reporting service dependency | High | Priya N. Raghunathan | 2026-08-30 | CVE-2021-44228 identified in a bundled dependency of the reporting service. Compensating control: the service does not accept untrusted user input into log statements and is not internet facing. |

### On POA-012, the Log4j finding

CVE-2021-44228 is a five year old vulnerability with a CVSS base score of 10.0, and
finding it in July 2026 in a bundled dependency of the reporting service is not a good
look. The honest account: the reporting service pulls a charting library that bundles
its own logging dependency, and the dependency scanner was configured to examine direct
dependencies only, not transitive ones.

The environmental risk is lower than the base score suggests. The reporting service is
not internet reachable, and it does not write untrusted user input into log statements,
which is the exploitation path. The base score stays at 10.0 because **a base score is a
property of the vulnerability and is not adjusted by local context.** The environmental
score, computed separately, is 6.1. Presenting a single adjusted number in place of the
base score is a common and misleading shortcut; both numbers are reported, and the
remediation date follows the base score.

Remediation: library upgraded and the scanner reconfigured to resolve the full
dependency tree. Target 30 August 2026, inside the 30 day service level.

## B4: Vulnerability scanning

| Scan type | Dates run | Cadence | New findings |
|---|---|---|---|
| Infrastructure, authenticated | 2026-07-06, 13, 20, 27 | Weekly | 0 Critical, 1 High, 4 Moderate, 9 Low |
| Web application, authenticated | 2026-07-14 | Monthly | 0 Critical, 0 High, 2 Moderate, 5 Low |
| Container images | Per build, 11 builds in July | Per build | 0 Critical, 1 High, 1 Moderate, 3 Low |
| Database tier, authenticated | 2026-07-06, 13, 20, 27 | Weekly | 0 Critical, 0 High, 1 Moderate, 2 Low |

All scheduled scans ran. Two managed database instances provisioned for the July
release were absent from the scan target group, raised as POA-011. That is a scope
completeness failure, not a scanning failure, and it is the same underlying weakness as
POA-010, the container images missing from inventory. **Scan coverage can never exceed
inventory accuracy.** The two are reported together for that reason.

## B5: Significant changes

| Change | Date | Impact analysis | AO notification | Outcome |
|---|---|---|---|---|
| July release: two managed database instances added for reporting workload | 2026-07-09 | Completed 2026-07-02 | Not required, no boundary change | Deployed. Scan scope gap found later, POA-011 |
| Reviewer portal federated to the agency identity provider | 2026-07-24 | Completed 2026-07-10 | Notified, authentication model change | Deployed. Closed POA-001 |
| Three container images registered in inventory | 2026-07-22 | Not required, documentation only | Not required | Complete |
| Secondary region customer managed key created | 2026-07-30 | Completed 2026-07-23 | Not required | Key created, re-encryption pending under POA-007 |

The reviewer portal change altered the authentication model for a user population, which
meets the significant change threshold in section A4, so the AO was notified before
deployment rather than after.

## B6: Incidents

No security incidents occurred in July 2026. One event was investigated and closed as a
false positive: an alert for anomalous bulk record export on 17 July traced to a
scheduled quarterly reporting job that had been rescheduled, so it ran outside its
usual window. The detection rule was tuned to reference the job schedule rather than a
fixed time window.

## B7: Control health

| Monitored item | July result | Note |
|---|---|---|
| Daily payment reconciliation | 22 of 22 business days | The control the integrity categorisation depends on. Verified monthly for that reason |
| Weekly privileged activity review | 2 of 4 weeks evidenced | POA-004 in progress. Automation not yet in production |
| Configuration drift exceptions | 0 open at period end | 3 raised, all remediated within 5 days |
| Quarterly access review | Not due | Next due September 2026 |
| Training completion | 418 of 420 agency users current | 2 within their grace period |
| Scan cadence adherence | 100 percent | All scheduled scans ran |
| Service level adherence on closed items | 100 percent | All items closed this period closed inside their service level |

## B8: Next period

| Action | Owner | Due |
|---|---|---|
| Complete POA-004, four consecutive weeks of evidenced privileged activity review | Derrick A. Whitmore | 2026-08-31 |
| Obtain System Owner approval on the supply chain procedure, POA-006 | Nkeiru Sarah Adesida | 2026-08-31 |
| Remediate CVE-2021-44228 in the reporting service, POA-012 | Priya N. Raghunathan | 2026-08-30 |
| Add the two database instances to the scan target group, POA-011 | Samuel P. Hargrave | 2026-08-14 |
| Begin snapshot re-encryption in the secondary region, POA-007 | Samuel P. Hargrave | 2026-09-15 |
| Confirm the contingency plan functional test booking, POA-005 | Marcus T. Delacroix | 2026-08-21 |

---

## Where this continues

Continuous monitoring is treated in depth in its own repository, including the scan
programme, the ServiceNow POA&M workflow, the RSA Archer control monitoring model and
the security control assessment procedures:
**[keystone-kgms-conmon-vulnmgmt](https://github.com/Nkee07/keystone-kgms-conmon-vulnmgmt)**.

---

**Navigation:** [<- Step 5: Authorize the System](../step-05-authorization/README.md) &nbsp;|&nbsp; [Repository home](../README.md)

---

*Author: Nkeiru Sarah Adesida, Information System Security Officer (ISSO), portfolio scenario*  
*Simulated system: Keystone Grants Management System (KGMS) | FWDA-KGMS-2026-MOD*  
*This document is a portfolio exercise built on a fictional organisation. It is not a government record.*  
*[GitHub portfolio](https://github.com/Nkee07) | [LinkedIn](https://www.linkedin.com/in/nkeiru-adesida-grc)*
