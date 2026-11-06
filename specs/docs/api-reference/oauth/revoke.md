> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Revoke Token

> Disconnect a client by revoking its refresh token.

RFC 7009 token revocation. Revoking a refresh token revokes the entire grant: every access and refresh token issued under it stops working.

Access tokens can't be revoked individually. Revoke the grant's refresh token instead. Per RFC 7009, this endpoint always returns `200` with an empty body.

Confidential clients must authenticate the same way they do at the [token endpoint](https://resend.com/docs/api-reference/oauth/token.md#client-authentication), using `client_secret_basic`, `client_secret_post`, or `private_key_jwt`. Public clients (`none`) send only `client_id`.

## Body Parameters

**token** `string` *required*

The refresh token to revoke.

**client\_id** `string`

Required, except with `client_secret_basic`, where the `Authorization` header
already carries it, and with `private_key_jwt`, where the assertion does.

**client\_secret** `string`

Required for a confidential client using `client_secret_post`. Omit for public
clients and for `client_secret_basic` (send the secret in the `Authorization`
header instead).

**client\_assertion\_type** `string`

Required with `private_key_jwt`. Must be
`urn:ietf:params:oauth:client-assertion-type:jwt-bearer`.

**client\_assertion** `string`

Required with `private_key_jwt`: a newly signed JWT, as at the [token
endpoint](https://resend.com/docs/api-reference/oauth/token.md#client-authentication).

**token\_type\_hint** `string`

Optional per RFC 7009. If set to `"access_token"`, the request fails: access
token revocation isn't supported. Any other value (including
`"refresh_token"`) is accepted and ignored. Unknown hints don't affect
behavior.

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

```bash Private Key JWT theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/oauth/revoke' \
     -H 'Content-Type: application/x-www-form-urlencoded' \
     -d 'client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=SIGNED_JWT&token=JcL7aYfE7S9h3L4qv0o2e1w8m6n5b3x9RkP2tD4uV6Q&token_type_hint=refresh_token'
```

```http Response theme={"theme":{"light":"github-light","dark":"vesper"}}
HTTP/1.1 200 OK
```

## Errors

| Status | `error` | When |
| - | - | - |
| `400` | `invalid_request` | `token` is missing, `client_id` is missing and neither a Basic header nor a `client_assertion` carries it, `token_type_hint` is `"access_token"`, or the client sent credentials via more than one mechanism. |
| `401` | `invalid_client` | Unknown or disabled `client_id`, or a confidential client failed authentication (missing or wrong `client_secret`, a missing, invalid, expired, or replayed `client_assertion`, or a key set that can't be used). |
| `503` | `temporarily_unavailable` | A `private_key_jwt` client's key set host timed out or answered with `429` or `5xx`, or the assertion couldn't be checked for replay. Retry the request. |
