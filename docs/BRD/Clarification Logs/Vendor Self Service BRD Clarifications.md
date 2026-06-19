# Vendor Self Service BRD Analysis and Clarifications

## 1. Summary
This document analyzes the attached Business Requirements Document for the Vendor Self Service portal. It identifies user roles and permissions, core entities and relationships, workflows, business rules, edge cases, and ambiguities. Every unresolved requirement is flagged with `[CLARIFICATION NEEDED]`.

---

## 2. User Roles and Permissions

### 2.1 Vendor Roles

#### Vendor Read Only
- Can view vendor invoice status.
- Can view invoice history.
- Cannot upload invoices.
- Cannot edit invoices.
- [CLARIFICATION NEEDED] Can this role view correction requests or only final status and history?
- [CLARIFICATION NEEDED] Can this role view invoices that were rejected or corrected, or only approved/processed invoices?

#### Vendor Finance Contact
- Can upload invoices.
- Can track invoice status.
- Can view invoice history.
- Can receive correction requests.
- [CLARIFICATION NEEDED] Can this role edit invoice data after initial submission or only resubmit corrected invoices following an AP correction request?
- [CLARIFICATION NEEDED] Does this role have permission to view invoices for all vendor sites/accounts they are associated with, or only one vendor account?

### 2.2 AP Internal Role

#### AP Clerk
- Can review uploaded invoices.
- Can validate invoice data.
- Can approve invoices.
- Can reject invoices.
- Can request corrections from the vendor.
- Can view invoices across vendors.
- [CLARIFICATION NEEDED] Can AP clerks edit vendor-entered invoice metadata, or only change status and request corrections?
- [CLARIFICATION NEEDED] Are AP clerks limited by business unit, region, or vendor segment, or do they truly see all vendors?

### 2.3 Access Rules
- Vendors may view only their own invoices.
- AP clerks can view invoices across vendors.
- [CLARIFICATION NEEDED] Does an AP clerk also have access to all historical invoice audit data and correction history by default?
- [CLARIFICATION NEEDED] Is there any need for an audit-only or administrator role beyond the three listed roles?

---

## 3. Core Entities and Relationships

### 3.1 Core Entities

- `Vendor`
  - Represents the company or supplier account.
  - Related to vendor users and vendor invoices.

- `Vendor User`
  - Authenticated portal user associated with a vendor.
  - Has role `Vendor Read Only` or `Vendor Finance Contact`.

- `AP Clerk`
  - Internal user responsible for invoice review and validation.

- `Invoice`
  - Primary business object that contains invoice metadata, status, and attachments.
  - Required fields include invoice number, invoice date, PO number, amount, currency, vendor name, line-item details, and payment terms.

- `InvoiceDocument`
  - Uploaded file(s) attached to an invoice, such as PDF invoice files.

- `InvoiceStatus`
  - Status states for an invoice such as Submitted, Under Review, Approved, Rejected, Correction Requested, or Resubmitted.
  - [CLARIFICATION NEEDED] The exact status model and allowed transitions are not defined.

- `CorrectionRequest`
  - A request created by AP when invoice data is missing, incorrect, or requires vendor action.
  - Includes rejection reasons and next-step guidance.

- `PurchaseOrder`
  - Represents the PO referenced on the invoice.
  - Used for validation when applicable.
  - [CLARIFICATION NEEDED] The relationship between invoice and PO is unclear when PO input is optional.

- `AuditTrail`
  - Tracks invoice submission timestamps, status changes, approvals, rejections, correction requests, and user actions.
  - [CLARIFICATION NEEDED] Specific audit fields and retention durations are not defined.

### 3.2 Entity Relationships

- `Vendor` 1..* `Vendor User`
- `Vendor` 1..* `Invoice`
- `Invoice` 1..* `InvoiceDocument`
- `Invoice` 1 `PurchaseOrder` (optional)
- `Invoice` 1..* `CorrectionRequest`
- `Invoice` 1..* `AuditTrail` entries
- `AP Clerk` 1..* `Invoice` (reviews and actions)

---

## 4. User Workflows

### 4.1 Vendor Workflow

1. Vendor logs in to the portal.
   - [CLARIFICATION NEEDED] The BRD assumes existing authentication but does not define login flow, vendor registration, password reset, or identity provider.
2. Vendor selects the invoice upload function.
3. Vendor enters required invoice metadata.
   - Invoice number
   - Invoice date
   - Purchase order number (if applicable)
   - Amount and currency
   - Vendor name
   - Line-item details
   - Payment terms
   - [CLARIFICATION NEEDED] Required line-item fields and vendor name validation behavior are not specified.
