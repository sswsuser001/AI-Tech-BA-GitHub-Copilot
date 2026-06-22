## Proposal Management System - Project 

# Discovery - 

## Elicitation - Reverse Engineering

/elicitation-interviews-questionnaires - conduct reverse engineering in order to proceed with the next step to generate features and use cases. 
Read html by the name propisal-list.html and proposal.html prototypes from project_references.
Generate the Reverser Engineering Elicitation results as RE-001_PMS062126_blackbox_v1.0.md file into the reverse-engineering folder

Gaps : Clarification Question 

1. Which user roles exist and what are their permissions for: create, edit, delete, convert, export? (High)
Ans: Admin, Manager and Executive ( already identity management system is available) Executive is going to Create Proposal

2. What is the exact lifecycle for a proposal status? Which transitions require approvals? (High) 
Ans: Draft/Sent/Negotiation/Accepted/Declined, As of Now NO. (Deferred)

3. What happens technically when a proposal is converted to an invoice/estimate? Which fields map to the target artifact? (High) 
Ans: On-Hold ( May defer)

4. Are attachments stored in the same system or external storage (S3/Blob)? Are there virus-scan or retention rules? (Medium) 
Ans: Yes local disk. No Cloud (Aws S3/ Azure Blob)

5. Are exports expected to be server-generated or client-side? Any scheduled exports or templates required? (Medium) 
Ans: Server generated. No Scheduled

6. Should the system enforce locking for concurrent edits? (Low)
Ans : NO


## Use Cases

/use-case-driven-discovery  Read the attached Confirmed Elcitied Reverse Engineering results, Generate Use cases and Scenarios. 
Generate the Use Cases as UC-004_PMS_UuseCases_DRAFT.md   follwing the template UC-004_TEMPLATE_DRAFT.md  file into Phase 3-> draft folder


## Generate User Stories
/user-story-standards 
Read the attached Confirmed Use Cases from Phase 3 03 use cases draft folder (attched reference . md file), Generate User Stories as UC-004_PMS_UserStories_DRAFT.md  follwing the template US-004_TEMPLATE_DRAFT.md  file into Phase 4-> backlog-> draft folder  

## review user Sttories
/user-story-standards Review for INVEST and GWT 
create a seprate file wuth version 2.0 and cleary add a Review summary in the end of the file.


## connect JIRA and ask to create user stories

connect https://1techbajun26.atlassian.net/ and fetch the Proposal Management System  (PMS) Project 

Create User Stories in the folder approved with naming PMS-STORY-001 (sequence) 
as a seprate file for each user story. 