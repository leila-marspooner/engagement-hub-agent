# Word Document Generation Prompt

## Purpose

This prompt generates structured content for a Word discovery brief document.

The content is grounded in Dataverse context and is designed to populate a Word template through Power Automate.

## Input

The prompt receives a Dataverse-grounded payload containing engagement, submission, analysis, service offering and human-review context.

Example payload fields may include:

- Engagement Number
- Engagement Title
- Client / Company
- Service Offering
- Submission Summary
- Analysis Number
- Analysis Summary
- Risk Flag Count
- AI Confidence Score
- Requires Human Review
- Human Review Reason
- Recommended Review Action
- Discovery Brief
- Missing Information
- Delivery Preparation Actions
- Governance Note
- Correlation ID

## Prompt instructions

You are generating content for an internal delivery discovery brief document.

Use only the information provided in the payload. Do not invent facts or replace payload values with examples.

Return valid JSON only with the following fields:

{
  "AnalysisSummary": "",
  "DiscoveryBrief": "",
  "DeliveryPreparationActions": "",
  "RecommendedReviewAction": "",
  "GovernanceNote": ""
}

Rules:

- Use actual payload values where available.
- Do not use generic sample clients such as Contoso unless Contoso is in the payload.
- Mention the company, service offering, analysis number, risk count and confidence score if they are present.
- Do not say information is missing if the payload contains it.
- Do not provide legal advice.
- Do not approve pricing, contract terms, commercial terms or final go/no-go decisions.
- If human review is required, state that the relevant risks must be reviewed, documented and either resolved or formally accepted by the appropriate human owner.
- Keep the content professional and suitable for an internal delivery handoff.
- Return JSON only.

## Output

The output is parsed by Power Automate and mapped into Word template content controls.

## Governance boundary

The generated document is an internal delivery-preparation artefact. It supports human review and delivery planning but does not approve legal, commercial, pricing or final go/no-go decisions.
