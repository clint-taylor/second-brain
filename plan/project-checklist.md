# Second Brain App: Project Checklist

- [ ] One single data entry point; no user-driven categorisation at entry
- [ ] Categories: People, Projects, Ideas, Admin, Audit Log
- [ ] Audit Log: track original text, submission date, categorisation, name, and LLM confidence score
- [ ] Store categories in a database or structured file; each category has specific fields:
	- People: name, context, follow up, last touched, tags
	- Projects: name, next action, last action, notes, status
	- Ideas: name, notes, tags, one liner
	- Admin: name, due date, status
	- Audit Log: original text, date, category, name, confidence score
- [ ] Suggest further fields for each category as needed
- [ ] Route new entries to LLM for categorisation; add to relevant database and audit log
- [ ] Data entry point accessible via PC and phone (Teams integration preferred)
- [ ] Categorisation confidence: score 0-1; if <0.5, request more info; allow user to adjust threshold
- [ ] Daily digest at 8am: top 3 actions, stuck items, small win; concise (≤2 min read)
- [ ] Weekly digest: review activity, top 3 actions for next week, biggest unprogressed item, recurring theme
- [ ] Review/fix option: user can re-categorise or rename items; corrections applied automatically
- [ ] Implement secure local or Microsoft cloud storage
- [ ] Set up monitoring and logging for automation reliability

## Further Considerations
- [ ] Preferred input method: Teams bot, Outlook add-in, web app, or mobile app?
- [ ] Where do you want to read summaries: Teams, email, OneNote, or elsewhere?
- [ ] Is local-only storage acceptable, or do you prefer Microsoft cloud (OneDrive/SharePoint)?
- [ ] Any specific compliance or privacy requirements?
- [ ] Should the app support attachments (files, images) with entries?
- [ ] Would you like a UI for browsing/searching past entries, or just summaries?
