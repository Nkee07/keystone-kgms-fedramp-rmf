# Step 2: Control Selection, Tailoring Log and Responsibility Matrix
### Keystone Grants Management System (KGMS) | Moderate baseline, responsibility split and parameters

> ### PORTFOLIO EXERCISE, SIMULATED SYSTEM
> **Keystone Grants Management System (KGMS) does not exist.** The Federal Workforce Development Agency (FWDA) is a fictional federal
> agency invented for this portfolio. Every organisation, person, system
> identifier, network address, finding, date and signature on this page is
> fabricated for training purposes, with one exception: the author, Nkeiru Sarah Adesida, is a real person. Where her name appears in a scenario role, that role is fictional, and she has never worked for this agency, which does not exist. Nothing here is drawn from any real
> employer, client or government system, and no real document, artifact or
> data has been reproduced. This file is coursework, not a government record.

---

**Document:** Control Selection, Tailoring Log and Customer Responsibility Matrix  
**Simulated system:** Keystone Grants Management System (KGMS) | `FWDA-KGMS-2026-MOD`  
**Framework and standards:** NIST SP 800-53 Rev 5, NIST SP 800-53B, FedRAMP Moderate baseline  
**Author:** Nkeiru Sarah Adesida  
**Document date:** 12 December 2025  
**Status:** Complete

**Navigation:** [<- Step 1: Categorise the System](../step-01-categorization/README.md) &nbsp;|&nbsp; [Repository home](../README.md) &nbsp;|&nbsp; [Step 3: Implement and Document Controls ->](../step-03-ssp/README.md)

---

## Purpose

Step 2 decides which controls apply, who is responsible for each one, and where the
standard wording has to be adjusted to fit how the system actually works.

Plain language version: the baseline is a long list of safety rules written for every
system in government. Most apply to yours as written. Some are handled entirely by
the company that runs the data centre. A few do not fit your system and need to be
reworded, with a reason. Writing down which is which is the job, because the thing
that fails an assessment most often is not a missing control, it is a control both
sides assumed the other one owned.

---

## Section 1: Responsibility categories

| Category | Meaning | Example in this system |
|---|---|---|
| Provider | Satisfied entirely by the cloud service provider. The agency inherits it and cites the provider's authorisation package as evidence. | PE-2, physical access to the data centre |
| Customer | Satisfied entirely by the agency. The agency produces the evidence. | AC-3, access enforcement inside the application |
| Shared | Both parties hold part of it. Each part needs its own evidence, and the split has to be written down. | SI-2, flaw remediation. The provider patches the platform, the agency patches guest operating systems and application dependencies. |

### The failure mode this table exists to prevent

Shared controls are where authorisation packages fail. Recording a shared control as
inherited feels efficient and produces no evidence on the agency side. When the
assessor asks how the agency knows its guest operating systems are patched, "the
cloud provider handles patching" is not an answer, because the provider patches the
hypervisor, not the customer's virtual machines. Of the 36 controls in the
sample below, 8 are shared. Every one of them carries a
written split.

---

## Section 2: Control tailoring log

Scope statement: the FedRAMP Moderate baseline as profiled for this system contains
more than 300 controls and control enhancements. **The table below is a sample of
36, not the full baseline.** It was selected to cover every control family
that produced an assessment finding, every control that required tailoring, and at
least one example of each responsibility category. The full tailoring log in a real
package is a spreadsheet, not a document.

