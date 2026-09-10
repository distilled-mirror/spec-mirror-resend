> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Chat SDK Attachments

> Handle inbound email attachments with the Chat SDK adapter.

When someone sends an email with file attachments, the adapter makes them available on `message.raw.attachments`. Each attachment includes the filename, MIME type, and a URL to download the content.

## Attachment shape

```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
interface ResendAttachment {
  filename: string;
  contentType: string;
  url?: string;
}
```

| Field         | Type     | Description                                      |
| ------------- | -------- | ------------------------------------------------ |
| `filename`    | `string` | Original filename (e.g., `invoice.pdf`)          |
| `contentType` | `string` | MIME type (e.g., `application/pdf`)              |
| `url`         | `string` | Optional download URL for the attachment content |

## Detecting and processing attachments

```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
chat.onNewMention(async (thread, message) => {
  const attachments = message.raw?.attachments ?? [];

  if (attachments.length === 0) {
    await thread.subscribe();
    await thread.post('Got your email — no attachments found.');
    return;
  }

  const summary = attachments
    .map((a) => `${a.filename} (${a.contentType})`)
    .join(', ');

  await thread.subscribe();
  await thread.post(`Received ${attachments.length} attachment(s): ${summary}`);
});
```

For more on receiving email attachments outside the Chat SDK, see [Receiving Attachments](/docs/dashboard/receiving/attachments).

## Try it yourself

<Card title="Attachments Example" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-chat-sdk/tree/main/examples/attachments">
  Detects attachments and replies with a summary
</Card>
