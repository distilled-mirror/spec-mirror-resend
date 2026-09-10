> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Grants

> Retrieve a list of OAuth grants for the authenticated team.

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

Returns all of the team's OAuth grants, including revoked ones. A grant's
`revoked_at` and `revoked_reason` are `null` while it is active. They are set
once the grant is revoked.

<QueryParams type="OAuth grants" isRequired={false} />

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.oauthGrants.list();
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result, list_opts::ListOptions};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _data = resend.oauth.list(ListOptions::default()).await?;

    Ok(())
  }
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/oauth/grants' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend oauth-grants list
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "has_more": false,
    "data": [
      {
        "id": "650e8400-e29b-41d4-a716-446655440001",
        "client_id": "430eed87-632a-4ea6-90db-0aace67ec228",
        "scopes": ["emails:send"],
        "resource": null,
        "created_at": "2026-04-08 00:11:13.110779+00",
        "revoked_at": null,
        "revoked_reason": null,
        "client": {
          "name": "Resend CLI",
          "logo_uri": "https://example.com/logo.png"
        }
      },
      {
        "id": "650e8400-e29b-41d4-a716-446655440002",
        "client_id": "430eed87-632a-4ea6-90db-0aace67ec228",
        "scopes": ["emails:send", "domains:read"],
        "resource": "https://api.resend.com",
        "created_at": "2026-04-07 00:11:13.110779+00",
        "revoked_at": "2026-04-09 00:11:13.110779+00",
        "revoked_reason": "revoked_from_api",
        "client": {
          "name": "Resend CLI",
          "logo_uri": "https://example.com/logo.png"
        }
      }
    ]
  }
  ```
</ResponseExample>