| Control | Control name | Responsibility | Tailoring decision | Note |
|---|---|---|---|---|
| AC-2 | Account Management | Customer | Implemented as specified | Agency owns all application and cloud account lifecycle |
| AC-2(1) | Automated System Account Management | Customer | Implemented as specified | Identity provider drives provisioning and deprovisioning |
| AC-3 | Access Enforcement | Customer | Implemented as specified | Nine application roles enforced server side |
| AC-6(5) | Privileged Accounts | Customer | Implemented as specified | Documented approval required; this control failed assessment as SAR-003 |
| AC-17 | Remote Access | Customer | Tailored | No direct remote shell access. Administrative access is brokered through a session manager service with full session logging, so the control is met by architecture rather than by VPN configuration |
| AT-2 | Literacy Training and Awareness | Customer | Implemented as specified | Annual, tracked by Human Capital. Note the Rev 5 control title; the Rev 4 title was Security Awareness Training |
| AU-2 | Event Logging | Customer | Implemented as specified | Event types defined per tier in the SSP |
| AU-6 | Audit Record Review, Analysis and Reporting | Customer | Implemented as specified | Daily alert review, weekly correlated review. Failed assessment as SAR-006 |
| AU-11 | Audit Record Retention | Shared | Implemented as specified | Provider supplies durable storage; agency sets retention. Failed as SAR-016 |
| CA-7 | Continuous Monitoring | Customer | Implemented as specified | See Step 6 and the continuous monitoring repository |
| CM-6 | Configuration Settings | Customer | Implemented as specified | Hardened baselines per tier. Failed assessment as SAR-005 |
| CM-8 | System Component Inventory | Shared | Implemented as specified | Provider inventory interface; agency owns accuracy. Failed as SAR-014 |
| CP-4 | Contingency Plan Testing | Customer | Implemented as specified | Annual functional test required. Failed assessment as SAR-007 |
| CP-9 | System Backup | Shared | Implemented as specified | Provider durable storage; agency schedule and scope |
| IA-2 | Identification and Authentication, organisational users | Customer | Implemented as specified | Federated through the agency identity provider |
| IA-2(1) | Multifactor Authentication to Privileged Accounts | Customer | Implemented as specified | Failed assessment as SAR-001 for the reviewer population |
| IA-5 | Authenticator Management | Customer | Implemented as specified | Length based with breached password screening. Documentation lagged, SAR-012 |
| IR-4 | Incident Handling | Shared | Implemented as specified | Agency plan; provider handles platform layer events |
| IR-6 | Incident Reporting | Customer | Implemented as specified | Reported to the agency security operations centre within one hour |
| MA-4 | Nonlocal Maintenance | Provider | Fully inherited | Physical and hypervisor layer maintenance is provider only |
| MP-6 | Media Sanitisation | Provider | Fully inherited | No agency controlled physical media in the boundary |
| PE-2 | Physical Access Authorisations | Provider | Fully inherited | Data centre access controlled by the provider |
| PE-3 | Physical Access Control | Provider | Fully inherited for the boundary | Regional offices hold no components. A regional office log practice was raised as SAR-015 and risk accepted |
| PL-2 | System Security and Privacy Plans | Customer | Implemented as specified | This package |
| PS-3 | Personnel Screening | Customer | Implemented as specified | Agency screening standard applies to contractors |
| PS-4 | Personnel Termination | Customer | Implemented as specified | Failed assessment as SAR-013 |
| RA-3 | Risk Assessment | Customer | Implemented as specified | Annual, plus on significant change |
| RA-5 | Vulnerability Monitoring and Scanning | Customer | Implemented as specified | Authenticated scanning required. Failed as SAR-009 |
| SC-7 | Boundary Protection | Shared | Implemented as specified | Provider edge plus agency security groups and web application firewall |
| SC-8 | Transmission Confidentiality and Integrity | Customer | Implemented as specified | TLS 1.2 minimum on every external path |
| SC-28 | Protection of Information at Rest | Customer | Implemented as specified | Customer managed key required. Failed in the replica region as SAR-011 |
| SI-2 | Flaw Remediation | Shared | Implemented as specified | Provider patches the platform; agency patches guest operating systems and application dependencies. Failed as SAR-004 |
| SI-4 | System Monitoring | Shared | Implemented as specified | Provider telemetry plus agency detection rules |
| SI-10 | Information Input Validation | Customer | Implemented as specified | Failed assessment as SAR-002 |
| SR-3 | Supply Chain Controls and Processes | Customer | Implemented as specified | Note the family: supply chain risk management lives in the SR family in Rev 5. Failed as SAR-008 |
| SR-11 | Component Authenticity | Shared | Implemented as specified | Signed base images, checksum verification in the build pipeline |

### Responsibility split across this sample

