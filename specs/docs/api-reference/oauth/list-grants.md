> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Grants

> Retrieve a list of OAuth grants for the authenticated team.

Returns all of the team's OAuth grants, including revoked ones. A grant's
`revoked_at` and `revoked_reason` are `null` while it is active. They are set
once the grant is revoked.

## Query Parameters

Note that the `limit` parameter is *optional*. If
you do not provide a `limit`, all OAuth grants will be returned
in a single response.

**limit** `number`

Number of OAuth grants to retrieve.
<ul><li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more OAuth grants (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more OAuth grants (for
pagination). This ID will *not* be included in the returned list.
Cannot be used with the `after` parameter.

> [!NOTE]
>
> You can only use either `after` or `before`
> parameter, not both. See our
> [pagination guide](https://resend.com/docs/api-reference/pagination.md) for more
> information.

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
