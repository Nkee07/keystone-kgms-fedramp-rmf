# Step 4: Security Assessment Plan and Security Assessment Report
### Keystone Grants Management System (KGMS) | 199 controls assessed, 16 findings, all reconciled

> ### PORTFOLIO EXERCISE, SIMULATED SYSTEM
> **Keystone Grants Management System (KGMS) does not exist.** The Federal Workforce Development Agency (FWDA) is a fictional federal
> agency invented for this portfolio. Every organisation, person, system
> identifier, network address, finding, date and signature on this page is
> fabricated for training purposes. Nothing here is drawn from any real
> employer, client or government system, and no real document, artifact or
> data has been reproduced. This file is coursework, not a government record.

---

**Document:** Security Assessment Plan and Security Assessment Report  
**Simulated system:** Keystone Grants Management System (KGMS) | `FWDA-KGMS-2026-MOD`  
**Framework and standards:** NIST SP 800-53A Rev 5, NIST SP 800-37 Rev 2 Step 4  
**Author:** Nkeiru Sarah Adesida  
**Document date:** 10 April 2026  
**Status:** Complete

**Navigation:** [<- Step 3: Implement and Document Controls](../step-03-ssp/README.md) &nbsp;|&nbsp; [Repository home](../README.md) &nbsp;|&nbsp; [Step 5: Authorize the System ->](../step-05-authorization/README.md)

---

## Purpose

Assessment is the step where somebody independent tries to prove the System Security
Plan wrong. This document is both halves of that: the plan for how the assessment will
be done, written before it starts, and the report of what was found, written after.

Plain language version: Part A is the inspector telling you in advance exactly what
they are going to check and how. Part B is the inspection report. Writing Part A first
matters, because an inspector who decides what to look at after they arrive can be
argued with.

---

# PART A: SECURITY ASSESSMENT PLAN

Approved 13 February 2026, before fieldwork began.

## A1: Scope and independence

| Element | Detail |
|---|---|
| System assessed | Keystone Grants Management System (KGMS) \| `FWDA-KGMS-2026-MOD` |
| Assessment type | Initial assessment supporting an initial Authorization to Operate |
| Baseline | NIST SP 800-53 Rev 5 Moderate, FedRAMP profile |
| Controls in scope | 199 controls and control enhancements, comprising all agency responsible and shared controls. Fully inherited provider controls were reviewed by reference to the platform authorisation package rather than retested |
| Assessment procedures | NIST SP 800-53A Rev 5 |
| Assessor organisation | Ardent Assurance Group LLC (fictional) |
| Lead assessor | Rebecca J. Tran |
| Independence | The assessor is contracted by the agency Office of Information Security, reports to the CISO, and had no role in designing, building or operating the system. The ISSO supported the assessment and did not assess her own work |
| Fieldwork window | 2 March 2026 to 27 March 2026 |
| Report issued | 10 April 2026 |

### Why independence is stated explicitly

In this scenario the ISSO wrote the SSP. An assessment of that SSP by the same person
would be worthless, and an assessor who reports to the System Owner is under pressure
to find less. The reporting line matters more than the badge. Recording it in the plan
is the only way a reader can judge whether the assessment result means anything.

## A2: Assessment methods

SP 800-53A defines three methods. Most controls need more than one, and the reason is
worth stating: interview tells you what people believe happens, examine tells you what
the paperwork claims, and test tells you what the system actually does. These three
answers are often different, and where they differ is where findings are.

| Method | What it is | Applied here as |
|---|---|---|
| Examine | Review documents, records, configurations and other artifacts | Read the SSP, policies, access request records, scan reports, configuration exports, quarterly access attestations, training records, separation checklists |
| Interview | Speak with people who perform or depend on the control | Structured interviews with the ISSO, Cloud Operations Lead, Application Development Lead, Security Operations Manager and Human Capital Liaison |
| Test | Exercise the control and observe the actual result | Attempted single factor login to the reviewer portal, submitted script payloads to input fields, attempted privilege escalation from a standard account, compared running instance configuration against the approved baseline, attempted retrieval of an object from the document store without credentials |

