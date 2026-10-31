> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send emails with Phoenix

> Learn how to send your first email using Phoenix and the Resend Elixir SDK.

> [!NOTE]
>
> This guides utilizes an [open source
> library](https://github.com/elixir-saas/resend-elixir) contributed by a
> community member. It's not developed, maintained, or supported by Resend
> directly.

## Prerequisites

Before you start, you'll need:

* A Resend [API key](https://resend.com/docs/create-an-api-key.md)
* A [verified domain](https://resend.com/docs/add-a-domain.md)

## Guide

**1. Install**

Install by adding `resend` to your list of dependencies in `mix.exs`:

```elixir mix.exs theme={"theme":{"light":"github-light","dark":"vesper"}}
def deps do
  [
    {:resend, "~> 0.4.5"}
  ]
end
```

**2. Send email using Swoosh**

This library includes a Swoosh adapter to make using Resend with a new Phoenix project straightforward. Configure your Mailer:

```elixir theme={"theme":{"light":"github-light","dark":"vesper"}}
config :my_app, MyApp.Mailer,
  adapter: Resend.Swoosh.Adapter,
  api_key: System.fetch_env!("RESEND_API_KEY")
```

If you're configuring your app for production, configure your adapter in `prod.exs`, and your API key from the environment in `runtime.exs`:

```elixir prod.exs theme={"theme":{"light":"github-light","dark":"vesper"}}
config :my_app, MyApp.Mailer, adapter: Resend.Swoosh.Adapter
```

```elixir runtime.exs theme={"theme":{"light":"github-light","dark":"vesper"}}
config :my_app, MyApp.Mailer, api_key: "re_xxxxxxxxx"
```

## Examples

> [card] [Phoenix App](https://github.com/resend/resend-examples/tree/main/elixir-resend-examples/phoenix_app)
>
> Full Phoenix web framework application

> [card] [Basic Send](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/basic_send.exs)
>
> Basic email sending

> [card] [Attachments](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/with_attachments.exs)
>
> Send emails with file attachments

> [card] [Templates](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/with_template.exs)
>
> Send emails using Resend hosted templates

> [card] [Scheduling](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/scheduled_send.exs)
>
> Schedule emails for future delivery

> [card] [Audiences](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/audiences.exs)
>
> Manage contacts and audiences

> [card] [Domains](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/domains.exs)
>
> Create and manage sending domains

> [card] [Inbound Webhooks](https://github.com/resend/resend-examples/blob/main/elixir-resend-examples/examples/inbound.exs)
>
> Receive and process inbound emails

> [card] [Double Opt-in](https://github.com/resend/resend-examples/tree/main/elixir-resend-examples/examples/double_optin)
>
> Double opt-in subscription flow