| Responsibility | Count in this sample |
|---|---|
| Customer | 24 |
| Provider | 4 |
| Shared | 8 |

Counts above are computed from the rows in the table, not entered separately.

### The one tailored control, explained

AC-17, Remote Access, is the only control in this sample recorded as Tailored rather
than Implemented as specified. The baseline language assumes remote access is
established, monitored and controlled, which usually means a virtual private network
with split tunnelling rules. KGMS has no remote shell access at all.
Administrative access is brokered through a session manager service: there is no
inbound port, no bastion listening on the internet, and every session is recorded.

The control objective, controlled and monitored remote access, is met more completely
by that architecture than it would be by a VPN. The tailoring statement records the
objective, the alternative implementation, and why it is at least as strong. That
last part is what an assessor is looking for; a tailoring statement that only says
"not applicable" gets reversed.

---

## Section 3: Organisation defined parameters

Several controls contain blanks the organisation has to fill in. Leaving them
unspecified is a finding in itself, because a control with an undefined frequency
cannot be tested.

| Control | Parameter | Value set for this system | Why this value |
|---|---|---|---|
| AC-2 | Account inactivity period before disabling | 35 days | Covers a one month absence without creating a monthly reauthorisation burden |
| AC-2 | Account review frequency | Quarterly | Aligns with the access review cycle in the ConMon repository |
| AC-7 | Consecutive invalid login attempts | 5 attempts, 30 minute lockout | Agency standard |
| AC-11 | Session lock after inactivity | 15 minutes | Agency standard for systems holding PII |
| AC-12 | Session termination after inactivity | 30 minutes | Balances reviewer workflow against exposure |
| AU-11 | Audit record retention | One year online, two years archived | Federal minimum for audit records supporting an investigation |
| CA-2 | Assessment frequency | Annual, one third of controls plus all previously failed controls | Keeps the annual effort feasible while retesting known weaknesses |
| CP-4 | Contingency plan test frequency | Annual functional test of the database tier restore | A tabletop alone does not verify a recovery time objective |
| IA-5 | Minimum authenticator length | 16 characters, screened against a breached password list, no forced rotation | Current federal guidance favours length and screening over rotation |
| RA-5 | Scan frequency | Weekly authenticated infrastructure, monthly web application, per build for containers | See the ConMon repository for the full schedule |
| SI-2 | Remediation timeframes | Critical and High 30 days, Moderate 90 days, Low 180 days | FedRAMP continuous monitoring requirement |
| SI-4 | Monitoring alert response | One hour for High, one business day for Moderate | Matches security operations centre staffing |

---

## Section 4: A note on control catalogue currency

Two catalogue details are easy to get wrong, and both were checked deliberately for
this package:

- **Supply chain risk management is the SR family in Revision 5.** SA-12, Supply Chain
  Protection, was withdrawn in Rev 5 and its content redistributed into SR-1 through
  SR-12. A package that cites Rev 5 as its baseline and then raises a supply chain
  finding against SA-12 is citing a withdrawn control, which is the fastest way to
  tell an assessor the current catalogue was never opened. This package uses SR-3.
- **AT-2 is Literacy Training and Awareness in Revision 5.** The Rev 4 title was
  Security Awareness Training. Using the old title in a Rev 5 package is a smaller
  error than the first, but it is the same kind of error.

Proceed to Step 3, implementation and documentation.

---

**Navigation:** [<- Step 1: Categorise the System](../step-01-categorization/README.md) &nbsp;|&nbsp; [Repository home](../README.md) &nbsp;|&nbsp; [Step 3: Implement and Document Controls ->](../step-03-ssp/README.md)

---

*Author: Nkeiru Sarah Adesida, Information System Security Officer (ISSO), portfolio scenario*  
*Simulated system: Keystone Grants Management System (KGMS) | FWDA-KGMS-2026-MOD*  
*This document is a portfolio exercise built on a fictional organisation. It is not a government record.*  
*[GitHub portfolio](https://github.com/Nkee07) | [LinkedIn](https://www.linkedin.com/in/nkeiru-adesida-grc)*
