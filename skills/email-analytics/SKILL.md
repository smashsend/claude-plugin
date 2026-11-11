---
name: email-analytics
description: Analyse SmashSend email performance - campaign and workflow open, click, bounce and unsubscribe rates, top links, comparisons over time, contact growth and Stripe revenue. Use when the user asks how their emails, campaigns, newsletters or automations are performing, which email or link works best or worst, or wants a performance report.
---

# SmashSend email analytics

Pick the narrowest tool for the question:

| Question | Tool |
|---|---|
| Workspace totals over a period | `get_email_analytics` |
| One campaign, workflow email or transactional template, including clicks per link | `get_email_performance` |
| Every email inside one workflow | `get_workflow_performance` (find the workflow with `list_workflows`) |
| Several campaigns side by side | `compare_campaigns` (find ids with `list_campaigns`) |
| List growth | `get_contact_growth` |
| Revenue (when Stripe is connected) | `get_revenue_metrics`, `get_customer_revenue` |

Rules for the answer:

- Report only numbers the tools returned. If a tool fails, say which number is missing; never estimate it.
- Give rates together with the counts behind them ("4.1% click rate, 82 of 2,000 delivered"). Treat anything under about 100 delivered as too small to compare.
- Opens are inflated by Apple Mail privacy protection, so prefer clicks for comparisons.
- End with two or three concrete next steps, such as a subject line to test or a workflow step to rewrite. If the key is an EDITOR, offer to draft the change; the email-campaigns and workflows skills cover how.
