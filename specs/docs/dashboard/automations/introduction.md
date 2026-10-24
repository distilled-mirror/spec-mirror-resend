> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Automations

> An introduction to automating emails with custom events.

## Automations

Automations allow you to create a series of executable [steps](https://resend.com/docs/dashboard/automations/steps.md) based on [custom trigger events](https://resend.com/docs/dashboard/automations/trigger.md) from your application.

You can use Automations for repeatable actions such as:

* Welcome emails
* Drip campaigns
* Payment recovery
* Abandoned cart
* Trial expiration

## Automation features

Automations allow you to build lifecycle messages and drip campaigns with triggers, personalization, and real-time observability. You can:

* [Create automations](https://resend.com/docs/dashboard/automations/create-automation.md) to send emails or manage contacts in the Dashboard, or via Resend's code tools.
* Define your own [custom events](https://resend.com/docs/dashboard/automations/custom-events.md) to trigger automations.
* Personalize each step with options to [wait for an event](https://resend.com/docs/dashboard/automations/wait-for-event.md) or [delay the automation](https://resend.com/docs/dashboard/automations/delay.md) for a certain period of time before moving on.
* Create branched workflows by executing different steps based on whether or not [conditions](https://resend.com/docs/dashboard/automations/condition.md) are met.
* Send personalized emails from [Templates using variables](https://resend.com/docs/dashboard/templates/template-variables.md).
* Include [`{{{RESEND_UNSUBSCRIBE_URL}}}`](https://resend.com/docs/dashboard/broadcasts/editor#broadcast-unsubscribe-link) for compliance with non-transactional product and marketing messaging.
* Monitor and debug your [Automation execution runs](https://resend.com/docs/dashboard/automations/runs.md).

## Quickstart

Get started by [creating an automation](https://resend.com/docs/dashboard/automations/create-automation.md) in the **Automations** Dashboard page. Or, get started with the [Automation API](https://resend.com/docs/api-reference/automations/create-automation.md) and [SDKs](https://resend.com/docs/sdks.md), [CLI commands](https://resend.com/docs/cli.md#automations), or [MCP](https://resend.com/docs/mcp-server.md).

The Automation process involves the following steps:

**1. Create Automation**

Start a new Automation and give it a descriptive name.

**2. Add Trigger**

Define the event that will trigger the Automation.

**3. Define Steps**

Configure the steps to be executed.

**4. Send an Event**

Trigger the Automation by sending an event from your application.

**5. Monitor Runs**

Track and debug your Automation executions using runs.

See step-by-step examples of [creating an automation](https://resend.com/docs/dashboard/automations/create-automation.md) through the Dashboard and using the API.

## Choose your infrastructure

You can build automations, define events, and inspect automation runs entirely from the Resend Dashboard. This allows all members of your team to create and manage every aspect of your automated email flows.

To create and manage Automations from your application, you can use a variety of tools:

* [SDK](https://resend.com/docs/sdks.md): automate with an SDK built for your language
* [Integrations](https://resend.com/docs/integrations.md): automate with a framework or tool you already use
* [API](https://resend.com/docs/api-reference/automations/create-automation.md): automate with raw cURL calls
* [CLI](https://resend.com/docs/cli.md#automations): automate from the terminal
* [MCP](https://resend.com/docs/mcp-server.md): automate through your agent using natural language

See more about creating and managing automated workflows in the [related automation guides](#related-guides).

## Manage your Automations

You can view and manage your Automations from the [Automations Dashboard page](https://resend.com/automations).

The [Automations API](https://resend.com/docs/api-reference/automations/create-automation.md) and [SDKs](https://resend.com/docs/sdks.md) offer endpoints for programmatically creating, updating, retrieving, stopping, and deleting your automated workflows.

Many of these actions can also be performed with [Resend CLI commands](https://resend.com/docs/cli.md#automations) and [MCP](https://resend.com/docs/mcp-server.md).

## Track performance

You can monitor and debug the execution of your Automations from the [Automations Dashboard page](https://resend.com/automotions). You can track the status of each individual step in your workflow via an [automation run](https://resend.com/docs/dashboard/automations/runs.md) that is created every time your automation is triggered.

You can also retrieve and monitor runs with the [Automation API](https://resend.com/docs/api-reference/automations/list-automation-runs.md), an [automations CLI command](https://resend.com/docs/cli.md#automations), or [AI building tools](https://resend.com/docs/ai-onboarding.md).

## Related Guides

See how to use Resend's automation features.

> **[Create automations](https://resend.com/docs/dashboard/automations/create-automation.md)**

> **[Custom triggers](https://resend.com/docs/dashboard/automations/custom-events.md)**

> **[Steps reference](https://resend.com/docs/dashboard/automations/steps.md)**

> **[Monitor execution runs](https://resend.com/docs/dashboard/automations/runs.md)**