4. Vendor uploads invoice document(s).
   - Supports standard invoice file types such as PDF.
   - [CLARIFICATION NEEDED] Exact supported file types, maximum file size, and number of documents per invoice are undefined.
5. Vendor receives confirmation of submission.
   - [CLARIFICATION NEEDED] The BRD does not specify what confirmation method is used (UI only, email, or in-portal notification).
6. Vendor tracks invoice status.
   - [CLARIFICATION NEEDED] Status definitions and lifecycle are not specified.
7. Vendor views invoice history.
   - [CLARIFICATION NEEDED] Retention period and whether history includes rejected/corrected invoices are not specified.
8. Vendor receives feedback or correction requests when required.
   - [CLARIFICATION NEEDED] The exact notification channel for correction requests is unspecified.

### 4.2 AP Clerk Workflow

1. AP clerk logs in to the portal.
   - [CLARIFICATION NEEDED] Authentication details and session handling for AP users are not defined.
2. AP clerk views newly submitted invoices.
3. AP clerk reviews invoice details and attached documents.
4. AP clerk validates required invoice data.
   - Required fields must be completed.
   - Duplicate invoice numbers should be flagged and prevented if detected.
   - PO number should match expected purchase order values if applicable.
   - Amount and currency should be validated for correct format.
   - [CLARIFICATION NEEDED] The degree of automated vs manual validation and who resolves validation failures is not described.
5. AP clerk approves or rejects invoices.
6. AP clerk submits correction requests if information is missing or incorrect.
   - [CLARIFICATION NEEDED] The difference between a rejection and a correction request is not clearly defined.
   - [CLARIFICATION NEEDED] It is unclear whether correction requests allow partial approval or hold the invoice in a pending state.

---

## 5. Business Rules and Validation Constraints

### 5.1 Validation Rules
- Required fields must be completed before submission.
- Duplicate invoice numbers should be flagged and prevented if detected.
  - [CLARIFICATION NEEDED] Does duplicate detection apply globally, per vendor, per PO, or per vendor-account/period?
- PO number should match expected purchase order values if applicable.
  - [CLARIFICATION NEEDED] What makes PO validation applicable, and what data source will provide expected values?
- Amount and currency should be validated for correct format.
  - [CLARIFICATION NEEDED] Are currency codes restricted to ISO 4217 only?
- Vendor name should likely align with the authenticated vendor account.
  - [CLARIFICATION NEEDED] Can vendor-entered vendor name differ from the authenticated vendor account name, or is it auto-derived?
- Line-item details must be captured.
  - [CLARIFICATION NEEDED] What level of line-item detail is required (description only, quantity/price/tax, service/goods classification)?

### 5.2 Correction and Rejection Handling
- Vendors can receive correction requests from AP.
- Vendors should be able to resubmit corrected invoices.
- Rejected invoices should have clear rejection reasons and next-step guidance.
- [CLARIFICATION NEEDED] Can a vendor resubmit a rejected invoice directly, or must they submit a fresh invoice record?
- [CLARIFICATION NEEDED] Are correction requests stored as separate entities, or simply as status notes on the invoice?

### 5.3 Access and Visibility Constraints
- Vendor users may only access and act on invoices for their vendor account.
- AP clerks have access to all vendor invoice submissions.
- [CLARIFICATION NEEDED] Is there any requirement to segregate invoices by business unit, region, or legal entity in addition to vendor account?

### 5.4 Performance and Operational Constraints
- Response time goals for AP review and vendor notification must be defined.
- Retention policies and audit retention periods must be defined.
- Maximum upload size and document count limits must be defined.
- [CLARIFICATION NEEDED] What are the target SLAs for vendor upload processing, AP review turnaround, and notification delivery?
- [CLARIFICATION NEEDED] Are there any regulatory or compliance retention requirements for invoice and audit data?

---

## 6. Edge Cases and Error Scenarios

### 6.1 Upload and Submission Errors
- Missing required fields during vendor submission.
- Invalid amount or currency format.
- Unsupported document type or file size exceeds limits.
- Batch upload policy conflict when the system only allows one invoice per upload.
- Network interruption during file upload.
- Duplicate invoice number detected after submission attempt.
- [CLARIFICATION NEEDED] Should the system support resumable uploads or retry behavior for failed uploads?

### 6.2 Authorization and Access Errors
- A vendor attempts to view another vendor's invoices.
- A Vendor Read Only user attempts to upload or edit an invoice.
- An AP clerk attempts to perform actions outside their permitted scope.
- Authentication failure or expired session.
- [CLARIFICATION NEEDED] How should the portal respond when a vendor login is valid but the user role is inactive or unassigned?

