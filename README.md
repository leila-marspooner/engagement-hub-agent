# Engagement Hub Agent

Engagement Hub is a multi-agent Microsoft Copilot Studio and Power Platform workflow that turns a client submission into a governed intake and delivery-preparation process.

It analyses submitted client documents, creates structured Dataverse records, surfaces risk flags and human-review requirements, prevents duplicate Engagement Requests, prepares a delivery discovery brief, generates a Word handoff document, posts Teams notifications for human review, and logs key actions for auditability.

This project was created as an entry for the Microsoft Agent Academy Hackathon — Operative track.

---

## Quick links

* Demo video: https://youtu.be/Tzn6pMMoEAw
* Architecture notes: ./architecture/
* Demo walkthrough: ./demo/
* Flow summaries: ./flows/
* Prompt examples: ./prompts/
* Screenshots and evidence: ./screenshots/


## Problem

Engagement managers and delivery leads at Microsoft partners or Power Platform consultancies often receive client documents, statements of work, requirements notes or service requests in a fragmented way.

Common problems include:

* Client documents arrive ad hoc.
* Risks and missing information are easy to miss.
* Duplicate engagement requests can be created.
* Delivery teams inherit inconsistent handoffs.
* Human-review requirements are not always surfaced early.
* Audit trails are often spread across emails, documents, chat messages and manual notes.

Engagement Hub addresses this by turning a submitted client document into one guided workflow from intake to delivery preparation.

---

## What the solution does

Engagement Hub supports the following process:

1. A user asks the Engagement Hub Agent to analyse a submitted client document.
2. A controlled Copilot Studio topic calls a Power Automate agent flow.
3. The flow retrieves the Dataverse Submission record and attached document.
4. Document text is extracted and analysed using an AI prompt.
5. The structured analysis result is saved to Dataverse.
6. The agent shows risk flags, confidence score, human-review status and a correlation ID.
7. The user can create or return a duplicate-safe Engagement Request.
8. The parent agent hands off to a Delivery Prep Child Agent.
9. The Delivery Prep Child Agent generates and saves a discovery brief.
10. The user can generate a Word discovery brief document.
11. The document is saved to SharePoint and linked back to the Engagement Request.
12. If human review is required, an autonomous Teams notification flow alerts the review channel.
13. Key automation events are written to Automation Logs.

---

## Architecture

The solution uses a multi-agent architecture:

### Engagement Hub Agent

The parent Copilot Studio agent. It orchestrates the user journey and manages the controlled workflow from submission analysis through to engagement creation and delivery preparation.

### Contract Analysis Agent

A connected specialist agent for contract, statement of work, requirements and commercial document analysis. It extracts factual details, risks, missing information, confidence score and human-review recommendations.

### Delivery Prep Child Agent

A specialist child agent for delivery preparation. It receives an Engagement Request reference from the parent agent and calls the approved Generate Discovery Brief flow.

### Power Automate flows

The main flows are:

* **EH AF - Analyse Contract Document v2**
  Retrieves the submission document, extracts text, runs an AI prompt, parses structured JSON, creates an Analysis Result, updates the Submission and writes Automation Logs.

* **EH AF - Create Engagement Request v2**
  Creates or returns a duplicate-safe Engagement Request using Submission, Analysis Result and Service Offering context.

* **EH AF - Generate Discovery Brief**
  Resolves an Engagement Request, retrieves related Dataverse context, generates a structured discovery brief and updates the Engagement Request.

* **EH AF - Generate Discovery Brief Document**
  Uses a Dataverse-grounded prompt to generate Word document content, populates a Word template, saves the document to SharePoint, creates a sharing link, updates Dataverse and writes an Automation Log.

* **EH - Notify Human Review Channel**
  A standalone Dataverse-triggered cloud flow that posts a Teams adaptive card when an Analysis Result requires human review. It uses Automation Log idempotency to avoid duplicate alerts.

### Dataverse

Dataverse is used as the system of record.

Core tables include:

* Client Contacts
* Submissions
* Service Offerings
* Qualification Criteria
* Analysis Results
* Engagement Requests
* Automation Logs

### Microsoft Teams

Teams is used for autonomous human-review notification when an Analysis Result is flagged as requiring review.

### SharePoint and Word

Generated discovery brief documents are saved to SharePoint and linked back to the Engagement Request record in Dataverse.

---

## Technology stack

* Microsoft Copilot Studio
* Microsoft Power Automate
* Microsoft Dataverse
* Model-driven Power Apps
* Microsoft Teams
* SharePoint
* Microsoft Word templates
* AI Builder / document text extraction
* AI prompts
* Adaptive Cards
* Power Fx
* Structured JSON
* Automation Logs and correlation IDs

---

