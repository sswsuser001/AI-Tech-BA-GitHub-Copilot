---
id: PMS-STORY-001
name: Create Proposal
status: DRAFT
version: 1.0
agent: user-story-standards
traces: [UC-004]
verdict: RED
---

# PMS-STORY-001_Create_Proposal

**Traces to:** UC-004

---

## Story

```
As an Executive
I want to create a new proposal with required client, project, date, value, status, and attachments
So that I can capture and share proposals with clients
```

---

## Acceptance Criteria (GWT Format)

### Scenario 1: Create proposal successfully
```gherkin
Given the Executive is authenticated (depends on the User Authentication story) and Client and Project reference data exist
When they complete the Add Proposal form with Subject, Client, Project, Date, Open Till, Currency, Value, Status and click Save
Then the system persists the proposal, stores uploaded attachments locally, and the new proposal appears in the proposal list with the selected status badge
```

### Scenario 2: Prevent create when required fields are missing
```gherkin
Given the Add Proposal form is open
When the user submits the form with Subject or Client or Project or Date or Status missing
Then the system displays validation errors for each missing required field and does not persist the proposal
```

### Scenario 3: Reject oversize attachments
```gherkin
Given the Add Proposal form is open
When the user uploads a file larger than 50 MB
Then the upload is rejected and the system displays an error message stating the 50 MB limit
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

- Notifications on proposal create are deferred
