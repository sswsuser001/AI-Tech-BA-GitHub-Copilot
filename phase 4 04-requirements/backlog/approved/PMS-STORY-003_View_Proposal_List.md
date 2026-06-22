---
id: PMS-STORY-003
name: View Proposal List
status: DRAFT
version: 1.0
agent: user-story-standards
traces: [UC-004]
verdict: RED
---

# PMS-STORY-003_View_Proposal_List

**Traces to:** UC-004

---

## Story

```
As a Manager
I want to view proposal records in a paged list
So that I can review proposals and identify items that need action
```

---

## Acceptance Criteria (GWT Format)

### Scenario 1: Display proposal list with columns
```gherkin
Given the Manager is authenticated and has Proposal Management access
When they open the Proposal Management screen
Then the system displays proposals with columns for Proposal ID, Subject, Send To, Total Value, Project, Created Date, Status, and Actions, using inherited pagination behavior
```

### Scenario 2: Show empty state when no proposals exist
```gherkin
Given no proposals match the user's access
When the Proposal Management screen loads
Then the system displays an empty state message and no proposal rows
```

---

## Additional Details

**Priority:** P1

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

- Pagination behavior is inherited from the existing proposal list
