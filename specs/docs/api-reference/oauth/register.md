> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Register Client

> Dynamically register an OAuth client for the authorization code + PKCE flow (RFC 7591).

Unauthenticated (no API key). Rate-limited to 20 registrations per hour per IP address.

<Note>
  Prefer a [Client ID Metadata
  Document](/docs/guides/building-a-resend-oauth-client#client-id-metadata-documents)
  if the client can host a static JSON file. See [Building an OAuth
  client](/docs/guides/building-a-resend-oauth-client) for choosing a registration
  method and client type.
</Note>

## Body Parameters

<ParamField body="client_name" type="string" required>
  A human-readable name for the client. Maximum 200 characters.
</ParamField>

<ParamField body="redirect_uris" type="string[]" required>
  1 to 10 URIs, each up to 2048 characters. See [Allowed redirect
  URIs](#allowed-redirect-uris).
</ParamField>

<ParamField body="grant_types" type="string[]" default="[&#x22;authorization_code&#x22;, &#x22;refresh_token&#x22;]">
  Must include `authorization_code`. `refresh_token` is also supported.
</ParamField>

<ParamField body="response_types" type="string[]" default="[&#x22;code&#x22;]">
  Only `code` is supported. Validated if present but not stored; the response
  always echoes back `["code"]`.
</ParamField>

<ParamField body="scope" type="string">
  Space-delimited list of scopes, e.g. `"emails:send"`. Must be a subset of the
  [supported scopes](/docs/api-reference/oauth/authorize#scopes). If omitted, the
  client is registered with every supported scope.
</ParamField>

<ParamField body="token_endpoint_auth_method" type="string" default="none">
  How the client authenticates at the [token](/docs/api-reference/oauth/token) and
  [revocation](/docs/api-reference/oauth/revoke) endpoints. `none` registers a public
  client (PKCE only). `client_secret_basic` and `client_secret_post` register a
  confidential client and issue a `client_secret` in the response. See
  [Confidential clients](#confidential-clients). PKCE is required on every
  authorization code exchange regardless of method.
</ParamField>

<ParamField body="client_uri" type="string">
  A URL for the client's homepage. Echoed back, not otherwise used.
</ParamField>

<ParamField body="logo_uri" type="string">
  A URL for the client's logo. Shown on the consent screen.
</ParamField>

### Confidential clients

Registering with `token_endpoint_auth_method` set to `client_secret_basic` or `client_secret_post` returns two extra fields, documented in [Response Fields](#response-fields) below.

### Allowed redirect URIs

* `https://` URIs are unrestricted.
* `http://` is only allowed for loopback addresses (`127.0.0.1`, `localhost`,
  `[::1]`).
* Private-use URI schemes (e.g. `cursor://`, `vscode://`) are allowed.
* `file`, `ftp`, `data`, `javascript`, `blob`, `about`, and `vbscript` schemes
  are rejected. No URI may include a fragment.

## Response Fields

The response echoes back the registered client metadata along with the issued `client_id`. Registering a [confidential client](#confidential-clients) returns two extra fields:

<ResponseField name="client_secret" type="string">
  The generated client secret. Returned **only once**, in this response. Resend
  stores a hash and can't show it again, so persist it securely at registration
  time. If it's lost, register a new client.
</ResponseField>

<ResponseField name="client_secret_expires_at" type="number">
  Unix time at which the secret expires. Always `0`: the secret does not expire.
</ResponseField>

<RequestExample>
  ```bash Public client theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/oauth/register' \
       -H 'Content-Type: application/json' \
       -d $'{
    "client_name": "Example OAuth Client",
    "redirect_uris": ["http://127.0.0.1/oauth/callback"],
    "grant_types": ["authorization_code", "refresh_token"],
    "response_types": ["code"],
    "token_endpoint_auth_method": "none",
    "scope": "emails:send"
  }'
  ```

  ```bash Confidential client theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/oauth/register' \
       -H 'Content-Type: application/json' \
       -d $'{
    "client_name": "Example OAuth Client",
    "redirect_uris": ["http://127.0.0.1/oauth/callback"],
    "grant_types": ["authorization_code", "refresh_token"],
    "response_types": ["code"],
    "token_endpoint_auth_method": "client_secret_basic",
    "scope": "emails:send"
  }'
  ```
</RequestExample>

<ResponseExample>
  ```json Public client theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "client_id": "550e8400-e29b-41d4-a716-446655440000",
    "client_id_issued_at": 1750000000,
    "client_name": "Example OAuth Client",
    "redirect_uris": ["http://127.0.0.1/oauth/callback"],
    "grant_types": ["authorization_code", "refresh_token"],
    "response_types": ["code"],
    "token_endpoint_auth_method": "none",
    "scope": "emails:send"
  }
  ```

  ```json Confidential client theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "client_id": "550e8400-e29b-41d4-a716-446655440000",
    "client_id_issued_at": 1750000000,
    "client_name": "Example OAuth Client",
    "redirect_uris": ["http://127.0.0.1/oauth/callback"],
    "grant_types": ["authorization_code", "refresh_token"],
    "response_types": ["code"],
    "token_endpoint_auth_method": "client_secret_basic",
    "scope": "emails:send",
    "client_secret": "3vProAFw7...store-this-now...KpQ",
    "client_secret_expires_at": 0
  }
  ```
</ResponseExample>

## Errors

Errors use the standard OAuth shape (`{"error": "...", "error_description": "..."}`) rather than Resend's usual [error format](/docs/api-reference/errors).

| Status | `error`             | When                                                                     |
| ------ | ------------------- | ------------------------------------------------------------------------ |
| `400`  | `invalid_request`   | A required field is missing, malformed, or a redirect URI is disallowed. |
| `400`  | `invalid_scope`     | `scope` includes a value outside the supported scope set.                |
| `429`  | `too_many_requests` | More than 20 registrations from this IP in the last hour.                |
