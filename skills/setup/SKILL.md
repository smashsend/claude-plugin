---
name: setup
description: Check that the SmashSend connection works and explain what this API key can do. Use when the user runs /smashsend:setup, says SmashSend isn't working, gets 401/unauthorized errors from SmashSend tools, or asks which workspace or permissions they're connected with.
disable-model-invocation: false
---

# SmashSend setup check

1. Call the `whoami` tool from the `smashsend` MCP server.
   - **It works:** tell the user the workspace name, the key's role (VIEWER or EDITOR) and what that role allows:
     - VIEWER: read contacts, campaigns, workflows and all analytics. Nothing can be changed or sent.
     - EDITOR: everything a viewer can do, plus contacts, campaign drafts, workflow drafts and transactional email. Campaigns are still sent by a person from the SmashSend dashboard, and workflows are published there.
   - **401 / missing key:** the key is empty, wrong or revoked. Tell the user to create a key at https://smashsend.com/latest/settings/api-keys and then run `/plugin configure smashsend@smashsend` to paste it. Never ask them to paste the key into the chat.
   - **The `smashsend` tools aren't available at all:** ask them to run `/mcp` and check the `plugin:smashsend:smashsend` server, then `/reload-plugins`.
2. Suggest two or three things to try next, matched to the role, for example:
   - "How did my last 5 campaigns perform? Which links got the most clicks?"
   - "Which workflow email has the worst click rate?"
   - "Draft a campaign announcing our new pricing page, built with react-email."
