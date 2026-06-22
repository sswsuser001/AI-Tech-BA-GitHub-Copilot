---
id: UC-004
name: PMS Proposal Management — User Stories (Draft)
status: DRAFT
version: 2.0
agent: user-story-standards
traces: [UC-004]
verdict: RED
---

# UC-004_PMS_UserStories_DRAFT_v2.0

Traces to: UC-004

---

## US-004-01_Create Proposal (DRAFT)

**Traces to:** UC-004

---

## Story

```
As an Executive
I want to create a new proposal with required client, project, date, value, status, and attachments
So that I can capture and share proposals with clients
```

---

## Acceptance Criteria (In Progress)

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

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- Attachment type whitelist still requires SME confirmation
- Notification behavior on proposal create is unclear

---

## Linked Artifacts

- **Use Case:** UC-004
- **Mockup:** [Link pending]
- **Data:** [Link pending]

---

## US-004-02_Edit Proposal (DRAFT)

**Traces to:** UC-004

---

## Story

```
As an Executive or Manager
I want to edit an existing proposal using the off-canvas form
So that I can keep proposal details current
```

---

## Acceptance Criteria (In Progress)

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

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- Concurrency/locking behavior is not required per SME and should be confirmed if needed

---

## US-004-03_View Proposal List (DRAFT)

**Traces to:** UC-004

---

## Story

```
As a Manager
I want to view proposal records in a paged list
So that I can review proposals and identify items that need action
```

---

## Acceptance Criteria (In Progress)

### Scenario 1: Display proposal list with columns
```gherkin
Given the Manager is authenticated and has Proposal Management access
When they open the Proposal Management screen
Then the system displays proposals with columns for Proposal ID, Subject, Send To, Total Value, Project, Created Date, Status, and Actions, using pagination or lazy loading
```

### Scenario 2: Show empty state when no proposals exist
```gherkin
Given no proposals match the user's access
When the Proposal Management screen loads
Then the system displays an empty state message and no proposal rows
```

---

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- None beyond standard list rendering behavior

---

## US-004-04_Filter and Search Proposals (DRAFT)

**Traces to:** UC-004

---

## Story

```
As a Manager
I want to filter and search proposals by status, project, and keyword
So that I can find relevant proposals quickly
```

---

## Acceptance Criteria (In Progress)

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

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- Export performance for large result sets is unknown

---

## US-004-05_Export Proposals (DRAFT)

**Traces to:** UC-004

---

## Story

```
As a Manager
I want to export a filtered proposal set to PDF or Excel
So that I can share proposal data with stakeholders
```

---

## Acceptance Criteria (In Progress)

### Scenario 1: Export filtered proposals to PDF
```gherkin
Given a filtered proposal result set is displayed
When the user selects Export -> PDF
Then the system returns a downloadable PDF file containing the proposals shown in the current filtered result set
```

### Scenario 2: Export filtered proposals to Excel
```gherkin
Given a filtered proposal result set is displayed
When the user selects Export -> Excel
Then the system returns a downloadable Excel file containing the proposals shown in the current filtered result set
```

### Scenario 3: Require selection for bulk export
```gherkin
Given no proposals are selected for a bulk export operation
When the user clicks Export -> Excel from the selected items action
Then the system disables the export button or prompts the user to select at least one proposal
```

---

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- Export performance for large result sets is unknown

---

## US-004-06_Change Proposal Status (DRAFT)

**Traces to:** UC-004

---

## Story

```
As an Executive or Manager
I want to update a proposal's lifecycle status through the documented workflow
So that the proposal reflects the current negotiation state
```

---

## Acceptance Criteria (In Progress)

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

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- Exact transition confirmation rules require SME validation

---

## US-004-07_Attachments (DRAFT)

**Traces to:** UC-004

---

## Story

```
As an Executive
I want to attach supporting files to a proposal
So that related documents are stored with the proposal record
```

---

## Acceptance Criteria (In Progress)

### Scenario 1: Accept attachment under limit
```gherkin
Given the Add/Edit form is open
When the user uploads a file that is 50 MB or smaller
Then the system accepts the file, stores it locally, and shows it in the attachments list
```

### Scenario 2: Reject oversize attachment
```gherkin
Given the Add/Edit form is open
When the user uploads a file larger than 50 MB
Then the system rejects the upload and displays an error message explaining the 50 MB limit
```

