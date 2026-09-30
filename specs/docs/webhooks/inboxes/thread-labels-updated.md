> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.thread.labels.updated

> Received when a label is applied to or removed from a thread.

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

  [Get early access](https://resend.com/help?type=report\&message=I+would+like+early+access+to+Inboxes.\&priority=low) if you're interested in testing this feature.

  <span />

  Once you have access, upgrade your Resend SDK to use the new methods:

  <CodeGroup>
    ```bash Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install resend@6.28.1-preview-inboxes.2
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.2
    ```
  </CodeGroup>
</Warning>

Event triggered whenever a **label is applied to or removed from a thread**.

*Note: Moving a thread to a label can send both this event and `inbox.thread.folder.updated` for the same thread.*

*Note: Deleting a label doesn't send this event for the threads that had it.*

<ResponseBodyParameters type="inbox.thread.labels.updated">
  <ParamField body="added" type="array">
    The labels applied, each with an `id`, `name`, and `color`. One event carries one label
  </ParamField>

  <ParamField body="removed" type="array">
    The labels removed, each with an `id`, `name`, and `color`. One event carries one label
  </ParamField>

  <ParamField body="source" type="api | dashboard | agent | system">
    What made the change
  </ParamField>

  <ParamField body="inbox_id" type="string">
    The ID of the inbox
  </ParamField>

  <ParamField body="thread_id" type="string">
    The ID of the thread
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
</ResponseBodyParameters>

<ResponseExample>
  ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "type": "inbox.thread.labels.updated",
    "created_at": "2026-09-29T12:00:00.000Z",
    "data": {
      "added": [
        {
          "id": "c0a8012e-3b4f-4d7a-9e21-5f6a7b8c9d0e",
          "name": "Billing",
          "color": "orange"
        }
      ],
      "removed": [],
      "source": "dashboard",
      "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "thread_id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
      "thread": {
        "object": "inbox_thread",
        "id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
        "subject": "Question about my invoice",
        "folder": "inbox",
        "labels": [
          {
            "id": "c0a8012e-3b4f-4d7a-9e21-5f6a7b8c9d0e",
            "name": "Billing",
            "color": "orange"
          }
        ],
        "read": false
      }
    }
  }
  ```
</ResponseExample>
