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
- Each category stored in a database or structured file
- Fields per category:
    - People: name, context, follow up, last touched, tags
    - Projects: name, next action, last action, notes, status
    - Ideas: name, notes, tags, one liner
    - Admin: name, due date, status
    - Audit Log: original text, date, category, name, confidence score
- Suggest further fields as needed during design
- Secure local or Microsoft cloud storage (OneDrive/SharePoint)

### 4. Automation
- Route new entries from Microsoft Forms to LLM for categorisation and storage
- Daily digest at 8am Monday to Friday: top 3 actions, stuck items, small win (≤2 min read)
- Weekly digest: review activity, top 3 actions for next week, biggest unprogressed item, recurring theme
- Automated delivery via Teams message (direct message to user for maximum visibility)
- Use the simplest automation solution available (Power Automate preferred)
- Attachments stored in OneDrive/SharePoint with links in the entry

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
- Finalise open questions
- Design data models and database structure
- Select technology stack and integration points
- Develop MVP for data entry, categorisation, and digests
- Test automation and review workflows