### 6.3 Review and Validation Errors
- AP clerk finds incomplete or inconsistent invoice metadata.
- PO number does not match expected values.
- Invoice total does not balance against line-item details.
- Correction request is issued but vendor does not respond within a defined timeframe.
- [CLARIFICATION NEEDED] Is there an escalation path or timeout-based auto-rejection for stale correction requests?

### 6.4 Correction and Rejection Scenarios
- Vendor resubmits corrected invoice with the same invoice number.
- Vendor uploads new supporting documents after a correction request.
- Invoice is rejected without a correction request.
- Invoice is approved but later found to have errors.
- [CLARIFICATION NEEDED] What is the desired behavior for previously approved invoices that require post-approval correction?

### 6.5 Integration Failure Scenarios
- AP system ingestion fails after approval.
- Authentication provider is unavailable.
- Notification service fails to send correction request alerts.
- PO master integration is unavailable when validating PO number.
- [CLARIFICATION NEEDED] Should the system queue integration events and retry, or fail open/closed?

---

## 7. Ambiguities and Missing Requirements

### 7.1 Authentication and Identity
- The BRD references an existing identity system but does not define vendor registration, login flow, password reset, MFA, or session management.
- [CLARIFICATION NEEDED] Which authentication provider or identity management system will be used?
- [CLARIFICATION NEEDED] How are vendor users provisioned and associated with vendor accounts?

### 7.2 Role Management
- It is unclear how a user is assigned `Vendor Read Only` vs `Vendor Finance Contact` roles.
- [CLARIFICATION NEEDED] Can a single user hold multiple vendor roles or switch roles?
- [CLARIFICATION NEEDED] Are AP clerks the only internal role needed, or should there be administrators, supervisors, or auditors?

### 7.3 Invoice Lifecycle and Status Model
- The BRD does not define invoice status values or valid transitions.
- [CLARIFICATION NEEDED] What are the required invoice states and who can change them?
- [CLARIFICATION NEEDED] Can invoices be reopened after rejection or correction, and under what conditions?

### 7.4 Correction Request Workflow
- The distinction between rejection and correction request is ambiguous.
- [CLARIFICATION NEEDED] Should correction requests automatically pause invoice review until responded to?
- [CLARIFICATION NEEDED] Should vendors be able to attach new documents only, adjust metadata, or both during resubmission?

### 7.5 PO Validation
- PO number validation is described as conditional and dependent on expected values.
- [CLARIFICATION NEEDED] What data source provides expected purchase order values, and when is PO validation required?
- [CLARIFICATION NEEDED] Is PO number required for all invoices or only when a purchase order exists?

### 7.6 Document Upload Requirements
- Exact supported file types are not listed.
- Maximum file size and batch upload behavior are undefined.
- [CLARIFICATION NEEDED] Is one invoice per upload mandatory, or is batch upload allowed with controls?
- [CLARIFICATION NEEDED] Are multiple document attachments permitted for a single invoice?

### 7.7 Reporting, Audit, and Retention
- The BRD mandates tracking and audit history but does not define report requirements or retention rules.
- [CLARIFICATION NEEDED] What audit fields are mandatory, and how long must they be retained?
- [CLARIFICATION NEEDED] Are specific reports required for AP review, vendor performance, or exception tracking?

### 7.8 Integration Details
- Integration with internal AP systems, authentication systems, notifications, and vendor/PO master data is described at a high level.
- [CLARIFICATION NEEDED] What are the exact integration endpoints, data contracts, and error-handling requirements?
- [CLARIFICATION NEEDED] Is integration required to be real-time, batch, or asynchronous?

### 7.9 Error Handling and Notifications
- Notification integration is referenced but not scoped.
- [CLARIFICATION NEEDED] Are vendor notifications required by email, in-portal messages, SMS, or all of the above?
- [CLARIFICATION NEEDED] What kinds of notification templates or content are required for rejection, correction, or status changes?

---

## 8. Suggested Next Clarifications
1. Define the exact invoice status model and allowed transitions.
2. Specify duplicate invoice number scope and PO validation rules.
3. Clarify upload requirements: file types, size limits, batch upload, and attachment count.
4. Confirm whether AP clerks can edit invoice metadata or only provide status/correction actions.
5. Define audit retention policies and required reporting outputs.
6. Confirm authentication provider and vendor user provisioning process.

---

## 9. Notes
- This analysis assumes the BRD is the primary source of requirements for the portal.
- All missing or ambiguous requirements were tagged with `[CLARIFICATION NEEDED]` to make them visible for stakeholder resolution.
