> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Automations

> An introduction to automating emails with custom events.

## Automations

Automations allow you to create a series of executable [steps](/docs/dashboard/automations/steps) based on [custom trigger events](/docs/dashboard/automations/trigger) from your application.

You can use Automations for repeatable actions such as:

* Welcome emails
* Drip campaigns
* Payment recovery
* Abandoned cart
* Trial expiration

## Automation features

Automations allow you to build lifecycle messages and drip campaigns with triggers, personalization, and real-time observability. You can:

* [Create automations](/docs/dashboard/automations/create-automation) to send emails or manage contacts in the Dashboard, or via Resend's code tools.
* Define your own [custom events](/docs/dashboard/automations/custom-events) to trigger automations.
* Personalize each step with options to [wait for an event](/docs/dashboard/automations/wait-for-event) or [delay the automation](/docs/dashboard/automations/delay) for a certain period of time before moving on.
* Create branched workflows by executing different steps based on whether or not [conditions](/docs/dashboard/automations/condition) are met.
* Send personalized emails from [Templates using variables](/docs/dashboard/templates/template-variables).
* Include [`{{{RESEND_UNSUBSCRIBE_URL}}}`](/docs/dashboard/broadcasts/editor#broadcast-unsubscribe-link) for compliance with non-transactional product and marketing messaging.
* Monitor and debug your [Automation execution runs](/docs/dashboard/automations/runs).

## Quickstart

Get started by [creating an automation](/docs/dashboard/automations/create-automation) in the **Automations** Dashboard page. Or, get started with the [Automation API](/docs/api-reference/automations/create-automation) and [SDKs](/docs/sdks), [CLI commands](/docs/cli#automations), or [MCP](/docs/mcp-server).

The Automation process involves the following steps:

<Steps>
  <Step title="Create Automation">
    Start a new Automation and give it a descriptive name.
  </Step>

  <Step title="Add Trigger">
    Define the event that will trigger the Automation.
  </Step>

  <Step title="Define Steps">Configure the steps to be executed.</Step>

  <Step title="Send an Event">
    Trigger the Automation by sending an event from your application.
  </Step>

  <Step title="Monitor Runs">
    Track and debug your Automation executions using runs.
  </Step>
</Steps>

See step-by-step examples of [creating an automation](/docs/dashboard/automations/create-automation) through the Dashboard and using the API.

## Choose your infrastructure

You can build automations, define events, and inspect automation runs entirely from the Resend Dashboard. This allows all members of your team to create and manage every aspect of your automated email flows.

To create and manage Automations from your application, you can use a variety of tools:

* [SDK](/docs/sdks): automate with an SDK built for your language
* [Integrations](/docs/integrations): automate with a framework or tool you already use
* [API](/docs/api-reference/automations/create-automation): automate with raw cURL calls
* [CLI](/docs/cli#automations): automate from the terminal
* [MCP](/docs/mcp-server): automate through your agent using natural language

See more about creating and managing automated workflows in the [related automation guides](#related-guides).

## Manage your Automations

You can view and manage your Automations from the [Automations Dashboard page](https://resend.com/automations).

The [Automations API](/docs/api-reference/automations/create-automation) and [SDKs](/docs/sdks) offer endpoints for programmatically creating, updating, retrieving, stopping, and deleting your automated workflows.

Many of these actions can also be performed with [Resend CLI commands](/docs/cli#automations) and [MCP](/docs/mcp-server).

## Track performance

You can monitor and debug the execution of your Automations from the [Automations Dashboard page](https://resend.com/automotions). You can track the status of each individual step in your workflow via an [automation run](/docs/dashboard/automations/runs) that is created every time your automation is triggered.

You can also retrieve and monitor runs with the [Automation API](/docs/api-reference/automations/list-automation-runs), an [automations CLI command](/docs/cli#automations), or [AI building tools](/docs/ai-onboarding).

## Related Guides

See how to use Resend's automation features.

<CardGroup>
  <Card title="Create automations" icon="cards-blank" href="/docs/dashboard/automations/create-automation" />

  <Card title="Custom triggers" icon="hand-point-right" href="/docs/dashboard/automations/custom-events" />

  <Card title="Steps reference" icon="gear-code" href="/docs/dashboard/automations/steps" />

  <Card title="Monitor execution runs" icon="tower-control" href="/docs/dashboard/automations/runs" />
</CardGroup>
