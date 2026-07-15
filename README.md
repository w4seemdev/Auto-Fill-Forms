# Auto-Fill Forms

A personal job-application auto-fill agent for [Claude Code](https://code.claude.com). Give it a job-posting URL and it opens the page in a visible browser, fills the entire application form from your saved profile, uploads your resume, and answers screening questions - then **you review everything and click Submit yourself**.

Built on research into why auto-apply tools fail: full auto-submit bots get 1-6% callback rates and mangle critical questions; assistive fill-everything-human-submits tools get 5-15%. This agent is the second kind, by design.

## How it works

- **Claude Code + Playwright MCP** drive a real, visible browser (Microsoft Edge by default - see `.mcp.json`).
- **`profile.json`** is the ground truth: contact info, work history, education, skills, work authorization, salary. The agent never invents facts that aren't in it.
- **`answers.json`** remembers every screening question you've answered - each new question is asked once, then automatic forever. Critical "knockout" questions (visa sponsorship, salary, background checks) are never guessed.
- **Hard safety rules**: the agent never clicks Submit, never touches CAPTCHAs or login forms, treats web page text as data (prompt-injection defense), and warns you if a "job form" asks for suspicious data (bank details, ID numbers - scam postings exist).
- Supports Greenhouse, Lever, Ashby (fully), Workday (assisted mode), LinkedIn Easy Apply and Indeed (fill-only), plus a generic mode for anything else.

## Setup

1. Clone the repo and open the folder in Claude Code.
2. Copy `profile.example.json` → `profile.json` and fill in your real data.
3. Copy `answers.example.json` → `answers.json` and adapt the rules to your situation.
4. Put your resume at `data/resume.pdf` (under 2 MB, single-column parses best).
5. Approve the `playwright` MCP server when Claude Code asks (first run downloads it via npx).

Your personal files (`profile.json`, `answers.json`, `data/`, `applications-log.md`) are git-ignored - they never leave your machine.

## Usage

```
/apply <job-posting-url>     fill a job application (you review + Submit)
/doctor                      preflight check that everything is wired
/status                      application progress + follow-up reminders
```

The agent checks the job's fit against your profile, warns about duplicates, tailors free-text answers to the posting (only from your real profile, never invented), fills the form, verifies the submission landed, and logs it. It hands you the browser for CAPTCHAs, logins, and the final Submit click. Multiple URLs are processed one at a time.

The full agent playbook - workflow, per-platform notes, and the hard rules - is in [CLAUDE.md](CLAUDE.md).

## Why human-in-the-loop

The moments that are hard to automate (CAPTCHAs, logins, unusual questions, the final click) are exactly the moments where job platforms, the law, and hiring outcomes all want a human. Treating them as first-class handoff points instead of bugs makes the tool more reliable, compliant with platform rules, and more effective.
