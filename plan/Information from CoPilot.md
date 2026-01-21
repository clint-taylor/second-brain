Information from CoPilot

Here’s what I can do with an uploaded .yaml or .yml file:
✅ I can:

Read and parse the YAML structure
Extract data, analyse it, or convert it (e.g., to JSON, CSV, Excel, Markdown)
Modify the contents and produce an updated YAML file
Generate visualisations or summaries based on its data
Validate the YAML format and highlight issues

All of that is done using the Python execution environment once you provide the file.
❌ I cannot:

Access YAML files stored elsewhere unless you upload them
“Ingest” YAML by description alone if you want processing — I need the actual file


Below is a practical integration blueprint that works well in NHS/M365 environments and doesn’t rely on me “running in the background.” In short: your app should call an LLM endpoint at the moment you detect/receive a file, enforce a JSON Schema for the return format, and validate + store the result. You can do that either from your own backend (recommended for automation) or via a low‑code M365 flow.

The short answer
Best pattern:
Have your app (or a Power Automate flow) send the YAML content to an LLM endpoint that’s configured to return strictly‑typed JSON (using a JSON Schema). Your app then validates the response, retries/repairs if needed, and upserts the structured data to your system of record (database/API). This avoids manual steps and scales for multiple files across the day.

Option A — App → LLM API with strict JSON output (recommended)
Why: End‑to‑end automation, full control, deterministic(ish) responses, straightforward to scale.
High‑level flow

Detect new file (e.g., in your storage bucket, SharePoint library, or inbox).
Read YAML as text; include metadata (file path, timestamp, checksum).
Call the LLM with:

A system prompt that explains the task and rules.
The YAML content (or a compacted version).
A JSON Schema that defines the exact structured response your app expects.


Validate the returned JSON against the same schema.
If invalid, retry with a “repair” instruction (see below).
Store/upsert the structured record and mark the file as processed (using checksum to de‑dupe).