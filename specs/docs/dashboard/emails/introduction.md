> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Sending Emails

> An introduction to sending emails with Resend.

## Sending transactional emails

Resend provides all the tools you need to send [transactional emails](https://resend.com/docs/email-types.md#send-transactional-emails) from your application. These are useful for:

* order confirmations
* password reset emails
* account notifications

> [!TIP]
>
> To send bulk marketing emails, use the
> [Broadcasts](https://resend.com/docs/dashboard/broadcasts/introduction.md) feature.

Once you [verify a domain](https://resend.com/docs/add-a-domain.md) in your Resend account, you can send from any email address at that domain. You do not need to “create an email address,” “set up a sender identity,” or “add a from-address” before sending.

## Sending Features

With Resend's email sending features, you can:

* Send, retrieve, cancel, and manage individual and transactional email delivery through the [Sending API](https://resend.com/docs/api-reference/emails/send-email.md) and [SDKs](https://resend.com/docs/sdks.md), [CLI commands](https://resend.com/docs/cli.md#emails), [automations](https://resend.com/docs/dashboard/automations/introduction.md), and [AI building tools](https://resend.com/docs/ai-onboarding.md).
* [View and manage all sent emails](https://resend.com/docs/dashboard/emails/manage-emails.md) in the Emails Dashboard page.
* Send single or [batch transactional emails](https://resend.com/docs/dashboard/emails/batch-sending.md).
* [Schedule emails](https://resend.com/docs/dashboard/emails/schedule-email.md) to be sent at a future date.
* Send emails [with attachments](https://resend.com/docs/dashboard/emails/attachments.md) and [embedded images](https://resend.com/docs/dashboard/emails/embed-inline-images.md).
* Include [custom headers](https://resend.com/docs/dashboard/emails/custom-headers.md) in your emails.
* Use [idempotency keys](https://resend.com/docs/dashboard/emails/idempotency-keys.md) to ensure emails are sent only once.
* Receive tailored [deliverability insights](https://resend.com/docs/dashboard/emails/deliverability-insights.md) about each email with suggestions for improvement.
* [View API endpoint logs](https://resend.com/docs/dashboard/logs/introduction.md) and deliverability metrics for monitoring and troubleshooting.

## Quickstart

Get started with a [quick setup sending example](https://resend.com/docs/introduction.md#quickstart) for your language or an [AI builder guide](https://resend.com/docs/ai-onboarding.md#ai-builder-guides) to see how to incorporate Resend into your application.

## Choose your infrastructure

To send transactional emails from your application, you can use a variety of tools:

* [SDK](https://resend.com/docs/sdks.md): send with an SDK built for your language
* [Integrations](https://resend.com/docs/integrations.md): send from a framework or tool you already use
* [API](https://resend.com/docs/api-reference/emails/send-email.md): send with raw cURL calls
* [CLI](https://resend.com/docs/cli.md#emails): send emails from the terminal
* [MCP](https://resend.com/docs/mcp-server.md): send through your agent with MCP (see also [skills](https://resend.com/docs/react-email-skill.md))
* [SMTP](https://resend.com/docs/send-with-smtp.md): send without external dependencies

You can also send emails as part of [automated workflows](https://resend.com/docs/dashboard/automations/introduction.md) such as abandoned cart reminders, and create [email templates](https://resend.com/docs/dashboard/templates/introduction.md) for repeatable content.

See how to use additional sending features, including scheduling and attachments, in the [sending email guides](#related-guides).

## Manage your sent emails

After you've sent or scheduled your first email, you'll be able to view and manage your emails in the [Emails Dashboard page](https://resend.com/emails). From here, you can view email details, share a public version, and more. This allows all members of your team to view and manage your sent emails.

You can also manage your emails programmatically using the [Sending API](https://resend.com/docs/api-reference/emails/send-email.md), [CLI commands](https://resend.com/docs/cli.md#emails), or the [MCP server](https://resend.com/docs/mcp-server.md).

Learn more about [managing your sent emails](https://resend.com/docs/dashboard/emails/manage-emails.md) in the dedicated guide.

## Related Guides

See how to use Resend's sending features.

> **[View and manage sent emails](https://resend.com/docs/dashboard/emails/manage-emails.md)**

> **[Send test emails](https://resend.com/docs/dashboard/emails/send-test-emails.md)**

> **[Include attachments](https://resend.com/docs/dashboard/emails/attachments.md)**

> **[Embed inline images](https://resend.com/docs/dashboard/emails/embed-inline-images.md)**

> **[Schedule emails](https://resend.com/docs/dashboard/emails/schedule-email.md)**

> **[Batch sending](https://resend.com/docs/dashboard/emails/batch-sending.md)**

> **[Customize headers](https://resend.com/docs/dashboard/emails/custom-headers.md)**

> **[Prevent duplicate emails](https://resend.com/docs/dashboard/emails/idempotency-keys.md)**

> **[Add an unsubscribe link](https://resend.com/docs/dashboard/emails/add-unsubscribe-to-transactional-emails.md)**

> **[Add identifier tags](https://resend.com/docs/dashboard/emails/tags.md)**
