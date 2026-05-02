# clinical-gap-audit

## What this skill does
A deterministic audit tool that evaluates practitioner notes for required documentation elements.

## Why this was chosen
AI alone cannot reliably enforce structured completeness; this script provides deterministic validation.

## Why a Script is Required

This task cannot rely on AI alone because:

- language models do not reliably enforce structured completeness
- outputs can vary between runs
- missing elements may not be consistently detected

The script ensures:

- deterministic validation
- repeatable results
- consistent completeness scoring
- reliable identification of missing sections

## How to use
Run the script with practitioner type and note text.

### Skill structure
```text
HW4 - Skill/
  .agents/
    skills/
      clinical-gap-audit/
        SKILL.md
        scripts/
          audit.py
        references/
  README.md
```

### Command-line use
```powershell
cd "C:\Users\shami\OneDrive\Documents\John Hopkins\Generative AI\Repository\HW4 - Skill"
python .agents\skills\clinical-gap-audit\scripts\audit.py
```

### Python import use
```python
from pathlib import Path
import importlib.util

script_path = Path(".agents/skills/clinical-gap-audit/scripts/audit.py")
spec = importlib.util.spec_from_file_location("audit", script_path)
module = importlib.util.module_from_spec(spec)
spec.loader.exec_module(module)

result = module.audit_clinical_note(
    "Assessment notes deficits and functional impact only",
    "Occupational Therapist",
)
print(result)
```

## What the script does
- parses input
- checks required elements
- returns missing + found sections
- calculates completeness score

## Skill Usage in Agent (Step 5 Evidence)

The following examples demonstrate how the skill is activated and used within an agent workflow.

### Prompt 1 - Normal Case (OT)
User Prompt:
```text
Audit this OT note for completeness: Patient reports fatigue and decreased grip strength affecting daily activities.
```

Expected Agent Behavior:
- Recognizes "audit" + "OT note"
- Activates clinical-gap-audit skill
- Calls audit.py script
- Returns structured completeness output

Expected Output Summary:
- Found elements: partial
- Missing elements: justification, intervention
- Completeness score: partial

### Prompt 2 - Edge Case
User Prompt:
```text
Check this note: patient tired
```

Expected Agent Behavior:
- Activates skill due to audit intent
- Script detects minimal structure

Expected Output Summary:
- Found: none
- Missing: all required elements
- Completeness score: 0.0

### Prompt 3 - Caution / Partial Decline Case
User Prompt:
```text
Audit this cardiology consult note for completeness
```

Expected Agent Behavior:
- Attempts to activate skill
- Script detects unsupported practitioner type
- Returns controlled limitation response

Expected Output:
```json
{
  "error": "Unsupported practitioner type"
}
```

Explanation:
The skill correctly declines unsupported practitioner types rather than generating unreliable output.

## Test cases
### Test 1 - Normal OT Case
Input:
```text
Practitioner: Occupational Therapist
Note: Assessment completed. Deficits observed in dressing. Functional impact includes reduced independence.
```
Expected behavior:
- detects assessment, deficits, functional impact
- misses justification, intervention
- returns a structured completeness score

### Test 2 - Edge Case
Input:
```text
Practitioner: Occupational Therapist
Note: follow-up
```
Expected behavior:
- detects little or nothing
- returns many missing elements
- still returns a valid structured report

### Test 3 - Unsupported Practitioner (Caution Case)
Input:
```text
Practitioner: Cardiologist
Note: Cardiology note
```
Expected:
- No analysis performed
- Error returned
- No hallucinated output

## What worked well
- reliable detection of explicit sections
- simple, reusable structure

## Limitations
- keyword-based (no semantic understanding)
- requires human interpretation

## Standalone design
- no Streamlit code
- no imports from the main project
- no UI dependencies
- no OpenAI or model calls required

## Final QC Check
- skill exists in the correct folder structure
- script runs independently
- no dependency on the main app
- SKILL.md is clear and specific
- script is required, not decorative
- output is deterministic
- README includes video placeholder
- agent usage section is clearly written
- 3 test prompts are included (normal, edge, caution)
- caution case demonstrates partial decline
- SKILL.md description is narrow and specific
- activation logic is clear
- script remains unchanged
- repository matches assignment requirements

## Video Demo

[PLACEHOLDER - Unlisted YouTube link to be inserted here after recording]

Example format:
https://www.youtube.com/watch?v=XXXXXXXXXXX

Note:
This will be replaced with the final unlisted YouTube demo before submission.

## Summary

This skill demonstrates a reusable, narrowly scoped capability where deterministic code performs the core validation task while the agent handles orchestration and user interaction.