## Agent Academy concepts demonstrated

This project demonstrates several Agent Academy concepts and patterns:

* Multi-agent orchestration
* Parent agent and specialist child agent pattern
* Connected specialist agent pattern
* Controlled topics for predictable workflow steps
* Agent tools backed by Power Automate flows
* Dataverse-grounded AI outputs
* Structured JSON prompt output
* Human-in-the-loop governance
* Autonomous event-driven notification
* Duplicate-safe record creation
* Safe failure handling
* Audit logging and traceability
* Adaptive Card user experience

---

## Governance and safety boundaries

Engagement Hub is designed to support human reviewers, not replace them.

The agent does **not**:

* Provide legal advice
* Approve contract terms
* Approve pricing
* Approve commercial decisions
* Make final go/no-go decisions
* Replace human review where risk is flagged

The agent does:

* Surface risks and missing information
* Store structured analysis evidence
* Flag when human review is required
* Provide confidence scores and governance notes
* Maintain correlation IDs and Automation Logs
* Help delivery teams prepare consistent handoff material

---

## Demo flow

The demo shows the following journey:

1. Analyse submission `SUB-0002`.
2. Store the Analysis Result in Dataverse.
3. Show risk flags, confidence score and human-review status.
4. Create or return a duplicate-safe Engagement Request.
5. Prepare delivery handoff through the Delivery Prep Child Agent.
6. Generate and save a Discovery Brief.
7. Generate a Word discovery brief document.
8. Save the document to SharePoint.
9. Link the document back to Dataverse.
10. Post a Teams notification when human review is required.
11. Show Automation Logs and safe failure handling.

Demo video: https://youtu.be/Tzn6pMMoEAw

---

## Repository contents

This repository is a documentation and evidence repository for a Microsoft Power Platform / Copilot Studio solution.

Current repository structure:

architecture/
demo/
flows/
prompts/
screenshots/

The repository contains architecture notes, implementation summaries, sanitised prompts, flow descriptions, screenshots and demo materials rather than a traditional code-first application.

---

## Setup summary

This project depends on Microsoft Power Platform services and cannot be run as a standalone local application.

To recreate a similar solution:

1. Create a Power Platform environment with Dataverse enabled.
2. Create the Dataverse tables:

   * Client Contacts
   * Submissions
   * Service Offerings
   * Qualification Criteria
   * Analysis Results
   * Engagement Requests
   * Automation Logs
3. Build the model-driven app for operational review.
4. Create the Copilot Studio parent agent and specialist agents.
5. Add controlled topics for:

   * Submission analysis
   * Engagement Request confirmation
   * Delivery handoff
   * Legal/commercial guardrails
6. Create the Power Automate flows listed above.
7. Connect the flows to the relevant agents as tools.
8. Configure SharePoint storage for generated Word documents.
9. Configure a Word template with content controls.
10. Configure Teams channel notification for human review.
11. Add sample data and test the full happy path.
12. Test duplicate detection and safe failure paths.

---

## Key implementation highlights

* Dataverse is used as the system of record.
* Friendly business references such as `SUB-0002` and `ENG-0020` are used in the user experience.
* Flows resolve friendly references to Dataverse row IDs behind the scenes.
* Engagement Request creation is duplicate-safe.
* Analysis Results include risk flags, confidence score and human-review status.
* Delivery preparation is handled by a specialist child agent.
* Generated Word documents are saved to SharePoint and linked to Dataverse.
* Human-review notification is autonomous and idempotent.
* Automation Logs capture success, failure, duplicate prevention and correlation IDs.
* Adaptive Cards provide clear success, duplicate and failure states.

---

## Lessons learned

Important lessons from the build:

* Agent outputs need clear naming when multiple tools are used in one topic.
* Parent-to-child agent handoff requires explicit input and output mapping.
* A message in chat is not the same as a mapped child-agent input.
* Power Automate action schemas can become stale and may need actions to be recreated.
* Dataverse lookups and row IDs require careful handling.
* Controlled topics are more reliable than free-text generative orchestration for demo-critical business processes.
* Long generated content is better stored in Dataverse or Word documents than displayed directly in chat cards.
* Human review should be built into the workflow, not added as an afterthought.
* Good enterprise agent design requires grounding, auditability, safe boundaries and deterministic writes.

---

## Security note

This repository does not include:

* API keys
* Secrets
* Connection credentials
* Tenant-specific configuration
* Real client data
* Confidential or proprietary information

All screenshots, prompts and documentation should be treated as sanitised demo material.

---

## Author

Created by Leila Marchant as a Microsoft Agent Academy Hackathon Operative track submission.

LinkedIn: https://www.linkedin.com/in/leilamarchant  
Demo video: https://youtu.be/Tzn6pMMoEAw
