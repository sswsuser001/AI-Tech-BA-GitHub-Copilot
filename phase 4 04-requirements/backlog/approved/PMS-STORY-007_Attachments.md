---
id: PMS-STORY-007
name: Attachments
status: DRAFT
version: 1.0
agent: user-story-standards
traces: [UC-004]
verdict: RED
---

# PMS-STORY-007_Attachments

**Traces to:** UC-004

---

## Story

```
As an Executive
I want to attach supporting files to a proposal
So that related documents are stored with the proposal record
```

---

## Acceptance Criteria (GWT Format)

### Scenario 1: Accept attachment under limit
```gherkin
Given the Add/Edit form is open
When the user uploads a file that is 50 MB or smaller and is of type PDF, DOC, DOCX, or XLSX
Then the system accepts the file, stores it locally, and shows it in the attachments list
```

### Scenario 2: Reject oversize attachment
```gherkin
Given the Add/Edit form is open
When the user uploads a file larger than 50 MB
Then the system rejects the upload and displays an error message explaining the 50 MB limit
```

### Scenario 3: Reject unsupported file type
```gherkin
Given the Add/Edit form is open
When the user uploads a file that is not PDF, DOC, DOCX, or XLSX
Then the system rejects the upload and displays an error message stating the accepted file types
```

### Scenario 4: Remove attachment before save
```gherkin
Given one or more files have been uploaded in the form
When the user removes a file and saves the proposal
Then the removed file is not persisted with the proposal
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

- Server-side validation accepts only PDF, DOC, DOCX, or XLSX
