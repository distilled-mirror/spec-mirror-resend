> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Sending emails with Resend

> Resend has a wide range of features for sending both transactional and marketing emails.

Resend provides an API, command-line interface (CLI), webhooks, and automations to support both types of emails you need to send:

* **Transactional emails:** personalized, event-driven communication
* **Marketing campaigns:** bulk email [Broadcasts](/docs/dashboard/broadcasts/introduction) distributed to a contact list

All of these email features and activities are also available through a user-friendly Dashboard and through AI tooling for agents. This allows your entire team to create and send emails, update automations, manage contacts, track performance, and more.

Get started with Resend's free plan, then choose from multiple [pricing plans and tiers](https://resend.com/pricing) depending on the number and type of emails you need to send as you grow.

## Send transactional emails

A **Transactional email** is a message triggered by a user action or required for legal compliance. Common examples include:

* Order confirmations
* Password reset emails
* Account notifications

Typically, transactional emails are **1-to-1** messages sent in response to a specific event.

With a Resend Transactional Plan, you can send transactional emails from your application using the [Resend API](/docs/api-reference/introduction), the [Resend CLI](/docs/cli), or with [SMTP](/docs/send-with-smtp). Resend also provides an [MCP server](/docs/mcp-server), [agent skills](/docs/react-email-skill), and more to work with your preferred [AI builder and tooling](/docs/ai-onboarding).

You can also trigger emails using [webhooks](/docs/webhooks/introduction), and even [create steps to automate emails](/docs/dashboard/automations/introduction) based on custom events from your application.

## Send bulk marketing emails

Marketing emails are **promotional**, **informative**, or **general communication** messages.

Marketing emails are regulated by laws like **CAN-SPAM** (US) and **CASL** (Canada), and **recipients must have the option to unsubscribe**.

Examples of marketing emails:

* Promotional offers and discounts
* Newsletters
* Product updates

Marketing emails are typically **1-to-many** messages, sent when you want to reach a larger audience (e.g., newsletters).

With a Resend Marketing Plan, you can send [Broadcasts](/docs/dashboard/broadcasts/introduction) to your subscribers using a no-code editor in your Resend Dashboard, or from the [Broadcast API](https://resend.com/docs/api-reference/broadcasts/create-broadcast).

When you use Broadcasts, you get tools for [managing your contacts](/docs/dashboard/audiences/introduction), [tracking performance](/docs/dashboard/broadcasts/performance-tracking), and [customizing your personal unsubscribe page](/docs/dashboard/settings/unsubscribe-page). Resend also handles all the queuing, throttling, and scheduling for you so that you don't have to roll your own infrastructure.

Marketing plans also allow you to create [Resend automations](/docs/dashboard/automations/introduction) for repeatable actions like welcoming new subscribers and updating your contact list. Resources such as the [Resend MCP server](/docs/mcp-server), [agent skills](/docs/react-email-skill), and more are all available to your preferred [AI builders and tooling](/docs/ai-onboarding) to help you send and manage your marketing emails.

## Send a combination of emails

It is common to need to send both transactional and marketing emails to your users. Your customers need personalized emails about their orders, but may also wish to subscribe to a newsletter that is delivered to your entire contact list.

Some emails do not fit neatly into one category:

* Marketing emails can be **1-to-1**, based on personalized user activity (e.g., abandoned cart reminders, drip marketing campaigns). You can use Resend's transactional APIs and automations to send these individual marketing emails, as long as proper consent and compliance regulations are followed.
* Resend's [batch sending API feature](/docs/dashboard/emails/batch-sending) can send multiple transactional emails at once (up to 100), even to different recipients with unique content, instead of making individual API requests for each email.

You can either go with Resend's opinionated, full-featured solutions or design your own architecture from the ground up. You can use all of Resend's features for any type of email sending that you can build. This includes APIs, CLI commands, webhooks, and automations, plus AI tools and Dashboard controls.

Resend allows you to choose both a Transactional and a Marketing plan, each at the tier that suits your specific use case for your email volume, and features needed. Update each plan individually at any time if your sending habits change, or add pay-as-you-go add-ons if you need a more flexible solution.

## Learn more

<CardGroup cols={2}>
  <Card title="Send Email API" icon="tools" href="/docs/api-reference/emails/send-email">
    Send, list, retrieve, update, and cancel transactional emails with the Send
    Email API.
  </Card>

  <Card title="Broadcasts" icon="megaphone" href="/docs/dashboard/broadcasts/introduction">
    Create and send marketing emails with Resend's no-code editor or the
    Broadcasts API.
  </Card>
</CardGroup>

## Next steps

<CardGroup cols={2}>
  <Card title="Import or add email contacts" icon="globe" href="/docs/dashboard/audiences/contacts">
    Add existing subscribers to your Resend contact list programmatically,
    manually, or by uploading a `.csv` file.
  </Card>

  <Card title="Quickstart tutorials" icon="stopwatch" href="/docs/introduction">
    Send your first transactional email with a quick tutorial for your language
    or framework.
  </Card>
</CardGroup>
