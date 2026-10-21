> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Chat SDK

> Build conversational email experiences using the Vercel Chat SDK and Resend.

# Resend Chat SDK Adapter

**Purpose:** Instructions for building bidirectional email bots using the `@resend/chat-sdk-adapter` package with the Vercel Chat SDK.

***

## Setup

### Prerequisites

* Resend API key stored in `RESEND_API_KEY` env var
* Verified domain at [https://resend.com/domains](https://resend.com/domains)
* Webhook configured for `email.received` events, or `inbox.email.received` events when you set `inboxId` or `inboxEmailAddress` (see [https://resend.com/docs/webhooks/introduction](https://resend.com/docs/webhooks/introduction))
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

| Parameter | Type | Required | Description |
| - | - | - | - |
| `fromAddress` | `string` | Yes | Sender email address |
| `fromName` | `string` | No | Display name for the From header |
| `apiKey` | `string` | No | Resend API key. Falls back to `RESEND_API_KEY` env var |
| `webhookSecret` | `string` | No | Webhook signing secret. Falls back to `RESEND_WEBHOOK_SECRET` env var |
| `inboxId` | `string` | No | Resend inbox ID. Handles `inbox.email.received` and replies in the inbox thread |
| `inboxEmailAddress` | `string` | No | Resend inbox email address. Works as `inboxId` does. Set one, not both |

***

## Threading

Threads are resolved automatically using `Message-ID`, `In-Reply-To`, and `References` headers. Reply chains are grouped into Chat SDK threads with no extra configuration.

Set `inboxId` or `inboxEmailAddress` to use an inbox, not both. With `inboxEmailAddress`, the adapter gets the inbox ID with `resend.inboxes.get()` on the first `inbox.email.received` event and keeps it. Each inbox thread maps to one Chat SDK thread with the ID `resend:{inboxId}:{threadId}`. The adapter fetches each email with `resend.inboxes.threads.emails.get()` and posts with `resend.inboxes.threads.emails.reply()`. Events for other inboxes and `email.received` events are ignored. A sender can set `Reply-To` to any address, so check `message.raw.replyTo` before replying with anything sensitive.

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
        type: 'actions',
        children: [
          {
            type: 'link-button',
            label: 'Track Order',
            url: 'https://example.com/track/1234',
          },
        ],
      },
    ],
  },
  fallbackText: 'Order #1234 confirmed',
});
```

Cards render to HTML via `react-email`. Always include `fallbackText` for plain-text clients.

***

## Proactive Outreach

Start a new email thread without waiting for inbound:

```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
const threadId = await resend.openDM('user@example.com');
await resend.postMessage(threadId, 'Hello from the bot!');
```

***

## Attachments

Inbound email attachments are available on `message.raw.attachments`:

```typescript theme={"theme":{"light":"github-light","dark":"vesper"}}
import type { ResendRawMessage } from '@resend/chat-sdk-adapter';

