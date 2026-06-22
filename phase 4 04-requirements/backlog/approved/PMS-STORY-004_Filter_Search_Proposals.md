---
id: PMS-STORY-004
name: Filter and Search Proposals
status: DRAFT
version: 1.0
agent: user-story-standards
traces: [UC-004]
verdict: RED
---

# PMS-STORY-004_Filter_Search_Proposals

**Traces to:** UC-004

---

## Story

```
As a Manager
I want to filter and search proposals by status, project, and keyword
So that I can find relevant proposals quickly
```

---

## Acceptance Criteria (GWT Format)

### Scenario 1: Filter by status and project
```gherkin
Given proposals exist across multiple statuses and projects
When the user filters by Status = "Sent" and Project = "Project X"
Then the system shows only proposals matching both selected filters
```

### Scenario 2: Search by keyword
```gherkin
Given proposals exist with various subjects and clients
When the user searches for keyword "Subject Y"
Then the system displays only proposals whose subject, client, or project contain the keyword
```

### Scenario 3: Combined filter and search
```gherkin
Given proposals exist across multiple statuses and subjects
When the user applies filters and enters a search keyword
Then the system returns proposals that satisfy both the filter selection and the keyword search
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

- Export size is limited to a 25 MB boundary for large result sets
