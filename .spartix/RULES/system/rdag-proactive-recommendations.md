# System Rule: RDAG Proactive Recommendations

**Rule ID**: SYS-009
**Priority**: 1 (highest — immutable)
**Scope**: system

## Description
RDAG must present relevant feature suggestions and recommendations as optional selectable items during the clarification phase. They are part of the clarification conversation, not a separate step. The user can select any they want as additional requirements, or ignore them entirely.

---

## Rule 1: Integrated with Clarification
Recommendations and feature suggestions must be presented as part of the clarification questions — not as a separate phase. When RDAG asks clarification questions, it should also include optional suggestions the user can select if they want.

## Rule 2: Optional and Selectable
Every recommendation must be clearly marked as optional. The user may:
- select specific suggestions to add to their requirements
- ignore all suggestions entirely
- modify a suggestion before accepting it
- skip the suggestions without any impact on approval

Suggestions must never be treated as required. They are pick-and-choose additions only.

## Rule 3: Presentation Format — Numbered Options
All clarification questions and suggestions must be presented as numbered options so the user can respond by typing numbers instead of writing full answers.

Format for clarification questions:
```
**Q1: [Question]**
  1. Option A
  2. Option B
  3. Option C
  4. Other (please specify)
```

Format for optional feature suggestions (presented alongside clarification):
```
**Optional additions you can select:**
  5. [Feature name] — one-line explanation
  6. [Feature name] — one-line explanation
  7. [Feature name] — one-line explanation
```

The user responds with numbers only, e.g.: `1, 3, 5, 7` or `1, 3` or `none`.

If the user needs to provide a custom answer (e.g. "Other"), they write it after the number. Otherwise, numbers are sufficient.

## Rule 4: Context-Aware
Suggestions must be relevant to:
- the specific project type and tech stack
- the user's stated goals
- the current project state
- the complexity level

Do not suggest enterprise features for a simple project. Keep suggestions proportional.

## Rule 5: No Pressure
- Do not re-present rejected suggestions
- Do not argue if the user says no
- Do not delay the workflow waiting for the user to review suggestions
- If the user answers clarification questions without mentioning suggestions, proceed normally

## Rule 6: Selected Items Become Requirements
Any suggestion the user selects becomes part of the approved requirements, treated the same as explicitly stated requirements.

## Rule 7: No Forced Adoption
Suggestions must never be:
- automatically included without user selection
- used to block approval
- treated as mandatory
- re-presented after rejection

## Override Policy
These rules cannot be overridden by any other rule at any level.
