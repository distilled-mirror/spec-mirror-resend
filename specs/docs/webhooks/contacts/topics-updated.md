> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# contact.topics.updated

> Received when a contact's topic subscriptions change.

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

Event triggered whenever a **contact's topic subscriptions change**.

<ResponseBodyParameters type="contact.topics.updated">
  <ParamField body="email" type="string">
    Contact's email address
  </ParamField>

  <ParamField body="topics" type="array">
    Topics changed in this update, each with its new subscription

    <Expandable title="topic object" defaultOpen>
      <ParamField body="id" type="string">
        Unique identifier for the topic
      </ParamField>

      <ParamField body="subscription" type="opt_in | opt_out">
        The contact's new subscription to the topic
      </ParamField>
    </Expandable>
  </ParamField>
</ResponseBodyParameters>

<ResponseExample>
  ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "type": "contact.topics.updated",
    "created_at": "2026-02-12T10:00:00.000Z",
    "data": {
      "email": "steve.wozniak@gmail.com",
      "topics": [
        {
          "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
          "subscription": "opt_in"
        },
        {
          "id": "07d84122-7224-4881-9c31-1c048e204602",
          "subscription": "opt_out"
        }
      ]
    }
  }
  ```
</ResponseExample>