## A3: Assessment objects

| Object type | Population | Sample | Sampling basis |
|---|---|---|---|
| User accounts | 485 across three populations | 25 | Stratified: 15 agency, 7 reviewer, 3 service, weighted toward privileged |
| Privileged group memberships | 16 across three groups | 16 | Full population. Small and high impact, so no sampling |
| Compute instances | 11 | 11 | Full population |
| Log groups | 7 | 7 | Full population |
| Weekly audit review records | 52 weeks available | 12 consecutive weeks | Consecutive rather than scattered, so a gap in cadence is visible |
| Separations | 9 in the period | 9 | Full population |
| Access request records | Tied to the 25 sampled accounts | 25 | Follows the account sample |
| Input fields accepting user data | 31 | 31 | Full population. Input validation is tested exhaustively because one missed field is a finding |
| Container images | 3 | 3 | Full population |

### Note on the two full population choices that matter

Privileged group membership and input fields were both tested exhaustively rather than
sampled. For privileged access, a sample that misses the one unapproved administrator
tells you nothing useful. For input validation, the control is only as strong as its
weakest field, so a sample would measure the wrong thing. Sampling is appropriate where
the population is homogeneous; neither of these is.

## A4: Schedule

| Activity | Dates | Lead |
|---|---|---|
| Plan approved | 13 February 2026 | Rebecca J. Tran |
| Document review | 2 to 6 March 2026 | Rebecca J. Tran |
| Interviews | 9 to 12 March 2026 | Rebecca J. Tran |
| Technical testing | 16 to 25 March 2026 | Rebecca J. Tran |
| Remediation of findings closed during fieldwork | 20 to 31 March 2026 | Nkeiru Sarah Adesida |
| Retest of remediated findings | 24 to 31 March 2026 | Rebecca J. Tran |
| Draft report to the agency | 3 April 2026 | Rebecca J. Tran |
| Final report issued | 10 April 2026 | Rebecca J. Tran |

### On findings remediated during fieldwork

Five findings were corrected while the assessment was still running, retested, and
recorded as closed. That practice is legitimate and common, and it is also the place
where packages get soft, so two rules were applied: the finding is reported in full
regardless of closure, with its root cause, and closure requires the assessor to retest
rather than the agency to assert. A finding that disappears from the report because it
was fixed quickly is a finding the AO never got to see.

---

# PART B: SECURITY ASSESSMENT REPORT

Issued 10 April 2026.

## B1: Executive summary

199 controls and enhancements were assessed. **183 were assessed as Satisfied
and 16 as Other Than Satisfied**, producing 16 findings.

| Severity | Count |
|---|---|
| High | 3 |
| Moderate | 8 |
| Low | 5 |
| **Total** | **16** |

No finding was rated Critical, and no finding indicated an active compromise. The
weaknesses fall into three recognisable groups:

1. **One genuine security gap with real exposure.** SAR-001, single factor
   authentication for 65 external reviewers who can read applicant personally
   identifiable information and unpublished scores, and SAR-002, stored cross site
   scripting reachable by any member of the public who starts an application. These two
   are the reason the assessment was worth doing.
2. **Controls performed but not evidenced.** SAR-006 above all. The activity appears to
   happen; the record of it does not exist. For an assessor these are indistinguishable
   from controls that are not performed.
3. **Documentation and completeness drift.** SAR-012, SAR-013, SAR-014 and SAR-016.
   Low individually, and collectively the signal that the system had outgrown its
   paperwork.

**Assessor recommendation:** the system is suitable for authorisation, with the High
finding SAR-001 tracked to closure under a Plan of Action and Milestones. The two High
findings closed during fieldwork were retested and confirmed.

## B2: Results by control family

