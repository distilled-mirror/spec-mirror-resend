> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Webhooks

> An introduction to using webhooks to notify your application about email events.

## Webhooks

Resend provides webhooks, which are real-time HTTPS requests that tell your application an event occurred, such as an email delivery notification or subscription status update. This allows you to receive real-time and actionable updates on the delivery, open, bounce, and click events of your emails.
You can create, update, observe, and retry webhooks from the dashboard or [via the API](/docs/api-reference/webhooks/create-webhook).

Webhooks deliver a JSON payload with metadata like the from, to, and status of your email event that can be used by your application. Use webhook feeds for common workflows such as:

* Automatically remove [bounced email addresses](/docs/webhooks/emails/bounced) from mailing lists.
* Create alerts in your messaging or incident tools based on [event types](/docs/webhooks/event-types).
* [Store all send events](/docs/webhooks/how-to-store-webhooks-data) in your own database for custom reporting/retention.
* [Receive inbound emails](/docs/dashboard/receiving/introduction) from your application.

## Webhook features

With Resend's webhook features, you can:

* [Replay any webhook event](/docs/webhooks/retries-and-replays). This is useful when your endpoint missed an event, or when you want to reprocess events with updated handler code.
* [Verify webhook requests](/docs/webhooks/verify-webhooks-requests) to ensure their authenticity.
* [Listen for webhook events locally during development](/docs/cli#webhooks).
* Self-host the [Resend Webhook Ingester](/docs/webhooks/ingester) to store all your webhook events with an open-source, ready-to-deploy solution that handles all the complexity for you.

## Quickstart

Get started by [creating a webhook](/docs/webhooks/create-webhook) to incorporate Resend into your application.

To receive real-time events in your app via webhooks, you need to:

**1. Create an endpoint in your application**

Create a route that can accept POST requests. This route will listen for and
receive events from Resend.

**2. Add a webhook in Resend**

Define a webhook with the URL of your endpoint, and the [email
events](/docs/webhooks/event-types) it handles.

See a step-by-step example of [creating a webhook](/docs/webhooks/create-webhook) through the Dashboard, including testing and deployment.

## Choose your infrastructure

After creating your application endpoint, you can define and manage your webhooks entirely from the Resend Dashboard. This allows all members of your team to have full access to your email event data and to perform any necessary maintenance.

To build workflows to manage and respond to email events from your application, you can use a variety of tools:

* [SDK](/docs/sdks): build and manage webhooks with an SDK built for your language
* [Integrations](/docs/integrations): build workflows with a framework or tool you already use
* [API](/docs/api-reference/webhooks/create-webhook): manage webhooks with raw cURL calls
* [CLI](/docs/cli#webhooks): register endpoints and listen for email event notifications from the terminal.
* [MCP](/docs/mcp-server): build workflows that respond to email events through your agent using natural language.

See how to use Resend's webhook features such as replaying webhooks and storing webhook data in the [webhooks guides](#related-guides).

## Related Guides

> **[Create webhook](/docs/webhooks/create-webhook)**

> **[Respond to emails](/docs/dashboard/receiving/create-receiving-webhook)**

> **[Retry replay webhooks](/docs/webhooks/retries-and-replays)**

> **[Email event types](/docs/webhooks/event-types)**

> **[Verify a webhook request](/docs/webhooks/verify-webhooks-requests)**

> **[Store webhook data](/docs/webhooks/how-to-store-webhooks-data)**

> **[Self-host the Resend Webhook Ingester](/docs/webhooks/ingester)**

> **[Webhook events reference](/docs/webhooks/emails/bounced)**

## Examples

> **[Next.js (TypeScript)](https://github.com/resend/resend-examples/tree/main/nextjs-resend-examples/typescript/src/app/inbound)**
>
> See the full source code.

> **[Next.js (JavaScript)](https://github.com/resend/resend-examples/tree/main/nextjs-resend-examples/javascript/src/app/inbound)**
>
> See the full source code.

> **[PHP](https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/inbound)**
>
> See the full source code.

> **[Laravel](https://github.com/resend/resend-examples/tree/main/laravel-resend-examples)**
>
> See the full source code.

> **[Python](https://github.com/resend/resend-examples/tree/main/python-resend-examples/examples)**
>
> See the full source code.

> **[Ruby](https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/examples)**
>
> See the full source code.
