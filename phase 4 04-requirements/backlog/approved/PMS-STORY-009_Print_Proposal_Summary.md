---
id: PMS-STORY-009
name: Print Proposal Summary
status: DRAFT
version: 1.0
agent: user-story-standards
traces: [UC-004]
verdict: RED
---

# PMS-STORY-009_Print_Proposal_Summary

**Traces to:** UC-004

---

## Story

```
As a Manager
I want to print the proposal summary for a selected proposal
So that I can produce a physical summary for review meetings
```

---

## Acceptance Criteria (GWT Format)

### Scenario 1: Print selected proposal summary
```gherkin
Given a proposal is selected in the list
When the user chooses Print Summary
Then the system opens or downloads a printable summary view of the selected proposal
```

### Scenario 2: Disable print when no proposal selected
```gherkin
Given no proposal is selected
When the user views the proposal list
Then the Print Summary action is disabled or the user is prompted to select a proposal
```

### Scenario 3: Include proposal details and attachments
```gherkin
Given a proposal has supporting attachments
When the user prints the summary
Then the printable output includes proposal key fields and the attachment names, but not the file contents
```

---

## Additional Details

**Priority:** P2

**Effort Estimate:** [Points]

**Definition of Ready (DoR):**
- [ ] All 3+ scenarios written
- [ ] Mockup linked and annotated
- [ ] Data dictionary complete
- [ ] No blocking dependencies
- [ ] Acceptance criteria unambiguous

**Definition of Done (DoD):**
- [ ] Code review passed
- [ ] All scenarios tested (pass/fail captured)
- [ ] Regression tests written
- [ ] Documentation updated

---

## Linked Artifacts

- **Use Case:** UC-004
- **Mockup:** [Link pending]
- **Data:** [Link pending]

---

## Notes

- This story covers printable output only, not PDF generation via export
