---
name: app-integration
description: Add SmashSend to the user's application code - send transactional emails (password reset, receipts, invites, notifications) with the @smashsend/node SDK, sync signups to contacts, and keep email templates in react-email. Use when the user wants their app or backend to send emails through SmashSend, or to replace another email provider (Resend, SendGrid, Postmark, Mailgun, SES) with SmashSend.
---

# Integrate SmashSend into an app

1. **Install and configure.** `npm install @smashsend/node` (plus `@react-email/components @react-email/render` for templates). Read the key from `process.env.SMASHSEND_API_KEY` and add the name to `.env.example`. Never hard-code a key or write a real one to a file in the repo.
   ```ts
   import { SmashSend } from "@smashsend/node";
   export const smashsend = new SmashSend(process.env.SMASHSEND_API_KEY!);
   ```
2. **One react-email component per email** under `emails/`, rendered to HTML and text at send time:
   ```ts
   import { render } from "@react-email/render";
   const html = await render(<PasswordReset url={url} />);
   const text = await render(<PasswordReset url={url} />, { plainText: true });
   await smashsend.emails.send({
     from: "Acme <no-reply@mail.acme.com>", // must be a verified SmashSend sender
     to: user.email,
     subject: "Reset your password",
     html,
     text,
     groupBy: "password-reset", // groups analytics for this email type
   });
   ```
   If the team wants to edit copy without deploys, use a dashboard template with `smashsend.emails.sendWithTemplate({ to, template: "password-reset", variables })` instead.
3. **Contacts.** On signup, `smashsend.contacts.create({ email, firstName, lastName, customProperties })` (custom properties must exist in the dashboard first) so marketing and workflows can reach the user. Only create contacts for people who agreed to hear from you.
4. **Error handling.** Send from a background job or after the response where possible, log failures, and retry only transient errors (network failures, 429, 5xx), never validation errors.
5. **Replacing another provider.** Map the old call site by call site, keep the same `from` domain (it must be verified in SmashSend first), and keep the old provider wired until a test send succeeds.

To check the integration, an EDITOR key can call the MCP `send_transactional_email` tool with the same HTML and a test address. Use `list_sending_identities` to see which senders are verified.
