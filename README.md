# EU AI Act Compliance Framework for AI-Enabled Medical Triage

A regulatory-ready conceptual design for an AI-assisted emergency
department triage system, built to satisfy the high-risk AI
requirements of the EU Artificial Intelligence Act.

---

## Project Overview

Emergency departments face persistent overcrowding, delayed triage,
and preventable adverse outcomes. This project proposes a
multimodal AI triage system that classifies patient urgency using
the Emergency Severity Index (ESI) — while embedding governance,
explainability, and human oversight directly into the architecture.

**This is not an afterthought compliance exercise.** Regulatory
requirements are designed into the system from the ground up:
auditability, bias mitigation, transparency, and clinician
authority are architectural features, not add-ons.

---

## System Architecture

The system combines two AI modalities in a hybrid architecture:

**Structured data pipeline**
Vital signs (HR, BP, SpO₂, temperature) and demographic data
processed through a gradient-boosted decision tree model.
Suitable for tabular clinical data and non-linear relationships.

**Unstructured text pipeline**
Triage nurse notes and patient complaints processed through
ClinicalBERT — a domain-specific language model pre-trained
on clinical text. Captures symptom descriptions and contextual
cues not present in numerical data alone.

**Fusion layer**
Feature representations from both models combined and passed
to a calibrated ESI classifier (levels 1–5).

**Output**
Recommended ESI level + confidence score + SHAP-based
explanation highlighting the features that drove the prediction.
Clinician makes the final decision — always.

---

## EU AI Act Compliance Features

| Requirement | Implementation |
|-------------|----------------|
| Article 12 — Traceability | All preprocessing steps logged for audit |
| Article 13 — Transparency | SHAP feature importance explanations |
| Article 14 — Human oversight | Clinician confirmation required for all decisions |
| Article 9 — Risk management | Continuous performance monitoring and drift detection |
| GDPR alignment | Privacy-by-design, pseudonymisation, federated learning consideration |

---

## Key Design Decisions

**Why hybrid architecture?**
Clinical data is inherently multimodal. Vital signs are structured
and tabular — gradient boosting handles this well. Nurse notes are
unstructured narrative text — ClinicalBERT captures semantic
meaning that structured models cannot.

**Why SHAP explainability?**
Clinicians need to understand why the system made a recommendation
before they can trust or override it. SHAP provides local,
concise explanations tied to specific input features — designed
for clinical heuristics, not technical audiences.

**Why human-in-the-loop?**
EU AI Act Article 14 mandates human oversight for high-risk AI.
More importantly, triage errors have direct patient safety
consequences. The system is clinical decision support — not
autonomous decision-making.

**Why regulatory sandbox validation?**
Real-world deployment requires controlled evidence generation.
Sandbox pilots with pre-specified KPIs, safety stop criteria,
and regulator co-design reduce uncertainty and build the
technical file required for conformity assessment.

---

## Literature Review

15 peer-reviewed papers reviewed (2021–2025) covering:
- AI triage accuracy and ED workflow optimisation
- Bias detection and mitigation in medical AI
- Federated learning for privacy-preserving training
- EU AI Act classification of medical software
- Regulatory sandbox frameworks for responsible AI deployment

Key finding: AI systems consistently improve triage accuracy
over manual methods, but real-world value depends on
explainability, fairness, and human oversight — not accuracy alone.

---

## Limitations & Future Work

This is a conceptual design — no implementation or clinical
evaluation has been conducted. Future work should:

- Prototype the system with MIMIC-IV-ED dataset
- Conduct staged sandbox trials measuring clinical outcomes,
  equity metrics, and workflow impact
- Evaluate clinician acceptance and override patterns
- Test federated learning feasibility across hospital sites

---

## Stack (Proposed Implementation)

- ClinicalBERT (HuggingFace Transformers)
- XGBoost / LightGBM for structured data
- SHAP for explainability
- FastAPI for system interface
- MLflow for experiment tracking and model registry

---

## Project Context

Group coursework for **CN7041 Fundamentals of Artificial
Intelligence**, MSc Artificial Intelligence and Data Science,
University of East London, December 2025.

**Team:** Victor Chukwudi Robinson, Nathaniel Onosemudiana Ovabor,
Sai Charan Burujukindi