### Scenario 3: Remove attachment before save
```gherkin
Given one or more files have been uploaded in the form
When the user removes a file and saves the proposal
Then the removed file is not persisted with the proposal
```

---

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- Allowed MIME types and server-side validation rules need confirmation from SME

---

## US-004-08_Bulk Delete Proposals (DRAFT)

**Traces to:** UC-004

---

## Story

```
As an Admin or Manager
I want to delete multiple proposals in a single action
So that I can remove outdated or irrelevant proposals efficiently
```

---

## Acceptance Criteria (In Progress)

### Scenario 1: Confirm bulk delete
```gherkin
Given multiple proposals are selected in the list
When the user chooses Delete and confirms the modal
Then the system removes the selected proposals and updates the UI to no longer show them
```

### Scenario 2: Cancel bulk delete
```gherkin
Given multiple proposals are selected in the list
When the user chooses Delete and cancels the confirmation modal
Then the system keeps all selected proposals and does not remove any records
```

### Scenario 3: Report partial delete failures
```gherkin
Given a bulk delete operation is executed and one or more items fail server-side
When the operation completes
Then the system displays which proposals failed to delete and which proposals were deleted successfully
```

---

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- Partial failure behavior during bulk operations is not fully defined and needs SME input

---

## US-004-09_Bulk Export Proposals (DRAFT)

**Traces to:** UC-004

---

## Story

```
As an Admin or Manager
I want to export selected proposals to Excel
So that I can review selected proposal data offline
```

---

## Acceptance Criteria (In Progress)

### Scenario 1: Export selected proposals
```gherkin
Given multiple proposals are selected in the list
When the user chooses Export -> Excel
Then the system returns a downloadable Excel file containing the selected proposals
```

### Scenario 2: Disable export with no selection
```gherkin
Given no proposals are selected in the list
When the user chooses Export -> Excel
Then the system disables the export option or prompts the user to select at least one proposal
```

---

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- Export performance for large result sets is unknown

---

## US-004-10_Convert Proposal Request (DRAFT)

**Traces to:** UC-004

---

## Story

```
As Finance or Executive
I want to request conversion of an Accepted proposal to an Invoice or Estimate
So that accepted proposals can be billed or recorded in downstream systems
```

---

## Acceptance Criteria (In Progress)

### Scenario 1: Record conversion request for Accepted proposal
```gherkin
Given a proposal is marked Accepted
When the user selects Convert to Invoice or Convert to Estimate
Then the system creates a conversion request linked to the proposal with conversion type, requestor, timestamp, and request status
```

### Scenario 2: Block conversion before acceptance
```gherkin
Given a proposal is in Draft, Sent, or Negotiation
When the user attempts to convert it
Then the Convert option is disabled or the system shows a message that conversion is allowed only after acceptance
```

### Scenario 3: Conversion request metadata is stored
```gherkin
Given a conversion request is created
When the request is persisted
Then the system stores the requested conversion type, requestor identity, date/time, and proposal link for audit
```

---

## Definition of Ready Checklist

- [ ] Story clearly written (no ambiguity)
- [ ] 3+ acceptance criteria scenarios
- [ ] Mockup exists and linked
- [ ] Data fields identified
- [ ] Dependencies listed
- [ ] Effort can be estimated

**Status:** [2/6 criteria met — needs work]

---

## Known Issues

- Technical conversion mapping to Invoice/Estimate fields is deferred and needs a follow-up story

---

## Next Steps (for the author)

- Review each story with SMEs (Engineering, Finance, Product) to confirm field mappings, allowed file types, notification behavior, and lifecycle transition rules.
- Attach mockups and data dictionary links to each story.
- Move stories to APPROVED once all Definition of Ready checklist items are satisfied.

---

## Review Summary

- This version splits the original UC-004 story into smaller, more estimable draft stories aligned to specific behaviors.
- Each story now includes GWT-style acceptance criteria and explicit dependency notes where needed.
- The file still holds a RED verdict because several stories require SME validation on lifecycle transitions, file type rules, export/bulk failure behavior, and conversion mapping.
- Next refinements should add explicit data field lists, mockup links, and any RBAC/notification requirements before moving stories toward APPROVED.
