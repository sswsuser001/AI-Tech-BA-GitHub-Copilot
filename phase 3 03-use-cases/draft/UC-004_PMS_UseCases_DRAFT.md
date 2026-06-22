---
id: UC-004
name: Manage Proposal Lifecycle
status: DRAFT
version: 0.1
agent: use-case-driven-discovery
traces: [BRD-v1.0]
updated: 2026-06-21
verdict: RED
---

# UC-004_Manage Proposal Lifecycle_DRAFT

## Goal

Enable a sales user to create, edit, review, and manage proposal records so they can track client proposals, update status, and export reports.

---

## Actor

- **Primary Actor:** Executive / Sales Representative
- **Secondary Actors:** Manager, Admin

---

## Preconditions

- The user is authenticated and has one of the confirmed roles: Executive, Manager, or Admin.
- The user has access to the Proposal Management module.
- Related data exists for Client/Company, Project, and optional Deal records.
- Proposal creation fields and attachment upload capabilities are available.

---

## Basic Flow

```
1. Actor opens the Proposal Management screen.
2. System displays the proposals list and grid views with filtering, search, and export controls.
3. Actor clicks Add New Proposal.
4. System opens the off-canvas proposal form.
5. Actor fills required fields: Subject, Client, Project, Date, Open Till, Currency, Value, Status.
6. Actor optionally selects Related To, Deals, Tags, Assigned To, and uploads attachments.
7. Actor saves the proposal.
8. System validates the input, persists the proposal, stores attachments locally, and returns the user to the proposal list.
9. Actor reviews the new proposal in the list or grid and optionally updates status or exports the report.
10. System shows the proposal with the selected status badge and makes it available for further actions.
```

---

## Alternative Flows

### A1: Use grid view instead of list view

Triggered when: the Actor prefers a card-based summary view.

```
At step 2:
  A1.1. Actor switches to the grid view.
  A1.2. System shows proposal cards with status badges, total value, dates, and action menus.
  A1.3. Actor uses card actions to view, edit, or convert a proposal.
  A1.4. System performs the requested action and returns the updated card state.
```

### A2: Change proposal status after creation

Triggered when: the Actor needs to update a proposal lifecycle state.

```
At step 10:
  A2.1. Actor opens the proposal action menu and selects Mark As Accepted/Declined/Draft.
  A2.2. System updates the proposal status and updates the status badge.
  A2.3. Actor confirms the proposal state change.
```

### A3: Convert proposal to estimate or invoice

Triggered when: the Actor chooses to convert a proposal.

```
At step 10:
  A3.1. Actor selects Convert to Estimate or Convert to Invoice.
  A3.2. System initiates the conversion flow (technical conversion flow currently deferred).
  A3.3. System indicates conversion has been requested or queued.
```

---

## Exception Flows

### E1: Missing required proposal fields

Triggered when: the Actor submits the form without required values.

```
At step 7, if required fields are missing:
  E1.1. System detects missing required fields.
  E1.2. System displays validation messages for Subject, Date, Client, Project, or Status.
  E1.3. Actor corrects the fields and retries saving.
```

### E2: Attachment exceeds size limit

Triggered when: the Actor uploads a file larger than 50 MB.

```
At step 6, if an uploaded file exceeds 50 MB:
  E2.1. System rejects the file upload.
  E2.2. System displays an error message explaining the 50 MB limit.
  E2.3. Actor removes the oversized file or uploads a valid file.
```

### E3: Delete proposal confirmation

Triggered when: the Actor chooses to delete a proposal.

```
At a later action step:
  E3.1. Actor selects Delete from the proposal action menu.
  E3.2. System displays a confirmation modal.
  E3.3. Actor confirms deletion.
  E3.4. System removes the proposal from the list and updates the UI.
```

---

## Postconditions

- A new proposal is persisted with the selected status, attachments, and related metadata.
- The proposal appears in the list and grid views.
- Status badges reflect the current lifecycle state.
- Export and conversion actions are available for the proposal as permitted.

---

## Linked Artifacts

- **Stories:** [TBD]
- **Mockup:** [TBD]
- **BRD:** BRD-v1.0

---

## Review Status

- [ ] Flows complete
- [ ] Decision points clear
- [ ] Error messages defined
- [ ] Stories ready
- [ ] Ready to move to APPROVED

---

## Notes

- Confirmed roles: Admin, Manager, Executive.
- Status lifecycle: Draft → Sent → Negotiation → Accepted/Declined.
- Attachments are stored locally on disk.
- Export is server-generated for PDF/Excel.
- Conversion technical flow is deferred and may require a follow-up use case once defined.
- Audit/history, exact attachment file types, notifications, and bulk failure behavior remain open questions.
