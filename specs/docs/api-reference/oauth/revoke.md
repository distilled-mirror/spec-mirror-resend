> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Revoke Token

> Disconnect a client by revoking its refresh token.

RFC 7009 token revocation. Revoking a refresh token revokes the entire grant: every access and refresh token issued under it stops working.

Access tokens can't be revoked individually. Revoke the grant's refresh token instead. Per RFC 7009, this endpoint always returns `200` with an empty body.

Confidential clients must authenticate the same way they do at the [token endpoint](/docs/api-reference/oauth/token#client-authentication), using `client_secret_basic` or `client_secret_post`. Public clients (`none`) send only `client_id`.

## Body Parameters

<ParamField body="token" type="string" required>
  The refresh token to revoke.
</ParamField>

<ParamField body="client_id" type="string">
  Required, except with `client_secret_basic`, where the `Authorization` header
  already carries it.
</ParamField>

<ParamField body="client_secret" type="string">
  Required for a confidential client using `client_secret_post`. Omit for public
  clients and for `client_secret_basic` (send the secret in the `Authorization`
  header instead).
</ParamField>

<ParamField body="token_type_hint" type="string">
  Optional per RFC 7009. If set to `"access_token"`, the request fails: access
  token revocation isn't supported. Any other value (including
  `"refresh_token"`) is accepted and ignored. Unknown hints don't affect
  behavior.
</ParamField>

<RequestExample>
  ```bash Public client theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/oauth/revoke' \
       -H 'Content-Type: application/x-www-form-urlencoded' \
       -d 'client_id=550e8400-e29b-41d4-a716-446655440000&token=JcL7aYfE7S9h3L4qv0o2e1w8m6n5b3x9RkP2tD4uV6Q&token_type_hint=refresh_token'
  ```

  ```bash Client Secret Basic theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/oauth/revoke' \
       -H 'Content-Type: application/x-www-form-urlencoded' \
       -u '550e8400-e29b-41d4-a716-446655440000:CLIENT_SECRET' \
       -d 'token=JcL7aYfE7S9h3L4qv0o2e1w8m6n5b3x9RkP2tD4uV6Q&token_type_hint=refresh_token'
  ```

  ```bash Client Secret Post theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/oauth/revoke' \
       -H 'Content-Type: application/x-www-form-urlencoded' \
       -d 'client_id=550e8400-e29b-41d4-a716-446655440000&client_secret=CLIENT_SECRET&token=JcL7aYfE7S9h3L4qv0o2e1w8m6n5b3x9RkP2tD4uV6Q&token_type_hint=refresh_token'
  ```
</RequestExample>

<ResponseExample>
  ```http Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  HTTP/1.1 200 OK
  ```
</ResponseExample>

## Errors

| Status | `error`           | When                                                                                                                                  |
| ------ | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `400`  | `invalid_request` | `token` or `client_id` is missing, `token_type_hint` is `"access_token"`, or the client sent credentials via more than one mechanism. |
| `401`  | `invalid_client`  | Unknown or disabled `client_id`, or a confidential client failed authentication (missing or wrong `client_secret`).                   |
