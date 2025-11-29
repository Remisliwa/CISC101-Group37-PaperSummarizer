# Change Log
- (2025-11-27) Added strict evidence mode (`evidence_mode = "strict"`).
- Added standardized warnings for missing/empty/short sections.
- Integrated hallucination-prevention instructions and evidence constraints.

# Module 03 — Guardrails & Evidence Constraints

## Purpose
This module defines **all** safety and hallucination-prevention mechanisms for the summarizer.  
It ensures the system outputs only information grounded in the provided paper and handles missing or insufficient text in a consistent manner.

---

## Evidence Mode

### `evidence_mode = "strict"`
When set to `"strict"`, the summarizer must:

1. Use **only** information that explicitly appears in the section text:
   - Claims  
   - Definitions  
   - Equations  
   - Results  
   - Descriptions  

2. Avoid:
   - External facts  
   - Domain guesses  
   - Filling in missing reasoning  
   - Inferring missing steps  

3. If a section does not contain enough information to meet summarization requirements:

The system must output the standardized message:

> **“The source text does not provide enough detail to summarize this section in strict evidence mode.”**

This message **replaces** the normal summary.

---

## Section Validity Warnings

Before generating a section summary, the system must apply the following checks:

### **1. Missing or Empty Sections**
If a section is missing or contains no usable text:

Output:

> **“Section skipped: no usable text was provided.”**

No summary is generated.

---

### **2. Very Short Sections (< 50 words)**

Output the warning **before** the summary:

> **“Section very short: summary may be incomplete.”**

Then proceed with the summary based on the available text.

---

## Integration Rules

- Module 02 must call this module for section validity checks.
- If strict evidence mode triggers a “lack of evidence” warning, this replaces the entire section output.
- These guardrails override all formatting and summary rules from Module 02.

---

## Priority Order

1. Missing/empty section warnings  
2. Strict evidence check  
3. Summary generation (short/detailed)  
4. Rendering (Module 04)

---

## Rationale
These guardrails prevent:
- Hallucinated equations  
- Invented methods  
- Fake citations  
- Overconfident statements not supported by text  
- Summaries based on insufficient or missing content  
