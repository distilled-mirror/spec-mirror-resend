> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# contact.updated

> Received when a contact is updated.

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

Event triggered whenever a **contact was successfully updated**.

<ResponseBodyParameters type="contact.updated">
  <ParamField body="id" type="string" required>
    Unique identifier for the contact
  </ParamField>

  <ParamField body="audience_id" type="string">
    Unique identifier for the audience this contact belongs to
  </ParamField>

  <ParamField body="segment_ids" type="array">
    Array of segment IDs the contact belongs to
  </ParamField>

  <ParamField body="created_at" type="string" required>
    ISO 8601 timestamp when the contact was created
  </ParamField>

  <ParamField body="updated_at" type="string" required>
    ISO 8601 timestamp when the contact was last updated
  </ParamField>

  <ParamField body="email" type="string" required>
    Contact's email address
  </ParamField>

  <ParamField body="first_name" type="string | null">
    Contact's first name. May be absent from the payload
  </ParamField>

  <ParamField body="last_name" type="string | null">
    Contact's last name. May be absent from the payload
  </ParamField>

  <ParamField body="unsubscribed" type="boolean" required>
    Whether the contact has unsubscribed from all emails sent from your team
  </ParamField>
</ResponseBodyParameters>

<ResponseExample>
  ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "type": "contact.updated",
    "created_at": "2026-10-11T23:47:56.678Z",
    "data": {
      "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
      "audience_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
      "segment_ids": ["78261eea-8f8b-4381-83c6-79fa7120f1cf"],
      "created_at": "2026-10-10T15:11:54.110Z",
      "updated_at": "2026-10-11T23:47:56.678Z",
      "email": "steve.wozniak@gmail.com",
      "first_name": "Steve",
      "last_name": "Wozniak",
      "unsubscribed": false
    }
  }
  ```
</ResponseExample>
