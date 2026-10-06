> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.draft.deleted

> Received when a draft is discarded.

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
    npm install resend@6.32.1-preview-inboxes.1
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.2
    ```
  </CodeGroup>
</Warning>

Event triggered whenever a **draft is discarded**.

*Note: The draft is already gone, so the payload has no `draft` object.*

<ResponseBodyParameters type="inbox.draft.deleted">
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
</ResponseBodyParameters>

<ResponseExample>
  ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "type": "inbox.draft.deleted",
    "created_at": "2026-09-29T12:00:00.000Z",
    "data": {
      "source": "dashboard",
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
      }
    }
  }
  ```
</ResponseExample>
