# SMASHSEND Email Marketing API for Claude

The official [SMASHSEND](https://smashsend.com) Email Marketing API plugin for Claude Code. It connects Claude to your SmashSend workspace through the SmashSend MCP server (`https://mcp.smashsend.com/mcp`) and adds skills that teach Claude how to do email work properly.

## What you can ask Claude

- "How did my last five campaigns perform, and which links got the most clicks?"
- "Which email in my onboarding workflow has the worst click rate? Draft a better version."
- "Build a launch announcement with react-email and get it ready to send to my customers."
- "Add password-reset and receipt emails to this app using SmashSend."

## Install

```
/plugin marketplace add smashsend/claude-plugin
/plugin install smashsend@smashsend
```

Claude Code asks for your API key during install and stores it in your system's secure credential store, not in a settings file. Create a key at [Settings → API keys](https://smashsend.com/latest/settings/api-keys):

- **Viewer** keys can read contacts, campaigns, workflows and analytics, and cannot change or send anything.
- **Editor** keys can also manage contacts, create campaign drafts, save workflow drafts and send transactional email.

To change the key later, run `/plugin configure smashsend@smashsend`. To check the connection, run `/smashsend:setup`.

## Skills

| Skill | Use it for |
|---|---|
| `/smashsend:setup` | Check the connection, workspace and key permissions |
| `email-campaigns` | Write a campaign with react-email, review it, test it and hand it off for sending |
| `email-analytics` | Campaign, workflow and link performance, contact growth, revenue |
| `workflows` | Analyse automations and save edits as drafts |
| `app-integration` | Add transactional email to your codebase with `@smashsend/node` |

Claude picks these up on its own when your request matches; you don't need to call them.

## Safety

Claude cannot send a campaign to your list. It prepares the draft and opens it in SmashSend, where a person reviews it and clicks Send. Workflow changes are saved as drafts that a person publishes. Every API key also has hourly and daily sending limits.

## License

MIT. [Privacy policy](https://smashsend.com/legal/privacy).