| Family | Name | Assessed | Satisfied | Other than satisfied |
|---|---|---|---|---|
| AC | Access Control | 21 | 20 | 1 |
| AT | Awareness and Training | 5 | 4 | 1 |
| AU | Audit and Accountability | 13 | 11 | 2 |
| CA | Assessment, Authorization and Monitoring | 9 | 9 | 0 |
| CM | Configuration Management | 14 | 12 | 2 |
| CP | Contingency Planning | 12 | 11 | 1 |
| IA | Identification and Authentication | 12 | 10 | 2 |
| IR | Incident Response | 10 | 10 | 0 |
| MA | Maintenance | 6 | 6 | 0 |
| MP | Media Protection | 6 | 6 | 0 |
| PE | Physical and Environmental Protection | 11 | 10 | 1 |
| PL | Planning | 5 | 5 | 0 |
| PS | Personnel Security | 8 | 7 | 1 |
| RA | Risk Assessment | 8 | 7 | 1 |
| SA | System and Services Acquisition | 13 | 13 | 0 |
| SC | System and Communications Protection | 23 | 22 | 1 |
| SI | System and Information Integrity | 16 | 14 | 2 |
| SR | Supply Chain Risk Management | 7 | 6 | 1 |
| **Total** |  | **199** | **183** | **16** |

Every count in that table is computed from the finding rows in section B4, so the
Other Than Satisfied column sums to exactly 16, the number of findings
reported. A summary that does not reconcile with its own detail is the most common
defect in an authorisation package and the easiest to check.

## B3: Every finding is accounted for

This is the table an assessor and an AO care about most, and the one most often
missing. Every finding has exactly one disposition, and the dispositions sum to the
total. No finding is left unexplained.

| Disposition | High | Moderate | Low | Total | Where it goes |
|---|---|---|---|---|---|
| Carried into the POA&M | 1 | 5 | 4 | **10** | [Step 5](../step-05-authorization/README.md) |
| Closed during fieldwork, retested by the assessor | 2 | 3 | 0 | **5** | Closure evidence retained, no POA&M entry required |
| Formally risk accepted by the AO | 0 | 0 | 1 | **1** | Risk acceptance recorded in the ATO memo |
| **Total findings** | **3** | **8** | **5** | **16** |  |

## B4: Findings register

| ID | Control | Finding | Severity | Disposition |
|---|---|---|---|---|
| SAR-001 | IA-2(1) | Multifactor authentication not enforced for the peer reviewer portal | High | Open, tracked as POA-001 |
| SAR-002 | SI-10 | Stored cross site scripting in the grant narrative field | High | Closed during fieldwork |
| SAR-003 | AC-6(5) | Three application administrators hold standing privileged access with no approval record | High | Closed during fieldwork |
| SAR-004 | SI-2 | Unremediated OpenSSH vulnerability on two bastion hosts | Moderate | Open, tracked as POA-002 |
| SAR-005 | CM-6 | Configuration baseline deviations on four of eleven application instances | Moderate | Open, tracked as POA-003 |
| SAR-006 | AU-6 | Audit record review is performed but not evidenced at the required frequency | Moderate | Open, tracked as POA-004 |
| SAR-007 | CP-4 | Contingency plan test not performed within the last twelve months | Moderate | Open, tracked as POA-005 |
| SAR-008 | SR-3 | Supply chain risk management procedures drafted but not approved | Moderate | Open, tracked as POA-006 |
| SAR-009 | RA-5 | Authenticated scanning not configured for the database tier | Moderate | Closed during fieldwork |
| SAR-010 | AT-2 | Literacy training and awareness overdue for eleven users | Moderate | Closed during fieldwork |
| SAR-011 | SC-28 | Backup snapshots in the secondary region not encrypted with the customer managed key | Low | Open, tracked as POA-007 |
| SAR-012 | IA-5 | Authenticator management policy predates the current agency standard | Low | Open, tracked as POA-008 |
| SAR-013 | PS-4 | Separation checklist not evidenced for two of nine separations | Low | Open, tracked as POA-009 |
| SAR-014 | CM-8 | Component inventory omits three container images | Low | Open, tracked as POA-010 |
| SAR-015 | PE-3 | Visitor access log at the regional office is maintained on paper | Low | Risk accepted by the AO |
| SAR-016 | AU-11 | Audit record retention set to ninety days in one log group | Moderate | Closed during fieldwork |

