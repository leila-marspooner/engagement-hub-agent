# Power Automate Flows

This folder summarises the main Power Automate flows used by Engagement Hub.

## EH AF - Analyse Contract Document v2

Retrieves a submitted document from Dataverse, extracts text, runs an AI prompt, parses structured JSON, creates an Analysis Result, updates the Submission and writes Automation Logs.

## EH AF - Create Engagement Request v2

Creates or returns a duplicate-safe Engagement Request using the Submission, Analysis Result and Service Offering context.

## EH AF - Generate Discovery Brief

Called by the Delivery Prep Child Agent. Resolves an Engagement Request, retrieves related Dataverse records, generates a structured discovery brief and updates the Engagement Request.

## EH AF - Generate Discovery Brief Document

Uses a Dataverse-grounded prompt to generate Word document content, populates a Word template, saves the document to SharePoint, creates a sharing link, updates Dataverse and writes an Automation Log.

## EH - Notify Human Review Channel

Standalone Dataverse-triggered flow that posts a Teams adaptive card when an Analysis Result requires human review. Uses Automation Log idempotency to avoid duplicate alerts.
