> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Introduction

> Understand general concepts, response codes, and authentication strategies.

> [!NOTE]
>
> For most use cases, we recommend using an [official Resend SDK](https://resend.com/docs/sdks.md) instead
> of calling the API directly. The SDKs handle authentication, required headers,
> and error handling for you. See [Resend API vs SDK](https://resend.com/docs/api-vs-sdk) to decide
> which fits your project.

## Base URL

The Resend API is built on **REST** principles. **HTTPS** is enforced in every request to improve data security, integrity, and privacy. The API does not support **HTTP**.

All requests contain the following base URL:

```
https://api.resend.com
```

## Authentication

To authenticate you need to add an *Authorization* header with the contents of the header being `Bearer re_xxxxxxxxx` where `re_xxxxxxxxx` is your [API Key](https://resend.com/api-keys).

```
Authorization: Bearer re_xxxxxxxxx
```

## User-Agent

All API requests must include a `User-Agent` header. Requests without this header will be rejected with a `403` status code. Most HTTP clients, all [Resend SDKs](https://resend.com/docs/sdks.md), and the [Resend CLI](https://resend.com/docs/cli.md) include this header automatically, but if you're making direct HTTP requests, make sure to set it:

```
User-Agent: my-app/1.0
```

> [!NOTE]
>
> If you're getting a `403` error with error code `1010` despite having a valid
> API key, a missing `User-Agent` header is likely the cause. See [Error
> 1010](https://resend.com/docs/knowledge-base/403-error-1010.md) for more details.

## Response codes

Resend uses standard HTTP codes to indicate the success or failure of your requests.

In general, `2xx` HTTP codes correspond to success, `4xx` codes are for user-related failures, and `5xx` codes are for infrastructure issues.

| Status | Description |
| - | - |
| `200` | Successful request. |
| `400` | Check that the parameters were correct. |
| `401` | The API key used was missing. |
| `403` | The API key used was invalid. |
| `404` | The resource was not found. |
| `429` | The rate limit was exceeded. |
| `5xx` | Indicates an error with Resend servers. |

> [!NOTE]
>
> Check [Error Codes](https://resend.com/docs/api-reference/errors.md) for a comprehensive breakdown of
> all possible API errors.

## Rate limit

The default maximum rate limit is **10 requests per second per team**. This limit applies across all API keys associated with your team. This number can be increased for trusted senders by request. You can view your team's current rate limit on the [Settings Usage page](https://resend.com/settings/usage). After that, you'll hit the rate limit and receive a `429` response error code.

Learn more about our [rate limits](https://resend.com/docs/api-reference/rate-limit.md).

## FAQ

> [accordion] How does pagination work with the API?
>
> Some endpoints support cursor-based pagination to help you browse through
> large datasets efficiently. Check our [pagination
> guide](https://resend.com/docs/api-reference/pagination.md) for detailed information on how to use
> pagination parameters.

> [accordion] How do you handle API versioning?
>
> Currently, there's no versioning system in place. We plan to add versioning
> via calendar-based headers in the future.
