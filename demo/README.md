# Demo

Demo video: https://youtu.be/Tzn6pMMoEAw

This demo shows Engagement Hub, a multi-agent Copilot Studio and Power Platform workflow for governed client intake and delivery preparation.

## Demo journey

The demo follows one client submission through the full process:

1. The user asks the Engagement Hub Agent to analyse a submitted client document.
2. The parent agent runs a controlled topic and calls the contract analysis flow.
3. The document is analysed and the result is stored in Dataverse.
4. The agent returns risk flags, confidence score, human-review status and a correlation ID.
5. The user confirms whether to create an Engagement Request.
6. The Engagement Request flow checks for duplicates and either creates a new request or returns the existing one.
7. The user selects **Prepare delivery handoff**.
8. The parent agent hands off to the Delivery Prep Child Agent.
9. The Delivery Prep Child Agent generates and saves a Discovery Brief.
10. The user chooses to generate a Word discovery brief document.
11. The Word document is created from a Dataverse-grounded prompt, saved to SharePoint and linked back to Dataverse.
12. A separate autonomous flow posts a Teams notification when human review is required.
13. Automation Logs show success, failure, duplicate prevention and correlation ID traceability.

## Key demo moments

* Multi-agent orchestration through a parent agent, connected specialist agent and child agent.
* Controlled topic flow rather than relying only on free-text responses.
* Structured Analysis Result saved to Dataverse.
* Duplicate-safe Engagement Request creation.
* Delivery Prep Child Agent handoff.
* Discovery Brief saved back to the Engagement Request.
* Word document generated from Dataverse-grounded context.
* SharePoint document link returned to the user.
* Teams adaptive-card notification for human review.
* Automation Logs and safe failure handling.

## Governance demonstrated

The demo shows that the agent supports human reviewers but does not replace them.

The agent does not approve:

* legal terms
* pricing
* commercial decisions
* final go/no-go decisions
* contract sign-off

Instead, it surfaces risk flags, missing information, confidence score, governance notes and human-review requirements before delivery proceeds.

## Demo video link

https://youtu.be/Tzn6pMMoEAw
