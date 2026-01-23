# BAE + Triad/Triad RM Requirements Specification

## Version 1.0 - NSF SBIR Phase I

**Project**: Behavioral Adaptation Engine with Triad Risk Management
**Organization**: 3rd Wave Edge
**Document Type**: System Requirements Specification (SRS)
**Date**: January 2026
**Status**: Phase I Requirements

-----

## Table of Contents

1. [Introduction](#1-introduction)
1. [Functional Requirements](#2-functional-requirements)
1. [Non-Functional Requirements](#3-non-functional-requirements)
1. [Performance Requirements](#4-performance-requirements)
1. [Data Requirements](#5-data-requirements)
1. [Security & Privacy Requirements](#6-security--privacy-requirements)
1. [Governance Requirements](#7-governance-requirements)
1. [Integration Requirements](#8-integration-requirements)
1. [Validation Requirements](#9-validation-requirements)
1. [Compliance Requirements](#10-compliance-requirements)
1. [Phase I Success Criteria](#11-phase-i-success-criteria)

-----

## 1. Introduction

### 1.1 Purpose

This document specifies requirements for the Behavioral Adaptation Engine (BAE) with Triad Risk Management (Triad RM) system - a governed human cognitive-state inference platform for adaptive learning.

### 1.2 Scope

Phase I requirements focus on proving technical feasibility, establishing validation methodology, and demonstrating governance effectiveness in pilot deployments (500-1,000 students, 5-10 schools).

### 1.3 Document Conventions

- **SHALL**: Mandatory requirement (must be implemented)
- **SHOULD**: Recommended requirement (implement if feasible)
- **MAY**: Optional requirement (nice-to-have)

### 1.4 System Overview

The BAE + Triad/Triad RM system comprises six layers:

1. Signal Capture (browser/device telemetry)
1. Feature Extraction (computational features)
1. BAE Inference Engine (ML models)
1. Triad Governance Layer (ethical boundaries)
1. Triad RM Risk Layer (continuous monitoring)
1. Action/API Layer (external integrations)

-----

## 2. Functional Requirements

### 2.1 Signal Capture Layer (FR-SC)

**FR-SC-001**: System SHALL capture mouse movement vectors with timestamp precision ≤10ms
**Priority**: P0 (Critical)
**Rationale**: Foundation for engagement inference

**FR-SC-002**: System SHALL capture click events including position, timestamp, and target element type
**Priority**: P0

**FR-SC-003**: System SHALL capture scroll events including velocity, direction, and distance
**Priority**: P0

**FR-SC-004**: System SHALL capture keystroke inter-arrival times (timing only, NO content)
**Priority**: P0
**Privacy Constraint**: Must never capture keystroke characters or content

**FR-SC-005**: System SHALL capture window focus/blur events with timestamp
**Priority**: P1 (High)

**FR-SC-006**: System SHALL detect idle periods (no interaction for >30 seconds)
**Priority**: P1

**FR-SC-007**: System SHALL capture touch gesture patterns on mobile/tablet devices
**Priority**: P2 (Medium)
**Phase**: Phase I stretch goal, Phase II standard

**FR-SC-008**: System SHALL operate across web browsers (Chrome, Safari, Firefox, Edge)
**Priority**: P0

**FR-SC-009**: System SHALL operate on desktop and mobile operating systems
**Priority**: P1

**FR-SC-010**: System SHALL buffer telemetry locally and transmit in batches (≤5 second intervals)
**Priority**: P1
**Rationale**: Reduce network overhead while maintaining near-real-time inference

-----

### 2.2 Feature Extraction Layer (FR-FE)

**FR-FE-001**: System SHALL compute Shannon entropy of interaction event sequences
**Priority**: P0
**Formula**: H(X) = -Σ p(x) log₂ p(x)

**FR-FE-002**: System SHALL compute coefficient of variation for keystroke timing
**Priority**: P0
**Formula**: CV = σ/μ (standard deviation / mean)

**FR-FE-003**: System SHALL compute reaction latency (time-to-first-action after stimulus)
**Priority**: P0

**FR-FE-004**: System SHALL compute path efficiency metrics (actual path length / optimal path length)
**Priority**: P1

**FR-FE-005**: System SHALL detect idle burst frequency (clusters of inactivity)
**Priority**: P1

**FR-FE-006**: System SHALL compute task-directed movement ratio (goal-oriented vs. exploratory)
**Priority**: P1

**FR-FE-007**: System SHALL compute temporal pattern consistency (session-to-session stability)
**Priority**: P2
**Phase**: Phase II enhancement

**FR-FE-008**: Feature extraction SHALL complete within 50ms of telemetry receipt
**Priority**: P0
**Performance Constraint**: Browser-side computation

**FR-FE-009**: System SHALL generate feature vectors with ≥20 dimensions
**Priority**: P1
**Rationale**: Sufficient complexity for engagement modeling

-----

### 2.3 BAE Inference Engine (FR-IE)

**FR-IE-001**: System SHALL generate engagement probability (0.00-1.00) with confidence intervals
**Priority**: P0

**FR-IE-002**: System SHALL generate disengagement risk score with early warning thresholds
**Priority**: P0

**FR-IE-003**: System SHALL generate cognitive load proxy indicator
**Priority**: P1

**FR-IE-004**: System SHALL provide model confidence score for each inference
**Priority**: P0
**Rationale**: Required for Triad governance thresholds

**FR-IE-005**: System SHALL provide feature attribution (SHAP values or equivalent) for explainability
**Priority**: P0
**Rationale**: Required for audit compliance and debugging

**FR-IE-006**: Inference engine SHALL use ensemble architecture:

- Random Forest (temporal patterns)
- Gradient Boosting (non-linear relationships)
- LSTM networks (sequence modeling)
- Bayesian aggregation (confidence estimation)
  **Priority**: P0

**FR-IE-007**: System SHALL support real-time inference mode (<100ms latency)
**Priority**: P0

**FR-IE-008**: System SHALL support batch inference mode for historical analysis
**Priority**: P1

**FR-IE-009**: System SHALL implement personalized baseline calibration (first 2-3 sessions)
**Priority**: P1
**Rationale**: Addresses individual behavioral variation

**FR-IE-010**: System SHALL maintain per-user adaptive thresholds
**Priority**: P1

**FR-IE-011**: Inference accuracy SHALL achieve ≥75% correlation with validated engagement instruments
**Priority**: P0
**Validation**: Expert observation (r ≥0.70), self-report surveys (r ≥0.70)

**FR-IE-012**: System SHALL achieve AUC-ROC ≥0.85 for engagement classification
**Priority**: P0

**FR-IE-013**: False positive rate SHALL be <15% vs. ground truth labels
**Priority**: P0

-----

### 2.4 Triad Governance Layer (FR-GOV)

**FR-GOV-001**: System SHALL enforce Precision Codex defining allowed inference scope
**Priority**: P0
**Example**: "May infer engagement, cognitive load; May NOT infer emotion, identity"

**FR-GOV-002**: System SHALL enforce confidence threshold (default ≥0.70) before automated actions
**Priority**: P0

**FR-GOV-003**: System SHALL enforce Integrity Codex specifying permissible automated actions
**Priority**: P0

**FR-GOV-004**: System SHALL maintain Living Ledger recording every inference with:

- Input feature vector with feature names and values
- Model identifier and version
- Output probability distribution
- Confidence interval
- Feature attribution scores (SHAP values)
- Governance rule applied
- Automated action taken or suppressed
- Timestamp (nanosecond precision)
- Hash pointer to previous record (tamper-evidence)
  **Priority**: P0

**FR-GOV-005**: Living Ledger SHALL implement append-only cryptographic data structure (Merkle tree or blockchain)
**Priority**: P0

**FR-GOV-006**: System SHALL log 100% of inference events (zero gaps)
**Priority**: P0

**FR-GOV-007**: System SHALL provide audit query interface enabling:

- Retrieval of all inferences for a given user session
- Filtering by confidence score ranges
- Analysis of feature attribution distributions
- Verification of cryptographic chain integrity
  **Priority**: P0

**FR-GOV-008**: System SHALL support granular user consent controls:

- Which behavioral signals may be collected (mouse, keyboard, scroll - independently toggleable)
- Which inferences may be generated (engagement, cognitive load - independently toggleable)
- Which automated actions are permitted (adaptation, alerts - independently toggleable)
- Data retention duration (session-only, 30 days, 1 year)
- Third-party data sharing permissions
  **Priority**: P0

**FR-GOV-009**: System SHALL validate current user consent status before collecting telemetry
**Priority**: P0

**FR-GOV-010**: System SHALL provide user dashboard showing:

- What data has been collected
- What inferences have been made
- What actions have been taken
- Real-time transparency
  **Priority**: P1

**FR-GOV-011**: System SHALL support consent withdrawal with immediate effect
**Priority**: P0

**FR-GOV-012**: System SHALL delete user data within 30 days of withdrawal request (GDPR compliance)
**Priority**: P0

-----

### 2.5 Triad RM Risk Layer (FR-RISK)

**FR-RISK-001**: System SHALL detect model drift using rolling 7-day accuracy windows
**Priority**: P0

**FR-RISK-002**: System SHALL detect feature distribution shift using Kolmogorov-Smirnov test (p<0.05 triggers alert)
**Priority**: P0

**FR-RISK-003**: System SHALL monitor confidence calibration via Expected Calibration Error
**Priority**: P0

**FR-RISK-004**: System SHALL track demographic subgroup performance (fairness metrics per ISO/IEC 23894)
**Priority**: P1

**FR-RISK-005**: System SHALL automatically downgrade to Safe-to-Fail mode when:

- Accuracy drops >10% from baseline
- Confidence intervals widen >20%
- Feature distribution shift detected (KS statistic >0.15)
- Confidence miscalibration exceeds threshold (ECE >0.10)
  **Priority**: P0

**FR-RISK-006**: Safe-to-Fail mode SHALL:

- Require human confirmation for all automated decisions
- Reduce automation level
- Increase inference logging verbosity
- Trigger model retraining workflow
- Escalate alerts to system administrators
  **Priority**: P0

**FR-RISK-007**: System SHALL flag false-positive spikes (>5% increase in Type I errors)
**Priority**: P1

**FR-RISK-008**: System SHALL detect anomalous access patterns (surveillance risk detection)
**Priority**: P1

**FR-RISK-009**: System SHALL generate drift alerts escalating to model retraining workflow
**Priority**: P1

**FR-RISK-010**: Drift alerts SHALL include:

- Metric that triggered alert
- Magnitude of drift
- Affected user segments
- Recommended mitigation
  **Priority**: P1

-----

### 2.6 Action/API Layer (FR-API)

**FR-API-001**: System SHALL provide real-time alert webhooks for engagement threshold violations
**Priority**: P1

**FR-API-002**: System SHALL provide adaptation triggers for LMS content difficulty adjustment
**Priority**: P1

**FR-API-003**: System SHALL implement rate limiting (max intervention frequency per time window)
**Priority**: P1
**Example**: 3 interventions per hour maximum

**FR-API-004**: System SHALL provide RESTful API for external integrations
**Priority**: P1

**FR-API-005**: System SHALL provide audit export API for compliance reporting
**Priority**: P0

**FR-API-006**: System SHALL support LMS integrations (Canvas, Blackboard, Moodle)
**Priority**: P2 (Phase II)

**FR-API-007**: System SHALL provide consent management API
**Priority**: P0

**FR-API-008**: API SHALL use OAuth 2.0 for authentication
**Priority**: P1

**FR-API-009**: API SHALL implement role-based access control (RBAC)
**Priority**: P1

-----

## 3. Non-Functional Requirements

### 3.1 Usability (NFR-USE)

**NFR-USE-001**: System SHALL require zero teacher training for basic deployment
**Priority**: P0

**NFR-USE-002**: Student onboarding SHALL complete in <2 minutes
**Priority**: P1

**NFR-USE-003**: Consent UI SHALL achieve comprehension by ≥90% of 6th grade reading level
**Priority**: P0

**NFR-USE-004**: System SHALL provide teacher dashboard with actionable insights
**Priority**: P1

-----

### 3.2 Reliability (NFR-REL)

**NFR-REL-001**: System uptime SHALL be ≥99.5% (measured monthly)
**Priority**: P1

**NFR-REL-002**: Data loss SHALL be <0.01% of telemetry events
**Priority**: P0

**NFR-REL-003**: System SHALL gracefully degrade if inference service unavailable
**Priority**: P0
**Behavior**: Fall back to non-adaptive mode, log telemetry for batch processing

**NFR-REL-004**: System SHALL support horizontal scaling to 100,000 concurrent users
**Priority**: P2 (Phase II)

-----

### 3.3 Maintainability (NFR-MAIN)

**NFR-MAIN-001**: Code SHALL maintain ≥80% test coverage
**Priority**: P1

**NFR-MAIN-002**: System SHALL use modular architecture enabling component replacement
**Priority**: P1

**NFR-MAIN-003**: All APIs SHALL be versioned (semantic versioning)
**Priority**: P1

**NFR-MAIN-004**: System SHALL provide comprehensive logging (structured JSON logs)
**Priority**: P0

-----

### 3.4 Portability (NFR-PORT)

**NFR-PORT-001**: System SHALL deploy on AWS, Azure, or GCP
**Priority**: P1

**NFR-PORT-002**: System SHALL support containerized deployment (Docker/Kubernetes)
**Priority**: P1

**NFR-PORT-003**: Client SDK SHALL support JavaScript, Python, and Java
**Priority**: P2 (Phase II)

-----

## 4. Performance Requirements

### 4.1 Latency (PERF-LAT)

**PERF-LAT-001**: End-to-end latency (signal capture → actionable output) SHALL be:

- p50: <200ms
- p95: <500ms
- p99: <1000ms
  **Priority**: P0

**PERF-LAT-002**: Feature extraction SHALL complete in <50ms
**Priority**: P0

**PERF-LAT-003**: Inference engine SHALL complete in <100ms
**Priority**: P0

**PERF-LAT-004**: Governance check SHALL complete in <20ms
**Priority**: P0

**PERF-LAT-005**: Living Ledger write SHALL complete in <30ms
**Priority**: P1

-----

### 4.2 Throughput (PERF-THR)

**PERF-THR-001**: System SHALL process ≥10,000 inference requests/second
**Priority**: P2 (Phase II scale requirement)

**PERF-THR-002**: System SHALL handle ≥100 concurrent user sessions (Phase I)
**Priority**: P0

**PERF-THR-003**: Telemetry ingestion SHALL handle ≥50,000 events/second
**Priority**: P2 (Phase II)

-----

### 4.3 Resource Utilization (PERF-RES)

**PERF-RES-001**: Client-side JavaScript SHALL consume <5MB memory
**Priority**: P1

**PERF-RES-002**: Client-side CPU utilization SHALL be <5% on average
**Priority**: P1

**PERF-RES-003**: Server-side inference SHALL use <2GB RAM per 1,000 concurrent users
**Priority**: P1

-----

## 5. Data Requirements

### 5.1 Training Data (DATA-TRAIN)

**DATA-TRAIN-001**: System SHALL require minimum training dataset:

- 50,000+ labeled interaction sessions (Phase I target)
- 500+ unique learners
- ≥100 interaction events per session
  **Priority**: P0

**DATA-TRAIN-002**: Ground truth labels SHALL include:

- Expert observation (inter-rater reliability >0.80)
- Self-report surveys (3-point engagement scale)
- Performance proxies (completion rate, time-on-task)
- Physiological validation subset (eye-tracking or EEG for 10% of data)
  **Priority**: P0

**DATA-TRAIN-003**: Dataset SHALL include diverse demographics:

- Age ranges (elementary, middle, high school, college)
- Subject domains (math, reading, science, coding)
- Platform contexts (web, desktop, mobile)
  **Priority**: P1

-----

### 5.2 Storage (DATA-STOR)

**DATA-STOR-001**: Raw telemetry SHALL be retained for ≤90 days (configurable)
**Priority**: P1

**DATA-STOR-002**: Aggregated features SHALL be retained for ≤1 year
**Priority**: P1

**DATA-STOR-003**: Living Ledger SHALL be retained for ≥7 years (compliance requirement)
**Priority**: P0

**DATA-STOR-004**: User SHALL be able to request data deletion (GDPR Right to Erasure)
**Priority**: P0

**DATA-STOR-005**: Deleted data SHALL be anonymized within 30 days
**Priority**: P0

-----

### 5.3 Data Quality (DATA-QUAL)

**DATA-QUAL-001**: Telemetry events SHALL include data quality metrics:

- Timestamp accuracy (±10ms)
- Event sequence completeness (no gaps >5 seconds)
- Signal-to-noise ratio (SNR >2.0)
  **Priority**: P1

**DATA-QUAL-002**: Sessions with <100 interaction events SHALL be flagged as low-quality
**Priority**: P1

**DATA-QUAL-003**: System SHALL detect and filter outlier telemetry (z-score >3)
**Priority**: P1

-----

## 6. Security & Privacy Requirements

### 6.1 Data Protection (SEC-PROT)

**SEC-PROT-001**: Telemetry data in transit SHALL be encrypted (TLS 1.3)
**Priority**: P0

**SEC-PROT-002**: Telemetry data at rest SHALL be encrypted (AES-256)
**Priority**: P0

**SEC-PROT-003**: Encryption keys SHALL be rotated every 90 days
**Priority**: P1

**SEC-PROT-004**: System SHALL never capture or transmit keystroke content
**Priority**: P0
**Critical**: Privacy violation if breached

**SEC-PROT-005**: System SHALL never capture or transmit screen content
**Priority**: P0

**SEC-PROT-006**: PII (name, email, student ID) SHALL be separated from behavioral data
**Priority**: P0

**SEC-PROT-007**: Inference outputs SHALL be linkable to users via pseudonymous identifiers only
**Priority**: P0

-----

### 6.2 Access Control (SEC-ACCESS)

**SEC-ACCESS-001**: System SHALL implement role-based access control:

- Student: View own data only
- Teacher: View aggregated class data + individual with consent
- Admin: View all data with audit trail
- Researcher: View anonymized data only
  **Priority**: P0

**SEC-ACCESS-002**: Access to Living Ledger SHALL be logged with actor, timestamp, query
**Priority**: P0

**SEC-ACCESS-003**: Multi-factor authentication SHALL be required for admin access
**Priority**: P1

**SEC-ACCESS-004**: Password policies SHALL enforce:

- Minimum 12 characters
- Complexity requirements
- 90-day rotation
  **Priority**: P1

-----

### 6.3 Privacy Preservation (SEC-PRIV)

**SEC-PRIV-001**: System SHALL support differential privacy for aggregated statistics
**Priority**: P2 (Phase II)

**SEC-PRIV-002**: Exported datasets SHALL be k-anonymized (k≥5)
**Priority**: P1

**SEC-PRIV-003**: Re-identification risk SHALL be assessed before data sharing
**Priority**: P1

**SEC-PRIV-004**: System SHALL not infer protected characteristics (race, religion, health status)
**Priority**: P0

-----

## 7. Governance Requirements

### 7.1 Ethical Constraints (GOV-ETH)

**GOV-ETH-001**: System SHALL never be used for employee surveillance without explicit consent
**Priority**: P0

**GOV-ETH-002**: System SHALL never be used for punitive actions (grading penalties, disciplinary)
**Priority**: P0

**GOV-ETH-003**: Engagement inferences SHALL be advisory only, never deterministic
**Priority**: P0

**GOV-ETH-004**: System SHALL provide opt-out without penalty
**Priority**: P0

-----

### 7.2 Transparency (GOV-TRANS)

**GOV-TRANS-001**: System SHALL provide user-facing explanation of:

- What data is collected
- How inferences are made
- What actions are triggered
- Who has access
  **Priority**: P0

**GOV-TRANS-002**: Feature attribution SHALL be available in non-technical language
**Priority**: P1

**GOV-TRANS-003**: Model version and training date SHALL be disclosed in UI
**Priority**: P1

-----

### 7.3 Accountability (GOV-ACCT)

**GOV-ACCT-001**: Every automated action SHALL have traceable decision rationale in Living Ledger
**Priority**: P0

**GOV-ACCT-002**: System SHALL support regulatory audit (export complete decision history)
**Priority**: P0

**GOV-ACCT-003**: Audit exports SHALL include:

- All inferences with timestamps
- Governance rules applied
- Actions taken
- Cryptographic verification hashes
  **Priority**: P0

-----

## 8. Integration Requirements

### 8.1 LMS Integration (INT-LMS)

**INT-LMS-001**: System SHALL integrate with Canvas via LTI 1.3
**Priority**: P2 (Phase II)

**INT-LMS-002**: System SHALL integrate with Blackboard via REST API
**Priority**: P2 (Phase II)

**INT-LMS-003**: System SHALL integrate with Moodle via plugin architecture
**Priority**: P2 (Phase II)

**INT-LMS-004**: LMS integration SHALL support single sign-on (SSO)
**Priority**: P2

-----

### 8.2 Assessment Tools (INT-ASSESS)

**INT-ASSESS-001**: System SHOULD integrate with ROAR (Rapid Online Assessment of Reading)
**Priority**: P2
**Rationale**: Validation partnership with Jason Yeatman

**INT-ASSESS-002**: System SHOULD integrate with OATutor (Open Adaptive Tutor)
**Priority**: P2
**Rationale**: Validation partnership with Zachary Pardos

-----

### 8.3 Third-Party Tools (INT-THIRD)

**INT-THIRD-001**: System SHALL provide Zapier integration for workflow automation
**Priority**: P2 (Phase II)

**INT-THIRD-002**: System SHALL provide webhooks for custom integrations
**Priority**: P1

**INT-THIRD-003**: System SHALL document REST API with OpenAPI 3.0 specification
**Priority**: P1

-----

## 9. Validation Requirements

### 9.1 Accuracy Validation (VAL-ACC)

**VAL-ACC-001**: Engagement inference SHALL achieve r ≥0.70 correlation with expert observation
**Priority**: P0

**VAL-ACC-002**: Engagement inference SHALL achieve r ≥0.70 correlation with self-report surveys
**Priority**: P0

**VAL-ACC-003**: Disengagement prediction SHALL achieve AUC-ROC ≥0.85
**Priority**: P0

**VAL-ACC-004**: False positive rate SHALL be <15% in controlled studies
**Priority**: P0

**VAL-ACC-005**: System SHALL achieve ≥75% accuracy across diverse learner populations
**Priority**: P0

-----

### 9.2 Fairness Validation (VAL-FAIR)

**VAL-FAIR-001**: Demographic disparate impact ratio SHALL be <1.2 (per ISO/IEC 23894)
**Priority**: P1

**VAL-FAIR-002**: Accuracy SHALL not vary >10% across demographic subgroups
**Priority**: P1

**VAL-FAIR-003**: System SHALL be tested with diverse populations:

- Age (K-12, college, adult learners)
- Subject (STEM, humanities, vocational)
- Platform (web, mobile, desktop)
- Ability (typical, learning differences)
  **Priority**: P0

-----

### 9.3 Drift Validation (VAL-DRIFT)

**VAL-DRIFT-001**: Drift detection SHALL flag 90% of accuracy drops >10%
**Priority**: P0

**VAL-DRIFT-002**: Drift detection SHALL trigger within 7 days of accuracy degradation
**Priority**: P1

**VAL-DRIFT-003**: Synthetic drift injection testing SHALL validate detection sensitivity
**Priority**: P1

-----

### 9.4 Usability Validation (VAL-USE)

**VAL-USE-001**: System Usability Scale (SUS) score SHALL be ≥70
**Priority**: P1

**VAL-USE-002**: Teacher Net Promoter Score (NPS) SHALL be ≥50
**Priority**: P1

**VAL-USE-003**: Student consent comprehension SHALL be ≥90% (6th grade reading level)
**Priority**: P0

-----

## 10. Compliance Requirements

### 10.1 Educational Privacy (COMP-EDU)

**COMP-EDU-001**: System SHALL comply with FERPA (Family Educational Rights and Privacy Act)
**Priority**: P0

**COMP-EDU-002**: System SHALL comply with COPPA (Children's Online Privacy Protection Act)
**Priority**: P0

**COMP-EDU-003**: System SHALL obtain parental consent for users <13 years old
**Priority**: P0

**COMP-EDU-004**: Educational records SHALL not be disclosed without consent
**Priority**: P0

-----

### 10.2 Data Protection (COMP-DATA)

**COMP-DATA-001**: System SHALL comply with GDPR (General Data Protection Regulation)
**Priority**: P0

**COMP-DATA-002**: System SHALL comply with CCPA (California Consumer Privacy Act)
**Priority**: P1

**COMP-DATA-003**: System SHALL support GDPR rights:

- Right to access
- Right to rectification
- Right to erasure
- Right to data portability
- Right to object
  **Priority**: P0

-----

### 10.3 AI Regulation (COMP-AI)

**COMP-AI-001**: System SHALL comply with EU AI Act (high-risk AI systems)
**Priority**: P0

**COMP-AI-002**: System SHALL comply with NIST AI Risk Management Framework
**Priority**: P1

**COMP-AI-003**: System SHALL maintain required documentation per EU AI Act Article 11:

- Technical documentation
- Quality management system
- Record-keeping (Living Ledger)
- Transparency provisions
- Human oversight
  **Priority**: P0

-----

### 10.4 Accessibility (COMP-ACCESS)

**COMP-ACCESS-001**: UI SHALL comply with WCAG 2.1 Level AA
**Priority**: P1

**COMP-ACCESS-002**: Consent forms SHALL be available in screen-reader accessible format
**Priority**: P1

**COMP-ACCESS-003**: System SHALL support keyboard-only navigation
**Priority**: P1

-----

## 11. Phase I Success Criteria

### 11.1 Technical Success Metrics

**SUCCESS-TECH-001**: Usable Signal Rate

- **Target**: ≥80% of sessions yield usable signal
- **Measurement**: Sessions with ≥100 interaction events and SNR >2.0

**SUCCESS-TECH-002**: Inference Accuracy

- **Target**: ≥75% correlation with validated baseline
- **Measurement**: Pearson r with expert observation and self-report (r >0.70)

**SUCCESS-TECH-003**: Improvement Over Random

- **Target**: ≥3× baseline performance
- **Measurement**: AUC-ROC vs. random classifier (target AUC ≥0.85)

**SUCCESS-TECH-004**: Drift Detection Sensitivity

- **Target**: Flag 90% of accuracy drops >10%
- **Measurement**: Synthetic drift injection with precision-recall analysis

**SUCCESS-TECH-005**: Audit Completeness

- **Target**: 100% of inferences logged
- **Measurement**: Living Ledger coverage (zero gaps)

**SUCCESS-TECH-006**: Safe-to-Fail Activation

- **Target**: Demonstrable suppression of risky automation
- **Measurement**: Actions cease when confidence <0.70 or drift detected

**SUCCESS-TECH-007**: Latency

- **Target**: <200ms p50, <500ms p95
- **Measurement**: Production telemetry under realistic load (100 concurrent users)

**SUCCESS-TECH-008**: False Positive Rate

- **Target**: <15%
- **Measurement**: Type I error rate vs. ground truth labels

-----

### 11.2 Pilot Deployment Metrics

**SUCCESS-PILOT-001**: Student Reach

- **Target**: 500-1,000 students across 5-10 schools

**SUCCESS-PILOT-002**: Session Completion

- **Target**: ≥80% of students complete ≥5 learning sessions

**SUCCESS-PILOT-003**: Teacher Adoption

- **Target**: ≥70% of pilot teachers use BAE insights in instruction

**SUCCESS-PILOT-004**: Consent Rate

- **Target**: ≥80% of students/parents consent to participation

-----

### 11.3 Research Output Metrics

**SUCCESS-RES-001**: Publications

- **Target**: 2-3 peer-reviewed papers submitted
- **Venues**: Journal of Learning Analytics, Computers & Education, CHI, AIED

**SUCCESS-RES-002**: Open-Source Releases

- **Target**: pyBAE library published with documentation
- **Measurement**: GitHub stars, downloads, community adoption

**SUCCESS-RES-003**: Conference Presentations

- **Target**: ≥2 presentations at LAK, AIED, Learning@Scale, or CHI

**SUCCESS-RES-004**: Dataset Release

- **Target**: Anonymized behavioral telemetry dataset for research community
- **Measurement**: Dataset downloads, citations in other work

-----

### 11.4 Partnership Metrics

**SUCCESS-PART-001**: Academic Collaborations

- **Target**: 2-3 active academic partnerships (Pardos, Yeatman, Abrahamson)
- **Evidence**: MOUs, data sharing agreements, co-authored publications

**SUCCESS-PART-002**: Letters of Interest

- **Target**: 3-5 LOIs from pilot schools for paid deployment

**SUCCESS-PART-003**: Industry Partnerships

- **Target**: Exploratory discussions with ≥2 LMS vendors (Canvas, Blackboard)

-----

## 12. Requirements Traceability Matrix

### 12.1 Critical Path Requirements (Must-Have for Phase I)

|ID              |Requirement                            |Priority|Validation Method                          |
|----------------|---------------------------------------|--------|-------------------------------------------|
|FR-IE-011       |≥75% accuracy vs. validated instruments|P0      |Correlation analysis (expert + self-report)|
|FR-GOV-004      |Living Ledger with 100% coverage       |P0      |Audit log analysis                         |
|PERF-LAT-001    |<200ms p50 latency                     |P0      |Production telemetry                       |
|SEC-PROT-004    |Never capture keystroke content        |P0      |Code review + security audit               |
|COMP-EDU-001    |FERPA compliance                       |P0      |Legal review + compliance checklist        |
|SUCCESS-TECH-002|≥75% inference accuracy                |P0      |Validation studies                         |

-----

### 12.2 Phase II Deferred Requirements

|ID           |Requirement               |Phase II Timeline|
|-------------|--------------------------|-----------------|
|FR-SC-007    |Touch gesture capture     |Q1 2027          |
|INT-LMS-001  |Canvas LTI 1.3 integration|Q2 2027          |
|PERF-THR-001 |10,000 req/sec throughput |Q3 2027          |
|INT-THIRD-001|Zapier integration        |Q4 2027          |

-----

## 13. Change Management

### 13.1 Requirement Change Process

1. **Proposal**: Stakeholder submits requirement change request
1. **Impact Analysis**: Technical team assesses impact on architecture, timeline, budget
1. **Prioritization**: Product owner prioritizes against existing requirements
1. **Approval**: Steering committee approves/rejects with rationale
1. **Implementation**: Requirement added to backlog with updated traceability
1. **Documentation**: SRS updated with version control

### 13.2 Version History

|Version|Date    |Author       |Changes                                  |
|-------|--------|-------------|-----------------------------------------|
|1.0    |Jan 2026|3rd Wave Edge|Initial requirements for NSF SBIR Phase I|

-----

## 14. Appendices

### Appendix A: Glossary

- **BAE**: Behavioral Adaptation Engine
- **Triad**: Governance framework (Precision Codex, Integrity Codex, Living Ledger)
- **Triad RM**: Triad Risk Management (complete system including risk monitoring)
- **Living Ledger**: Immutable audit trail of all inferences and decisions
- **Safe-to-Fail**: Automated downgrade mode when system uncertainty exceeds thresholds
- **SHAP**: SHapley Additive exPlanations (feature attribution method)

### Appendix B: Referenced Standards

- ISO/IEC 23894: Information technology — Artificial intelligence — Guidance on risk management
- WCAG 2.1: Web Content Accessibility Guidelines
- NIST AI RMF: NIST Artificial Intelligence Risk Management Framework
- EU AI Act: Regulation (EU) 2024/1689 on Artificial Intelligence

### Appendix C: Stakeholder Matrix

|Stakeholder   |Interest           |Influence|Key Requirements    |
|--------------|-------------------|---------|--------------------|
|Students      |Privacy, fairness  |Medium   |SEC-PROT, VAL-FAIR  |
|Teachers      |Usability, insights|High     |NFR-USE, FR-API-004 |
|Administrators|Compliance, cost   |High     |COMP-EDU, NFR-REL   |
|Researchers   |Rigor, publications|Medium   |VAL-ACC, SUCCESS-RES|
|Regulators    |Compliance, safety |High     |COMP-AI, GOV-ETH    |

-----

**END OF REQUIREMENTS SPECIFICATION**

*Document Status*: Version 1.0 - NSF SBIR Phase I
*Next Review Date*: March 2026 (post-NSF decision)
*Owner*: Eric, CEO 3rd Wave Edge
*Approvers*: Academic Advisors (Pardos, Yeatman, Abrahamson)
