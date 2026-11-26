**English** · [Türkçe](README.tr.md)

# Job Opportunity & Gmail Assistant

Task instructions for an AI assistant that tidies your Gmail every morning, then scans LinkedIn and the web for job opportunities and sends you a single **daily summary email**.

> **Goal:** never miss a job opportunity while job hunting. The assistant does not apply anywhere and does not message anyone; it finds, classifies and reminds. You make the decisions.

> **This repository is an instruction template, not an application.** It contains no executable code, no GitHub Actions workflow and no Gmail/LinkedIn connection. You paste the instructions into an assistant environment that has Gmail and web-search access (e.g. ChatGPT scheduled tasks). Pushing changes here does not update a running task by itself. The instruction texts are written in Turkish.

## How it works

```
09:00  Gmail cleanup and invoice archiving
         │  ads → Trash · invoices → label + archive · important mail kept
         ▼
10:00  Job opportunities + daily summary
         │  LinkedIn / web scan · recruiter mail · tracking table
         ▼
       Daily summary email → sent only to your own Gmail address
```

Times are in `Europe/Istanbul`.

## What the daily summary contains

Subject: `Günlük özet | Gmail ve iş fırsatları | <date>`

1. **Gmail cleanup result:** counts of reviewed messages, messages moved to Trash, and invoices labelled.
2. **Reminders:** applications with no reply for a while, postings about to close, strong matches still undecided.
3. **Recruiter inbox:** messages from the last 2 days classified as *Urgent / Warm / Cold / Irrelevant*, with short suggested replies for urgent and warm ones.
4. **New opportunities:** up to 10, with role, work model, matching points, missing requirements and a direct link. Posts that ask for a CV are shown separately.
5. **Today's visibility suggestion:** a post outline or comment draft for sharing technical experience.
6. **Tracking table:** the status of every opportunity (New, Seen, Applied, Awaiting reply, Closed).

**Tracking memory:** there is no separate database. Each day the assistant continues from the tracking table in the previous summary in your Gmail Sent folder. "Applied" is only recorded when you tell the assistant in chat.

## Safety and guardrails

| The assistant does | The assistant does not |
|---|---|
| Moves ads to the recoverable Trash | Permanently delete, or empty the Trash |
| Marks reviewed LinkedIn notification emails as read | Unsubscribe, or change permanent filters or notification settings |
| Labels and archives genuine invoices | Archive or delete ambiguous documents |
| Only reads and classifies recruiter mail | Send replies or save drafts in Gmail |
| Suggests reply/post drafts inside the summary | Post, comment, like or send connection requests on LinkedIn |
| Sends the summary only to your own address | Apply to jobs or message/email third parties |

Also: when in doubt a message is kept, instructions found inside emails are never treated as authorization, closed postings are not listed as active, and no experience is invented that is not in your profile. The summary is not sent twice on the same day.

## Setup

1. Copy `config.example.json` to `config.local.json`. It is in `.gitignore`; do not upload it to GitHub.
2. Fill in your email address and a verified candidate profile: experience, target roles, technologies, location and commute preferences, work model (remote/hybrid/office).
3. Replace `YOUR_EMAIL` and `CANDIDATE_PROFILE` in `prompts/gmail-cleanup.txt` and `prompts/linkedin-opportunities.txt` with your own details, and schedule them as two separate tasks in your assistant environment (09:00 and 10:00).
4. Make sure the assistant has Gmail read/label access and web search.
5. Run the task once manually and check the first email. "Previous tracking table not found" in the first summary is normal.

> **Authorization:** the instructions assume the account owner has authorized these actions. If you are not the account owner, or you move to a new environment, get the owner's authorization for Gmail changes and summary sending separately.

## Repository layout

```
prompts/
  gmail-cleanup.txt            09:00 task: Gmail cleanup and invoice archiving
  linkedin-opportunities.txt   10:00 task: opportunity scan, recruiter inbox, daily summary
config.example.json            Local settings template (contains no real data)
LICENSE                        MIT
```

## Privacy

This repository is public. Names, email addresses, detailed candidate profiles, email contents, account keys and OAuth tokens are not included; keep them only in your private runtime environment.

## Limitations

- This repository does not guarantee the state of a live scheduler; verify that tasks run from your assistant environment.
- If the LinkedIn connector only offers people search, job and post scanning relies on web search and cannot cover your whole personal feed. The assistant states the coverage limit in its report.
- Reported results are an assistant's output; verify a posting on its original page before applying.

## License

MIT. See [`LICENSE`](LICENSE).
