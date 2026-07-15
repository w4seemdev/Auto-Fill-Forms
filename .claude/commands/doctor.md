---
description: Preflight self-check — verify the agent is fully wired before applying
---

Run these checks and report a clear PASS / FIX table. Do NOT open a browser.

1. **Resume**: `data/resume.pdf` exists and is under 2 MB. (FIX: add the file, single-column parses best.)
2. **profile.json**: valid JSON; `personal_information` has non-empty `first_name`, `last_name`, `email`, `phone`, `city`, `country`; no field still contains a template placeholder (`Your `, `Jane Doe`, `example.com`, `-here`, `Company Name`). (FIX: fill in real data.)
3. **answers.json**: valid JSON; has both `confirmed` and `rules` sections.
4. **.mcp.json**: present and registers the `playwright` server.
5. **credentials.json** (only if present): valid JSON; no `password` equal to a placeholder (`your-...-here`); flag any entry with `verified: true` the user should confirm still works.
6. **Manual checks the files can't verify** — list these for the user to confirm:
   - The `playwright` MCP server is approved in this Claude Code session (needed to drive the browser).
   - Gmail is signed in once in the automation browser (only needed for auto-reading verification codes — optional).

Output a short `check → PASS/FIX` table with the exact fix for anything failing. End with **"Ready to /apply"** only if every file check passes.
