> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.email.sent

> Received when an outbound email is accepted for delivery and added to a thread.

export const ResponseBodyParameters = ({type, children}) => {
  return <div>
      <h2>Response Body Parameters</h2>
      <p>
        All webhook payloads follow a consistent top-level structure with
        event-specific data nested within the <code>data</code> object.
      </p>
      <ParamField body="type" type="string">
        The event type that triggered the webhook (e.g., <code>{type}</code>).
      </ParamField>
      <ParamField body="created_at" type="string">
        ISO 8601 timestamp when the webhook event was created.
      </ParamField>
      <ParamField body="data" type="object">
        Event-specific data containing detailed information about the event. The
        data object for the <code>{type}</code> event contains the following
        parameters:
        <Expandable defaultOpen title="object parameters">
          {children}
        </Expandable>
      </ParamField>
    </div>;
};

<Warning>
  Inboxes are currently in private beta and only available to a limited
  number of users. The response shape might change before GA.

  <span />

  [Get early access](https://resend.com/settings/labs) if you're interested in testing this feature.

  <span />

  Once you have access, upgrade your Resend SDK to use the new methods:

  <CodeGroup>
    ```bash Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install resend@6.32.1-preview-inboxes.4
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.6
    ```
  </CodeGroup>
</Warning>

Event triggered whenever an **outbound email is accepted for delivery** and added to a thread.

*Note: `source` is always `system`, because the email pipeline sends this event, even when the API or an agent sent the email.*

*Note: When the email comes from a draft, `inbox.draft.sent` fires first, from the send call. This event follows once the email is accepted for delivery.*

<ResponseBodyParameters type="inbox.email.sent">
  <ParamField body="source" type="api | dashboard | agent | system">
    What made the change
  </ParamField>

  <ParamField body="inbox_id" type="string">
    The ID of the inbox
  </ParamField>

  <ParamField body="thread_id" type="string">
    The ID of the thread
  </ParamField>

  <ParamField body="email_id" type="string">
    The ID of the email
  </ParamField>

  <ParamField body="thread" type="object">
    The thread, as it is when the webhook is sent

    <Expandable title="thread object" defaultOpen>
      <ParamField body="object" type="string">
        Always `inbox_thread`
      </ParamField>

      <ParamField body="id" type="string">
        The ID of the thread
      </ParamField>

      <ParamField body="subject" type="string | null">
        The subject of the thread
      </ParamField>

      <ParamField body="folder" type="inbox | archive | spam | sent | trash">
        The folder the thread lives in
      </ParamField>

      <ParamField body="labels" type="array">
        The labels attached to the thread, each with an `id`, `name`, and `color`
      </ParamField>

      <ParamField body="read" type="boolean">
        True only when every message in the thread is read
      </ParamField>
    </Expandable>
  </ParamField>

  <ParamField body="email" type="object">
    The email, as it is when the webhook is sent, without `html` or `text`. Fetch the body with [Retrieve Thread Email](/docs/api-reference/inboxes/get-thread-email)

    <Expandable title="email object" defaultOpen>
      <ParamField body="id" type="string">
        The ID of the email
      </ParamField>

      <ParamField body="direction" type="inbound | outbound">
        Whether the email was received by the inbox or sent from it
      </ParamField>

      <ParamField body="from" type="string">
        Sender email address
      </ParamField>

      <ParamField body="to" type="string[]">
        The recipients of the email
      </ParamField>

      <ParamField body="cc" type="string[]">
        The CC recipients of the email
      </ParamField>

      <ParamField body="bcc" type="string[]">
        The BCC recipients of the email
      </ParamField>

      <ParamField body="reply_to" type="string[]">
        The Reply-To addresses
      </ParamField>

      <ParamField body="subject" type="string | null">
        The subject of the email
      </ParamField>

      <ParamField body="message_id" type="string | null">
        The Message-ID header of the email
      </ParamField>

      <ParamField body="attachments" type="array">
        The attachments on the email

        <Expandable title="attachment object" defaultOpen>
          <ParamField body="id" type="string">
            The ID of the attachment
          </ParamField>

          <ParamField body="filename" type="string | null">
            The filename of the attachment
          </ParamField>

          <ParamField body="size" type="number | null">
            The size of the attachment in bytes
          </ParamField>
        </Expandable>
      </ParamField>

      <ParamField body="read" type="boolean">
        Whether the email has been read
      </ParamField>

      <ParamField body="received_at" type="string">
        ISO 8601 timestamp when the email arrived or was sent
      </ParamField>
    </Expandable>
  </ParamField>
</ResponseBodyParameters>

<ResponseExample>
  ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "type": "inbox.email.sent",
    "created_at": "2026-09-29T12:00:00.000Z",
    "data": {
      "source": "system",
      "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "thread_id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
      "email_id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
      "thread": {
        "object": "inbox_thread",
        "id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
        "subject": "Question about my invoice",
        "folder": "inbox",
        "labels": [],
        "read": true
      },
      "email": {
        "id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
        "direction": "outbound",
        "from": "Ada from Support <support@example.com>",
        "to": ["steve.wozniak@gmail.com"],
        "cc": [],
        "bcc": [],
        "reply_to": [],
        "subject": "Re: Question about my invoice",
        "message_id": "<0100019a4ef9a417@email.amazonses.com>",
        "attachments": [],
        "read": true,
        "received_at": "2026-09-29T12:00:00.000Z"
      }
    }
  }
  ```
</ResponseExample>