## B5: Finding detail

### SAR-001 Multifactor authentication not enforced for the peer reviewer portal (High)

**Control:** IA-2(1) &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-001

Agency staff authenticate through the FWDA identity provider with a PIV card. The 65 contracted peer reviewers authenticate to a separate portal with a username and password only. Reviewers can read unpublished merit review scores and applicant PII, so single factor authentication on that path is not acceptable at the Moderate baseline.

### SAR-002 Stored cross site scripting in the grant narrative field (High)

**Control:** SI-10 &nbsp;|&nbsp; **Disposition:** Closed during fieldwork and retested

The assessor submitted a script payload in the project narrative field of the application form. The payload was stored without encoding and executed when a reviewer opened the application. Remediated during fieldwork by adding context aware output encoding and a server side allow list; retested and confirmed closed on 24 March 2026.

### SAR-003 Three application administrators hold standing privileged access with no approval record (High)

**Control:** AC-6(5) &nbsp;|&nbsp; **Disposition:** Closed during fieldwork and retested

Three accounts in the application administrator group had no completed access request form on file. Two were required for operations and were reauthorised with documented approval; one belonged to a contractor whose task order had ended and was disabled. Closed 31 March 2026.

### SAR-004 Unremediated OpenSSH vulnerability on two bastion hosts (Moderate)

**Control:** SI-2 &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-002

Authenticated scanning identified CVE-2024-6387, a signal handler race condition in OpenSSH sshd on glibc based Linux that can lead to remote code execution as root, on bastion-01 and bastion-02. The hosts sit behind a restricted management security group, which reduces but does not remove exposure.

### SAR-005 Configuration baseline deviations on four of eleven application instances (Moderate)

**Control:** CM-6 &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-003

Four of eleven application tier instances deviated from the approved hardening baseline: two permitted password based SSH authentication, one had an unused web administration interface listening on a non standard port, and one had audit rules missing for privileged command execution.

### SAR-006 Audit record review is performed but not evidenced at the required frequency (Moderate)

**Control:** AU-6 &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-004

The security operations team reviews alerts daily, but the weekly correlated review of privileged account activity required by the system security plan produced evidence for only 6 of the 12 weeks sampled. The control activity appears to occur; the record of it does not exist.

### SAR-007 Contingency plan test not performed within the last twelve months (Moderate)

**Control:** CP-4 &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-005

The contingency plan was last exercised as a tabletop in February 2025. A functional restore test of the database tier from backup into an isolated subnet has never been performed, so the documented four hour recovery time objective is unverified.

### SAR-008 Supply chain risk management procedures drafted but not approved (Moderate)

**Control:** SR-3 &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-006

Supply chain controls in the SR family require documented processes for vetting and monitoring suppliers of system components. A draft procedure exists covering the container base image pipeline and the third party merit scoring library, but it has not been approved by the System Owner or socialised with the development team.

### SAR-009 Authenticated scanning not configured for the database tier (Moderate)

**Control:** RA-5 &nbsp;|&nbsp; **Disposition:** Closed during fieldwork and retested

Vulnerability scans of the database tier ran unauthenticated, so scan coverage was limited to network reachable services and missed installed package versions. A read only scanning service account with credentialed access was provisioned and a full authenticated scan completed on 20 March 2026. Closed.

### SAR-010 Literacy training and awareness overdue for eleven users (Moderate)

**Control:** AT-2 &nbsp;|&nbsp; **Disposition:** Closed during fieldwork and retested

Eleven of 420 agency users were past the annual due date for security literacy and awareness training. All eleven completed training during fieldwork and the Human Capital Liaison enabled an automated 30 day reminder. Closed 26 March 2026.

