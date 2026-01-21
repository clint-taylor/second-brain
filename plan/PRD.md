# Product Requirements Document (PRD)

## App Name: Second Brain

### Purpose
A personal productivity app for a single user to capture thoughts, reminders, actions, and ideas, auto-categorized by an LLM, with daily and weekly automated summaries. The app leverages Microsoft 365 and Copilot, is fully automated except for user input, and avoids external paid services.

---

## Functional Requirements

### 1. Data Entry
- Single entry point for all user input (no manual categorisation)
- Accessible via PC and mobile (Microsoft Forms)
- Microsoft Form will be used for data capture, allowing quick and easy entry from any device

### 2. Categorisation
- Categories: People, Projects, Ideas, Admin
- Fifth category: Audit Log (tracks original text, submission date, categorisation, name, confidence score)
- LLM auto-categorises entries; confidence score (0-1)
- If confidence < 0.5, prompt user for clarification; user can adjust threshold
- Audit Log records all categorisation actions

### 3. Data Storage
- Each category is stored in a YAML file (the 'database'), with one or more YAML files per category as needed.
- Fields per category:
    - People: name, context, follow up, last touched, tags
    - Projects: name, next action, last action, notes, status
    - Ideas: name, notes, tags, one liner
    - Admin: name, due date, status
    - Audit Log: original text, date, category, name, confidence score
- Suggest further fields as needed during design.
- YAML files are stored in a secure location (OneDrive/SharePoint or local folder).

### 4. Automation
- Route new entries from Microsoft Forms to a Power Automate flow or backend process.
- The process writes the entry to the appropriate YAML file.
- When a YAML file is updated or a new file is created, trigger a call to Copilot (LLM endpoint) with the YAML content, a system prompt, and a JSON Schema for the expected response.
- Validate the returned JSON against the schema. If invalid, retry with a repair instruction.
- Store/upsert the structured record and mark the file as processed (using checksum to de-duplicate).
- Daily digest at 8am Monday to Friday: top 3 actions, stuck items, small win (≤2 min read)
- Weekly digest: review activity, top 3 actions for next week, biggest unprogressed item, recurring theme
- Automated delivery via Teams message (direct message to user for maximum visibility)
- Use the simplest automation solution available (Power Automate preferred). Power Automate can be used to detect new/changed YAML files and trigger the Copilot call.
- Attachments stored in OneDrive/SharePoint with links in the YAML entry

### 5. Review & Correction
- User can review categorisation and request changes (re-categorise, rename, etc.)
- Corrections applied automatically

### 6. Monitoring & Logging
- Track automation reliability and errors

### 7. UI for Browsing/Searching
- Initial UI will be a SharePoint page for browsing/searching entries
- Can be enhanced later as needed

---

## Non-Functional Requirements
- No external paid services
- Data privacy and security (compliance with corporate standards)
- High availability and reliability
- Scalable for future enhancements

---

## Open Questions
- Preferred input method: Teams bot, Outlook add-in, web app, or mobile app?
    - Teams message - private channel?
- Preferred summary delivery: Teams, email, OneNote, or other?
    Teams
- Local-only storage or Microsoft cloud?
    Understand the implications of the 2 options. I could see Microsoft Lists being the storage solution but does that make automation difficult?
- Compliance/privacy requirements?
    Needs to remain private to me so no data should be visible to other users or the internet
- Support for attachments (files, images)?
    Yes this would be useful
- UI for browsing/searching entries?
    Yes

---

## Next Steps
-
## Copilot Integration Trigger

## Copilot Response Handling

After sending the YAML file to Copilot, the system must:

1. Receive the JSON response from Copilot.
2. Validate the response against the provided JSON Schema.
3. If the response is invalid, retry the request with a "repair" instruction to Copilot, or log the error for manual review if repeated failures occur.
4. If valid, upsert the structured data into the system of record (update the YAML file or another database as needed).
5. Mark the file as processed (using checksum or metadata) to prevent duplicate processing.
6. Log all actions for audit and troubleshooting.

This flow ensures robust, automated processing of YAML data with Copilot, including error handling and data integrity.

When a YAML file is created or updated (e.g., by a new entry from Microsoft Forms or a user correction), the system must trigger a process to send the YAML content to Copilot for processing. This can be achieved by:

- Using Power Automate to monitor the storage location (OneDrive/SharePoint/local folder) for new or changed YAML files, then automatically call the Copilot (LLM) endpoint with the file content, a system prompt, and a JSON Schema for the expected response.
- Alternatively, a backend service can watch for file changes and perform the same call to Copilot.

The trigger should include file metadata (path, timestamp, checksum) to support deduplication and audit logging.

This ensures that every new or modified YAML file is processed by Copilot in a timely and automated fashion, with no manual upload required.
- Finalise open questions
- Design YAML data models and file structure
- Select technology stack and integration points (including Power Automate triggers for YAML file changes and Copilot API calls)
- Develop MVP for data entry, categorisation, and digests
- Test automation and review workflows
