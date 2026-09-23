> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# OpenClaw Guide

> Learn how to give your AI agent an inbox to send and receive emails.

## Why give your agent an inbox

Giving your agent an inbox enables it to:

* **Sign up for its own accounts** to GitHub, hosting platforms, and more, so you don't need to share your own credentials.
* **Process attachments** (such as receipts and invoices) and act accordingly
* **Receive newsletters**, parse them, and send the most important information to you
* **Send you daily reports and digests**
* **Send and receive emails**

## How to set up an inbox for OpenClaw

### Step 1: Connect Resend

Add the remote MCP server, then sign in. This is the same setup as the [OpenClaw page](https://resend.com/openclaw).

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
openclaw mcp add resend --url https://mcp.resend.com/mcp --transport streamable-http
openclaw mcp login resend
```

Ask your agent to install the skills:

```
Let's get you set up with an email inbox! Install the resend-skills from https://github.com/resend/resend-skills and review them before continuing.
```

<Tip>
  Giving your agent the GitHub link helps it to install the latest version of
  the skill since OpenClaw skills operate differently than traditional agent
  skills.
</Tip>

Your agent may also benefit from installing the [Resend CLI](/docs/cli).

### Step 2: Get an API key

Your agent will ask you to create an API key.

<Tip>
  Your API key will be scoped to the team that's currently selected. If you'd
  like to sandbox your agent, create a new team just for your agent.
</Tip>

<Steps>
  <Step title="Open the API Keys dialog">
    Navigate to the [API Keys](https://resend.com/api-keys) page in Resend and
    click **Create API Key**.
  </Step>

  <Step title="Choose a name and permission scope">
    Choose a name for your API key and ensure **Full access** is selected as the
    permission scope.
  </Step>

  <Step title="Create the API key">
    Click **Add** to create the API key, and copy it to your clipboard.
  </Step>
</Steps>

We recommend not pasting API keys into the chat. Instead, use one of these two methods:

1. SSH into your agent's machine and **store the API key in an `.env` file**.
2. **Store the API key in a password manager** like 1Password, and give your agent access to its own vault. This can be done using a [1Password Service Account](https://developer.1password.com/docs/service-accounts/) on team plans.

### Step 3: Verify a domain

Next, your agent needs to know the email address it will use to send and receive emails. [Strongly consider](/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain) using a subdomain (`agent.example.com`) instead of the root domain (`example.com`), especially if you want to receive emails.

You can also use the [Resend CLI](/docs/cli) to verify a domain, although you will need to manually add the DNS records to your DNS provider.

<Steps>
  <Step title="Add a domain">
    Navigate to the [Domains tab](https://resend.com/domains) and click **Add
    Domain**.
  </Step>

  <Step title="Select a subdomain and region">
    Add the subdomain you want to verify, and choose the region that's closest
    to your agent.

    You may see one of three options:

    * **Auto Configure**: This will automatically configure the DNS records for you if your provider supports it.
    * **Go to (provider)**: This will take you to the provider's website to add the DNS records manually if we can detect your provider.
    * **I've added the records**: If we cannot detect your provider, you can manually add the DNS records by opening your DNS provider's website.

    If you want only to send emails with your agent, add the DNS records and confirm. If you want to also receive emails, continue to the next step to enable receiving (for autoconfigure, you can add receiving after you autoconfigure).
  </Step>

  <Step title="Enable receiving">
    **Receiving** allows your agent to receive emails at your domain, rather
    than simply sending. Scroll to the bottom of the page and toggle the switch
    to **On**.
  </Step>

  <Step title="Add the DNS records to your domain">
    Add the DNS records to your domain's DNS provider. For
    more guidance, see our [guides on adding DNS records to various
    providers](knowledge-base/introduction#dns-guides).
  </Step>

  <Step title="Wait for verification">
    Wait for the domain to be verified. This can take up to 72 hours, but is
    typically finished within a few minutes.
  </Step>
</Steps>

<Tip>
  For a more in-depth guide on domain verification, see our [guide on verifying
  a domain](/docs/dashboard/domains/introduction).
</Tip>

Once your domain is verified in Resend, you can use it to send (and receive) emails with your agent. Add the email address to your agent's memory and tell it to send you a test email to your own email address.

### Step 4: Use webhooks to receive emails

At this point, your agent can send emails, but **it can't receive emails yet**.

To receive, you need to set up a webhook.

<Steps>
  <Step title="Ask your agent to set up a webhook server">
    Your agent should be equipped to do this using the Resend skill. Prompt it to get started:

    ```
    I want you to be able to receive emails, too. Let's set up a webhook to receive emails at my domain using the agent email inbox agent skill.
    ```
  </Step>

  <Step title="Set up a tunnel">
    Your agent should spin up a local server and suggest using a tunneling tool
    to expose it to the internet. We recommend [Tailscale
    Funnel](https://tailscale.com/kb/1223/funnel):

    ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
    tailscale funnel 3000
    ```

    This gives your agent a stable public URL at
    `https://hostname.tailnet-name.ts.net`.
  </Step>

  <Step title="Give your agent access to secrets securely">
    When your agent asks for webhook signing secrets, give it access securely using one of the methods described in [Step 2: Get an API key](#step-2-get-an-api-key). Don't paste them directly into the chat.
  </Step>

  <Step title="Add the webhook to Resend">
    Ask your agent to register the webhook with Resend:

    ```
    Let's add a webhook to Resend using the server you just built. Use the email.received event, as instructed by the resend-skills agent skill, and securely save the returned webhook signing secret.
    ```
  </Step>

  <Step title="Test receiving an email">
    Send your agent a test email and ask it to check its inbox.
  </Step>
</Steps>

Your webhook server might look something like this:

```js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend(process.env.RESEND_API_KEY);

// Security: strict allowlist
const ALLOWED_SENDERS = ['your@email.com'];

async function handler(req) {
  const payload = await req.text();

  const id = req.headers.get('svix-id');
  const timestamp = req.headers.get('svix-timestamp');
  const signature = req.headers.get('svix-signature');

  if (!id || !timestamp || !signature) {
    return new Response('Missing headers', { status: 400 });
  }

  const event = resend.webhooks.verify({
    payload,
    headers: { id, timestamp, signature },
    webhookSecret: process.env.RESEND_WEBHOOK_SECRET,
  });

  if (event.type === 'email.received') {
    // Security check
    if (!ALLOWED_SENDERS.includes(event.data.from.toLowerCase())) {
      return new Response('OK', { status: 200 });
    }

    // Get full email
    const { data: email } = await resend.emails.receiving.get(
      event.data.email_id,
    );

    // Notify user instantly
    await notifyUser(email);
  }

  return new Response('OK', { status: 200 });
}
```

<Info>
  For more help working with inbound emails, including how to see the full email
  body, attachments, and more, see our [guide on receiving emails with
  Resend](/docs/dashboard/receiving/introduction).
</Info>

### Step 5: Hook into OpenClaw's APIs for instant notifications

One of the benefits of using Resend over other tools is that you don't need to constantly ask your agent to check its inbox, or rely on cron jobs to check every so often. With Resend, you can use OpenClaw's Gateway API to be notified instantly when your agent receives an email.

<Steps>
  <Step title="Ask your agent to hook into the Gateway API">
    ```text theme={"theme":{"light":"github-light","dark":"vesper"}}
    Use the OpenClaw Gateway API to notify me instantly when you receive an email webhook call from Resend. Use the resend-skills agent skill for guidance.
    ```
  </Step>

  <Step title="Test instant notifications">
    Send your agent another test email. It should notify you instantly.
  </Step>
</Steps>

## Security considerations

Giving your agent an inbox is incredibly powerful, but it also comes with some security concerns. The risk of prompt injection via email is a real concern.

The Resend Skill [includes security guidelines](https://github.com/resend/resend-skills/blob/main/skills/agent-email-inbox/SKILL.md#security-levels). Use the leveled security approach below to decide which security level is right for your use case.

1. **Strict Allowlist**: Only allow emails from specific senders. **Recommended for most use cases**.
2. **Domain Allowlist**: Allow emails from any sender from a given domain (e.g. anyone from `example.com`).
3. **Content Filtering with Sanitization**: Accept emails from anyone, but sanitize content to remove potential injection attempts.
4. **Sandboxed Processing**: Process all emails but in a restricted context where the agent has limited capabilities.
5. **Human-in-the-Loop**: Process all emails but require human approval for each email.

In general, we recommend starting with the **Strict Allowlist** and gradually decreasing security if needed. Review additional security best practices in the [Resend Skill](https://github.com/resend/resend-skills/blob/main/skills/agent-email-inbox/SKILL.md#security-levels).

If you have any questions, please [contact support](https://resend.com/help).
