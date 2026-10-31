> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# AI onboarding

> Everything you need to onboard your AI agent to Resend.

If you're developing with AI, Resend offers several resources to improve your experience.

* [Resend MCP Server](#resend-mcp-server)
* [Resend CLI](#resend-cli)
* [Resend Docs for Agents](#resend-docs-for-agents)
* [Email Skills for Agents](#email-skills-for-agents)
* [Quick Start Guides](#quick-start-guides)
* [OpenClaw Guide](#openclaw-guide)
* [Chat SDK](#chat-sdk)
* [AI Builder Guides](#ai-builder-guides)
* [AI Integrations](#ai-integrations)

## Prerequisite: Create an API Key

A human must create the Resend account. Once you have an account, you'll need to [create an API key](https://resend.com/docs/create-an-api-key.md). With an API key, your agent can perform many other tasks.

> [!NOTE]
>
> To send or receive with Resend, you'll need to [verify a domain](https://resend.com/domains). While an agent can [create a domain](https://resend.com/docs/api-reference/domains/create-domain.md), the API returns DNS records you will need to add in your DNS provider before [verifying your DNS records](https://resend.com/docs/api-reference/domains/verify-domain.md). You may find it easier to verify your domain in the dashboard.

## Resend MCP Server

MCP is an open protocol that standardizes how applications provide context to LLMs. Among other benefits, it provides LLMs tools to act on your behalf. Our [MCP server](https://github.com/resend/resend-mcp) is open-source and covers our full API surface area.

Resend hosts the MCP server, so you can connect any MCP client without installing anything:

```
https://mcp.resend.com/mcp
```

When you connect, your client authenticates with OAuth by opening a browser to log in to Resend. Clients that can't complete a browser login can pass an API key as a Bearer token instead. You can also run the server locally with `npx` using the `resend-mcp` package on NPM.

The [Resend plugin](https://github.com/resend/resend-skills) follows the [Agent Plugins](https://agent-plugins.org) spec. On clients whose landing page installs that plugin, it adds the remote MCP server and the Resend skills together. Setup for each client is on the [MCP server page](https://resend.com/docs/mcp-server.md), and it matches the page at resend.com. Claude and Codex also keep these one-click installs:

* [Resend connector for Claude](https://claude.ai/directory/connectors/resend)
* [Resend plugin for Codex](https://chatgpt.com/plugins/plugin_asdk_app_6a3c407853888191beddc2151c2b6f8b?open_in_codex)

> [card] [MCP Server](https://resend.com/docs/mcp-server.md)
>
> View setup instructions for Claude, Cursor, Codex, Copilot, Hermes, OpenClaw,
> and more.

## Resend CLI

The Resend CLI lets you send emails, manage your account, and develop locally, all from the terminal. It's built for humans, AI agents, and CI/CD pipelines.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
# Authenticate
resend login

# Send an email
resend emails send \
  --from "you@example.com" \
  --to hello@example.com \
  --subject "Hello" \
  --text "Sent from my terminal."
```

The CLI also includes a full local webhook setup for developing with inbound email events without deploying anything.

> [card] [Resend CLI](https://resend.com/docs/cli.md)
>
> Install the CLI and set up a local webhook development environment.

## Resend Docs for Agents

You can give your agent current docs in a context-aware way in three ways:

1. **Markdown docs**

   Every doc includes a markdown version (append `md` to any page)

   ```
   Docs for this page: https://resend.com/docs/ai-onboarding.md
   ```

2. **Full llms.txt**

   Give your agent all our docs in a single file.

   ```
   Here are the Resend docs: https://resend.com/docs/llms-full.txt
   ```

3. **MCP Docs server**

   For a more structured approach using MCP tools, you can install our MCP docs server in any MCP client, like Cursor, Codex, or Claude Code.

   ```
   npx add-mcp https://resend.com/docs/mcp
   ```

## Email Skills for Agents

Skills give AI agents specialized knowledge for specific tasks.

Install skills with a single command:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
npx skills add resend/resend-skills
```

Or install individually:

| Skill | Install | What it does |
| - | - | - |
| [Resend](https://resend.com/docs/resend-skill.md) | `npx skills add resend/resend-skills` | Send and receive emails, handle errors, and prevent duplicate sends. Get code examples from various SDKs. |
| [React Email](https://resend.com/docs/react-email-skill.md) | `npx skills add resend/react-email` | Build emails in React, Tailwind, and TypeScript. Audit existing React emails for style and cross-client rendering. |
| [Email Best Practices](https://resend.com/docs/email-best-practices-skill.md) | `npx skills add resend/email-best-practices` | Audit SPF/DKIM/DMARC setup, compliance (CAN-SPAM, GDPR), webhook handling |

## Quick Start Guides

The documentation includes quick start guides for common tasks with Resend. They contain step-by-step instructions for sending emails, creating templates, and more. Copy the prompt for your agent or click to open in Cursor.

Example agent quick start guide for sending emails.

Resend provides two endpoints for sending emails:

| Approach | Endpoint | Use Case |
| - | - | - |
| **Single** | `POST /emails` | Individual transactional emails, emails with attachments, scheduled sends |
| **Batch** | `POST /emails/batch` | Multiple distinct emails in one request (max 100), bulk notifications |

**Choose batch when:**

* Sending 2+ distinct emails at once
* Reducing API calls is important (by default, rate limit is 10 requests per second)
* No attachments or scheduling needed

**Choose single when:**

* Sending one email
* Email needs attachments
* Email needs to be scheduled
* Different recipients need different timing

## Quick Start

1. **Detect project language** from config files (package.json, requirements.txt, go.mod, etc.)
2. **Install SDK** (preferred) or use cURL
3. **Choose single or batch** based on the decision matrix above
4. **Implement best practices** - Idempotency keys, error handling, retries

## Best Practices (Critical for Production)

Always implement these for production email sending.

### Idempotency Keys

Prevent duplicate emails when retrying failed requests.

| Key Facts | |
| - | - |
| **Format (single)** | `<event-type>/<entity-id>` (e.g., `welcome-email/user-123`) |
| **Format (batch)** | `batch-<event-type>/<batch-id>` (e.g., `batch-orders/batch-456`) |
| **Expiration** | 24 hours |
| **Max length** | 256 characters |
| **Duplicate payload** | Returns original response without resending |
| **Different payload** | Returns 409 error |

### Error Handling

| Code | Action |
| - | - |
| 400, 422 | Fix request parameters, don't retry |
| 401, 403 | Check API key / verify domain, don't retry |
| 409 | Idempotency conflict - use new key or fix payload |
| 429 | Rate limited - retry with exponential backoff (by default, rate limit is 10 requests/second) |
| 500 | Server error - retry with exponential backoff |

### Retry Strategy

* **Backoff:** Exponential (1s, 2s, 4s...)
* **Max retries:** 3-5 for most use cases
* **Only retry:** 429 (rate limit) and 500 (server error)
* **Always use:** Idempotency keys when retrying

## Single Email

**Endpoint:** `POST /emails` (prefer SDK over cURL)

### Required Parameters

| Parameter | Type | Description |
| - | - | - |
| `from` | string | Sender address. Format: `"Name <email@domain.com>"` |
| `to` | string\[] | Recipient addresses (max 50) |
| `subject` | string | Email subject line |
| `html` or `text` | string | Email body content |

### Optional Parameters

| Parameter | Type | Description |
| - | - | - |
| `cc` | string\[] | CC recipients |
| `bcc` | string\[] | BCC recipients |
| `reply_to`\* | string\[] | Reply-to addresses |
| `scheduled_at`\* | string | Schedule send time (ISO 8601) |
| `attachments` | array | File attachments (max 40MB total) |
| `tags` | array | Key/value pairs for tracking |
| `headers` | object | Custom headers |

\*Parameter naming varies by SDK (e.g., `replyTo` in Node.js, `reply_to` in Python).

### Minimal Example (Node.js)

```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('YOUR_RESEND_API_KEY');

const { data, error } = await resend.emails.send(
  {
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Hello World',
    html: '<p>Email body here</p>',
  },
  { idempotencyKey: `welcome-email/${userId}` },
);

if (error) {
  console.error('Failed:', error.message);
  return;
}
console.log('Sent:', data.id);
```

## Batch Email

**Endpoint:** `POST /emails/batch` (but prefer SDK over cURL)

### Limitations

* **No attachments** - Use single sends for emails with attachments
* **No scheduling** - Use single sends for scheduled emails
* **Atomic** - If one email fails validation, the entire batch fails
* **Max 100 emails** per request
* **Max 50 recipients** per individual email in the batch

### Pre-validation

Since the entire batch fails on any validation error, validate all emails before sending:

* Check required fields (from, to, subject, html/text)
* Validate email formats
* Ensure batch size is less than or equal to 100

### Minimal Example (Node.js)

```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('YOUR_RESEND_API_KEY');

const { data, error } = await resend.batch.send(
  [
    {
      from: 'Acme <hello@example.com>',
      to: ['delivered@resend.dev'],
      subject: 'Order Shipped',
      html: '<p>Your order has shipped!</p>',
    },
    {
      from: 'Acme <hello@example.com>',
      to: ['delivered@resend.dev'],
      subject: 'Order Confirmed',
      html: '<p>Your order is confirmed!</p>',
    },
  ],
  { idempotencyKey: `batch-orders/${batchId}` },
);

if (error) {
  console.error('Batch failed:', error.message);
  return;
}
console.log(
  'Sent:',
  data.map((e) => e.id),
);
```

## OpenClaw Guide

Equipping your agent with its own email inbox can be a powerful tool to unlock new workflows. Alternatively, give it access to your Resend account to support agentic flows for sending and receiving emails.

> [card] [Email Automation for OpenClaw using Resend](https://resend.com/docs/openclaw-guide.md)
>
> View the OpenClaw guide.

## Chat SDK

The `@resend/chat-sdk-adapter` package is a Vercel Chat SDK adapter that turns email into a two-way communication channel. Receive inbound emails through webhooks, reply through the Resend API, and let the adapter handle threading automatically. It also supports card emails, attachments, and proactive outreach.

> [card] [Chat SDK](https://resend.com/docs/chat-sdk.md)
>
> Build conversational email experiences with the Chat SDK adapter.

## AI Builder Guides

Get started using Resend with popular AI builders:

* [Anything Integration](https://resend.com/docs/anything-integration.md)
* [Lovable Integration](https://resend.com/docs/lovable-integration.md)
* [v0 Integration](https://resend.com/docs/v0-integration.md)
* [Bolt.new Integration](https://resend.com/docs/bolt-new-integration.md)
* [Replit Integration](https://resend.com/docs/replit-integration.md)
* [Base44 Integration](https://resend.com/docs/base44-integration.md)
* [Leap.new Integration](https://resend.com/docs/leap-new-integration.md)

## AI Integrations

Several AI tools have created integrations for working with Resend. Visit their documentation for information on integrating Resend with their tools.

> [card] [Lovable](https://docs.lovable.dev/integrations/resend)
>
> Tell the Lovable AI to send emails

> [card] [Anything](https://www.createanything.com/docs/integrations/resend)
>
> Add email to your Anything projects

> [card] [Wildcard](https://github.com/wild-card-ai/agents-json/blob/master/examples/resend.ipynb)
>
> Send natural language emails using Wildcard

> [card] [mcp.run](https://www.mcp.run/nilslice/resend)
>
> Build email AI agents using mcp.run

> [card] [Rocket](https://docs.rocket.new/integrations/resend)
>
> Send emails from apps built with Rocket

> [card] [Base44](https://docs.base44.com/Integrations/Resend-integration)
>
> Add email to your Base44 apps

> [card] [Leap.new](https://docs.leap.new/integrations/resend)
>
> Add email to your Leap apps

> [card] [Parsley](https://www.parsley.id/integrations/resend)
>
> Send alerts and follow-ups with Parsley

> [card] [Pica](https://www.picaos.com/integrations/resend)
>
> Integrate Pica with Resend
