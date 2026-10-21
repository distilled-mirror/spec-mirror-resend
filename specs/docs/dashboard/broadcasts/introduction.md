> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Sending Broadcasts

> An introduction to sending bulk marketing emails with Resend.

## Sending marketing emails

Resend provides all the tools you need to send bulk marketing emails to your Contacts. These are useful for:

* Newsletters
* Product Launches
* Investor Updates
* Promotions
* Changelogs

Resend's Broadcast features include tools for content creation, contact management, and performance tracking while handling queuing, throttling, and scheduling for you so that you don't have to roll your own infrastructure.

> [!TIP]
>
> To send transactional emails, use the
> [Sending](/docs/dashboard/emails/introduction) feature.

## Broadcast features

With Resend's Broadcast features, you can:

* Compose, schedule, and send marketing emails using a [no-code editor](/docs/dashboard/broadcasts/editor) directly in your Dashboard.
* Organize your contacts into [segments](/docs/dashboard/segments/introduction) and send bulk emails to only targeted contacts.
* Categorize your marketing emails by [topics](/docs/dashboard/topics/introduction) to allow recipients to choose which emails to receive.
* Turn your emails into reusable [templates](/docs/dashboard/templates/introduction).
* [Track performance metrics](/docs/dashboard/broadcasts/performance-tracking) such as delivery, click, and open rates.

## Quickstart

You can send bulk marketing emails from [a verified domain](/docs/dashboard/domains/introduction) to a [segment](/docs/dashboard/segments/introduction) of your contact list.

> [!TIP]
>
> You can create a draft Broadcast and send a test email to preview your content
> even before you add any contacts. However, you will need to create a segment
> before you can send your Broadcast.

**1. Add contacts.**

[Add or import contacts](/docs/dashboard/contacts/add-contacts) manually or
programmatically. You can also upload a `.csv` file of existing contacts.

**2. Create a segment and add contacts.**

Broadcasts are sent to a [segment](/docs/dashboard/segments/introduction) of your
audience.

**3. Write and send your Broadcast.**

[Create and send a Broadcast entirely using the no-code
editor](/docs/dashboard/broadcasts/editor). Alternatively, you can [use the
Broadcast API to build and distribute your
Broadcast](/docs/dashboard/broadcasts/send-broadcast-with-api) from your
application.

**4. Check your performance.**

View the details of any sent Broadcast in the [**Broadcasts Dashboard
Page**](https://resend.com/broadcasts) to see real-time deliverability
metrics, open and click tracking (if enabled), and subscriber actions.

## Choose your infrastructure

You can build and send your Broadcasts entirely from the [Resend Dashboard](https://resend.com/broadcasts). This allows all members of your team to create and manage every aspect of your marketing emails.

To create, send, and manage Broadcasts from your application, you can also use a variety of tools:

* [SDK](/docs/sdks): send with an SDK built for your language
* [Integrations](/docs/integrations): send from a framework or tool you already use
* [API](/docs/api-reference/emails/send-email): send with raw cURL calls
* [CLI](/docs/cli#emails): send emails from the terminal
* [MCP](/docs/mcp-server): send through your agent with MCP

> [!NOTE]
>
> &#x20;
>
> You can also create [automations](/docs/dashboard/automations/introduction) for
> repeatable transactional emails like welcoming new subscribers, and Broadcast
> needs like updating your contact list.

See how to use Resend's Broadcast and contact management features in the [related guides](#related-guides).

## Manage your Broadcasts

You can view and manage your Broadcasts from the [Broadcasts Dashboard page](https://resend.com/broadcasts).

You can also [manage your Broadcasts through the Broadcast API](/docs/api-reference/broadcasts/create-broadcast) which offers endpoints for programmatically creating, updating, and sending Broadcasts. Many of these actions can also be performed with [Resend Broadcast CLI commands](/docs/cli#broadcasts) and [AI building tools](/docs/ai-onboarding). You can also create [automations](/docs/dashboard/automations/introduction) for workflows related to your Broadcasts, such as managing your contact list.

Learn more about [managing your Broadcasts](/docs/dashboard/broadcasts/manage-broadcasts) in the dedicated guide.

## Export your data

Admins can download your data in CSV format for the following resources:

* Emails
* Broadcasts
* Contacts
* Segments
* Domains
* Logs
* API keys

> [!NOTE]
>
> Currently, exports are limited to admin users of your team.

To start, apply filters to your data and click on the "Export" button. Confirm your filters before exporting your data.

<video autoPlay muted loop playsinline src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/exports.mp4?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=1149ee4e83b4414e75a0ecaa92774c38" />

If your exported data includes 1,000 items or less, the export will download immediately. For larger exports, you'll receive an email with a link to download your data.

All admins on your team can securely access the export for 7 days. Unavailable exports are marked as "Expired."

> [!NOTE]
>
> All exports your team creates are listed in the
> [Exports](https://resend.com/exports) page under **Settings** > **Team** >
> **Exports**. Select any export to view its details page. All members of your
> team can view your exports, but only admins can download the data.

## Related Guides

See how to use Resend's Broadcast features.

> **[No-code editor](/docs/dashboard/broadcasts/editor)**

> **[Send with API](/docs/dashboard/broadcasts/send-broadcast-with-api)**

> **[Manage Broadcasts](/docs/dashboard/broadcasts/manage-broadcasts)**

> **[Contacts](/docs/dashboard/contacts/introduction)**

> **[Segments](/docs/dashboard/segments/introduction)**

> **[Topics](/docs/dashboard/topics/introduction)**

> **[Track performance](/docs/dashboard/broadcasts/performance-tracking)**

> **[Handle unsubscribes](/docs/dashboard/audiences/managing-unsubscribe-list)**
