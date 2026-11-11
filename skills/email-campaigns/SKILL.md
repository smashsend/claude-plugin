---
name: email-campaigns
description: Build a SmashSend email campaign (newsletter, announcement, promotion) end to end - write the email with react-email, use only real personalization variables, create the draft, review and fix it, send a test, and hand it to a person to send. Use when the user wants to write, draft, design, test or send a marketing email or newsletter to their list or a segment.
---

# Build a SmashSend campaign

Read the `smashsend_guide` tool once before the first email in a session; it is the source of truth and this skill only orders the steps.

**Pick the right channel first.** One person who just did something (password reset, receipt, invite) → transactional email, not a campaign. Every future contact who does X → a workflow. Many people at once → a campaign (this skill).

## Steps

1. **Variables.** Call `list_variables` and use only the `{{variables}}` it returns, with a fallback where the guide shows one. Don't invent `{{first_name}}`-style names.
2. **Sender.** Call `list_sending_identities` and use a verified address. If none exists, stop and tell the user to verify a domain in SmashSend.
3. **Write the email with react-email.** If the current project has Node, write a component under `emails/` and render it with `@react-email/render` (`render(<Email />)` for HTML, `render(<Email />, { plainText: true })` for text). Otherwise hand-write email-safe HTML: tables for layout, inline styles, absolute `https://` image URLs with `alt` text, no scripts, no web fonts as the only font, max width around 600px. Keep `{{variables}}` as literal text in the output.
4. **Preview, then create.** `preview_campaign` to check rendering, then `create_campaign` to save a DRAFT. SmashSend generates the plain-text version if you don't send one.
5. **Review and fix.** `review_campaign` returns errors and warnings. Fix every error with `update_campaign` (it returns a fresh review). Fix warnings when they're cheap: missing alt text, long subject, Gmail clipping.
6. **Test.** Offer `send_campaign_test` to the user's own address.
7. **Hand off. Never send it yourself.** Call `request_campaign_send`. It returns the campaign's SmashSend link: open it for the user (`open` on macOS, `xdg-open` on Linux, `start` on Windows) and tell them the subject, the audience and the recipient count. They review and click Send there.

If a tool says a per-key limit was hit, stop and tell the user when it resets. Don't retry or split the send to get around it.
