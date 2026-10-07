> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.draft.created

> Received when a draft is created.

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
    npm install resend@6.32.1-preview-inboxes.2
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.4
    ```
  </CodeGroup>
</Warning>

Event triggered whenever a **draft is created**, standalone or reply.

<ResponseBodyParameters type="inbox.draft.created">
  <ParamField body="source" type="api | dashboard | agent | system">
    What made the change
  </ParamField>

  <ParamField body="inbox_id" type="string">
    The ID of the inbox
  </ParamField>

  <ParamField body="thread_id" type="string">
    The ID of the thread. Only on reply drafts
  </ParamField>

  <ParamField body="draft_id" type="string">
    The ID of the draft
  </ParamField>

  <ParamField body="thread" type="object">
    The thread, as it is when the webhook is sent. Only on reply drafts

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

  <ParamField body="draft" type="object">
    The draft, as it is when the webhook is sent, without `html` or `text`. Fetch the body with [Retrieve Draft](/docs/api-reference/inboxes/get-draft)

    <Expandable title="draft object" defaultOpen>
      <ParamField body="object" type="string">
        Always `inbox_draft`
      </ParamField>

      <ParamField body="id" type="string">
        The ID of the draft
      </ParamField>

      <ParamField body="type" type="standalone | reply">
        `standalone` for a new conversation, or `reply`
      </ParamField>

      <ParamField body="to" type="string[] | null">
        Recipients
      </ParamField>

      <ParamField body="cc" type="string[]">
        CC recipients
      </ParamField>

      <ParamField body="bcc" type="string[]">
        BCC recipients
      </ParamField>

      <ParamField body="subject" type="string | null">
        The subject
      </ParamField>

      <ParamField body="thread_id" type="string | null">
        The Thread ID when this draft is a reply. `null` otherwise
      </ParamField>

      <ParamField body="reply_to_email_id" type="string | null">
        The Email ID being replied to. `null` otherwise
      </ParamField>

      <ParamField body="email_id" type="string | null">
        The queued outbound email after send. `null` until then
      </ParamField>

      <ParamField body="created_at" type="string">
        ISO 8601 timestamp when the draft was created
      </ParamField>

      <ParamField body="updated_at" type="string">
        ISO 8601 timestamp when the draft was last saved
      </ParamField>
    </Expandable>
  </ParamField>
</ResponseBodyParameters>

<ResponseExample>
  ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "type": "inbox.draft.created",
    "created_at": "2026-09-29T12:00:00.000Z",
    "data": {
      "source": "api",
      "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "thread_id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
      "draft_id": "9a2b7c4d-1e3f-4a5b-8c6d-0e1f2a3b4c5d",
      "thread": {
        "object": "inbox_thread",
        "id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
        "subject": "Question about my invoice",
        "folder": "inbox",
        "labels": [],
        "read": false
      },
      "draft": {
        "object": "inbox_draft",
        "id": "9a2b7c4d-1e3f-4a5b-8c6d-0e1f2a3b4c5d",
        "type": "reply",
        "to": ["steve.wozniak@gmail.com"],
        "cc": [],
        "bcc": [],
        "subject": "Re: Question about my invoice",
        "thread_id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
        "reply_to_email_id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
        "email_id": null,
        "created_at": "2026-09-29T11:58:00.000Z",
        "updated_at": "2026-09-29T12:00:00.000Z"
      }
    }
  }
  ```
</ResponseExample>
