> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Email Suppressions

> Managing your team Suppressions to protect your sending reputation.

When a mailbox provider hard-bounces a recipient, or someone marks your email as spam, continuing to send to that address harms your reputation.

Your suppressions list protects you by intentionally skipping sending to any addresses on your list.

## How addresses are suppressed

An address is added to Suppressions for one of three origins:

* `bounce`: the recipient's mail server [permanently rejected the email](/docs/dashboard/emails/email-bounces).
* `complaint`: the recipient marked your email as spam.
* `manual`: you add the recipient's address yourself.

Suppressions apply to your entire team. Any address added to the suppression list will be skipped across all your domains and subdomains when sending transactional or [Broadcast](/docs/dashboard/broadcasts/introduction) emails.

<Tip>
  Not all Inbox Service Providers return a `complained` event, most notably,
  Gmail/Google Workspace.
</Tip>

## Viewing Suppressions in Resend

You can see all Suppressions [in the Dashboard](https://resend.com/emails/suppressions) or list them [in the API](/docs/api-reference/suppressions/list-suppressions).

<img alt="Email Suppressions" src="https://mintcdn.com/resend/Nyu32IXsxRkmP92c/images/suppression-list-board.png?fit=max&auto=format&n=Nyu32IXsxRkmP92c&q=85&s=437d48fa3afbc7e4885ecaa139ce83bc" width="1842" height="1000" data-path="images/suppression-list-board.png" />

You can also programmatically retrieve [a single Suppression](/docs/api-reference/suppressions/get-suppression) or [your entire suppression list](/docs/api-reference/suppressions/list-suppressions), which returns key data about the Suppression.

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "suppression",
  "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
  "email": "steve.wozniak@example.com",
  "origin": "bounce",
  "source_id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
  "created_at": "2026-10-06 23:47:56.678+00"
}
```

`source_id` references the email id that triggered the suppression (is `null` for `manual` origin suppressions).

## Add emails to the Suppression List

In the Dashboard, go to the [Suppressions page](https://resend.com/emails/suppressions) and click **+ Add email address** to add an email address to the suppression list.

* **Add manually**: enter the email address you want to suppress.
* **Import CSV**: upload a file with a list of email addresses to suppress.

You can also [suppress individual emails](/docs/api-reference/suppressions/add-suppression) or [bulk suppress up to 100 at a time](/docs/api-reference/suppressions/add-batch-suppressions) using the API.

<Info>
  Remember that adding a Suppression will skip all sending to that recipient
  until it is removed from your team's suppression list.
</Info>

## Remove emails from the Suppression List

Before removing an email address from the suppression list, ensure the reason for suppression has been addressed, or it will be automatically re-suppressed.

You can remove an email address from the suppression list in the Dashboard from the [Suppressions page](https://resend.com/emails/suppressions).

1. Search or filter for a suppression.
2. Click the **more options button** <Icon icon="ellipsis" iconType="solid" /> and select **Remove email address**.

You can also [remove individual emails](/docs/api-reference/suppressions/remove-suppression) or [bulk remove up to 100 at a time](/docs/api-reference/suppressions/remove-batch-suppressions) using the API.

<Warning>
  Removing an address from the suppression list does not guarantee delivery. If
  it bounces or is marked as spam again, it will be suppressed again
  automatically and damage your sender reputation.
</Warning>

## Webhook suppression notifications

For maximum visibility, track suppressions using webhook notifications.

* [**suppression.added**](/docs/webhooks/suppressions/added): triggered when an address is added.
* [**suppression.removed**](/docs/webhooks/suppressions/removed): triggered when an address is removed.

You can, for example, use these webhook notifications to sync your suppressions with your own database or third-party service.

## Export your Suppressions

You can export your suppressions as a CSV file from the [Suppressions page](https://resend.com/emails/suppressions). Click the **Download CSV** button to export your suppressions.

<img alt="Email Suppressions" src="https://mintcdn.com/resend/Nyu32IXsxRkmP92c/images/suppression-list-export.png?fit=max&auto=format&n=Nyu32IXsxRkmP92c&q=85&s=ff09fe52117ce4847a43126f84f58cc8" width="1776" height="1153" data-path="images/suppression-list-export.png" />
