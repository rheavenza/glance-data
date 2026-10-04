# Daily Briefing datastore

Generated briefing content for Glance. Consumers should treat `briefing/latest.json` as the canonical current briefing. The repository is public and readable without a token.

## Publishing

Every briefing run:

1. Generate today's personalized briefing.
2. Convert it into the agreed JSON schema.
3. Write the result to:
   briefing/latest.json
4. Also write an identical archive copy to:
   briefing/history/YYYY-MM-DD.json
5. Commit both files to main.

Use Asia/Bangkok timezone for the archive date. Replace the same-day archive with the identical current payload on subsequent runs that day. Use UTF-8 JSON and an ISO 8601/RFC3339 generation timestamp with timezone offset. Keep all fields below; `schema_version` must remain the integer `1`, `title` must be `Daily Briefing`, and `stories` must be an array (an empty array is allowed).

## JSON contract

```json
{
  "schema_version": 1,
  "generated_at": "2026-10-04T19:00:00+07:00",
  "title": "Daily Briefing",
  "stories": [
    {
      "category": "System",
      "title": "Daily briefing integration is ready",
      "summary": "Glance is successfully reading briefing data from GitHub.",
      "why": "This verifies the ChatGPT → GitHub → Glance data path.",
      "url": ""
    }
  ]
}
```

Each story requires string fields `category`, `title`, `summary`, `why`, and `url`. Categories are free-form; the consumer renders all stories in order. `why` explains why the story matters. Preserve public article/source URLs; use an empty string when no article exists. Do not fabricate news or source links.

## Public-content rule

Commit only generated briefing content: news titles, summaries, why-it-matters text, categories, public article URLs, and generation timestamps, alongside this publishing documentation. Never commit credentials, API tokens, secrets, environment variables, private notes, NAS IP addresses, Tailscale addresses, Tailnet names, SSH information, or any other sensitive/private NAS data.
