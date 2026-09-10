> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Token

> Exchange an authorization code for tokens, or refresh an access token.

Handles two grants, selected by the `grant_type` body field: `authorization_code` (with mandatory PKCE) and `refresh_token` (with rotation and reuse detection). Accepts both `application/json` and `application/x-www-form-urlencoded`. Prefer form encoding, since that's what most OAuth libraries send by default.

Access tokens are JWTs signed with `ES256`, valid for 900 seconds. Refresh tokens are opaque strings, valid for 60 days from whenever they were last issued, and rotate on every use.

## Client authentication

How the client proves its identity depends on the `token_endpoint_auth_method` it [registered](/docs/api-reference/oauth/register#param-token-endpoint-auth-method) with:

* **Public clients (`none`)** don't send a secret. PKCE (`code_verifier`) is the only proof. This is the default and covers native, CLI, and other clients that can't keep a secret.
* **Confidential clients** additionally present their `client_secret`, on top of PKCE:
  * `client_secret_basic`: send `client_id` and `client_secret` in the HTTP `Authorization: Basic` header (each URL-encoded, joined with `:`, base64-encoded). With this method `client_id` can be omitted from the body.
  * `client_secret_post`: send `client_secret` as a body parameter alongside `client_id`.

A client must use exactly one mechanism. Sending both a Basic header and a body `client_secret` fails with `invalid_request`.

## PKCE

Before starting the [authorization request](/docs/api-reference/oauth/authorize), generate:

* `code_verifier`: a high-entropy random string, 43–128 characters, from the
  unreserved character set (`A-Z`, `a-z`, `0-9`, `-`, `.`, `_`, `~`). Keep it
  client-side only.
* `code_challenge`: the base64url-encoded SHA-256 hash of `code_verifier`,
  sent during authorization.

```javascript theme={"theme":{"light":"github-light","dark":"vesper"}}
import { createHash, randomBytes } from 'node:crypto';

function base64url(input) {
  return Buffer.from(input).toString('base64url');
}

const codeVerifier = base64url(randomBytes(64));
const codeChallenge = base64url(
  createHash('sha256').update(codeVerifier).digest(),
);
```

## Authorization code grant

### Body Parameters

<ParamField body="grant_type" type="string" required>
  Must be `"authorization_code"`.
</ParamField>

<ParamField body="client_id" type="string">
  Required, except with `client_secret_basic`, where the `Authorization` header
  already carries it.
</ParamField>

<ParamField body="client_secret" type="string">
  Required for a confidential client using `client_secret_post`. Omit for public
  clients and for `client_secret_basic` (send the secret in the `Authorization`
  header instead). See [Client authentication](#client-authentication).
</ParamField>

<ParamField body="code" type="string" required>
  The code from the `/oauth/authorize` callback. Single-use: redeeming it twice
  fails with `invalid_grant`. Expires 10 minutes after it was issued.
</ParamField>

<ParamField body="redirect_uri" type="string" required>
  Must exactly match the `redirect_uri` used in the authorization request.
</ParamField>

<ParamField body="code_verifier" type="string" required>
  The original value that
  [code\_challenge](/docs/api-reference/oauth/authorize#param-code-challenge) was
  derived from.
</ParamField>

<RequestExample>
  ```bash Public client theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/oauth/token' \
       -H 'Content-Type: application/x-www-form-urlencoded' \
       -d 'grant_type=authorization_code&client_id=550e8400-e29b-41d4-a716-446655440000&code=AUTHORIZATION_CODE&redirect_uri=http%3A%2F%2F127.0.0.1%3A49152%2Foauth%2Fcallback&code_verifier=CODE_VERIFIER_VALUE'
  ```

  ```bash Client Secret Basic theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/oauth/token' \
       -H 'Content-Type: application/x-www-form-urlencoded' \
       -u '550e8400-e29b-41d4-a716-446655440000:CLIENT_SECRET' \
       -d 'grant_type=authorization_code&code=AUTHORIZATION_CODE&redirect_uri=http%3A%2F%2F127.0.0.1%3A49152%2Foauth%2Fcallback&code_verifier=CODE_VERIFIER_VALUE'
  ```

  ```bash Client Secret Post theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/oauth/token' \
       -H 'Content-Type: application/x-www-form-urlencoded' \
       -d 'grant_type=authorization_code&client_id=550e8400-e29b-41d4-a716-446655440000&client_secret=CLIENT_SECRET&code=AUTHORIZATION_CODE&redirect_uri=http%3A%2F%2F127.0.0.1%3A49152%2Foauth%2Fcallback&code_verifier=CODE_VERIFIER_VALUE'
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "access_token": "eyJhbGciOiJFUzI1NiIsImtpZCI6Im9hdXRoX2tleSIsInR5cCI6ImF0K2p3dCJ9...",
    "token_type": "Bearer",
    "expires_in": 900,
    "refresh_token": "JcL7aYfE7S9h3L4qv0o2e1w8m6n5b3x9RkP2tD4uV6Q",
    "scope": "emails:send"
  }
  ```
</ResponseExample>

### Body Parameters

<ParamField body="grant_type" type="string" required>
  Must be `"refresh_token"`.
</ParamField>

<ParamField body="client_id" type="string">
  Required, except with `client_secret_basic`, where the `Authorization` header
  already carries it.
</ParamField>

<ParamField body="client_secret" type="string">
  Required for a confidential client using `client_secret_post`. Omit for public
  clients and for `client_secret_basic`. See [Client
  authentication](#client-authentication).
</ParamField>

<ParamField body="refresh_token" type="string" required />

<ParamField body="scope" type="string">
  Optionally narrow the scope of the new access token. Must be a subset of what
  the grant already has. You can't use this to escalate scope.
</ParamField>

<RequestExample>
  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/oauth/token' \
       -H 'Content-Type: application/x-www-form-urlencoded' \
       -d 'grant_type=refresh_token&client_id=550e8400-e29b-41d4-a716-446655440000&refresh_token=JcL7aYfE7S9h3L4qv0o2e1w8m6n5b3x9RkP2tD4uV6Q'
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "access_token": "eyJhbGciOiJFUzI1NiIsImtpZCI6Im9hdXRoX2tleSIsInR5cCI6ImF0K2p3dCJ9...",
    "token_type": "Bearer",
    "expires_in": 900,
    "refresh_token": "N3wRefreshTokenValue...",
    "scope": "emails:send"
  }
  ```
</ResponseExample>

## Errors

| Status | `error`               | When                                                                                                                                                                                           |
| ------ | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `400`  | `invalid_request`     | A required field is missing or malformed, or the client sent credentials via more than one mechanism (both a Basic header and a body `client_secret`).                                         |
| `400`  | `invalid_scope`       | Refresh requests a scope outside what the grant already has.                                                                                                                                   |
| `400`  | `invalid_grant`       | The code/refresh token is invalid, expired, already used, or reused after rotation (which also revokes the grant). Also returned when PKCE verification fails or `redirect_uri` doesn't match. |
| `401`  | `invalid_client`      | Unknown or disabled `client_id`, or a confidential client failed authentication (missing or wrong `client_secret`, or `client_id` in the Basic header doesn't match the request).              |
| `400`  | `unauthorized_client` | The client isn't registered for the grant type it's using.                                                                                                                                     |
