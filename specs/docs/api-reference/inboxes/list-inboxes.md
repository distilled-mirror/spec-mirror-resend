> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Inboxes

> Retrieve a list of inboxes for the authenticated user.

export const QueryParams = ({type, isRequired}) => {
  return <>
      <h2>Query Parameters</h2>

      {isRequired ? <ParamField query="limit" type="number">
          Number of {type} to retrieve.
          <ul>
            <li>
              Default value: <code>20</code>
            </li>
            <li>
              Maximum value: <code>100</code>
            </li>
            <li>
              Minimum value: <code>1</code>
            </li>
          </ul>
        </ParamField> : <>
          <p>
            Note that the <code>limit</code> parameter is <em>optional</em>. If
            you do not provide a <code>limit</code>, all {type} will be returned
            in a single response.
          </p>
          <ParamField query="limit" type="number">
            Number of {type} to retrieve.
            <ul>
              <li>
                Maximum value: <code>100</code>
              </li>
              <li>
                Minimum value: <code>1</code>
              </li>
            </ul>
          </ParamField>
        </>}

      <ParamField query="after" type="string">
        The ID <em>after</em> which we'll retrieve more {type} (for pagination).
        This ID will <em>not</em> be included in the returned list. Cannot be
        used with the
        <code>before</code> parameter.
      </ParamField>
      <ParamField query="before" type="string">
        The ID <em>before</em> which we'll retrieve more {type} (for
        pagination). This ID will <em>not</em> be included in the returned list.
        Cannot be used with the <code>after</code> parameter.
      </ParamField>
      <Info>
        You can only use either <code>after</code> or <code>before</code>{' '}
        parameter, not both. See our{' '}
        <a href="/docs/api-reference/pagination">pagination guide</a> for more
        information.
      </Info>
    </>;
};

<Warning>
  Inboxes are currently in private beta and only available to a limited
  number of users. The response shape might change before GA. [Get in
  touch](https://resend.com/help) if you're interested in testing this
  feature.

  <span />

  Once you have access, upgrade your Resend SDK to use the methods on this
  page:

  <CodeGroup>
    ```bash Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install resend@6.28.1-preview-inboxes.1
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.1
    ```
  </CodeGroup>
</Warning>

Inboxes are returned newest first. Results are paginated with cursors. See
[Pagination](/docs/api-reference/pagination) for how `after` and `before` work.

<QueryParams type="inboxes" isRequired={true} />

## Response Fields

<ParamField body="object" type="string">
  Always `list`.
</ParamField>

<ParamField body="has_more" type="boolean">
  Whether more inboxes exist beyond this page.
</ParamField>

<ParamField body="data" type="array">
  The inboxes on this page.

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="id" type="string">
      The ID of the inbox.
    </ParamField>

    <ParamField body="name" type="string | null">
      Internal name for the inbox. Recipients do not see it.
    </ParamField>

    <ParamField body="email_address" type="string">
      The address of the inbox.
    </ParamField>

    <ParamField body="friendly_name" type="string | null">
      The name recipients see when mail is sent from this inbox. A plain name,
      not a `Name <email>` address.
    </ParamField>

    <ParamField body="unread" type="number">
      The number of unread threads in the inbox.
    </ParamField>

    <ParamField body="last_received" type="string | null">
      ISO 8601 timestamp when a thread in this inbox was last active.
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.list();
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/inboxes' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend inboxes list
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "has_more": false,
    "data": [
      {
        "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
        "name": "Customer Support",
        "email_address": "support@example.com",
        "friendly_name": "Ada from Support",
        "unread": 3,
        "last_received": "2026-08-05T14:03:11.229Z"
      },
      {
        "id": "1c5e0f3a-6b21-4d9a-8e77-5c0a9d8b4e12",
        "name": "billing@example.com",
        "email_address": "billing@example.com",
        "friendly_name": null,
        "unread": 0,
        "last_received": null
      }
    ]
  }
  ```
</ResponseExample>
