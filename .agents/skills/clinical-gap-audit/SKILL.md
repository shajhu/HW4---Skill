---
name: clinical-gap-audit
description: Audits Occupational Therapist and Pharmacist notes for missing required documentation elements using deterministic keyword validation. Use when verifying structured note completeness for supported practitioner types.
---

### When to use:
- auditing OT or Pharmacist notes for completeness
- validating required documentation structure
- identifying missing sections in practitioner notes

### When NOT to use:
- unsupported practitioner types
- generating clinical notes
- interpreting or diagnosing conditions

### Activation cues:
- "audit this note"
- "check completeness"
- "validate documentation"
- "what is missing from this note"

### Inputs:
- practitioner_type (e.g., "Occupational Therapist", "Pharmacist")
- note text

### Steps:
1. Pass note text to audit script
2. Identify required elements
3. Return found and missing sections
4. Compute completeness score

### Output:
- list of detected elements
- list of missing elements
- completeness score

### Limitations:
- Only supports:
	- Occupational Therapist
	- Pharmacist
- Keyword-based detection only
- Does not interpret clinical meaning
- requires human review
