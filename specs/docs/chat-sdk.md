> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Chat SDK

> Build conversational email experiences using the Vercel Chat SDK and Resend.

<Prompt description="Use this pre-built prompt with your AI agent to build with the Resend Chat SDK adapter." icon="comments" iconType="solid" actions={["copy", "cursor"]}>
  # Resend Chat SDK Adapter

  **Purpose:** Instructions for building bidirectional email bots using the `@resend/chat-sdk-adapter` package with the Vercel Chat SDK.

  ***

  ## Setup

  ### Prerequisites

  * Resend API key stored in `RESEND_API_KEY` env var
  * Verified domain at [https://resend.com/domains](https://resend.com/domains)
  * Webhook configured for `email.received` events (see [https://resend.com/docs/webhooks/introduction](https://resend.com/docs/webhooks/introduction))
  * Inbound email receiving enabled (see [https://resend.com/docs/dashboard/receiving/introduction](https://resend.com/docs/dashboard/receiving/introduction))

  ### Install

  ```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
  npm install @resend/chat-sdk-adapter chat @chat-adapter/state-memory
  # or: yarn add / pnpm add / bun add
  ```

  ### Initialize

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { createResendAdapter } from '@resend/chat-sdk-adapter';
  import { MemoryStateAdapter } from '@chat-adapter/state-memory';
  import { Chat } from 'chat';

  const resend = createResendAdapter({
    fromAddress: 'bot@example.com',
    fromName: 'My Bot', // optional
    // apiKey: "re_...",       // or set RESEND_API_KEY env var
    // webhookSecret: "whsec_..." // or set RESEND_WEBHOOK_SECRET env var
  });

  const chat = new Chat({
    userName: 'email-bot',
    adapters: { resend },
    state: new MemoryStateAdapter(),
  });
  ```

  ### Handle Inbound Emails

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  // New email (new thread)
  chat.onNewMention(async (thread, message) => {
    await thread.subscribe();
    await thread.post(`Got your email: ${message.text}`);
  });

  // Follow-up email in a subscribed thread
  chat.onSubscribedMessage(async (thread, message) => {
    await thread.post(`Reply: ${message.text}`);
  });
  ```

  ### Forward Webhooks

  Point Resend webhooks to your server's `/webhook` endpoint. The adapter handles verification and parsing.

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  // Inside your HTTP server handler for POST /webhook
  const result = await chat.webhooks.resend(request);
  ```

  `request` must be a Web `Request` object. If you're using Node.js `http`, convert `IncomingMessage` to a `Request` first.

  ***

  ## Configuration

  | Parameter       | Type     | Required | Description                                                           |
  | --------------- | -------- | -------- | --------------------------------------------------------------------- |
  | `fromAddress`   | `string` | Yes      | Sender email address                                                  |
  | `fromName`      | `string` | No       | Display name for the From header                                      |
  | `apiKey`        | `string` | No       | Resend API key. Falls back to `RESEND_API_KEY` env var                |
  | `webhookSecret` | `string` | No       | Webhook signing secret. Falls back to `RESEND_WEBHOOK_SECRET` env var |

  ***

  ## Threading

  Threads are resolved automatically using `Message-ID`, `In-Reply-To`, and `References` headers. Reply chains are grouped into Chat SDK threads with no extra configuration.

  ***

  ## Card Emails

  Send rich HTML emails using Card elements:

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  await thread.post({
    card: {
      type: 'card',
      title: 'Order Confirmed',
      children: [
        { type: 'text', content: 'Your order #1234 has been shipped.' },
        { type: 'divider' },
        {
          type: 'link-button',
          label: 'Track Order',
          url: 'https://example.com/track/1234',
        },
      ],
    },
    fallbackText: 'Order #1234 confirmed',
  });
  ```

  Cards render to HTML via `@react-email/components`. Always include `fallbackText` for plain-text clients.

  ***

  ## Proactive Outreach

  Start a new email thread without waiting for inbound:

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  const threadId = await chat.adapters.resend.openDM('user@example.com');
  const thread = await chat.thread('resend', threadId);
  await thread.post('Hello from the bot!');
  ```

  ***

  ## Attachments

  Inbound email attachments are available on `message.raw.attachments`:

  ```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
  chat.onNewMention(async (thread, message) => {
    const attachments = message.raw?.attachments ?? [];
    for (const file of attachments) {
      console.log(file.filename, file.contentType, file.url);
    }
  });
  ```

  ***

  ## Unsupported Operations

  Email is immutable. These operations throw `NotImplementedError`:

  * `editMessage` / `deleteMessage`
  * `addReaction` / `removeReaction`
  * `startTyping`

  ***

  ## AI Model Instructions

  1. **Always** use `createResendAdapter` from `@resend/chat-sdk-adapter`
  2. **Always** store API keys in env vars, never hardcode
  3. **Always** call `thread.subscribe()` in `onNewMention` if you want to receive follow-ups
  4. **Always** include `fallbackText` when sending card emails
  5. **Never** attempt `editMessage`, `deleteMessage`, `addReaction`, `removeReaction`, or `startTyping` — email does not support these
  6. The webhook handler expects a Web `Request` object — convert Node.js `IncomingMessage` if needed
  7. The adapter name in Chat config must be `"resend"` for thread routing to work

  For the full Resend docs: [https://resend.com/docs/llms-full.txt](https://resend.com/docs/llms-full.txt)
</Prompt>

The `@resend/chat-sdk-adapter` package is a [Vercel Chat SDK](https://github.com/nichochar/chat) adapter that turns email into a two-way communication channel via Resend. Receive inbound emails through webhooks, reply through the Resend API, and let the adapter handle threading automatically.

The adapter is open source and [available on GitHub](https://github.com/resend/resend-chat-sdk).

## Prerequisites

To get started, you'll need to:

* [Create an API key](https://resend.com/api-keys)
* [Verify your domain](https://resend.com/domains)
* [Set up webhooks](/docs/webhooks/introduction) for `email.received` events
* [Enable receiving](/docs/dashboard/receiving/introduction) on your domain

## Guide

<Steps>
  <Step title="Install">
    <CodeGroup>
      ```bash npm theme={"theme":{"light":"github-light","dark":"vesper"}}
      npm install @resend/chat-sdk-adapter chat @chat-adapter/state-memory
      ```

      ```bash yarn theme={"theme":{"light":"github-light","dark":"vesper"}}
      yarn add @resend/chat-sdk-adapter chat @chat-adapter/state-memory
      ```

      ```bash pnpm theme={"theme":{"light":"github-light","dark":"vesper"}}
      pnpm add @resend/chat-sdk-adapter chat @chat-adapter/state-memory
      ```

      ```bash bun theme={"theme":{"light":"github-light","dark":"vesper"}}
      bun add @resend/chat-sdk-adapter chat @chat-adapter/state-memory
      ```
    </CodeGroup>
  </Step>

  <Step title="Configure the adapter">
    Create a Resend adapter and pass it with [adapter configuration options](#configuration-options) to the Chat SDK.

    ```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
    import { createResendAdapter } from '@resend/chat-sdk-adapter';
    import { MemoryStateAdapter } from '@chat-adapter/state-memory';
    import { Chat } from 'chat';

    const resend = createResendAdapter({
      fromAddress: 'bot@example.com',
      fromName: 'My Bot',
    });

    const chat = new Chat({
      userName: 'email-bot',
      adapters: { resend },
      state: new MemoryStateAdapter(),
    });
    ```

    <Info>
      Set `RESEND_API_KEY` and `RESEND_WEBHOOK_SECRET` as environment variables. You can also pass `apiKey` and `webhookSecret` directly in the config — explicit values take precedence over env vars.
    </Info>
  </Step>

  <Step title="Handle inbound emails">
    Register handlers for incoming emails. `onNewMention` fires when a new thread starts, and `onSubscribedMessage` fires for follow-up emails in threads you've subscribed to.

    ```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
    chat.onNewMention(async (thread, message) => {
      console.log(`New email from ${message.author.userId}: ${message.text}`);
      await thread.subscribe();
      await thread.post(`Got your email: ${message.text}`);
    });

    chat.onSubscribedMessage(async (thread, message) => {
      await thread.post(`Reply: ${message.text}`);
    });
    ```
  </Step>

  <Step title="Forward webhooks">
    Point your Resend webhooks to your server's `/webhook` endpoint. The adapter verifies the signature and parses the payload.

    ```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
    if (req.method === 'POST' && req.url === '/webhook') {
      const result = await chat.webhooks.resend(request);
      res.writeHead(result.status);
      res.end();
    }
    ```

    The handler expects a Web `Request` object. If you're using Node.js `http`, convert `IncomingMessage` to a `Request` first. See the [basic example](https://github.com/resend/resend-chat-sdk/tree/main/examples/basic) for a full working server.

    For webhook setup details, see [Managing Webhooks](/docs/webhooks/introduction) and [Verify Webhook Requests](/docs/webhooks/verify-webhooks-requests).
  </Step>
</Steps>

## How threading works

The adapter resolves threads using standard `Message-ID`, `In-Reply-To`, and `References` email headers. Reply chains are automatically grouped into Chat SDK threads, with no extra configuration needed.

<Warning>
  Email is immutable. The following operations throw `NotImplementedError`: `editMessage`, `deleteMessage`, `addReaction`, `removeReaction`, and `startTyping`.
</Warning>

## Configuration options

| Parameter       | Type     | Required | Description                                                           |
| --------------- | -------- | -------- | --------------------------------------------------------------------- |
| `fromAddress`   | `string` | Yes      | Sender email address                                                  |
| `fromName`      | `string` | No       | Display name for the From header                                      |
| `apiKey`        | `string` | No       | Resend API key. Falls back to `RESEND_API_KEY` env var                |
| `webhookSecret` | `string` | No       | Webhook signing secret. Falls back to `RESEND_WEBHOOK_SECRET` env var |

## Features

<CardGroup cols={3}>
  <Card title="Card Emails" icon="palette" href="/docs/chat-sdk-card-emails">
    Send rich HTML emails with structured card elements.
  </Card>

  <Card title="Attachments" icon="paperclip" href="/docs/chat-sdk-attachments">
    Handle inbound email attachments.
  </Card>

  <Card title="Proactive Outreach" icon="paper-plane" href="/docs/chat-sdk-proactive-outreach">
    Start new email threads without waiting for inbound.
  </Card>
</CardGroup>

## Examples

<CardGroup cols={3}>
  <Card title="Basic" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-chat-sdk/tree/main/examples/basic">
    Echo bot that replies to every email
  </Card>

  <Card title="Welcome Cards" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-chat-sdk/tree/main/examples/welcome-cards">
    Styled card email on first contact
  </Card>

  <Card title="Notifications" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-chat-sdk/tree/main/examples/notifications">
    Proactive outbound via openDM and HTTP POST
  </Card>

  <Card title="Support Bot" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-chat-sdk/tree/main/examples/support-bot">
    Multi-turn conversations with subscribe/unsubscribe
  </Card>

  <Card title="Attachments" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-chat-sdk/tree/main/examples/attachments">
    Detect attachments and reply with a summary
  </Card>
</CardGroup>
