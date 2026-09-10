> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Authorize

> Start the OAuth authorization code + PKCE flow.

This is a browser redirect endpoint, not a JSON API call. Open this URL in the user's browser. Don't fetch it from a backend or CLI process and follow the redirect yourself, since the user has to see and approve the consent screen.

The flow:

1. The client opens `/oauth/authorize` in the user's browser.
2. Resend redirects (`302`) to the Resend dashboard consent screen, which handles login if needed.
3. The user reviews and approves (or denies) the request.
4. The dashboard redirects the browser back to the client's `redirect_uri` with a `code` and the original `state`.

## Query Parameters

<ParamField query="client_id" type="string" required>
  The `client_id` from [registration](/docs/api-reference/oauth/register), or the
  HTTPS URL of a [Client ID Metadata Document](#client-id-metadata-documents).
  Resend tells the two apart by the `https://` prefix.
</ParamField>

<ParamField query="response_type" type="string" required>
  Must be `"code"`.
</ParamField>

<ParamField query="redirect_uri" type="string" required>
  Must exactly match one of the client's registered redirect URIs. The only
  exception is loopback URIs (`127.0.0.1`, `localhost`, `[::1]`), where the port
  is allowed to differ from what was registered.
</ParamField>

<ParamField query="scope" type="string">
  Space-delimited list of requested scopes. If omitted, defaults to the client's
  full registered scope set.
</ParamField>

### Scopes

* `emails:send` is enough for send-only routes: `POST /emails`, `POST /email`,
  `POST /emails/sending`, `POST /email/sending`, and `POST
  /broadcasts/:broadcastId/send`.
* `full_access` is required for every other API route. Also satisfies any
  `emails:send`-scoped check.

<ParamField query="state" type="string">
  An opaque value round-tripped back on the callback unchanged. Use it to bind
  the callback to the request that started the flow. Recommended, not required
  by the server, but a client that skips it can't detect CSRF on the callback.
  Maximum 1024 characters.
</ParamField>

<ParamField query="code_challenge" type="string" required>
  Base64url-encoded SHA-256 hash of a
  [code\_verifier](/docs/api-reference/oauth/token#param-code-verifier) your client
  generates.
</ParamField>

<ParamField query="code_challenge_method" type="string" required>
  Must be `"S256"`. Resend does not support the `plain` method.
</ParamField>

<Info>
  A `resource` parameter (RFC 8707) is accepted but ignored. Resend does not
  support resource indicators yet.
</Info>

### Client ID Metadata Documents

A `client_id` that starts with `https://` is read as the URL of a JSON document describing the client, so the client never registers. This follows the [OAuth Client ID Metadata Document](https://datatracker.ietf.org/doc/draft-ietf-oauth-client-id-metadata-document/) draft.

This is the only endpoint that fetches the document. See [Client ID Metadata Documents](/docs/guides/building-a-resend-oauth-client#client-id-metadata-documents) for the document fields and for how Resend fetches and caches it.

<RequestExample>
  ```bash Browser navigation theme={"theme":{"light":"github-light","dark":"vesper"}}
  GET https://api.resend.com/oauth/authorize?client_id=550e8400-e29b-41d4-a716-446655440000&response_type=code&redirect_uri=http%3A%2F%2F127.0.0.1%3A49152%2Foauth%2Fcallback&scope=emails%3Asend&state=STATE_VALUE&code_challenge=CODE_CHALLENGE_VALUE&code_challenge_method=S256
  ```
</RequestExample>

<ResponseExample>
  ```http Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  HTTP/1.1 302 Found
  Location: https://resend.com/oauth/authorize/3f9c1e2a-...
  ```
</ResponseExample>

## Errors

Before `client_id` and `redirect_uri` are validated (unknown `client_id`, invalid or unregistered `redirect_uri`), Resend returns a JSON error body, since it can't safely redirect to an unvalidated URL.

Once Resend validates `client_id` and `redirect_uri`, errors redirect (`302`) back to `redirect_uri` with `error`, `error_description`, and (if provided) `state` as query parameters only when the `redirect_uri` is trusted: a loopback address, a private-use URI scheme, or a verified client. An unverified `https` callback gets a JSON error body instead, which prevents the endpoint from being used as an open redirect. Handle both.

| `error`               | When                                                                                                       |
| --------------------- | ---------------------------------------------------------------------------------------------------------- |
| `invalid_request`     | `response_type` isn't `code`, or `code_challenge_method` isn't `S256`.                                     |
| `invalid_client`      | Unknown or disabled `client_id`. Also a metadata document that couldn't be fetched or didn't validate.     |
| `unauthorized_client` | The client isn't registered for the `authorization_code` grant.                                            |
| `invalid_scope`       | No scope requested, a scope isn't supported, or a scope isn't in the client's registered `scopes_allowed`. |
| `server_error`        | Resend failed to persist the authorization request.                                                        |
