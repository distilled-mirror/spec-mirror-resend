> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Elixir

> Learn how to send your first email using the Resend Elixir SDK.

> [!NOTE]
>
> This guides utilizes an [open source
> library](https://github.com/elixir-saas/resend-elixir) contributed by a
> community member. It's not developed, maintained, or supported by Resend
> directly.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](/docs/create-an-api-key)
* A [verified domain](/docs/add-a-domain)

## Guide

**1. Install**

Install by adding `resend` to your list of dependencies in `mix.exs`:

```elixir mix.exs theme={"theme":{"light":"github-light","dark":"vesper"}}
def deps do
  [
    {:resend, "~> 0.4.0"}
  ]
end
```

**2. Send email using HTML**

The easiest way to send an email is by using the `html` parameter.

```elixir send.exs theme={"theme":{"light":"github-light","dark":"vesper"}}
client = Resend.client(api_key: System.get_env("RESEND_API_KEY"))

Resend.Emails.send(client, %{
  from: "Acme <onboarding@resend.dev>",
  to: ["delivered@resend.dev"],
  subject: "hello world",
  html: "<strong>it works!</strong>"
})
```

## Examples

> **[Basic Send](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/basic_send.exs)**
>
> Basic email sending

> **[Attachments](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/with_attachments.exs)**
>
> Send emails with file attachments

> **[Templates](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/with_template.exs)**
>
> Send emails using Resend hosted templates

> **[Scheduling](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/scheduled_send.exs)**
>
> Schedule emails for future delivery

> **[Audiences](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/audiences.exs)**
>
> Manage contacts and audiences

> **[Domains](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/domains.exs)**
>
> Create and manage sending domains

> **[Inbound Webhooks](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/inbound.exs)**
>
> Receive and process inbound emails

> **[Double Opt-in](https://github.com/resend/resend-examples/tree/main/elixir-resend-examples/examples/double_optin)**
>
> Double opt-in subscription flow

> **[Phoenix App](https://github.com/resend/resend-examples/tree/main/elixir-resend-examples/phoenix_app)**
>
> Full Phoenix web framework application
