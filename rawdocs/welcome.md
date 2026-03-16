# Welcome to your context vault

This is a sample document to test ingestion. Once you've set up your vault, ingest this file to verify everything works:

1. Use the `ingest_document` tool with the path to this file
2. Then use `search_context` to search for "welcome" — you should find this document
3. Delete this file and replace `rawdocs/` with your own documents

## What to capture

- **Thoughts and decisions** — use `capture_thought` during conversations
- **Structured facts** — use `save_fact` for data with temporal tracking (balances, statuses, dates)
- **Documents** — place markdown, PDF, or text files in `rawdocs/` and ingest them

Your context grows over time. The more you capture, the more useful your vault becomes across every LLM conversation.
