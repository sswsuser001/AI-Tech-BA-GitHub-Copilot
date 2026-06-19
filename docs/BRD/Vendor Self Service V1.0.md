# Vendor Self Service V1.0

## 1. Document Overview

**Project name:** Vendor Self Service

**Version:** 1.0

**Author:** [To be determined]

**Date:** May 31, 2026

**Purpose:**
This Business Requirements Document defines the requirements for a vendor self-service portal that enables vendors to upload invoices directly to internal Accounts Payable teams for review, processing, and status tracking.

## 2. Business Objectives

- Reduce time and manual effort required for invoice submission.
- Improve invoice visibility and communication between vendors and Accounts Payable.
- Enforce consistent invoice validation and capture required invoice data at upload.
- Provide a secure, role-based system for vendor and AP users.

## 3. Scope

### In scope
- Vendor login and invoice upload capabilities.
- Vendor invoice status tracking and history viewing.
- Feedback / correction request notifications to vendors.
- AP clerk review of uploaded invoices.
- Role-based access controls for vendor and AP users.

### Out of scope
- Advanced supplier onboarding features.
- Full procure-to-pay purchase order creation.
- Payment execution and disbursement processing.

## 4. User Roles and Permissions

### Vendor roles
- **Vendor Read Only**
  - Can view vendor invoice status and history.
  - Cannot upload or edit invoices.

- **Vendor Finance Contact**
  - Can upload invoices.
  - Can track status, view invoice history, and receive correction requests.

### AP internal role
- **AP Clerk**
  - Can review uploaded invoices.
  - Can validate invoice data.
  - Can approve or reject invoices.
  - Can request corrections from the vendor.

### Access rules
- Vendors can view only their own invoices.
- AP clerks can view invoices across vendors.

## 5. Core Features and Workflows

### Vendor workflow
1. Vendor logs in to the portal.
2. Vendor selects the invoice upload function.
3. Vendor enters required invoice metadata.
4. Vendor uploads invoice document(s).
5. Vendor receives confirmation of submission.
6. Vendor tracks invoice status.
7. Vendor views invoice history.
8. Vendor receives feedback or correction requests when required.

### AP Clerk workflow
1. AP clerk logs in to the portal.
2. AP clerk views newly submitted invoices.
3. AP clerk reviews invoice details and attached documents.
4. AP clerk validates required invoice data.
5. AP clerk approves or rejects invoices.
6. AP clerk submits correction requests if information is missing or incorrect.

### Required invoice capture fields
- Invoice number
- Invoice date
- Purchase order number (PO number)
- Amount and currency
- Vendor name
- Line-item details
- Payment terms

### Document upload requirements
- Support for standard invoice file types such as PDF.
- Maximum file size and batch upload policies to be defined in implementation.
- One invoice per upload or a controlled batch upload process.

## 6. Business Rules and Constraints

### Validation rules
- Required fields must be completed before submission.
- Duplicate invoice numbers should be flagged and prevented if detected.
- PO number should match expected purchase order values if applicable.
- Amount and currency should be validated for correct format.

### Correction and rejection handling
- Vendors can receive correction requests from AP.
- Vendors should be able to resubmit corrected invoices.
- Rejected invoices should have clear rejection reasons and next-step guidance.

### Access and visibility constraints
- Vendor users may only access and act on invoices for their vendor account.
- AP clerks have access to all vendor invoice submissions.
- Any additional segregation by business unit or region should be documented later if required.

### Performance and operational constraints
- Define response time goals for AP review and vendor notification.
- Define retention policies and audit retention periods for invoice data and documents.
- Define maximum upload size and document count limits as part of the implementation plan.

## 7. Integration Requirements

- Integration with internal Accounts Payable systems for invoice ingestion and processing.
- Integration with authentication system for vendor and AP user login.
- Notification integration for email or in-portal messaging to vendors when corrections are requested.
- Optional integration with purchase order and vendor master systems for validation.

## 8. Reporting and Audit

- Track invoice submission timestamps.
- Track status changes, approvals, rejections, and correction requests.
- Maintain audit history for vendor uploads and AP actions.

## 9. Risks and Assumptions

### Risks
- Vendor submission errors due to missing or incorrect invoice data.
- Delays in AP review and correction turnaround time.
- Security or access issues if role permissions are not tightly enforced.

### Assumptions
- Vendor users are pre-registered and authenticated through an existing identity system.
- AP clerks are internal users with appropriate access to Accounts Payable data.
- Invoice upload volume is manageable within the portal’s planned capacity.

## 10. Next Steps

- Review and validate this BRD with stakeholders.
- Define detailed functional requirements for upload validation and AP review.
- Determine exact file type, size, and batch upload constraints.
- Confirm integration endpoints and authentication details.
