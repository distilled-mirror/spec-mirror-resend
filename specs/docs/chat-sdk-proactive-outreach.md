> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Chat SDK Proactive Outreach

> Start new email conversations proactively with the Chat SDK adapter.

By default, the Chat SDK adapter responds to inbound emails. With `openDM`, you can go the other way and start a new email thread with any address, without waiting for them to email you first.

## Sending a proactive email

Call `openDM` on the adapter from `createResendAdapter` to create a new thread. Then call `postMessage` to send a message to the thread.

```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
const threadId = await resend.openDM('user@example.com');
await resend.postMessage(threadId, 'Hello from the bot!');
```

You can also send card emails in proactive threads. The same card structure from [Card Emails](/docs/chat-sdk-card-emails) works here.

## Triggering via HTTP

A common pattern is exposing an HTTP endpoint that triggers outbound emails. This lets external systems (cron jobs, webhooks from other services, admin dashboards) send emails through your bot.

```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
import type { IncomingMessage, ServerResponse } from 'node:http';

async function readBody(req: IncomingMessage): Promise<string> {
  const chunks: Buffer[] = [];
  for await (const chunk of req) {
    chunks.push(Buffer.from(chunk));
  }
  return Buffer.concat(chunks).toString();
}

async function handleNotify(req: IncomingMessage, res: ServerResponse) {
  const { to, message } = JSON.parse(await readBody(req));

  const threadId = await resend.openDM(to);
  await resend.postMessage(threadId, message);

  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({ ok: true, threadId }));
}
```

Then call it:

```bash theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST http://localhost:3000/notify \
  -H "Content-Type: application/json" \
  -d '{"to": "user@example.com", "message": "Your order has shipped!"}'
```

## When to use this

* Welcome emails when a user signs up
* Order confirmations and shipping updates
* Alert notifications (monitoring, billing, security)
* Scheduled digests or reminders

If the recipient replies, the response arrives through the normal `onNewMention` or `onSubscribedMessage` handlers, and the threading is handled automatically.

## Try it yourself

<Card title="Notifications Example" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-chat-sdk/tree/main/examples/notifications">
  Proactive outbound emails via openDM and an HTTP POST endpoint
</Card>
