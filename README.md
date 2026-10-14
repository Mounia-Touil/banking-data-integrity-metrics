# Banking Data Integrity Measurement Plan (GQIM)

A measurement plan for a smart banking platform that turns one business goal – *data integrity and security* – into clear metrics, targets, and corrective actions. Also includes function point and COCOMO II cost estimates.

---

## Overview

Banks must prove that their data is **accurate, protected, and auditable**. But "good data quality" is too vague to manage. You need numbers.

Our group used the **GQIM** method (Goal → Question → Indicator → Metric) to build that bridge:

1. **Goal** – what the business wants.
2. **Question** – what we need to know to see if we reach the goal.
3. **Indicator** – a summary number or chart that answers the question.
4. **Metric** – the exact data we collect and the formula we use.

Each metric has a **threshold** (the line between OK and not OK) and a **corrective action** (what to do when the line is crossed).

This is the same work a **Data Steward** does: define quality rules, measure them, and make sure someone acts when they fail.

## Business goal

> **Ensure data integrity and security across all banking operations to protect user assets and maintain regulatory compliance.**

## GQIM summary

| Sub-goal | Question | Indicator | Metric (formula) | Threshold / target | Corrective action |
|---|---|---|---|---|---|
| **Transaction accuracy** | Are transactions recorded correctly? Do balances reconcile? | Accuracy ratio | Verified transactions ÷ total transactions × 100; **# reconciliation errors per day** | ≥ 99% excellent · 95–98% acceptable · < 95% critical | Investigate validation and processing logic; fix data, refine reconciliation scripts, patch within **1 week** |
| **Data integrity / consistency** | How consistent and traceable are data changes? Do balances match transaction history? | Integrity score; Data consistency | Accounts with zero discrepancy ÷ total accounts × 100; unauthorized changes; audit-log completeness | ≥ 98% strong · 95–97% minor issues (audit review) · < 95% major (root-cause analysis) | Find cause (reconciliation error, incomplete audit logs); correct data and re-check next cycle |
| **Access security** | What % of users and services have MFA? Do accounts hold only approved roles? | Access Security Compliance Ratio (ASCR); MFA coverage | Principals meeting all access controls ÷ total active principals × 100; % with MFA | ASCR ≥ 98% target · 95–98% watch · < 95% alert. MFA: users ≥ 98%, admins = 100%, service accounts = 100% | Enable MFA, remove extra access, disable stale accounts, block legacy logins. Alert: fix in **7 days**; watch: **14 days** |
| **Security incidents** | How fast are anomalies found and fixed? How many leaks happen? | Incident rate; response time | # confirmed data-leakage incidents; time to detect; MTTR (mean time to recover) | 0 leaks · detect ≤ 24 h · recover ≤ 4 h (critical services) | Contain the leak, revoke risky access (≤ 7 days); tune monitoring; update runbooks and run postmortems within **14 days** |
| **System availability** | Is the platform up and recovering fast? | Availability rate | Uptime % per month; MTTR | ≥ 99.9% monthly uptime | Add redundancy, automate recovery, root-cause analysis for repeated downtime |
| **Compliance and audit readiness** | Are controls tested regularly? How many audit findings per cycle? | Compliance score | % of controls passed in audits; # non-conformities per cycle | All high-severity findings fixed within policy deadlines | Fix control gaps, document updates, re-test controls **before the next audit** |

*MFA = multi-factor authentication (a second login step, like a code on your phone). Principal = any user or service account.*

## Data elements (where the numbers come from)

| Indicator | Data collected |
|---|---|
| Accuracy ratio | Transaction IDs, reconciliation flags, timestamps |
| Integrity score | Log entry IDs, change types, authorization flags, audit-log completeness fields, checksums |
| Security index | Login attempts, MFA status, user-role assignments, encryption state |
| Availability rate | Uptime and downtime minutes, incident IDs, recovery timestamps |
| Compliance score | Control IDs, test results, audit findings, remediation dates |

## How the plan runs: Analysis → Diagnosis → Action

1. **Analysis** – compare each metric to its target (weekly).
2. **Diagnosis** – find the root cause (for example: reconciliation logic error, missing audit logs, role drift).
3. **Action** – fix it, assign an owner, set a deadline, and verify in the next cycle.

| Phase | Owner | Frequency |
|---|---|---|
| Plan metrics and thresholds | Measurement team, DevOps lead, Compliance officer | Once |
| Collect data | Security and DevOps engineers | Continuous / weekly roll-ups |
| Store and manage data | Database admin, Compliance analyst | Continuous / monthly integrity checks |
| Analyze and report | Measurement and Security analysts | Weekly analysis / monthly report |
| Review | CISO, Product manager, Compliance officer | Monthly and quarterly |
| Improve | DevOps, Security, Compliance teams | Quarterly / as needed |

Outputs: CSV reports, dashboards, and a ticket list for each issue.

## Size and cost estimates

Later assignments used the same banking system to estimate size and cost.

**Function points** (a way to measure software size by what it does for the user, not by lines of code):

- Each GQIM goal was linked to function types (inputs, outputs, queries, internal files, external files).
- Unadjusted function count = **80 FP**; adjusted with 14 system characteristics (total degree of influence 42, so VAF = 0.65 + 0.01 × 42 = 1.07) → **≈ 86 FP**.

**COCOMO II** (a model that predicts effort, time, and cost from software size):

| Sizing method | Size | Effort | Schedule | Cost (at $10,000 / person-month) |
|---|---|---|---|---|
| Function points (310 UFP) | 19,840 SLOC | 78.6 person-months | 14.7 months | ≈ $786K |
| Source lines of code | 20,015 SLOC | 79.3 person-months | 14.7 months | ≈ $793K |

Both methods gave very similar results, which shows the estimate is consistent.

## What I did

This was a **group project (4 members)**. I worked with the team on defining the sub-goals, questions, indicators, metrics, thresholds, and corrective actions, and on the function point and COCOMO II assignments.

## Documents

```
docs/GQIM-measurement-plan-draft.pdf   first draft (goal-by-goal working version)
docs/GQIM-measurement-plan-final.pdf   final 10-step GQIM plan
docs/function-points.pdf               function point count linked to GQIM goals
docs/cocomo-estimate.pdf               COCOMO II effort and cost estimate
```

## What I learned

- How to turn a vague goal ("good data") into **measurable rules** with clear owners.
- Every metric needs a **threshold** and an **action**; a number nobody acts on is useless.
- Data quality, access control, and audit readiness are connected: good governance needs all three.
- How function points and COCOMO II estimate project size, effort, and cost.

## Team

Group 2: Louis Muhammad · Shahiba Shamshad · **Mounia Touil** · Michael Butler

**Course:** SWE 6763 Software Evaluation and Measurement · Kennesaw State University · Fall 2025
