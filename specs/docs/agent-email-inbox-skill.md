> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent Email Inbox Skill

> Give your AI agent a secure email inbox to receive and act on inbound emails.

The Agent Email Inbox skill enables AI agents to securely receive and respond to emails through Resend's webhook-based architecture. It provides security patterns that prevent untrusted email content from controlling your agent, including sender allowlists, content filtering, and sandboxed processing.

## Why your agent needs a secure inbox

An AI agent's inbox receives **untrusted input**. Without proper security, anyone who knows your agent's email address can send instructions that your agent will execute. The Agent Email Inbox skill solves this with a leveled security approach built in from the start.

Unlike polling-based approaches, Resend uses **webhooks** for inbound email. Your agent is notified instantly when an email arrives. No cron jobs, no wasted API calls checking empty inboxes.

## Installation

This skill is part of the [resend-skills](https://github.com/resend/resend-skills) repository, which also includes the [Resend skill](/docs/resend-skill) for sending emails. When you run the install command, you'll be prompted to choose which skills to install.

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
npx skills add resend/resend-skills
```

## Advantages

* **5 security levels**: From strict sender allowlists to human-in-the-loop approval, choose the right level of security for your use case.
* **Real-time webhook architecture**: Event-driven design means your agent reacts to emails in seconds, not minutes.
* **Webhook signature verification**: Built-in patterns for verifying Resend webhook signatures to prevent spoofed events.
* **Multi-language SDK support**: Works with Node.js, Python, Go, Ruby, PHP, Rust, Java, and .NET.
* **Common threat protection**: Built-in guidance for handling prompt injection, sender spoofing, and email flooding.

## Architecture

```
Email → Resend → Webhook → Your Server → Validate
                                             ↓
                                     Process or Reject
```

Your agent only processes emails that pass your chosen security level. Rejected emails are logged and silently acknowledged to prevent retries.

## Security Levels

Choose a security level before setting up your webhook endpoint. Start with **Level 1** and relax only if needed.

| Level | Name                 | Best For                                                  |
| ----- | -------------------- | --------------------------------------------------------- |
| **1** | Strict Allowlist     | Most use cases, only process emails from known senders    |
| **2** | Domain Allowlist     | Organization-wide access from trusted domains             |
| **3** | Content Filtering    | Accept from anyone, but filter unsafe patterns            |
| **4** | Sandboxed Processing | Process all emails with restricted agent capabilities     |
| **5** | Human-in-the-Loop    | Require human approval for actions from untrusted senders |

Each level includes full implementation code in the skill. After installation, your AI agent will have access to the detailed security patterns and can help you implement the right level.

## Example

A minimal webhook handler that verifies the signature, checks the sender against an allowlist, and retrieves the full email content:

```js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend(process.env.RESEND_API_KEY);
const ALLOWED_SENDERS = ['your@email.com'];

async function handler(req) {
  const payload = await req.text();

  const event = resend.webhooks.verify({
    payload,
    headers: {
      id: req.headers.get('svix-id'),
      timestamp: req.headers.get('svix-timestamp'),
      signature: req.headers.get('svix-signature'),
    },
    secret: process.env.RESEND_WEBHOOK_SECRET,
  });

  if (event.type === 'email.received') {
    if (!ALLOWED_SENDERS.includes(event.data.from.toLowerCase())) {
      return new Response('OK', { status: 200 });
    }

    const { data: email } = await resend.emails.receiving.get(
      event.data.email_id,
    );

    await processEmailForAgent(email);
  }

  return new Response('OK', { status: 200 });
}
```

## Learn More

<CardGroup cols={2}>
  <Card title="OpenClaw Setup Guide" icon="robot" href="/docs/openclaw-guide">
    Step-by-step guide for giving an OpenClaw agent a fully functional email
    inbox.
  </Card>

  <Card title="View on GitHub" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-skills/tree/main/skills/agent-email-inbox">
    See the full source code, security patterns, and documentation.
  </Card>
</CardGroup>
