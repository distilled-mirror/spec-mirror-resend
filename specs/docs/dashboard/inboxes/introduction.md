> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Inboxes

> An introduction to sending, receiving, and managing email conversations with Inboxes.

Resend provides all the tools you need to host email inboxes on your [verified domains](/docs/dashboard/domains/introduction.md). Create an inbox to manage conversation threads for a single email address, such as a dedicated address for support emails.

Inboxes are useful for:

* AI agent email.
* Support and triage for contact forms.
* Shared team inboxes.
* Replies for transactional email.

## How Inboxes work

Inboxes mirror the familiar email inbox structure, using [**threads**](/docs/dashboard/inboxes/threads.md), [**labels**](/docs/dashboard/inboxes/labels.md), and [**drafts**](/docs/dashboard/inboxes/drafts.md) to organize your conversations. `inbox`, `sent`, `archive`, `trash`, and `spam` folders are built in to your Resend Inbox.

> [!NOTE]
>
> Receiving email in an inbox is different from [receiving
> emails](/docs/dashboard/receiving/introduction.md), which delivers inbound messages
> for a domain to your own webhook endpoint. Use Inboxes when you want Resend to
> store, thread, and organize conversations for you.

All of this is available through the dashboard, the API, the CLI, and the MCP server. You can use the dashboard with your team, build your own experience upon the API, and provide inboxes to AI agents.

## Inboxes features

With Resend Inboxes you can:

* Draft and send new emails from a dedicated email address that users can reply to.
* Receive inbound emails and attachments and reply to them in a threaded conversation.
* Forward received emails to another email address.
* Read threads, and move them between `inbox`, `archive`, `spam` or `trash` folders.
* Assign threads to teammates.
* Organize threads with custom labels.
* Search and filter threads.
* Configure an agent to perform actions on inbound mail.
* Receive webhooks for inbox events.

## Prerequisites

* A [verified domain with receiving enabled](/docs/dashboard/receiving/custom-domains.md). If you are unable to configure your custom domain to receive email, then you must configure [Inbox forwarding](/docs/dashboard/inboxes/create-inboxes.md#forward-an-existing-address) when you create your Inbox.

## Quickstart

Create an Inbox in the [Inboxes Dashboard](https://resend.com/inboxes). Or, get started with the [Inboxes API](/docs/api-reference/inboxes/create-inbox.md) and [SDKs](/docs/sdks.md), [CLI commands](/docs/cli.md#inboxes), or [MCP server](/docs/mcp-server.md).

To create an inbox in the Dashboard:

**1. Navigate to the Inboxes Dashboard page.**

**2. Select **Create inbox**.**

**3. Enter the address.**

**4. Choose the domain from your list of verified domains.**

**5. Send a test email to the new address.**

From any email account, send a message to the inbox address. It appears in
the **Inbox** folder as a new thread within a few seconds.

**6. Open the thread and reply.**

Select the thread, click **Reply**, write your message, and click **Send**.
The reply goes out from the inbox address and stays in the same thread.

## Related Guides

> **[Create inboxes](/docs/dashboard/inboxes/create-inboxes.md)**
>
> Create an address on a verified domain, or forward an existing address.

> **[Manage inboxes](/docs/dashboard/inboxes/manage-inboxes.md)**
>
> Rename, update, and delete inboxes.

> **[Manage threads](/docs/dashboard/inboxes/threads.md)**
>
> Read, search, and organize conversations, and reply to or forward emails.

> **[Drafts](/docs/dashboard/inboxes/drafts.md)**
>
> Write a message now and send it later.

> **[Labels](/docs/dashboard/inboxes/labels.md)**
>
> Tag threads with colored labels to keep them organized.

> **[Inbox agent](/docs/dashboard/inboxes/agent.md)**
>
> Let the built-in agent triage incoming threads from your instructions.
