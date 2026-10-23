> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Sending Emails

> An introduction to sending emails with Resend.

## Sending transactional emails

Resend provides all the tools you need to send [transactional emails](/docs/email-types.md#send-transactional-emails) from your application. These are useful for:

* order confirmations
* password reset emails
* account notifications

> [!TIP]
>
> To send bulk marketing emails, use the
> [Broadcasts](/docs/dashboard/broadcasts/introduction.md) feature.

Once you [verify a domain](/docs/add-a-domain.md) in your Resend account, you can send from any email address at that domain. You do not need to “create an email address,” “set up a sender identity,” or “add a from-address” before sending.

## Sending Features

With Resend's email sending features, you can:

* Send, retrieve, cancel, and manage individual and transactional email delivery through the [Sending API](/docs/api-reference/emails/send-email.md) and [SDKs](/docs/sdks.md), [CLI commands](/docs/cli.md#emails), [automations](/docs/dashboard/automations/introduction.md), and [AI building tools](/docs/ai-onboarding.md).
* [View and manage all sent emails](/docs/dashboard/emails/manage-emails.md) in the Emails Dashboard page.
* Send single or [batch transactional emails](/docs/dashboard/emails/batch-sending.md).
* [Schedule emails](/docs/dashboard/emails/schedule-email.md) to be sent at a future date.
* Send emails [with attachments](/docs/dashboard/emails/attachments.md) and [embedded images](/docs/dashboard/emails/embed-inline-images.md).
* Include [custom headers](/docs/dashboard/emails/custom-headers.md) in your emails.
* Use [idempotency keys](/docs/dashboard/emails/idempotency-keys.md) to ensure emails are sent only once.
* Receive tailored [deliverability insights](/docs/dashboard/emails/deliverability-insights.md) about each email with suggestions for improvement.
* [View API endpoint logs](/docs/dashboard/logs/introduction.md) and deliverability metrics for monitoring and troubleshooting.

## Quickstart

Get started with a [quick setup sending example](/docs/introduction.md#quickstart) for your language or an [AI builder guide](/docs/ai-onboarding.md#ai-builder-guides) to see how to incorporate Resend into your application.

## Choose your infrastructure

To send transactional emails from your application, you can use a variety of tools:

* [SDK](/docs/sdks.md): send with an SDK built for your language
* [Integrations](/docs/integrations.md): send from a framework or tool you already use
* [API](/docs/api-reference/emails/send-email.md): send with raw cURL calls
* [CLI](/docs/cli.md#emails): send emails from the terminal
* [MCP](/docs/mcp-server.md): send through your agent with MCP (see also [skills](/docs/react-email-skill.md))
* [SMTP](/docs/send-with-smtp.md): send without external dependencies

You can also send emails as part of [automated workflows](/docs/dashboard/automations/introduction.md) such as abandoned cart reminders, and create [email templates](/docs/dashboard/templates/introduction.md) for repeatable content.

See how to use additional sending features, including scheduling and attachments, in the [sending email guides](#related-guides).

## Manage your sent emails

After you've sent or scheduled your first email, you'll be able to view and manage your emails in the [Emails Dashboard page](https://resend.com/emails). From here, you can view email details, share a public version, and more. This allows all members of your team to view and manage your sent emails.

You can also manage your emails programmatically using the [Sending API](/docs/api-reference/emails/send-email.md), [CLI commands](/docs/cli.md#emails), or the [MCP server](/docs/mcp-server.md).

Learn more about [managing your sent emails](/docs/dashboard/emails/manage-emails.md) in the dedicated guide.

## Related Guides

See how to use Resend's sending features.

> **[View and manage sent emails](/docs/dashboard/emails/manage-emails.md)**

> **[Send test emails](/docs/dashboard/emails/send-test-emails.md)**

> **[Include attachments](/docs/dashboard/emails/attachments.md)**

> **[Embed inline images](/docs/dashboard/emails/embed-inline-images.md)**

> **[Schedule emails](/docs/dashboard/emails/schedule-email.md)**

> **[Batch sending](/docs/dashboard/emails/batch-sending.md)**

> **[Customize headers](/docs/dashboard/emails/custom-headers.md)**

> **[Prevent duplicate emails](/docs/dashboard/emails/idempotency-keys.md)**

> **[Add an unsubscribe link](/docs/dashboard/emails/add-unsubscribe-to-transactional-emails.md)**

> **[Add identifier tags](/docs/dashboard/emails/tags.md)**