### SAR-011 Backup snapshots in the secondary region not encrypted with the customer managed key (Low)

**Control:** SC-28 &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-007

Primary region snapshots use a customer managed KMS key. Snapshots replicated to the secondary region were encrypted with the default service managed key, which means key rotation and key access logging are outside agency control for that copy.

### SAR-012 Authenticator management policy predates the current agency standard (Low)

**Control:** IA-5 &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-008

The password and authenticator section of the system security policy still reflects a 90 day forced rotation model. The current agency standard, and the configured behaviour of the identity provider, is length based with screening against a breached password list. The implemented control is stronger than the documented one, so the defect is documentation accuracy rather than security posture.

### SAR-013 Separation checklist not evidenced for two of nine separations (Low)

**Control:** PS-4 &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-009

Nine separations occurred in the sample period. Accounts were disabled within one business day in all nine cases, confirmed from identity provider logs, but the signed separation checklist covering property return and access revocation attestation was on file for only seven.

### SAR-014 Component inventory omits three container images (Low)

**Control:** CM-8 &nbsp;|&nbsp; **Disposition:** Open at report issue, tracked as POA-010

The authoritative component inventory lists eleven instances and four managed services but omits three container images introduced in the March release. Inventory completeness drives scan coverage, so the omission is a control dependency rather than an isolated paperwork gap.

### SAR-015 Visitor access log at the regional office is maintained on paper (Low)

**Control:** PE-3 &nbsp;|&nbsp; **Disposition:** Risk accepted by the AO on 15 May 2026

One of nine regional offices maintains a paper visitor log rather than an electronic badge record. The office holds no system components; staff there access KGMS as ordinary users over the agency network. The AO accepted this risk on 15 May 2026 on the basis that no system component is housed at the location, with review at the annual assessment.

### SAR-016 Audit record retention set to ninety days in one log group (Moderate)

**Control:** AU-11 &nbsp;|&nbsp; **Disposition:** Closed during fieldwork and retested

One of seven CloudWatch log groups, covering application error logs, retained records for 90 days against a required one year online plus two year archive. Retention was corrected and an archive lifecycle policy applied on 30 March 2026. Closed.

---

## B6: What the assessor said about the programme, not just the system

Three observations recorded outside the finding set, because they are about how the
programme runs rather than about a specific control:

1. **The readiness assessment was honest and therefore useful.** Seven of the
   16 findings were predicted in October 2025. Most readiness assessments
   predict nothing because nobody wants to write down a gap. This one did, which
   shortened fieldwork.
2. **The evidence gap is a process gap, not a discipline gap.** SAR-006 and SAR-013
   both describe work that was done without leaving a record. The pattern points at
   tooling: controls performed from live dashboards produce no artifact. Automating the
   artifact is more reliable than asking people to remember.
3. **Inventory accuracy is the load bearing control.** SAR-014, three container images
   missing from inventory, and SAR-009, the database tier outside authenticated scan
   scope, are the same failure. Scan coverage cannot exceed inventory accuracy, so CM-8
   deserves more attention than its Low rating suggests.

---

## Machine readable version

All 16 findings are published as
[artifacts/kgms-assessment-findings.csv](../artifacts/kgms-assessment-findings.csv).

Proceed to Step 5, authorisation.

---

**Navigation:** [<- Step 3: Implement and Document Controls](../step-03-ssp/README.md) &nbsp;|&nbsp; [Repository home](../README.md) &nbsp;|&nbsp; [Step 5: Authorize the System ->](../step-05-authorization/README.md)

---

*Author: Nkeiru Sarah Adesida, Information System Security Officer (ISSO), portfolio scenario*  
*Simulated system: Keystone Grants Management System (KGMS) | FWDA-KGMS-2026-MOD*  
*This document is a portfolio exercise built on a fictional organisation. It is not a government record.*  
*[GitHub portfolio](https://github.com/Nkee07) | [LinkedIn](https://www.linkedin.com/in/nkeiru-adesida-grc)*
