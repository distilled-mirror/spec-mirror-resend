> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# topic.created

> Received when a topic is created.

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

Event triggered whenever a **topic is created**.

<ResponseBodyParameters type="topic.created">
  <ParamField body="id" type="string">
    Unique identifier for the topic
  </ParamField>

  <ParamField body="name" type="string">
    The topic name
  </ParamField>

  <ParamField body="description" type="string | null">
    The topic description
  </ParamField>

  <ParamField body="default_subscription" type="opt_in | opt_out">
    The default subscription preference for new contacts
  </ParamField>

  <ParamField body="deleted" type="boolean">
    Whether the topic was deleted
  </ParamField>

  <ParamField body="created_at" type="string">
    ISO 8601 timestamp when the topic was created
  </ParamField>

  <ParamField body="updated_at" type="string">
    ISO 8601 timestamp when the topic was last updated
  </ParamField>
</ResponseBodyParameters>

<ResponseExample>
  ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "type": "topic.created",
    "created_at": "2026-02-12T10:00:00.000Z",
    "data": {
      "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
      "name": "Product Updates",
      "description": "New features and improvements",
      "default_subscription": "opt_in",
      "deleted": false,
      "created_at": "2026-02-12T10:00:00.000Z",
      "updated_at": "2026-02-12T10:00:00.000Z"
    }
  }
  ```
</ResponseExample>
