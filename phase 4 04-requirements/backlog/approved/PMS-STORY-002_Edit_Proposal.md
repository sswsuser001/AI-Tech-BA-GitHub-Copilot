---
id: PMS-STORY-002
name: Edit Proposal
status: DRAFT
version: 1.0
agent: user-story-standards
traces: [UC-004]
verdict: RED
---

# PMS-STORY-002_Edit_Proposal

**Traces to:** UC-004

---

## Story

```
As an Executive or Manager
I want to edit an existing proposal using the off-canvas form
So that I can keep proposal details current
```

---

## Acceptance Criteria (GWT Format)

### Scenario 1: Open edit form pre-filled
```gherkin
Given a proposal exists and the user has permission to edit it
When the user selects Edit from the proposal actions
Then the system opens the off-canvas form pre-filled with the proposal's current values
```

### Scenario 2: Save edited proposal
```gherkin
Given the proposal edit form is open and valid changes are made
When the user clicks Save
Then the system validates the changes, persists the updated proposal, and the updated values appear in the list or grid
```

### Scenario 3: Prevent invalid edit save
```gherkin
Given the user clears a required field in the edit form
When they click Save
Then the system displays validation errors and does not persist the invalid update
```

---

## Additional Details

**Priority:** P0

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

- Concurrency/locking is not required in this phase