chat.onNewMention(async (thread, message) => {
  const raw = message.raw as ResendRawMessage;
  const attachments = raw.attachments ?? [];
  for (const file of attachments) {
    console.log(file.filename, file.contentType);
  }
});
```

For an inbox email, each attachment has `id`, `filename`, `size` and `contentType`. The `contentType` is always `application/octet-stream`.

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

The `@resend/chat-sdk-adapter` package is a [Vercel Chat SDK](https://github.com/nichochar/chat) adapter that turns email into a two-way communication channel via Resend. Receive inbound emails through webhooks, reply through the Resend API, and let the adapter handle threading automatically.

The adapter is open source and [available on GitHub](https://github.com/resend/resend-chat-sdk).

## Prerequisites

To get started, you'll need to:

* [Create an API key](https://resend.com/api-keys)
* [Verify your domain](https://resend.com/domains)
* [Set up webhooks](/docs/webhooks/introduction) for `email.received` events, or for `inbox.email.received` events when you [use an inbox](#use-an-inbox)
* [Enable receiving](/docs/dashboard/receiving/introduction) on your domain

## Guide

**1. Install**

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

**2. Configure the adapter**

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

> [!NOTE]
>
> Set `RESEND_API_KEY` and `RESEND_WEBHOOK_SECRET` as environment variables. You can also pass `apiKey` and `webhookSecret` directly in the config — explicit values take precedence over env vars.

**3. Handle inbound emails**

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

**4. Forward webhooks**

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

## How threading works

The adapter resolves threads using standard `Message-ID`, `In-Reply-To`, and `References` email headers. Reply chains are automatically grouped into Chat SDK threads, with no extra configuration needed.

> [!WARNING]
>
> Email is immutable. The following operations throw `NotImplementedError`: `editMessage`, `deleteMessage`, `addReaction`, `removeReaction`, and `startTyping`.

## Configuration options

| Parameter | Type | Required | Description |
| - | - | - | - |
| `fromAddress` | `string` | Yes | Sender email address |
| `fromName` | `string` | No | Display name for the From header |
| `apiKey` | `string` | No | Resend API key. Falls back to `RESEND_API_KEY` env var |
| `webhookSecret` | `string` | No | Webhook signing secret. Falls back to `RESEND_WEBHOOK_SECRET` env var |
| `inboxId` | `string` | No | Resend inbox ID. Handles `inbox.email.received` and replies in the inbox thread |
| `inboxEmailAddress` | `string` | No | Resend inbox email address. Works as `inboxId` does. Set one, not both |

## Use an inbox

Set `inboxId` or `inboxEmailAddress` to build the bot on a Resend [Inbox](/docs/api-reference/inboxes/create-inbox). The inbox groups email into threads, and the bot replies inside the thread. Resend sets the recipients and the threading headers.

```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
const resend = createResendAdapter({
  fromAddress: 'agent@example.com', // the inbox address
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
});
```

You can also select the inbox by its email address:

```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
const resend = createResendAdapter({
  fromAddress: 'agent@example.com',
  inboxEmailAddress: 'agent@example.com',
});
```

Set `inboxId` or `inboxEmailAddress`, not both. Setting both is a type error, and the adapter throws `Set inboxId or inboxEmailAddress, not both.` The `inbox.email.received` payload identifies the inbox by its ID. With `inboxEmailAddress`, the adapter gets the inbox ID with `resend.inboxes.get()` on the first `inbox.email.received` event and keeps it.

Subscribe your webhook to `inbox.email.received`. With an inbox set, the adapter:

* Handles `inbox.email.received` events for that inbox only, and ignores other inboxes and `email.received` events.
* Maps each inbox thread to one Chat SDK thread.
* Gives each attachment `id`, `filename`, `size` and `contentType` on `message.raw.attachments`. The `contentType` is always `application/octet-stream`.
* Replies to the last received email of the thread. The reply goes to the email's `Reply-To` addresses, or to its sender when it has none. It is sent from the inbox address, so `fromName` does not apply to it.

A sender can set `Reply-To` to any address. Check `message.raw.replyTo` before the bot replies with anything sensitive. `openDM()` still sends with `resend.emails.send()` from `fromAddress`.

The inbox mode needs `@resend/chat-sdk-adapter` 0.5.0 or later and `resend` 6.34.1 or later.

## Features

> **[Card Emails](/docs/chat-sdk-card-emails)**
>
> Send rich HTML emails with structured card elements.

> **[Attachments](/docs/chat-sdk-attachments)**
>
> Handle inbound email attachments.

> **[Proactive Outreach](/docs/chat-sdk-proactive-outreach)**
>
> Start new email threads without waiting for inbound.

## Examples

> **[Basic](https://github.com/resend/resend-chat-sdk/tree/main/examples/basic)**
>
> Echo bot that replies to every email

> **[Welcome Cards](https://github.com/resend/resend-chat-sdk/tree/main/examples/welcome-cards)**
>
> Styled card email on first contact

> **[Notifications](https://github.com/resend/resend-chat-sdk/tree/main/examples/notifications)**
>
> Proactive outbound via openDM and HTTP POST

> **[Support Bot](https://github.com/resend/resend-chat-sdk/tree/main/examples/support-bot)**
>
> Multi-turn conversations with subscribe/unsubscribe

> **[Attachments](https://github.com/resend/resend-chat-sdk/tree/main/examples/attachments)**
>
> Detect attachments and reply with a summary
