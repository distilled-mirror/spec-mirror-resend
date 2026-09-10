> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Resend API vs SDK

> For most use cases, the Resend SDK offers a better developer experience.

For most use cases, **the Resend SDK offers a better developer experience** than
calling the raw HTTP API directly. Resend maintains official, open source SDKs
for Node.js, PHP, Python, Ruby, Go, Rust, Java, and .NET.

<Info>
  **Recommendation:** Use a [Resend SDK](/docs/sdks) for your language. Call the [raw
  API](/docs/api-reference/introduction) directly only when no SDK exists for your
  stack.
</Info>

## Choosing between the SDK and API

Reach for the SDK unless you have a specific reason not to. It handles
authentication, the required `User-Agent` header, request serialization, typed
responses, and error handling for you. That leaves less boilerplate to get
wrong.

|                      | Resend SDK (recommended) | Raw HTTP API                                  |
| -------------------- | ------------------------ | --------------------------------------------- |
| Auth & headers       | Handled automatically    | Set `Authorization` and `User-Agent` manually |
| Types & autocomplete | Built in                 | None                                          |
| Errors               | Structured error objects | Parse status codes and JSON yourself          |
| Maintained by        | Resend                   | You                                           |

## When to use the raw API directly

Calling the API directly is a good fit when:

* There's **no official SDK** for your language or runtime.
* You're making a one-off request and don't want to add a dependency.
* You're building your own integration or wrapper.

If you do call the API directly, remember to set the required
[`User-Agent` header](/docs/api-reference/introduction#user-agent).

## Next steps

<CardGroup cols={2}>
  <Card title="Official SDKs" icon="cube" href="/docs/sdks">
    Install the SDK for your language.
  </Card>

  <Card title="Quickstart" icon="rocket" href="/docs/introduction">
    Send your first email in minutes.
  </Card>

  <Card title="API Reference" icon="code" href="/docs/api-reference/introduction">
    Full HTTP API documentation.
  </Card>

  <Card title="MCP Server" icon="robot" href="/docs/mcp-server">
    Give your AI agent access to Resend.
  </Card>
</CardGroup>
