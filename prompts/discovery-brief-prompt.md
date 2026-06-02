# Discovery Brief Prompt

## Purpose

This prompt generates a structured delivery discovery brief for an existing Engagement Request.

The brief is intended for internal delivery preparation and consultant handoff. It helps the delivery team understand the client context, selected service route, risks, missing information, discovery questions and recommended next steps.

## Input

The prompt receives a Dataverse-grounded payload prepared by Power Automate.

Example payload fields may include:

- Engagement Number
- Engagement Title
- Client Contact
- Company Name
- Submission Title
- Submission Summary
- Service Offering
- Service Description
- Typical Delivery Model
- Analysis Summary
- Risk Flag Count
- AI Confidence Score
- Requires Human Review
- Human Review Reason
- Recommended Review Action
- Missing Information
- Suggested Follow-up Questions

## Prompt instructions

You are preparing a delivery discovery brief for an internal consulting team.

Use only the information provided in the payload. Do not invent facts.

Create a structured delivery handoff brief with these sections:

1. Engagement overview
2. Client and submission context
3. Selected service route
4. Key risks and constraints
5. Human review status
6. Discovery questions for the client
7. Delivery preparation actions
8. Recommended next step
9. Governance note

Rules:

- Keep the brief practical and delivery-focused.
- If human review is required, state clearly that delivery should not proceed until review is complete.
- Do not provide legal advice.
- Do not approve pricing, contract terms, commercial terms or final go/no-go decisions.
- If information is missing, list it under Discovery questions.
- Keep the tone professional and concise.
- Return structured text only, not JSON.

## Output

The output is structured text that can be saved to the Engagement Request record in Dataverse.

## Governance boundary

The brief supports delivery preparation only. It does not approve delivery, legal terms, pricing, commercial terms or final go/no-go decisions.
