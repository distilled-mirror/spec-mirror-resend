> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Chat SDK Attachments

> Handle inbound email attachments with the Chat SDK adapter.

When someone sends an email with file attachments, the adapter makes them available on `message.raw.attachments`. The adapter does not download the attachment content.

* An attachment of an `email.received` email has `filename` and `contentType`.
* An attachment of an inbox email has `id`, `filename`, `size` and `contentType`. The inbox API does not return the MIME type, so `contentType` is always `application/octet-stream`.

## Attachment shape

```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
interface ResendAttachment {
  content?: string;
  contentType: string;
  filename: string;
  id?: string;
  size?: number;
  url?: string;
}
```

| Field | Type | Description |
| - | - | - |
| `content` | `string` | Base64-encoded content. The adapter does not set it |
| `contentType` | `string` | MIME type (e.g., `application/pdf`). Always `application/octet-stream` for an inbox email |
| `filename` | `string` | Original filename (e.g., `invoice.pdf`) |
| `id` | `string` | Attachment ID. Set on inbox emails only |
| `size` | `number` | Size in bytes. Set on inbox emails only |
| `url` | `string` | Download URL. The adapter does not set it |

## Detecting and processing attachments

```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
import type { ResendRawMessage } from '@resend/chat-sdk-adapter';

chat.onNewMention(async (thread, message) => {
  const raw = message.raw as ResendRawMessage;
  const attachments = raw.attachments ?? [];

  if (attachments.length === 0) {
    await thread.subscribe();
    await thread.post('Got your email. No attachments found.');
    return;
  }

  const summary = attachments
    .map((a) => `${a.filename} (${a.contentType})`)
    .join(', ');

  await thread.subscribe();
  await thread.post(`Received ${attachments.length} attachment(s): ${summary}`);
});
```

For more on receiving email attachments outside the Chat SDK, see [Receiving Attachments](https://resend.com/docs/dashboard/receiving/attachments.md).

## Try it yourself

> [card] [Attachments Example](https://github.com/resend/resend-chat-sdk/tree/main/examples/attachments)
>
> Detects attachments and replies with a summary
