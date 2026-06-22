# RE-001_PMS062126_blackbox_v1.0

Project: Proposals (CRMS UI)
Source: project_references/proposals-list.html, project_references/proposals.html
Scope: Black-box observation of proposal management UIs and behaviours (list, grid, create, edit, export, convert)
Date: 2026-06-21

---

## Observed Functionality

- Proposals listing (table view) with columns: Proposal ID, Subject, Send To, Total Value, Project, Created Date, Status, Actions.
- Proposals grid (card view) showing proposal summary, status badge, total value, date, open-till, sent-to company, actions menu per card.
- Filters: by status (Accepted/Declined/Draft/Deleted/Sent), subject, sent-to (company), project, date ranges, customizable columns.
- Search box (keyword) and sort options (Newest/Oldest).
- Export options: Export as PDF, Export as Excel.
- Create / Add Proposal: off-canvas form supporting fields: Subject, Date, Open Till, Client, Project, Related To (Deals/Leads/Pipeline), Deals, Currency, Status, Assigned to (multi-select), Attachments (drag & drop), Tags, Description (rich editor), Value.
- Edit Proposal: off-canvas edit form similar to create; pre-filled values for existing proposals.
- Proposal actions (per-row or per-card): Edit, Delete (confirmation modal), View Proposal, Mark As Accepted/Draft/Declined, Convert to estimate, Convert to Invoice, Print.
- Bulk actions: Select-all checkbox implies multi-select and bulk operations (delete/export).
- Pagination and data table controls present; grid has "Load More" button for lazy loading.
- Columns management: toggles to show/hide columns.
- File upload constraints visible: maximum size 50 MB; accepted file types (images/videos implied).
- Status badges displayed with color mapping (Accepted, Draft, Deleted, Declined, Sent).

## User Roles & Permissions (confirmed)

- Admin: full proposal management permissions including create, edit, delete, convert, export, bulk actions.
- Manager: standard proposal management permissions including edit, delete, convert, export; may also review and update status.
- Executive: primary creator role; can create proposals and view/edit as needed.

Note: identity management is already available in the system and roles are expected to be enforced by that layer.

## Core Entities & Data Flows

- Proposal
  - Attributes: id, subject, project, client (company), sent_to (company), total_value, currency, date, open_till, status, tags, description, attachments[], assigned_to[], related_deal, created_by, created_at
- Company / Client
- Project
- Deal
- Attachment/File
- User (assigned, proposal send-by)

Flows:
- Create proposal → persists Proposal with attachments → appears in list and grid views.
- Update status (accepted/draft/declined) → updates status badge and may trigger conversion flows (convert to invoice/estimate).
- Convert proposal → Generate estimate/invoice artifact and link/record conversion date and confirmation method.
- Export → generate PDF/XLS of selected or filtered proposals.

## Complete User Workflows (step-by-step)

1) Create Proposal (basic)
   - Precondition: user is authenticated and has permission to create proposals.
   - Trigger: Click "Add New Proposal" → open offcanvas form.
   - Steps: fill Subject, Client, Project, Date, Open Till, Value, Currency, Attachments; set Status; Assign users; Save/Create.
   - Output: new Proposal record appears in list/grid; count badge increments.
   - Postcondition: Proposal persisted; attachments uploaded; notifications possibly sent (inferred).

2) Edit Proposal
   - Trigger: Action menu → Edit (offcanvas pre-filled).
   - Steps: modify fields → Save Changes.
   - Output: Proposal updated in UI; history/audit not visible in UI (unknown).

3) Change Status / Actions
   - Trigger: Action menu → Mark As Accepted/Declined/Draft or direct control on card/list.
   - Steps: choose action → confirm if delete; status badge updates.
   - Output: status changed; may enable conversion actions.

4) Convert to Invoice / Estimate
   - Trigger: Action menu → Convert to Invoice/Estimate.
   - Steps: select option → (UI suggests conversion happens; any required confirmation flow not visible).
   - Output: generated Invoice/Estimate entity (inferred) or a link to conversion screen.

5) Export
   - Trigger: Export dropdown → choose PDF/Excel.
   - Steps: select filtered set or current view → export file returned/download starts.
   - Output: downloadable file (PDF/XLS).

## Business Rules & Validation Constraints (confirmed/inferred)

- Attachment maximum size: 50 MB (UI-provided). Enforced client-side or server-side (unknown).
- Required fields on create: Subject, Date, Client, Project, Status (UI marks with *). Validate present.
- Status lifecycle: Draft → Sent → Negotiation → Accepted/Declined. No approval step is currently required.
- Convert to Invoice/Estimate technical flow is on-hold / deferred; no field mapping is available yet.
- Deleting proposals requires confirmation (modal visible).
- Date fields use `flatpickr` format; date validation client-side present.

## Inputs & Outputs

- Inputs: form fields, file uploads, filter selections, search keywords, column toggles, user actions.
- Outputs: UI updates (list/grid), badges, downloadable files (PDF/Excel), modals, offcanvas forms, possible notifications.

## Edge Cases & Error Handling (observed / missing)

