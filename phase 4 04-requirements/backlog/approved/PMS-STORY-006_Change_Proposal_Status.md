---
id: PMS-STORY-006
name: Change Proposal Status
status: DRAFT
version: 1.0
agent: user-story-standards
traces: [UC-004]
verdict: RED
---

# PMS-STORY-006_Change_Proposal_Status

**Traces to:** UC-004

---

## Story

```
As an Executive or Manager
I want to update a proposal's lifecycle status through the documented workflow
So that the proposal reflects the current negotiation state
```

---

## Acceptance Criteria (GWT Format)

### Scenario 1: Move proposal from Draft to Sent
```gherkin
Given a proposal is in Draft
When the user changes status to Sent
Then the system updates the proposal status, displays the Sent badge, and persists the change
```

### Scenario 2: Move proposal from Negotiation to Accepted or Declined
```gherkin
Given a proposal is in Negotiation
When the user changes status to Accepted or Declined
Then the system updates the proposal status, displays the new badge, and persists the change
```

### Scenario 3: Prevent invalid lifecycle transition
```gherkin
Given a proposal is in Draft
When the user attempts to change status directly to Accepted
Then the system prevents the invalid transition and shows a message explaining the allowed lifecycle path Draft -> Sent -> Negotiation -> Accepted/Declined
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

- Refer to the reference file in the folder for exact lifecycle transition rules
