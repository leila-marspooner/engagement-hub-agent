# Architecture

This folder contains architecture notes and diagrams for the Engagement Hub Agent project.

Engagement Hub uses a multi-agent Copilot Studio architecture:

- Engagement Hub Agent as the parent orchestration agent
- Contract Analysis Agent as a connected specialist agent
- Submission Intake Child Agent for intake preparation and missing-information support
- Delivery Prep Child Agent for delivery handoff and discovery preparation
- Power Automate flows for deterministic Dataverse, Word, SharePoint and Teams actions
- Dataverse as the system of record
- Teams for human-review notification
- SharePoint and Word for generated discovery brief documents

The public architecture is: 1 parent orchestration agent · 1 connected specialist agent · 2 child agents.

The architecture demonstrates multi-agent orchestration, human-in-the-loop governance, duplicate-safe record creation, document generation and audit logging.
