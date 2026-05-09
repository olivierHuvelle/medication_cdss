# CDS Track A — Fast Exploration MVP Roadmap

## Purpose

This roadmap is intentionally focused on:

- validating the idea quickly
- minimizing over-engineering
- identifying real complexity early
- testing whether the workflow is enjoyable and sustainable
- building a functional but small prototype

This roadmap is NOT intended to:

- build a production-grade CDS
- achieve exhaustive medication coverage
- solve all edge cases
- optimize everything upfront

---

# Status System

## Task Statuses

- [ ] TODO
- [~] IN_PROGRESS
- [x] DONE
- [!] BLOCKED

---

## Example

- [!] Define renal thresholds for hyperkalemia logic
  - Blocking reason: inconsistent guideline thresholds between ESC and KDIGO

---

# Global Estimated Timeline

| Phase | Estimated Time |
|---|---|
| Phase A0 — Minimal Schema | 1–2h |
| Phase A1 — AI Ingestion Setup | 1–2h |
| Phase A2 — Initial Dataset | 2–4h |
| Phase A3 — Rule Engine MVP | 2–4h |
| Phase A4 — Mini UI | 1–2h |
| Phase A5 — Validation | 1–2h |
| TOTAL | ~8–15h |

---

# Sources & References

## Belgian Clinical Sources

### CBIP / BCFI

https://www.cbip.be/

Usage:

- indications
- contraindications
- warnings
- adverse effects
- monitoring recommendations
- Belgian clinical consistency

Important:

CBIP should primarily be used as:

- validation source
- reasoning source
- explanatory source

NOT as the sole structured CDS database.

---

### SAM

https://www.samportal.be/

Usage:

- medication normalization
- molecule naming
- ATC mapping
- Belgian medication ecosystem

---

## Structural / International Sources

### DrugBank

https://go.drugbank.com/

Usage:

- interaction inspiration
- structured drug relationships
- metadata inspiration

---

### OpenFDA

https://open.fda.gov/

Usage:

- labeling data
- warnings
- contraindications
- adverse events

---

## Clinical Guidelines

### ESC

https://www.escardio.org/

### KDIGO

https://kdigo.org/

### NICE

https://www.nice.org.uk/

Usage:

- contextual severity
- renal thresholds
- monitoring logic
- acceptable clinical combinations

### STOPP / START Criteria

https://www.ucc.ie/en/media/research/geriatricmedicine/STOPPSTARTV3.pdf

Usage:

- geriatric prescribing validation
- deprescribing support
- detection of potentially inappropriate medications
- detection of omitted but clinically indicated therapies
- elderly-specific risk contextualization
- polypharmacy assessment
- fall-risk and frailty-related medication review

Important:

STOPP/START should primarily be used as:

- geriatric reasoning layer
- contextual prescribing framework
- prioritization support system

NOT as a replacement for core interaction or contraindication logic.

---

# Initial MVP Scope

## Medication Coverage

Target: 10–15 medications only.

### Recommended Initial Medications

#### Cardiovascular

- ramipril
- lisinopril
- spironolactone
- furosemide

---

#### Analgesics

- ibuprofen
- naproxen

---

#### Sedation / Psychiatry

- diazepam
- lorazepam

---

#### Pain Management

- tramadol
- morphine

---

#### Endocrinology

- metformin
- empagliflozin

---

#### Anticoagulation

- apixaban
- rivaroxaban

---

# Initial Risk Coverage

Only support:

- hyperkalemia
- acute kidney injury
- sedation
- respiratory depression
- bleeding
- lactic acidosis

---

# Development Principles

## Core Principles

### Stable > Exhaustive

The schema does NOT need to be exhaustive initially.

The schema MUST:

- remain stable
- remain extensible
- avoid major future refactors

---

### Deterministic Logic First

The first versions should prioritize:

- explicit rules
- explainability
- predictable outputs

AI reasoning layers are secondary.

---

### Human Validation Mandatory

AI should accelerate:

- structuring
- normalization
- summarization

AI should NOT become the source of truth.

---

### Clinical Relevance First

Focus on:

- common medications
- common dangerous combinations
- high-yield scenarios

NOT exhaustive coverage.

---

# Phase A0 — Minimal Schema

Estimated Time: 1–2h

## Objectives

- define minimal stable structure
- avoid future large refactors
- keep schema intentionally small

---

## Tasks

- [ ] Define minimal medication schema
  - Estimated Time: 20–40min

- [ ] Define minimal rule schema
  - Estimated Time: 20–40min

- [ ] Define patient context schema
  - Estimated Time: 15–30min

- [ ] Define severity enum
  - Estimated Time: 5–10min

- [ ] Define recommendation structure
  - Estimated Time: 10–20min

- [ ] Validate schema against 3 clinical scenarios
  - Estimated Time: 20–40min

---

## Example Subtasks

- [ ] Define severity levels
  - Estimated Time: 5–10min

- [ ] Define modifier format
  - Estimated Time: 10–15min

