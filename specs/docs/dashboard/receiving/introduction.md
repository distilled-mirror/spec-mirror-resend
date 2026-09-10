> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Receiving Emails

> An introduction to receiving emails with Resend.

## Receiving emails through Resend

Resend provides all the tools you need to receive emails (commonly called inbound) at [a verified domain](/docs/dashboard/domains/introduction), or at your account's Resend-managed `<id>.resend.app` subdomain.

This is useful for:

* Receiving support emails from users.
* Processing forwarded attachments.
* Replying to emails from customers.

## Receiving features

With Resend's email receiving features, you can:

* View all received emails in the [**Emails** Dashboard page](https://resend.com/emails).
* Receive incoming emails and [get notified with a webhook](/docs/dashboard/receiving/create-receiving-webhook) event.
* [Poll for new inbound emails in the terminal](/docs/cli#receiving) and display them as they arrive.
* [Retrieve full email content](/docs/dashboard/receiving/get-email-content) (HTML, text, headers) for use in your application.
* [Process attachments](/docs/dashboard/receiving/attachments) using attachment metadata and temporary download URLs.
* [Forward emails](/docs/dashboard/receiving/forward-emails) to another email address.
* [Reply to emails](/docs/dashboard/receiving/reply-to-emails) in the same thread
* [View API endpoint logs](/docs/dashboard/logs/introduction) and deliverability metrics for monitoring and troubleshooting.

## Quickstart

To start receiving emails using a domain managed by Resend, get your unique `<id>.resend.app` domain:

<Steps>
  <Step title="Go to the Emails page in your Resend dashboard." />

  <Step title="Select the Receiving tab." />

  <Step title="Get your custom Resend domain.">
    Click the three dots button and select Receiving address to see your custom Resend subdomain.

    <img alt="Get your Resend domain" src="https://mintcdn.com/resend/stmz8SfTchQy1hpq/images/inbound-resend-domain.jpg?fit=max&auto=format&n=stmz8SfTchQy1hpq&q=85&s=c26fcec3f9dc5def25041d44cb8c501a" width="1159" height="297" data-path="images/inbound-resend-domain.jpg" />
  </Step>

  <Step title="Send yourself a test email.">
    Send an email to any username at your subdomain (e.g., `test@<id>.resend.app`). You will receive emails sent to any address at your Resend domain.
  </Step>

  <Step title="View your received email in the Receiving tab of the Emails Dashboard page." />
</Steps>

You can also [configure a verified domain for receiving emails](/docs/dashboard/receiving/custom-domains) at your custom domain. Once you add the MX record to your custom domain, you will receive emails through Resend for any address at that domain.

## Configure Webhook

Once you can receive mail, you can [create a received mail webhook](/docs/dashboard/receiving/create-receiving-webhook) to receive real-time notifications about incoming email.

Resend processes all incoming emails to your receiving domain, parses the contents and attachments, and then sends a `POST` request to an endpoint that you choose to handle the received email.

<img alt="Receiving email process" src="https://mintcdn.com/resend/bxWCBKtofKnXvbvf/images/receiving-emails.jpeg?fit=max&auto=format&n=bxWCBKtofKnXvbvf&q=85&s=faa9d79f48a43f320d2b5a800256060e" width="1590" height="790" data-path="images/receiving-emails.jpeg" />

## Choose your infrastructure

To handle your received emails, you can use a variety of tools:

* [SDK](/docs/sdks): process inbound emails with an SDK built for your language
* [Integrations](/docs/integrations): process inbound emails using a framework or tool you already use
* [API](/docs/api-reference/emails/retrieve-received-email): process inbound emails with raw HTTP API calls
* [CLI](/docs/cli#receiving): process inbound emails and stream incoming messages from the terminal
* [MCP](/docs/mcp-server): list, read, and download inbound emails through your agent with MCP

See how to use all of Resend's receiving features such as processing attachments and forwarding emails to another address in the [receiving email guides](#related-guides).

## Manage your received emails

After you've received your first email, you'll be able to view and manage your emails in the [Emails Dashboard page](https://resend.com/emails) under the Receiving tab. From here, you can view email details, share a public version, and more.

You can also manage your emails programmatically using the [Receiving API](/docs/api-reference/emails/retrieve-received-email), [CLI commands](/docs/cli#receiving), or the [MCP server](/docs/mcp-server).

Learn more about [managing your received emails](/docs/dashboard/receiving/manage-emails) in the dedicated guide.

## Related Guides

See how to use Resend's receiving features.

<CardGroup cols={2}>
  <Card title="Custom domains" icon="globe" href="/docs/dashboard/receiving/custom-domains" />

  <Card title="Received email webhook" icon="mailbox-open-letter" href="/docs/dashboard/receiving/create-receiving-webhook" />

  <Card title="Get email content" icon="envelope-open-text" href="/docs/dashboard/receiving/get-email-content" />

  <Card title="Process attachments" icon="file-plus" href="/docs/dashboard/receiving/attachments" />

  <Card title="Forward emails" icon="arrow-turn-right" href="/docs/dashboard/receiving/forward-emails" />

  <Card title="Threaded replies" icon="comment-arrow-down" href="/docs/dashboard/receiving/reply-to-emails" />
</CardGroup>

## Examples

<CardGroup>
  <Card title="Next.js (TypeScript)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/nextjs-resend-examples/typescript/src/app/inbound">
    See the full source code.
  </Card>

  <Card title="Next.js (JavaScript)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/nextjs-resend-examples/javascript/src/app/inbound">
    See the full source code.
  </Card>

  <Card title="PHP" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/inbound">
    See the full source code.
  </Card>

  <Card title="Laravel" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/laravel-resend-examples">
    See the full source code.
  </Card>

  <Card title="Python" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/python-resend-examples/examples">
    See the full source code.
  </Card>

  <Card title="Ruby" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/examples">
    See the full source code.
  </Card>
</CardGroup>
