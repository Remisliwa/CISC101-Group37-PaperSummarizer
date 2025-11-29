# Change Log
- (2025-11-27) Added `summary_level` variable ("short" or "detailed").
- Implemented conditional summary behavior for each section based on summary_level.
- Added required formatting and consistent output structure.

# Module 02 — Section Loop

## Overview
This module controls how the summarizer processes each section of the paper in order.  
The behavior must be deterministic, modular, and follow all global guardrails.

---

## Required Variable

`summary_level` — determines how detailed each section summary should be.

Options:
- `"short"` → produce a compact 1–2 sentence summary.
- `"detailed"` → produce a short paragraph + a 3–5 bullet list of key points.

---

## Section Loop Logic

For each section `S` in `paper_sections`:

### 1. Validate Section
- If the section is empty or missing, Module 03 will output the correct warning message.
- If the section is present, continue.

### 2. Generate Summary  

#### IF `summary_level = "short"`:
- Output 1–2 sentences that concisely capture the section’s main idea.
- No bullet points.

#### IF `summary_level = "detailed"`:
Output must include:
1. A short paragraph (3–5 sentences) summarizing the main ideas.
2. A bullet list (3–5 items) highlighting:
   - key claims  
   - findings  
   - equations (if any)  
   - definitions  
   - methodological steps

### 3. Formatting Rules
- Use the section header provided by Module 01.
- Summary text must follow directly under the header.
- Bullet lists appear after a blank line.
- No external information may be introduced (Module 03 guardrails apply).

---

## Example Output (detailed mode)

### Section 2 — Related Work
A short paragraph explaining the main themes of the related work section...

- Key point 1  
- Key point 2  
- Key point 3  

---

## Example Output (short mode)

### Section 2 — Related Work
A concise 1–2 sentence summary of the section.
