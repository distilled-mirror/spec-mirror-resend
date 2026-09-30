> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.updated

> Received when an inbox's settings change.

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

Event triggered whenever an **inbox's settings change**.

<ResponseBodyParameters type="inbox.updated">
  <ParamField body="source" type="api | dashboard | agent | system">
    What made the change
  </ParamField>

  <ParamField body="inbox_id" type="string">
    The ID of the inbox
  </ParamField>

  <ParamField body="inbox" type="object">
    The inbox, as it is when the webhook is sent

    <Expandable title="inbox object" defaultOpen>
      <ParamField body="object" type="string">
        Always `inbox`
      </ParamField>

      <ParamField body="id" type="string">
        The ID of the inbox
      </ParamField>

      <ParamField body="name" type="string">
        Internal name for the inbox. Recipients do not see it. Falls back to the inbox
        address
      </ParamField>

      <ParamField body="email_address" type="string">
        The address of the inbox
      </ParamField>

      <ParamField body="domain_id" type="string">
        The ID of the domain the inbox belongs to
      </ParamField>

      <ParamField body="receiving_address" type="string | null">
        The address to forward mail to when forwarding is enabled. `null` otherwise
      </ParamField>

      <ParamField body="friendly_name" type="string | null">
        The name recipients see when mail is sent from this inbox
      </ParamField>

      <ParamField body="unread" type="number">
        The number of unread threads in the inbox
      </ParamField>

      <ParamField body="created_at" type="string">
        ISO 8601 timestamp when the inbox was created
      </ParamField>
    </Expandable>
  </ParamField>
</ResponseBodyParameters>

<ResponseExample>
  ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "type": "inbox.updated",
    "created_at": "2026-09-29T12:00:00.000Z",
    "data": {
      "source": "dashboard",
      "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "inbox": {
        "object": "inbox",
        "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
        "name": "Customer Support",
        "email_address": "support@example.com",
        "domain_id": "d91cd9bd-1176-453e-8fc1-35364d380206",
        "receiving_address": null,
        "friendly_name": "Ada from Support",
        "unread": 3,
        "created_at": "2026-09-01T09:30:00.000Z"
      }
    }
  }
  ```
</ResponseExample>
