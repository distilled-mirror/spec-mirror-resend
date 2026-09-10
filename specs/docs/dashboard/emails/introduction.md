> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Sending Emails

> An introduction to sending emails with Resend.

## Sending transactional emails

Resend provides all the tools you need to send [transactional emails](/docs/email-types#send-transactional-emails) from your application. These are useful for:

* order confirmations
* password reset emails
* account notifications

<Tip>
  To send bulk marketing emails, use the
  [Broadcasts](/docs/dashboard/broadcasts/introduction) feature.
</Tip>

Once you [verify a domain](/docs/add-a-domain) in your Resend account, you can send from any email address at that domain. You do not need to “create an email address,” “set up a sender identity,” or “add a from-address” before sending.

## Sending Features

With Resend's email sending features, you can:

* Send, retrieve, cancel, and manage individual and transactional email delivery through the [Sending API](/docs/api-reference/emails/send-email) and [SDKs](/docs/sdks), [CLI commands](/docs/cli#emails), [automations](/docs/dashboard/automations/introduction), and [AI building tools](/docs/ai-onboarding).
* [View and manage all sent emails](/docs/dashboard/emails/manage-emails) in the Emails Dashboard page.
* Send single or [batch transactional emails](/docs/dashboard/emails/batch-sending).
* [Schedule emails](/docs/dashboard/emails/schedule-email) to be sent at a future date.
* Send emails [with attachments](/docs/dashboard/emails/attachments) and [embedded images](/docs/dashboard/emails/embed-inline-images).
* Include [custom headers](/docs/dashboard/emails/custom-headers) in your emails.
* Use [idempotency keys](/docs/dashboard/emails/idempotency-keys) to ensure emails are sent only once.
* Receive tailored [deliverability insights](/docs/dashboard/emails/deliverability-insights) about each email with suggestions for improvement.
* [View API endpoint logs](/docs/dashboard/logs/introduction) and deliverability metrics for monitoring and troubleshooting.

## Quickstart

Get started with a [quick setup sending example](/docs/introduction#quickstart) for your language or an [AI builder guide](/docs/ai-onboarding#ai-builder-guides) to see how to incorporate Resend into your application.

## Choose your infrastructure

To send transactional emails from your application, you can use a variety of tools:

* [SDK](/docs/sdks): send with an SDK built for your language
* [Integrations](/docs/integrations): send from a framework or tool you already use
* [API](/docs/api-reference/emails/send-email): send with raw cURL calls
* [CLI](/docs/cli#emails): send emails from the terminal
* [MCP](/docs/mcp-server): send through your agent with MCP (see also [skills](/docs/react-email-skill))
* [SMTP](/docs/send-with-smtp): send without external dependencies

You can also send emails as part of [automated workflows](/docs/dashboard/automations/introduction) such as abandoned cart reminders, and create [email templates](/docs/dashboard/templates/introduction) for repeatable content.

See how to use additional sending features, including scheduling and attachments, in the [sending email guides](#related-guides).

## Manage your sent emails

After you've sent or scheduled your first email, you'll be able to view and manage your emails in the [Emails Dashboard page](https://resend.com/emails). From here, you can view email details, share a public version, and more. This allows all members of your team to view and manage your sent emails.

You can also manage your emails programmatically using the [Sending API](/docs/api-reference/emails/send-email), [CLI commands](/docs/cli#emails), or the [MCP server](/docs/mcp-server).

Learn more about [managing your sent emails](/docs/dashboard/emails/manage-emails) in the dedicated guide.

## Related Guides

See how to use Resend's sending features.

<CardGroup cols={2}>
  <Card title="View and manage sent emails" icon="envelope" href="/docs/dashboard/emails/manage-emails" />

  <Card title="Send test emails" icon="flask-gear" href="/docs/dashboard/emails/send-test-emails" />

  <Card title="Include attachments" icon="file-plus" href="/docs/dashboard/emails/attachments" />

  <Card title="Embed inline images" icon="image" href="/docs/dashboard/emails/embed-inline-images" />

  <Card title="Schedule emails" icon="clock" href="/docs/dashboard/emails/schedule-email" />

  <Card title="Batch sending" icon="envelopes" href="/docs/dashboard/emails/batch-sending" />

  <Card title="Customize headers" icon="rectangle-history-circle-user" href="/docs/dashboard/emails/custom-headers" />

  <Card title="Prevent duplicate emails" icon="key" href="/docs/dashboard/emails/idempotency-keys" />

  <Card title="Add an unsubscribe link" icon="person-from-portal" href="/docs/dashboard/emails/add-unsubscribe-to-transactional-emails" />

  <Card title="Add identifier tags" icon="tags" href="/docs/dashboard/emails/tags" />
</CardGroup>
