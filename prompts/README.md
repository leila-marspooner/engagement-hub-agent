# Prompts

This folder contains sanitised prompt summaries used in the Engagement Hub Agent project.

The prompts are designed to be grounded in Dataverse and flow-generated payloads. They should use only the information provided in the payload and should not invent client details, commercial approvals or legal conclusions.

## Prompt design principles

The prompts follow these rules:

* Use only the provided payload.
* Do not invent facts.
* Do not provide legal advice.
* Do not approve pricing, commercial terms or final go/no-go decisions.
* Surface risk, missing information and human-review requirements.
* Return structured outputs where downstream Power Automate steps need reliable parsing.
* Keep human reviewers in control where risk is flagged.

## Prompts included

* `contract-analysis-prompt.md`
  Analyses a submitted document and returns structured analysis data.

* `discovery-brief-prompt.md`
  Generates a structured delivery discovery brief for an Engagement Request.

* `word-document-generation-prompt.md`
  Generates structured content for a Word discovery brief document using Dataverse-grounded context.

## Security note

The prompts in this repository are sanitised examples. They do not include tenant-specific details, private client data, credentials, URLs, environment IDs or confidential information.