- [ ] Define recommendation format
  - Estimated Time: 10–15min

---

## Recommended Stress-Test Scenarios

### Scenario 1

- ACE inhibitor
- spironolactone
- CKD stage 3

Expected:

- hyperkalemia alert
- monitoring recommendation

---

### Scenario 2

- NSAID
- diuretic
- elderly patient

Expected:

- AKI risk detection

---

### Scenario 3

- opioid
- benzodiazepine

Expected:

- respiratory depression warning

---

# Phase A1 — AI-Assisted Ingestion Setup

Estimated Time: 1–2h

## Objectives

- accelerate database population
- maintain consistency
- reduce hallucinations

---

## Pipeline Overview

1. Extract source text
2. AI structures into JSON
3. Human validates
4. Integrate into database

---

## Tasks

- [ ] Create stable ingestion prompt
  - Estimated Time: 20–40min

- [ ] Define hallucination prevention rules
  - Estimated Time: 10–20min

- [ ] Create ingestion folder structure
  - Estimated Time: 10–20min

- [ ] Create validation checklist
  - Estimated Time: 15–30min

- [ ] Test ingestion workflow on 3 medications
  - Estimated Time: 20–40min

---

## Hallucination Prevention Rules

- never invent thresholds
- never infer contraindications without support
- use null if uncertain
- preserve uncertainty explicitly
- validate clinically important outputs manually

---

## Example Validation Checklist

- [ ] Thresholds verified
- [ ] Contraindications verified
- [ ] No invented risks
- [ ] Severity coherent
- [ ] Monitoring recommendations coherent

---

# Phase A2 — Initial Dataset

Estimated Time: 2–4h

## Objectives

- create clinically useful minimal dataset
- prioritize high-yield scenarios

---

## Tasks

- [ ] Create medication normalization rules
  - Estimated Time: 15–30min

- [ ] Populate first 5 medications
  - Estimated Time: 30–60min

- [ ] Populate first 10 medications
  - Estimated Time: 1–2h

- [ ] Populate first 15 medications
  - Estimated Time: 1–2h

- [ ] Create first 10 interaction rules
  - Estimated Time: 1–2h

---

## Recommended First Rules

- ACEi + spironolactone
- NSAID + diuretic
- opioid + benzodiazepine
- metformin + severe CKD
- anticoagulant + NSAID

---

# Phase A3 — Rule Engine MVP

Estimated Time: 2–4h

## Objectives

- generate clinically coherent alerts
- support contextual severity
- remain deterministic and explainable

---

## Tasks

- [ ] Create simple rule evaluator
  - Estimated Time: 30–90min

- [ ] Support multi-drug matching
  - Estimated Time: 20–40min

- [ ] Support patient modifiers
  - Estimated Time: 30–60min

- [ ] Implement severity escalation
  - Estimated Time: 20–40min

- [ ] Implement recommendation generation
  - Estimated Time: 20–40min

- [ ] Implement readable outputs
  - Estimated Time: 20–40min

---

# Phase A4 — Mini UI

Estimated Time: 1–2h

## Objectives

- allow rapid experimentation
- minimize frontend complexity

---

## Recommended Choice

### Streamlit

Reason:

- extremely fast iteration
- minimal frontend overhead
- ideal for prototyping

---

## Tasks

- [ ] Create medication input form
  - Estimated Time: 20–40min

- [ ] Create patient context form
  - Estimated Time: 20–40min

- [ ] Create alert display
  - Estimated Time: 20–40min

- [ ] Create recommendation display
  - Estimated Time: 20–40min

---

# Phase A5 — Validation

Estimated Time: 1–2h

## Objectives

- identify major logical flaws
- verify practical usefulness

---

## Tasks

- [ ] Test 5 clinical scenarios
  - Estimated Time: 30–60min

- [ ] Compare outputs with CBIP
  - Estimated Time: 20–40min

- [ ] Review false positives
  - Estimated Time: 15–30min

- [ ] Review missing dangerous alerts
  - Estimated Time: 15–30min

---

# Track A Success Criteria

The prototype is considered successful if:

- major dangerous combinations are detected
- contextual severity works
- recommendations are clinically coherent
- schema remains manageable
- ingestion workflow is sustainable
- false positives remain acceptable

---

# Important Anti-Scope-Creep Rules

- do NOT start with all medications
- do NOT start with dosage adjustment engine
- do NOT attempt exhaustive coverage
- do NOT over-engineer architecture initially
- do NOT optimize prematurely
- do NOT build AI-only reasoning initially

---

# Recommended Next Step After Track A

ONLY after validating Track A:

- expand medication coverage
- improve normalization
- improve explainability
- improve UI
- improve rule sophistication
- improve guideline integration
- consider PostgreSQL migration

---

# Final Important Insight

The value of the project is NOT:

> having the biggest medication database

The value is:

> providing clinically relevant, contextualized, explainable alerts while minimizing alert fatigue.

