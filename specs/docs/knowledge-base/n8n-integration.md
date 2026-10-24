> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with n8n and Resend

> Learn how to install and use the official Resend node for n8n to send emails, manage contacts and inboxes, handle webhooks, and more.

[n8n](https://n8n.io) is a workflow automation platform that lets you connect apps and build powerful automations. The official [Resend node](https://github.com/resend/n8n-nodes-resend) (`n8n-nodes-resend`) provides full coverage of the Resend API. From within n8n, you can send emails, run broadcasts and automations, manage contacts, domains, and inboxes, and trigger workflows from Resend events.

![Resend node in the n8n editor](https://mintcdn.com/resend/bsGJjyDJfHnB7xCx/images/n8n-integration.png?fit=max\&auto=format\&n=bsGJjyDJfHnB7xCx\&q=85\&s=ed6c44c61540d4e88607a123ffb9c1c9)

## How to use Resend's n8n node

**1. Install the Resend node**

1. Open the nodes panel by selecting **+** or pressing **Tab**
2. Search for **Resend**
3. Select **Install** to install the node for your instance
4. The node is now available in all your workflows

<video autoPlay muted loop playsInline src="https://mintcdn.com/resend/z1A2Ch2mBjrpogJr/images/n8n-integration-install.mp4?fit=max&auto=format&n=z1A2Ch2mBjrpogJr&q=85&s=368da1206f532b6fecc21af4887a5934" />

**2. Setup Resend**

1. [Create an API Key](https://resend.com/api-keys): copy this key to your clipboard
2. [Verify your own domain](https://resend.com/domains): to send to email addresses other than your own

**3. Connect your Resend account**

The Resend node supports two authentication methods. Choose one in the node's **Authentication** field.

**OAuth2 (recommended)**

1. In n8n, go to **Credentials** > **Add credential**.
2. Search for **Resend OAuth2 API** and select **Connect my account**.

n8n registers itself as an OAuth client with Resend, so you don't need to create or paste an API key.

> [!NOTE]
>
> OAuth2 relies on Dynamic Client Registration support in n8n core. If **Connect
> my account** doesn't work, update to a recent n8n version or use the **Resend
> API** credential instead.

**API key**

1. In n8n, go to **Credentials** > **Add credential**.
2. Search for **Resend API** and paste your API key.

<video autoPlay muted loop playsInline src="https://mintcdn.com/resend/bsGJjyDJfHnB7xCx/images/n8n-integration-credential.mp4?fit=max&auto=format&n=bsGJjyDJfHnB7xCx&q=85&s=fb0b36a5de248b7a2eee873f427e4481" />

The credential you choose is used by the main **Resend** node for all API operations.

**4. Send your first email**

1. Click the **+** (Add node) connector on the canvas.
2. Search for **Resend** in the nodes panel.
3. n8n displays a list of available actions — select **Send an Email**.
4. The Resend node is added to your workflow with the **Send** operation pre-selected.
5. Fill in the **From**, **To**, **Subject**, and **Email Body** fields.
6. Execute the node.

> [!NOTE]
>
> By default, you can only send emails to your own email address using the
> `onboarding@resend.dev` sender domain. To send to other recipients, [add a
> custom domain](https://resend.com/docs/dashboard/domains/introduction.md) to your Resend account.

## Human in the Loop (Send and Wait)

The **Send and Wait for Response** operation enables human-in-the-loop workflows. Send an email and pause the workflow until the recipient responds, via approval buttons or a free-text form.

1. In the nodes panel, go to **Human in the Loop** > **Resend**, or select the **Email** resource and the **Send and Wait for Response** operation.
2. Choose a **Response Type**: **Approval** (buttons) or **Free Text** (form).
3. Configure the email content and any wait-time limits.
4. The workflow pauses until the recipient clicks a button or submits the form.

| Option | Description |
| - | - |
| **Response Type** | Choose between Approval (buttons) or Free Text (form) |
| **Approval Type** | Single button (Approve only) or Double (Approve/Decline) |
| **Button Labels** | Customize the button text |
| **Button Styles** | Primary or Secondary button styling |
| **Message Button Label** | Label for the form link button (Free Text mode) |
| **Response Form Title** | Title shown on the response form |
| **Limit Wait Time** | Set a timeout for the wait period |

## Receive webhooks with the Resend Trigger

The **Resend Trigger** node lets you start workflows automatically when events occur in Resend (e.g., an email is delivered or bounced, a contact is created, or an inbox receives an email). Webhook signatures are verified automatically using Svix.

### Set up the Trigger node

1. Add a **Resend Trigger** node to your workflow.
2. Create a **Resend Webhook Signing Secret** credential:
   * Create a webhook endpoint in the [Resend Dashboard](https://resend.com/webhooks).
   * Copy the signing secret (starts with `whsec_`).
   * In n8n, go to **Credentials** > **Add credential**, search for **Resend Webhook Signing Secret**, and paste the secret.

> [!NOTE]
>
> Give each webhook credential a unique name (e.g., "Resend Webhook — Bounces"
> or "Resend Webhook — Delivery Events"). This makes it much easier to identify
> the right credential when you have multiple triggers connected to different
> webhooks.

3. Select the events you want to listen for.
4. Copy the **webhook URL** from the Trigger node and paste it into your Resend Dashboard webhook configuration.

### Supported trigger events

| Event | Description |
| - | - |
| `email.sent` | Email sent to recipient |
| `email.delivered` | Email delivered successfully |
| `email.delivery_delayed` | Email delivery delayed |
| `email.failed` | Email failed to send due to an error (for example, invalid recipients, API key issues, domain verification, or quota limits) |
| `email.opened` | Recipient opened the email |
| `email.clicked` | Link clicked in email |
| `email.bounced` | Email bounced |
| `email.complained` | Spam complaint received |
| `email.received` | Resend successfully received an inbound email |
| `email.scheduled` | Email is scheduled to be sent |
| `email.suppressed` | Email is suppressed by Resend |
| `contact.created` | New contact added |
| `contact.updated` | Contact modified |
| `contact.deleted` | Contact removed |
| `contact.topics.updated` | Contact's topic subscriptions changed |
| `domain.created` | New domain added |
| `domain.updated` | Domain modified |
| `domain.deleted` | Domain removed |
| `suppression.added` | Email address added to your suppression list |
| `suppression.removed` | Email address removed from your suppression list |
| `topic.created` | New topic added |
| `topic.updated` | Topic modified |
| `topic.deleted` | Topic removed |
| `inbox.created` | New inbox added |
| `inbox.updated` | Inbox modified |
| `inbox.deleted` | Inbox removed |
| `inbox.email.received` | Inbox received an email |
| `inbox.email.sent` | Email sent from an inbox |
| `inbox.thread.created` | New inbox thread started |
| `inbox.thread.assigned` | Inbox thread assigned |
| `inbox.thread.unassigned` | Inbox thread unassigned |
| `inbox.thread.folder.updated` | Inbox thread moved to a different folder |
| `inbox.thread.labels.updated` | Inbox thread labels changed |
| `inbox.draft.created` | Inbox draft created |
| `inbox.draft.updated` | Inbox draft modified |
| `inbox.draft.sent` | Inbox draft sent |
| `inbox.draft.deleted` | Inbox draft removed |

For event payloads, see [Event Types](https://resend.com/docs/webhooks/event-types.md).

## Supported resources

The **Resend** node covers the full Resend API:

| Resource | Operations |
| - | - |
| **Email** | Send, Send Batch, Send and Wait, List, Get, Update, Cancel, Share, Get Metrics, List Attachments, Get Attachment |
| **Receiving Emails** | List, Get, List Attachments, Get Attachment |
| **Inboxes** | Create, List, Get, Update, Delete, Get Agent Settings, Update Agent Settings, Create Label, List Labels, Update Label, Delete Label |
| **Inbox Threads** | List, Search, Get, Update, Delete, Add Labels, Set Labels, Remove Label, List Emails, Get Email, Reply, Forward |
| **Inbox Drafts** | Create, List, Get, Update, Delete, Send |
| **Broadcasts** | Create, List, Get, Update, Delete, Send, Cancel, Duplicate, List Clicked Links, List Recipients |
| **Templates** | Create, List, Get, Update, Delete, Publish, Duplicate |
| **Automations** | Create, List, Get, Update, Delete, Duplicate, Stop, List Runs, Get Run |
| **Events** | Create, List, Get, Update, Delete, Send |
| **Contacts** | Create, List, Get, Update, Delete, Add to Segment, List Segments, Remove from Segment, Get Topics, Update Topics, Create Import, List Imports, Get Import |
| **Contact Properties** | Create, List, Get, Update, Delete |
| **Segments** | Create, List, Get, Update, Delete, List Contacts, Get Metrics |
| **Topics** | Create, List, Get, Update, Delete |
| **Suppressions** | Create, List, Get, Delete, Batch Add, Batch Remove |
| **Domains** | Create, List, Get, Update, Delete, Verify, Claim, Get Claim, Verify Claim |
| **Webhooks** | Create, List, Get, Update, Delete, Rotate Signing Secret, List Events, Get Event, Replay Event, List Event Attempts |
| **Logs** | List, Retrieve |
| **Account** | Get Usage, List Grants, Revoke Grant, Disconnect (OAuth2 credential only) |

> [!NOTE]
>
> Upgrading from v2? Version 3 renames the **Workflow** resource to
> **Automation** and moves tracking domains into the **Tracking Subdomain**
> option on **Domain** > **Create** and **Update**. See the [migration
> guide](https://github.com/resend/n8n-nodes-resend#migrating-to-v300) for all
> breaking changes.

## Example workflow: Send a welcome email when a contact is created

Here's a simple workflow you can build with the Resend nodes:

1. **Resend Trigger**: listens for `contact.created` events.
2. **Resend** (Email > Send): sends a welcome email to the new contact using data from the trigger.

The Trigger-Action pattern works for any event. For example, you can notify your team on Slack when an email bounces, or log delivery events to a spreadsheet.

For ready-to-import workflows, including bounce handling, newsletter broadcasts, drip campaigns, and approval flows, see the [example workflows](https://github.com/resend/n8n-nodes-resend/tree/main/examples) in the node's repository.

> [!NOTE]
>
> The Resend node is also available as an [AI
> tool](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolworkflow/)
> in n8n, so you can use it inside AI agent workflows.
