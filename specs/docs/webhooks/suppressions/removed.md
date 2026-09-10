> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# suppression.removed

> Received when an email address is removed from your suppression list.

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

Event triggered whenever an **email address is removed from your suppression
list**.

<ResponseBodyParameters type="suppression.removed">
  <ParamField body="id" type="string">
    Unique identifier for the suppression
  </ParamField>

  <ParamField body="email" type="string">
    The suppressed email address
  </ParamField>

  <ParamField body="origin" type="string">
    How the address was suppressed: `bounce`, `complaint`, or `manual`
  </ParamField>

  <ParamField body="source_id" type="string | null">
    ID of the email that triggered the suppression. For suppressions with a
    `manual` origin, `source_id` is `null`
  </ParamField>

  <ParamField body="created_at" type="string">
    ISO 8601 timestamp when the suppression was created
  </ParamField>
</ResponseBodyParameters>

<ResponseExample>
  ```json theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "type": "suppression.removed",
    "created_at": "2026-11-17T19:32:22.980Z",
    "data": {
      "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
      "email": "steve.wozniak@gmail.com",
      "origin": "manual",
      "source_id": null,
      "created_at": "2026-11-15T08:12:45.120Z"
    }
  }
  ```
</ResponseExample>
