# Power Automate Flows

This folder documents selected core Power Automate flows used by Engagement Hub. The wider solution uses 8+ flows; this repository focuses on the flows that best explain the public portfolio architecture and demo path.

This is a Power Platform / Copilot Studio project, so the repository contains sanitised implementation summaries rather than raw exported environment files.

## EH AF - Analyse Contract Document v2

**Purpose**  
Analyses a submitted client document and stores the result in Dataverse.

**Trigger**  
Called by Copilot Studio as an agent flow.

**Input**  
- Submission reference / Submission Row ID

**Main steps**  
1. Retrieve the Submission record from Dataverse.
2. Download the attached document.
3. Extract document text.
4. Build a contract analysis payload.
5. Run an AI prompt.
6. Parse the structured JSON response.
7. Create an Analysis Result record in Dataverse.
8. Update the Submission with the analysis summary and human-review flag.
9. Write Automation Log records.
10. Return a controlled response to the agent.

**Outputs**  
- Success
- User message
- Error message
- Analysis summary
- Requires human review
- Risk flag count
- Confidence score
- Analysis Result reference
- Correlation ID

**Governance pattern**  
The flow surfaces risk and human-review requirements but does not approve legal, commercial or go/no-go decisions.

---

## EH AF - Create Engagement Request v2

**Purpose**  
Creates or returns a duplicate-safe Engagement Request from an analysed Submission.

**Trigger**  
Called by Copilot Studio after the user confirms creation.

**Inputs**  
- Submission Row ID
- Analysis Result Row ID
- Service Offering Row ID
- Assigned Consultant
- Initial Fit Recommendation
- Requires Human Review

**Main steps**  
1. Retrieve the related Submission, Analysis Result, Service Offering and Client Contact.
2. Check whether an active Engagement Request already exists for the same business context.
3. If a duplicate exists, return the existing Engagement Request.
4. If no duplicate exists, create a new Engagement Request.
5. Write success or duplicate Automation Log records.
6. Return a controlled response to the agent.

**Outputs**  
- Success
- User message
- Engagement Request number
- Engagement Request row ID
- Duplicate detected
- Correlation ID

**Governance pattern**  
The flow prevents duplicate records and treats duplicate detection as a successful controlled outcome, not an error.

---

## EH AF - Generate Discovery Brief

**Purpose**  
Generates and saves a delivery discovery brief for an existing Engagement Request.

**Trigger**  
Called by the Delivery Prep Child Agent.

**Input**  
- Engagement Request reference, such as ENG-0020 or a Dataverse row ID

**Main steps**  
1. Resolve the Engagement Request reference.
2. Retrieve the Engagement Request from Dataverse.
3. Retrieve related Submission, Analysis Result, Service Offering and Client Contact records.
4. Generate a structured discovery brief.
5. Update the Engagement Request with Brief Generated, Brief Generated On and Discovery Brief content.
6. Write Automation Log records.
7. Return outputs to the Delivery Prep Child Agent and parent topic.

**Outputs**  
- Success
- User message
- Error message
- Engagement Request number
- Discovery Brief
- Brief generated timestamp
- Requires human review
- Correlation ID

**Governance pattern**  
The brief supports delivery preparation only. It does not approve legal, pricing, commercial or final go/no-go decisions.

---

## EH AF - Generate Discovery Brief Document

**Purpose**  
Generates a Word discovery brief document from Dataverse-grounded engagement context.

**Trigger**  
Called from the controlled parent topic after the user chooses to generate a Word document.

**Input**  
- Engagement Request reference

**Main steps**  
1. Resolve the Engagement Request.
2. Retrieve related Dataverse records.
3. Build a Dataverse-grounded document payload.
4. Run an AI prompt to produce structured JSON document content.
5. Parse the JSON output.
6. Populate a Microsoft Word template.
7. Save the generated document to SharePoint.
8. Create a sharing link.
9. Update the Engagement Request with the document link.
10. Write Automation Log records.
11. Return the document link to Copilot Studio.

**Outputs**  
- Success
- User message
- Error message
- Engagement Request number
- Document name
- Document link
- Document generated timestamp
- Correlation ID

**Governance pattern**  
The generated document is an internal delivery-preparation artefact. It includes governance notes and correlation ID traceability.

---

## EH - Notify Human Review Channel

**Purpose**  
Posts an autonomous Teams notification when an Analysis Result requires human review.

**Trigger**  
Dataverse automated cloud flow triggered when an Analysis Result is added or modified.

**Main steps**  
1. Check whether Requires Human Review is true.
2. Check Automation Logs to see whether a human-review notification has already been sent for the same Analysis Result.
3. If a notification already exists, skip posting another Teams card.
4. If no notification exists, post a Teams adaptive card to the review channel.
5. Write a success Automation Log record.
6. If the notification fails, write a failure Automation Log record.

**Outputs / evidence**  
- Teams adaptive card
- Automation Log success or failure row
- Correlation ID

**Governance pattern**  
This is notification only. It does not approve, reject, assign or update review decisions. It uses Automation Log idempotency to avoid duplicate alerts.