- Empty state: table body `<tbody>` is empty in static HTML; application likely populates via `assets/json/proposals-list.js` or API.
- File too large: UI shows 50 MB limit but error messaging behavior not visible.
- Invalid dates or open_till < date: validation not visible; needs SME confirmation.
- Concurrency: two users editing same proposal — no visible locking or warning in UI.
- Partial uploads / network failure during file upload — no visible retry UX in static pages.
- Bulk operations (delete/export) confirmation and undo behavior unclear.

## Non-Functional Observations

- Client-side dependencies: jQuery, Bootstrap, DataTables, Select2, Choices.js, Quill, Flatpickr.
- Performance hints: list view uses DataTables (server-side or client-side paging unknown); grid view uses cards with "Load More" (lazy-load expected).
- Accessibility: not evaluated; form labels present but ARIA attributes partial.

## Ambiguities & Gaps [CLARIFICATION NEEDED]

1. Audit/history: is there versioning/audit trail for edits? (SME)
2. Exact file types allowed for attachments and server-side validation rules for uploads. (SME)
3. Bulk actions: behavior for partial failures during export or delete. (SME)
4. Notifications: does changing status or creating proposals send emails/notifications? (SME)

Notes from SME confirmation:
- Roles are Admin, Manager, Executive.
- Executive is the primary proposal creator.
- Status lifecycle is Draft → Sent → Negotiation → Accepted/Declined, with no approvals currently required.
- Conversion technical flow is on-hold / deferred.
- Attachments are stored locally on disk, not in cloud storage.
- Exports are server-generated; no scheduled exports or templates are required.
- No locking is required for concurrent edits.

## System Scope Summary

The observed UI delivers a complete proposal management surface: create, edit, list/grid, filter, export, convert and lifecycle actions. It integrates with projects, clients, deals and supports attachments and user assignment. Missing from the UI: explicit audit/history, workflow approvals, and explicit permission enforcement display.

## Gap Analysis (what current UI does NOT show but likely needed for a product)

- Server-side APIs and data model details (endpoints, payloads).
- Detailed permission mapping and role-based access control.
- Formal conversion artifacts (invoice/estimate) definition and downstream integrations (billing module).
- Notification/Email templates and triggers.
- Error handling UX for large uploads and partial failures.
- Audit trail and change history for compliance.

## Prioritized SME Clarification Questions (remaining)

1. Audit/history: is there versioning/audit trail for edits? (SME)
2. Exact file types allowed for attachments and server-side validation rules for uploads. (SME)
3. Bulk actions: behavior for partial failures during export or delete. (SME)
4. Notifications: does changing status or creating proposals send emails/notifications? (SME)

Notes from SME confirmation:
- Roles are Admin, Manager, Executive.
- Executive is the primary proposal creator.
- Status lifecycle is Draft → Sent → Negotiation → Accepted/Declined, with no approvals currently required.
- Conversion technical flow is on-hold / deferred.
- Attachments are stored locally on disk, not in cloud storage.
- Exports are server-generated; no scheduled exports or templates are required.
- No locking is required for concurrent edits.

## Features & Candidate Use Cases (derived)

- Feature: Proposal CRUD (Create / Read / Update / Delete)
  - Use case: As a Sales Rep, I create a proposal with client, project, value and attachments so I can send it to the client.

- Feature: Proposal List & Grid Views with filters & search
  - Use case: As a Manager, I filter proposals by status and project to review outstanding proposals for the month.

- Feature: Status Management & Lifecycle
  - Use case: As a Sales Rep, I mark a proposal Accepted which triggers conversion options and updates dashboards.

- Feature: Convert Proposal → Estimate / Invoice
  - Use case: As Finance, I convert accepted proposals into invoices to bill the client.

- Feature: Export to PDF / Excel
  - Use case: As Sales Ops, I export filtered proposals to Excel for monthly reporting.

- Feature: Attachments with drag & drop and size limits
  - Use case: As a Sales Rep, I attach supporting files (proposal PDF, SOW) to the proposal for client review.

- Feature: Column Management & Customizable Views
  - Use case: As a user, I hide columns I don't need and save a focused view for my daily workflow.

## Action Items (MOM format)

| Next Step | Owner | Due Date | Notes |
|-----------|-------|----------|-------|
| Confirm role-permissions matrix | SME / Product Owner | +3 days | Provide role list and allowed actions |
| Define status lifecycle and transitions | Product Owner | +3 days | Specify allowed transitions and approval gates |
| Document conversion mapping to Invoice/Estimate | Finance/Engineering | +5 days | Fields mapping and required validations |
| Confirm attachment storage & validation | Engineering | +5 days | Storage location, allowed types, size, retention |
| Decide on audit/history requirements | Compliance/Product | +7 days | Required retention and UI for change history |

---

## Next recommended moves

- Run a short SME interview (Manager + Finance + Engineering) to answer the High priority clarifications above. Use the Divergence Diagnostic if stakeholders disagree on "conversion" semantics.
- After clarifications, draft API contract and data model for Proposal and Conversion artifacts.

---

Prepared by: Reverse Engineering — Elicitation
